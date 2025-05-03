# Screencast Projekt 1

Bitte Anzahl Unterkapitel entsprechend der Gruppengrösse anpassen. Der eigene Screencast soll nicht reviewed werden.

## Screencast 1

|       | Bitte ausfüllen |
|-------|-----------------|
| Review durch (ZHAW-Kürzel) | ravinsen |
| Review von (ZHAW-Kürzel) | akguelar |
| Sprache, Kommunikation, roter Faden | Präsentation ist sprachlich klar und strukturiert aufgebaut. Fachbegriffe wie Scrapy Spider, MongoDB, XGBoost, Docker oder GitHub Actions werden korrekt eingesetzt. Der rote Faden ist über die gesamte Dauer erkennbar: Von der Zieldefinition über die Architektur und Datenverarbeitung bis hin zur Cloud-Deployment-Infrastruktur. |
| Nachvollziehbarkeit Inhalt, Demonstration | Alle Schritte des End-to-End-Projekts wurden nachvollziehbar vermittelt. Die Projektstruktur ist klar gegliedert, mit einer sauberen Trennung nach Komponenten wie Backend, Frontend und Modell. Für die Datenerfassung wurde ein eigener Scrapy Spider genutzt, der sinnvolle Merkmale wie Zimmeranzahl, Wohnfläche, Preis und Standort extrahiert. In der Modellierungsphase wurden verschiedene Regressionsverfahren getestet. Das beste Modell wurde automatisch versioniert und in Azure Blob Storage hochgeladen. Zwei GitHub Actions Pipelines übernehmen das Training und Deployment vollständig automatisiert. Die Anwendung wurde containerisiert und auf Azure bereitgestellt. Zudem wurde die Benutzeroberfläche so gestaltet, dass ungültige Eingaben erkannt und dem Benutzer entsprechende Hinweise gegeben werden. |

## Screencast 2

|       | Bitte ausfüllen |
|-------|-----------------|
| Review durch (ZHAW-Kürzel) | ravinsen |
| Review von (ZHAW-Kürzel) | herscmat |
| Sprache, Kommunikation, roter Faden | Die Präsentation ist logisch aufgebaut und die Struktur in drei Teilen (Datenquelle, Modell, Live-Demo) wird zu Beginn klar angekündigt und eingehalten. Die Sprache ist durchgängig verständlich. Fachbegriffe wie Random Forest Regressor, MongoDB, Scrapy Spider, Docker Image oder GitHub Actions werden korrekt verwendet. Die Kommunikation ist durchdacht, mit klaren Übergängen zwischen den Abschnitten, was dem roten Faden zugutekommt. |
| Nachvollziehbarkeit Inhalt, Demonstration | Technisch wird das Projekt nachvollziehbar umgesetzt: Ein Scrapy Spider extrahiert stündliche Wetterdaten von timeanddate.com, speichert sie als CSV und überträgt sie in eine MongoDB. Ein Random Forest Regressor aus Scikit-Learn sagt die Durchschnittstemperatur für bis zu sieben Tage voraus. Das Preprocessing bereinigt Einheiten und formatiert die Daten. Zwei GitHub Actions Workflows automatisieren das Training und das Deployment der Docker-basierten Anwendung auf Azure. In der Demo wird die Webanwendung erfolgreich gezeigt inklusive konkreter Vorhersagen. |

## Screencast 3

|       | Bitte ausfüllen |
|-------|-----------------|
| Review durch (ZHAW-Kürzel) | ravinsen |
| Review von (ZHAW-Kürzel) | maniyman |
| Sprache, Kommunikation, roter Faden | TODO |
| Nachvollziehbarkeit Inhalt, Demonstration | TODO |

## Screencast 4

|       | Bitte ausfüllen |
|-------|-----------------|
| Review durch (ZHAW-Kürzel) | ravinsen |
| Review von (ZHAW-Kürzel) | selimdri |
| Sprache, Kommunikation, roter Faden | Die Präsentation ist verständlich und frei gesprochen, mit einem sachlichen und authentischen Ton. Die einzelnen Komponenten – Datenquelle, Datenverarbeitung, Modellierung, Deployment – werden in einer sinnvollen Reihenfolge vorgestellt. Durch die natürliche Erzählweise entsteht ein erkennbarer roter Faden. |
| Nachvollziehbarkeit Inhalt, Demonstration | Die Präsentation bietet einen guten Einblick in alle wesentlichen Teile des Projekts. Die Datenquelle (Transport API), das Ziel (Verspätungsvorhersage), das Modell (lineare Regression), sowie das Preprocessing (Umrechnung von Zeitangaben, Encoding) werden transparent erläutert. Die technische Umsetzung mit MongoDB, Docker und Flask wird in der Demo gut veranschaulicht. Zwar funktioniert der GitHub Actions Workflow nicht vollständig, dennoch werden sowohl der lokale Containerbetrieb als auch die Azure-Einbindung nachvollziehbar gezeigt. Die UI-Demo mit konkretem Beispiel rundet die Präsentation gelungen ab. |
