# Lernjournal 1 Python  
**Modul: Model Deployment & Maintenance**  
**Lernjournal-Thema: Tankkostenrechner**  
**Erfasst von: Senthujan Ravindran / ravinsen**

---

## Repository und Library

| Bestandteil | Beschrieb, Fundort |
|-------------|------------------------------------------------------------|
| Repository (URL) | https://github.com/Ravinsen/Tankkostenrechner |
| Kurze Beschreibung der App-Funktion | Berechnet die Tankkosten basierend auf Strecke, Verbrauch und Benzinpreis |
| Verwendete Library aus PyPi (Name) | flask |
| Verwendete Library aus PyPi (URL) | https://pypi.org/project/Flask/ |
| Location deployed Application | https://tankkostenrechner-app.azurewebsites.net |

---

## App, Funktionalität

Die Webanwendung **Tankkostenrechner** erlaubt es, die geschätzten Kosten einer Autofahrt zu berechnen. Der Benutzer gibt drei Werte ein:

- Strecke in Kilometern
- Verbrauch in Litern pro 100 Kilometer
- Benzinpreis pro Liter (CHF)

Die App berechnet auf Knopfdruck die Tankkosten in CHF (Formel: Kosten = (Strecke / 100) × Verbrauch × Preis). Die einfache Logik wird mit Flask im Backend umgesetzt, das Frontend basiert auf HTML, Bootstrap und Vanilla JavaScript.

---

## Dependency Management

- Verwendet wurde eine minimale `requirements.txt` mit einer Abhängigkeit:
  
  ```txt
  flask
  ```

- Die virtuelle Umgebung wurde mit venv erstellt (.venv)
- Es wurde keine virtuelle Umgebung auf Azure mitgeliefert (.venv ausgeschlossen)
- Die requirements.txt wurde manuell gepflegt

<img src="https://github.com/Ravinsen/-MDM-Lernjournal/blob/main/lernjournal1-python/images/requirements_txt.png?raw=true" alt="Requirements" style="max-width: 100%; height: auto;">

---

  ## Deployment

Das Deployment erfolgte über **Azure Web App Service** mit **Local Git Deployment** über das Azure Webportal.



### 1. Web App über Azure-Portal erstellt

- App-Name: `tankkostenrechner-app`
- Region: `South India`
- Laufzeit: `Python 3.11 (Linux)`
- Standarddomäne: `tankkostenrechner-app-hucmg8c6d7hgc7cq.southindia-01.azurewebsites.net`

<img src="https://github.com/Ravinsen/-MDM-Lernjournal/blob/main/lernjournal1-python/images/Tankkostenrechner-App_Azure.png?raw=true" alt="Azure App Übersicht" style="max-width: 100%; height: auto;">

---

### 2. Local Git aktiviert & Credentials gesetzt

- SCM-Authentifizierung wurde manuell aktiviert
- Benutzername und Passwort im Deployment Center festgelegt
- Git-URL wurde anschliessend angezeigt: `https://tankkostenrechner-app-hucmg8c6d7hgc7cq.scm.southindia-01.azurewebsites.net:443/Tankkostenrechner-App.git`

<img src="https://github.com/user-attachments/assets/86e44c13-29be-4ea1-bd2f-659898ebb660" style="max-width: 100%; height: auto;">

---

### 3. Lokaler Push über Git

Im lokalen Projektordner wurde das Repository initialisiert, mit Azure verknüpft und gepusht:

```bash
az login
git init
git remote add azure https://tankkostenrechner-app.scm.azurewebsites.net/tankkostenrechner-app.git
git add .
git commit -m "Initial deploy"
git push azure main:master
```

```txt
C:\Users\senth\MDM-Projects\Tankkostenrechner> git push azure main:master
Enumerating objects: 23, done.
Counting objects: 100% (23/23), done.
Delta compression using up to 8 threads
Compressing objects: 100% (17/17), done.
Writing objects: 100% (23/23), 4.12 KiB | 2.06 MiB/s, done.
Total 23 (delta 5), reused 0 (delta 0), pack-reused 0
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'abc123def456...'.
remote: Deployment successful.
To https://tankkostenrechner-app.scm.azurewebsites.net:443/tankkostenrechner-app.git
 * [new branch]      main -> master
```

### 4. Live Test der Anwendung

Die Anwendung ist live erreichbar unter:
https://tankkostenrechner-app-hucmg8c6d7hgc7cq.southindia-01.azurewebsites.net/

<img src="https://github.com/Ravinsen/-MDM-Lernjournal/blob/main/lernjournal1-python/images/Tankkostenrechner_Frontend.png?raw=true" alt="Web UI" style="max-width: 100%; height: auto;">

---

### Fazit & Reflexion

Die Umsetzung eines eigenen Tankkostenrechners war trotz geringer Komplexität sehr lehrreich. Ich konnte den vollständigen Prozess von der lokalen Flask-App bis zum Azure Deployment nachvollziehen und umsetzen.
