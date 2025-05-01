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

Jede Klasse enthält zwischen 50–250 Bilder. Dadurch konnte ein relativ ausgewogenes Modell trainiert werden.

### Training

Das Training des Modells erfolgte in einem separaten Python-Repository mit PyTorch - https://github.com/Ravinsen/weather_training und wurde durch eine minimalistische Trainingsumgebung realisiert. Das Ziel war es ein robustes, fehlerfreies Modell für den späteren Java-Einsatz zu erstellen.

Die Umgebung wurde mit folgenden Paketen konfiguriert:

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

<img src="images/Modeltraining_I.png" alt="Modeltraining_I.png" style="max-width: 100%; height: auto;">

Nach dem Training wurde das Modell mithilfe von `torch.onnx.export(...)` in das ONNX-Format überführt, um es später mit DJL in Java nutzen zu können.

<img src="images/Export_Onnx.png" alt="Export_Onnx" style="max-width: 100%; height: auto;">



### Inference / Serving

Die Inferenz findet in einer Spring Boot Anwendung statt, die mithilfe von DJL (Deep Java Library) das ONNX-Modell lädt und verarbeitet.

Beim Start wird das Modell geladen und ein `Predictor<Image, Classifications>` erzeugt. Dabei wird die ONNX Engine verwendet und der `ImageClassificationTranslator` entsprechend konfiguriert.

```txt
Criteria<Image, Classifications> criteria = Criteria.builder()
    .optModelPath(Paths.get("src/main/resources/models/weather_classifier.onnx"))
    .optTranslator(translator)
    .optEngine("OnnxRuntime")
    .build();
```
Das synset-File (synset.txt) enthält die Klassennamen:



### Deployment

* [ ] TODO
