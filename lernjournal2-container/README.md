# Lernjournal 2 Container

## Docker Web-Applikation

### Verwendete Docker Images

| | |
| -------- | ------- |
| Image 1 | traccar/traccar:latest |
| Image 1 – URL Docker Hub | https://hub.docker.com/r/traccar/traccar |
| Image 2 | mysql:5.7 |
| Image 2 – URL Docker Hub | https://hub.docker.com/_/mysql |
| Docker Compose | https://github.com/Ravinsen/-MDM-Lernjournal/blob/main/lernjournal2-container/docker-compose.yml |

### Dokumentation manuelles Deployment

Ziel war es, eine bestehende Container-Web-Applikation mit mindestens zwei Containern zu recherchieren, manuell und via Docker Compose zu deployen. Ich habe mich für das Fahrzeug-Ortungssystem Traccar entschieden, da es eine moderne GPS-Tracking-Plattform ist.

Die Anwendung Traccar besteht aus zwei verbundenen Containern:

– Traccar-Webserver  
– MySQL-Datenbank

<img src="images/ZweiContainer.png" alt="Container" style="max-width: 100%; height: auto;">

### Dokumentation Docker-Compose Deployment

Als erstes wurde das  <a href="docker-compose.yml">docker-compose.yml</a> erstellt mit den Anwendungen Traccar und MySQL. Das docker-compose File braucht es, um mehrere Container gemeinsam gestartet werden können.

Um zu starten wurde folgender Befehlt im Terminal ausgeführt:

 ```txt
  docker-compose up -d
  ```
<img src="images/DockerComposeCommand.png" alt="DockerComposeCommand" style="max-width: 100%; height: auto;">

Nach erfolgreichem Laden war die Traccar-Seite über den Localhost (http://localhost:8082) erreichbar. Nach der Registrierung konnte die Hauptseite geöffnet werden.


* [ ] TODO

## Deployment ML-App

### Variante und Repository

| Gewähltes Beispiel | Bitte ausfüllen |
| -------- | ------- |
| onnx-sentiment-analysis | Ja/Nein |
| onnx-image-classification | Ja/Nein |
| Repo URL Fork | URL |
| Docker Hub URL | URL |

### Dokumentation lokales Deployment

* [ ] TODO

### Dokumentation Deployment Azure Web App

* [ ] TODO

### Dokumentation Deployment ACA

* [ ] TODO

### Dokumentation Deployment ACI

* [ ] TODO
