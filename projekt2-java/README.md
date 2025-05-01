# Projekt 2 Java

## Übersicht

| | Bitte ausfüllen |
| -------- | ------- |
| Variante | Vorhandener Datensatz |
| Datensatz | Bilddatensatz (JPG), klassifiziert nach Wetterbedingungen |
| Datensatz | 1) https://www.kaggle.com/datasets/somesh24/multiclass-images-for-weather-classification?select=dataset2<br>2) https://www.kaggle.com/datasets/jehanbhathena/weather-dataset |
| Modell (wenn selbstgewählt) | Lokal trainiertes PyTorch-Modell, exportiert als ONNX - https://github.com/Ravinsen/weather_training |
| ML-Algorithmus | Transfer Learning mit ResNet18 |
| Repo URL | https://github.com/Ravinsen/WeatherClassifier |



## Dokumentation

### Daten
Für das Projekt wurden zwei öffentlich verfügbare Datensätze von Kaggle kombiniert, um die Klassifikation von Wetterbildern zu ermöglichen.

Dataset 1 - https://www.kaggle.com/datasets/somesh24/multiclass-images-for-weather-classification?select=dataset2 - enthält die Klassen:

- cloudy
- rainy
- sunny
- sunrise

Dataset 2 -https://www.kaggle.com/datasets/jehanbhathena/weather-dataset - wurde verwendet, um zusätzliche Wetterphänomene zu integrieren:

- snowy
- rainbow
- lightning
- hail

Die Bilder liegen im JPG-Format vor und wurden lokal in passende Ordnerstrukturen überführt, damit sie mit torchvision.datasets.ImageFolder geladen werden können.

<img src="images/Weather_Training_Folder.png" alt="Weather_Training_Folder" style="max-width: 100%; height: auto;">

### Training

Ein separates Repository wurde erstellt, um das Modell unabhängig zu trainieren https://github.com/Ravinsen/weather_training . Die Umgebung bestand aus einem klassischen PyTorch Setup mit Jupyter Notebooks.

Folgende Pakete wurden verwendet:

```txt
pip install torch torchvision torchaudio
pip install matplotlib scikit-learn pandas tqdm onnx
pip install notebook
```

Das Modell basiert auf ResNet18 und wurde mit PyTorch mittels Transfer Learning angepasst.
Die Trainingsumgebung bestand aus:

- 8 Klassen
- Fine-Tuning von resnet18 auf 5 Epochen
- Verwendung von CrossEntropyLoss und Adam-Optimizer
- Accuracy nach 5 Epochen: ca. 87 %

<img src="images/Modeltraining.png" alt="Modeltraining.png" style="max-width: 100%; height: auto;">

Das trainierte Modell wurde anschliessend als .onnx Datei exportiert und in ein Spring Boot Backend mit DJL integriert.

<img src="images/Export_Onnx.png" alt="Export_Onnx" style="max-width: 100%; height: auto;">



### Inference / Serving

* [ ] TODO

### Deployment

* [ ] TODO
