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

Nach erfolgreichem Laden war die Traccar-Seite über den Localhost (http://localhost:8082) erreichbar. Nach der Registrierung konnte die Hauptseite ebenfalls erfolgreich geöffnet werden.

<img src="images/TraccarRegisterScreen.png" alt="TraccarRegisterScreen" style="max-width: 100%; height: auto;">

<img src="images/TraccarMainScreen.png" alt="TraccarMainScreen" style="max-width: 100%; height: auto;">

Nun zum Schluss kann die Applikation beendet und der Container entfernt werden. Dazu wird folgender Code ausgeführt:

 ```txt
  docker-compose down
  ```
<img src="images/DockerComposeDown.png" alt="DockerComposeDown" style="max-width: 100%; height: auto;">

## Deployment ML-App

### Variante und Repository

| Gewähltes Beispiel | Bitte ausfüllen |
| -------- | ------- |
| onnx-sentiment-analysis | Nein |
| onnx-image-classification | Ja|
| Repo URL Fork | https://github.com/Ravinsen/onnx-image-classification |
| Docker Hub URL | https://hub.docker.com/repository/docker/ravinsen/onnx-image-classification |

### Dokumentation lokales Deployment

Für den zweiten Teil habe ich mich für die `onnx-image-classification` entschieden. Im diesen Teil liegt der Schwerpunkt im lokalen Deployment einer Machine Learning App, welche von diesem Repository zu Verfügung gestellt wurde https://github.com/mosazhaw/onnx-image-classification. Das Repository wurde wie gewohnt geforkt und geclont.

Danach wurde das Docker-Image für die onnx-image-classification-App lokal erstellt und geprüft, ob die Webanwendung funktioniert.

1. Für das lokale Deployment wurde `docker build` ausgeführt.
  ```txt
  docker build -t onnx-image-classification .
  ```

<img src="images/dockerbuildpng.png" alt="dockerbuildpng" style="max-width: 100%; height: auto;">

2. Danach wird der Container mit `docker run` gestartet.
```txt
docker run --name onnx-image-classification -p 9000:5000 -d onnx-image-classification`. 
```

<img src="images/dockerrun.png" alt="dockerrun" style="max-width: 100%; height: auto;">

3. Und das Docker Image wurde erstellt, dies ist im Docker Desktop ersichtlich.

<img src="images/dockerimage.png" alt="dockerimage" style="max-width: 100%; height: auto;"> 

4. Nun ist das Modell über den Localhost `http://localhost:9000` erreichbar.

<img src="images/onnxlocalhost.png" alt="onnxlocalhost" style="max-width: 100%; height: auto;">  

5. Zum Schluss wird mit `docker login` Docker-Client auf Docker Hub authentifiziert, das Docker Image getaggt `docker tag` und das Image auf Docker Hub veröffentlicht `docker push`.
```txt
docker login
docker tag onnx-image-classification ravinsen/onnx-image-classification:latest
docker push ravinsen/onnx-image-classification:latest
  ```
<img src="images/dockerlogintagpush.png" alt="dockerlogintagpush" style="max-width: 100%; height: auto;">

<img src="images/dockerhubimage.png" alt="dockerhubimage" style="max-width: 100%; height: auto;">

### Dokumentation Deployment Azure Web App

Nach erfolgreichem lokalen Test wurde das Image in die Azure Cloud auf einen Azure App Service deployed. Ziel war es, die ML-App als skalierbare Web-App über eine öffentlich erreichbare URL verfügbar zu machen.

1. Der erste Schritt ist die Erstellung einer Resourcengruppe mit `az group create`. Ich habe mich für das Aufsetzen für die CLI entschieden.
```txt
az group create --name lj2-onnx-rg --location westeurope
az webapp create --resource-group lj2-onnx-rg --plan lj2-onnx-plan --name lj2-onnx-app --deployment-container-image-name ravinsen/onnx-image-classification:latest
```
<img src="images/azgroupcreate.png" alt="azgroupcreate" style="max-width: 100%; height: auto;">

<img src="images/azwebappcreate.png" alt="azwebappcreate" style="max-width: 100%; height: auto;">


### Dokumentation Deployment ACA

* [ ] TODO

### Dokumentation Deployment ACI

* [ ] TODO
