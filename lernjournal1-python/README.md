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
 
<img src="https://github.com/Ravinsen/-MDM-Lernjournal/blob/main/lernjournal1-python/images/Tankkostenrechner_Frontend.png?raw=true" alt="Web UI" style="max-width: 100%; height: auto;">

---

## Dependency Management

- Verwendet wurde eine minimale `requirements.txt` mit einer Abhängigkeit:
  
  ```txt
  flask

- Die virtuelle Umgebung wurde mit venv erstellt (.venv)
- Es wurde keine virtuelle Umgebung auf Azure mitgeliefert (.venv ausgeschlossen)
- Die requirements.txt wurde manuell gepflegt

<img src="https://github.com/Ravinsen/-MDM-Lernjournal/blob/main/lernjournal1-python/images/requirements_txt.png?raw=true" alt="Requirements" style="max-width: 100%; height: auto;">


  ## Deployment

Das Deployment erfolgte über **Azure Web App Service** mit **Local Git Deployment** über das Azure Webportal.

---

### 1. Web App über Azure-Portal erstellt

- App-Name: `tankkostenrechner-app`
- Region: South India
- Laufzeit: Python 3.11 (Linux)
- Standarddomäne: tankkostenrechner-app-hucmg8c6d7hgc7cq.southindia-01.azurewebsites.net

<img src="https://github.com/Ravinsen/-MDM-Lernjournal/blob/main/lernjournal1-python/images/Tankkostenrechner-App_Azure.png?raw=true" alt="Azure App Übersicht" style="max-width: 100%; height: auto;">

---

### 2. Local Git aktiviert & Credentials gesetzt

- SCM-Authentifizierung wurde manuell aktiviert
- Benutzername und Passwort im Deployment Center festgelegt
- Git-URL wurde anschließend angezeigt, z. B.:  
  `https://tankkostenrechner-app.scm.azurewebsites.net/tankkostenrechner-app.git`

<img src="images/azure-deployment-center.png" alt="Deployment Center" style="max-width: 100%; height: auto;">

---

### 3. Lokaler Push über Git

Im lokalen Projektordner wurde das Repository initialisiert, mit Azure verknüpft und gepusht:

`az login
git init
git remote add azure https://tankkostenrechner-app.scm.azurewebsites.net/tankkostenrechner-app.git
git add .
git commit -m "Initial deploy"
git push azure main:master`

Platzhalter Screenshot:
👉 Terminal-Output vom erfolgreichen git push zeigen
<img src="images/git-push-success.png" alt="Git Push" style="max-width: 100%; height: auto;">

4. Live Test der Anwendung
Die Anwendung ist jetzt live erreichbar unter:
🔗 https://tankkostenrechner-app.azurewebsites.net

Platzhalter Screenshot:
👉 Zeige deine App live im Browser auf Azure
<img src="images/live-app.png" alt="Live App" style="max-width: 100%; height: auto;">

Fazit & Reflexion
Die Umsetzung eines eigenen Tankkostenrechners war trotz geringer Komplexität sehr lehrreich. Ich konnte den vollständigen Prozess von der lokalen Flask-App bis zum Azure Deployment nachvollziehen und umsetzen.
