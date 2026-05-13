# 🌟 SNO-perfekt-Heating

**Die ultimative, intelligente Heizungssteuerung für Home Assistant.**

SNO-perfekt-Heating ist ein fortschrittlicher Home Assistant Blueprint, der deine Heizungssteuerung auf ein neues Level hebt. Er kombiniert Tageszeitpläne, Anwesenheitserkennung, Fenster-Sensoren und Jahreszeitenlogik in einer einzigen, leistungsstarken Automatisierung. Anstatt starr nach Uhrzeit zu heizen, passt sich das System dynamisch an deinen Alltag an und maximiert den Komfort bei minimalem Energieverbrauch.

---

## ✨ Features & Vorteile

*   **Konfliktfreie Prioritäten-Logik:** Das System weiß jederzeit genau, was zu tun ist. Manuelle Eingriffe überschreiben den Sommer-Modus, dieser überschreibt offene Fenster, und diese wiederum überschreiben den normalen Zeitplan. Keine überlappenden Befehle mehr!
*   **Regler vs. Entität:** Wähle für *jede* Zieltemperatur, ob du einen festen Wert im Blueprint einstellst oder sie dynamisch über eine Dashboard-Entität (z.B. einen Slider) steuern möchtest. Das System fällt bei fehlender Entität sicher auf den Festwert zurück.
*   **Multi-Fenster & Extern-Modus:** Bündle beliebig viele Fenstersensoren in einer Gruppe. Binde externe Heizquellen (wie einen Kamin) ein, um die Hauptheizung automatisch abzusenken.
*   **Live Status-Ausgabe:** Lass dir in Echtzeit auf deinem Dashboard anzeigen, was die Automatisierung gerade tut (z.B. *"🪟 1 Fenster (Balkontür) offen - Soll: 5.0 °C"* oder *"🕒 Auto (Abend | ECO) - Soll: 18.0 °C"*).
*   **Batterieschonend:** Eine hochgradig optimierte Jinja2-State-Engine berechnet den Sollzustand und sendet nur dann Funkbefehle (Zigbee/Z-Wave), wenn sich die Zieltemperatur tatsächlich geändert hat.

---

## 🚀 Installation

Du kannst den Blueprint direkt in Home Assistant importieren:

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FSyncNetOps%2FSNO-perfekt-Heating-V2%2Fblob%2Fd7b4ff329d2e47bd1ed3ccb812e54776a9bd1d43%2Fsno_perfekt_heating_V2.yaml)

*(Alternativ: Lade die Datei `sno_perfekt_heating_V2.yaml` herunter und speichere sie in deinem Ordner `config/blueprints/automation/`.)*

---

## 📚 Dokumentation & Hilfe

Wir haben umfangreiche Dokumentationen erstellt, um dir die Einrichtung so einfach wie möglich zu machen:

*   **[Interaktive FAQ & Guide (HTML)](https://sno.mb222.de/ph-faq/):** Unsere webbasierte Wissensdatenbank mit detaillierten Erklärungen, Diagrammen und Antworten auf alle gängigen Fragen.
*   **Benutzerhandbuch:** Eine Schritt-für-Schritt-Anleitung von der Helfer-Einrichtung bis zur finalen Konfiguration, inkl. Praxisbeispielen (siehe Dateien im Repository).
*   **Entwicklerdokumentation:** Für alle, die die asynchrone State-Engine und die Code-Architektur im Detail verstehen wollen (siehe Dateien im Repository).

---

## 🛠️ Voraussetzungen

*   Home Assistant (aktuellste Version empfohlen)
*   Mindestens eine steuerbare Klima-Entität (`climate`)
*   *(Optional)* Helfer-Entitäten (Zahlen, Schalter, Text) für das Dashboard-Erlebnis
*   *(Optional)* Präsenzmelder, Fenster-Sensoren oder externe Temperatursensoren

---

**Entwickelt von SyncNetOps für die Home Assistant Community.**
Heize klüger, nicht härter! 🌡️