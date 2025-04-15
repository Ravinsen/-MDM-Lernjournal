# Lernjournal 1 Python
**Modul: Model Deployment & Maintenance**  
**Lernjournal-Thema: News-Keyword Analyzer**  
**Erfasst von: Senthujan Ravindran / ravinsen**

## Repository und Library

| | Bitte ausfüllen |
| -------- | ------- |
| Repository (URL)  |
| Kurze Beschreibung der App-Funktion | XXX |
| Verwendete Library aus PyPi (Name) | flashtext |
| Verwendete Library aus PyPi (URL) | https://pypi.org/project/flashtext/ |
| Weitere Libraries | Flask, Bootstrap, JavaScript (Fetch API) |

## App, Funktionalität
- Die App bietet ein Textfeld zur Eingabe eines beliebigen Nachrichtentextes
- Nach Klick auf „Analysieren“ wird der Text per JavaScript Fetch API an das Flask-Backend gesendet
- Das Backend verwendet die Library `flashtext`, um definierte Keywords im Text zu extrahieren
- Die erkannten Keywords werden unterhalb des Textfelds dynamisch angezeigt

## Dependency Management

- Es wurde ein virtuelles Environment (`venv`) im Projektverzeichnis angelegt
- Abhängigkeiten wurden in `requirements.in` definiert und mit `pip-compile` in `requirements.txt` überführt
- Installierte Pakete mit:
  ```bash
  pip install -r requirements.txt

## Deployment

* [ ] TODO

