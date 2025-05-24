# Projekt 1 Python

## Übersicht

| | |
| -------- | ------- |
| Variante | Eigenes Projekt |
| Datenherkunft | JSON, Echtzeitdaten von API |
| Datenherkunft | https://creativecommons.tankerkoenig.de |
| ML-Algorithmus | Lineare Regression (pro Tankstelle) |
| Repo URL | https://github.com/Ravinsen/Benzin-App |

---

## Dokumentation

### Data Scraping

Für das Projekt habe ich keine statischen Daten gescraped, sondern auf die **Tankerkönig API** zugegriffen, welche Echtzeit-Daten von über 14.000 Tankstellen in Deutschland zur Verfügung stellt.

<img src="images/tankerkönig.png" alt="tankerkönig" style="max-width: 100%; height: auto;">

Über das Skript `data/main.py` werden täglich Daten für 20 deutsche Städte abgerufen. Die Preise werden mit einem Zeitstempel versehen und in MongoDB Atlas gespeichert.

**Genutzte Bibliotheken:**  
- `requests` für die API-Anfrage  
- `geopy` für die Koordinaten  
- `pymongo` zur Verbindung mit MongoDB

```bash
# Befehl, um die Daten zu laden in die MongoDB
python data/main.py
```


Die API-URL für jede Stadt sieht so aus:

```txt
url = https://creativecommons.tankerkoenig.de/json/list.php?lat={lat}&lng={lng}&rad=25&sort=dist&type=all&apikey={api_key}"
```
<img src="images/datascrapping.png" alt="datascrapping" style="max-width: 100%; height: auto;">

<img src="images/MongoDB.png" alt="MongoDB" style="max-width: 100%; height: auto;">
---
## Training

### Architekturüberblick

Das Modell verfolgt einen **anfragegetriebenen Trainingsansatz**: Es gibt **keinen zentralen Trainingslauf**, sondern das Modell wird **on-the-fly** bei jeder Nutzeranfrage individuell für die jeweilige Tankstelle trainiert. Dabei wird ausschliesslich auf bereits in MongoDB gespeicherte Daten zurückgegriffen (siehe *Data Scraping*).

### Datengrundlage

- **Zeitraum**: Letzte 60 Tage  
- **Quelle**: MongoDB Collection `tankstellen`  
- **Filter**: Standort und Umkreis (Standard: 5 km)  
- **Kraftstofftypen**: `e5`, `e10`, `diesel`  
- **Geodaten**: Koordinatenberechnung mittels `geopy.distance.geodesic`

Nur Tankstellen mit ausreichender Datenhistorie (≥2 Tage) werden berücksichtigt.

### Feature Engineering

Aus den historischen Preisdaten wird das folgende Merkmal generiert:

```python
sub_df["day"] = (pd.to_datetime(sub_df["date"]) - pd.to_datetime(sub_df["date"]).min()).dt.days
X = sub_df["day"].values.reshape(-1, 1)
y = sub_df[kraftstoff].astype(float).values
```

### Modelltyp & Training

Für jede Tankstelle:

- **Modelltyp**: Lineare Regression (`sklearn.linear_model.LinearRegression`)
- **Trainingsprozess**: Einfacher Fit mit `X` und `y`
- **Ziel**: Prognose der Preise für die nächsten 5 Tage

```python
model = LinearRegression().fit(X, y)
future_days = np.array([sub_df["day"].max() + i for i in range(1, 6)])
preds = model.predict(future_days.reshape(-1, 1))
```

Das Modell wird nicht persistent gespeichert, da es bei jedem Aufruf neu erzeugt wird.

### Ausgabe & Visualisierung

Die Ergebnisse beinhalten:

- **Tägliche Vorhersage** der günstigsten Preise je Datum (über alle Tankstellen hinweg)
- **Zusammengeführte Daten** aus Forecast + aktuelle Preise

```python
df_combined = pd.concat([df_forecast, df_today], ignore_index=True)
```

### Empfehlungskomponente

Zusätzlich zur Prognose wird eine **empfohlene Aktion** ausgegeben:

- „Heute tanken“ vs. „Später tanken“
- Basierend auf Vergleich des aktuellen Preises mit der 5-Tages-Prognose
- Information enthält Name, Marke, Distanz und Datum des besten Preises

```python
best_entry = df_combined.loc[df_combined["price"].idxmin()]
recommendation = {
    "date": best_entry["date"].strftime("%A, %d. %B %Y"),
    "price": best_entry["price"],
    "name": best_entry["name"],
    "brand": best_entry["brand"],
    "distance": best_entry.get("distance", None)
}
```


---
## ModelOps Automation

Die App aktualisiert sich automatisch täglich über GitHub Actions. Die Workflow-Datei `update_data.yml` liegt unter `.github/workflows`.

Der CRON-Zeitplan ist so konfiguriert, dass täglich um 04:00 Uhr UTC neue Daten geladen werden:

```txt
on:
  schedule:
    - cron: '0 4 * * *'
```

**Wichtige Schritte im Workflow:**

- Installieren der Abhängigkeiten

- Laden der Secrets (MongoDB URI, API Key)

- Ausführung von main.py

---

## Deployment

Die App wurde vollständig containerisiert mit Docker und auf Azure App Service for Containers deployed.

Dockerfile-Ausschnitt:
```
FROM python:3.10-slim
RUN apt-get update && apt-get install -y locales
ENV LANG=de_DE.UTF-8
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app/app.py"]
```

Nach dem lokalen Build wurde das Image zu Azure Container Registry gepusht:

```bash
docker build -t benzin-app:v1 .
docker tag benzin-app:v1 benzinpreisportal.azurecr.io/benzin-app:v1
docker push benzinpreisportal.azurecr.io/benzin-app:v1
```

Anschliessend wurde das Image in Azure Web App verlinkt. Die Anwendung läuft öffentlich unter einer benutzerdefinierten Subdomain.

---

## Fazit

Das Projekt hat mir geholfen, den kompletten Lebenszyklus eines ML-Modells praktisch zu durchlaufen: Von der Datenbeschaffung über die Modellierung bis zur automatisierten Bereitstellung in der Cloud.

Besonders herausfordernd war es, die Performance durch Indexierung, Caching und datenbasierte Filterung zu optimieren. Gleichzeitig war es spannend, die täglichen Abläufe über GitHub Actions komplett zu automatisieren.
