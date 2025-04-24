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

Über das Skript `data/main.py` werden täglich Daten für 20 deutsche Städte abgerufen. Die Preise werden mit einem Zeitstempel versehen und in MongoDB Atlas gespeichert.

**Genutzte Bibliotheken:**  
- `requests` für die API-Anfrage  
- `geopy` für die Koordinaten  
- `pymongo` zur Verbindung mit MongoDB

```bash
# Beispielhafte Terminal-Ausführung
python data/main.py
```

Die API-URL für jede Stadt sieht so aus:
```url = https://creativecommons.tankerkoenig.de/json/list.php?lat={lat}&lng={lng}&rad=25&sort=dist&type=all&apikey={api_key}"```

---
## Training

Das Modell ist in forecast_model.py implementiert. Es wird keine zentrale Trainingspipeline verwendet – stattdessen wird pro Anfrage eine Vorhersage in Echtzeit erzeugt, basierend auf historischen Daten der letzten 60 Tage.

Für jede Tankstelle wird dabei eine lineare Regression mit Scikit-Learn durchgeführt. Die Features sind der Zeitstempel (umgewandelt in "Tage seit Beginn") und die Zielgröße ist der Kraftstoffpreis.

```model = LinearRegression().fit(X, y)```

Die Prognose deckt 5 zukünftige Tage ab. Zusätzlich wird eine Empfehlung gegeben, ob heute oder ein späterer Tag günstiger ist.

```
# Beispielhafte Funktion
predict_prices(df, kraftstoff="e5")
```

---
## ModelOps Automation

Die App aktualisiert sich automatisch täglich über GitHub Actions. Die Workflow-Datei update_data.yml liegt unter .github/workflows.

Der CRON-Zeitplan ist so konfiguriert, dass täglich um 04:00 Uhr UTC neue Daten geladen werden:

```
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

Anschließend wurde das Image in Azure Web App verlinkt. Die Anwendung läuft öffentlich unter einer benutzerdefinierten Subdomain.

---

## Fazit

Das Projekt hat mir geholfen, den kompletten Lebenszyklus eines ML-Modells praktisch zu durchlaufen: Von der Datenbeschaffung über die Modellierung bis zur automatisierten Bereitstellung in der Cloud.

Besonders herausfordernd war es, die Performance durch Indexierung, Caching und datenbasierte Filterung zu optimieren. Gleichzeitig war es spannend, die täglichen Abläufe über GitHub Actions komplett zu automatisieren.
