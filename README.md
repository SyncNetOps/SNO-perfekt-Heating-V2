# 🌟 SNO-perfekt-Heating

**Die ultimative, intelligente Heizungssteuerung für Home Assistant.**

SNO-perfekt-Heating (Pro-Edition V2.4.0) ist ein fortschrittlicher Home Assistant Blueprint, der deine Heizungssteuerung auf ein neues Level hebt. Er kombiniert Tageszeitpläne, Anwesenheitserkennung, dynamische Fenster-Sensoren, Urlaubslogik und Jahreszeitensteuerung in einer einzigen, leistungsstarken Automatisierung. Anstatt starr nach Uhrzeit zu heizen, passt sich das System dynamisch an deinen Alltag an und maximiert den Komfort bei minimalem Energieverbrauch.

---

## ✨ Features & Vorteile

* **Native Mehrfachauswahl (Neu in V2.4.0):** Steuere mehrere Thermostate oder bündle mehrere Fenstersensoren direkt über ein Dropdown-Menü im Blueprint – ganz ohne vorherige Helfer-Gruppen in Home Assistant anlegen zu müssen!
* **Smartes Listen-Handling & 100% abwärtskompatibel (Neu in V2.4.0):** Dank neuer `expand()`-Logik verarbeitet das System einzelne Entitäten, Multi-Select-Listen und bestehende Helfer-Gruppen gleichermaßen fehlerfrei.
* **Erweiterter Netzwerk-Schutz (Neu in V2.4.0):** Ein intelligenter Loop prüft nun auch bei großen Thermostat-Gruppen für jedes Gerät einzeln ab, ob ein Funkbefehl (Zigbee/Z-Wave) wirklich nötig ist. Das schont Batterien und reduziert Netzwerk-Spam drastisch.
* **Aufgeräumtes Design (Neu in V2.4.0):** Moderne, benutzerfreundliche UI durch logische Sektionen, die nun für eine bessere Übersicht auf mobilen Endgeräten standardmäßig eingeklappt starten.
* **Urlaubsmodus:** Setze die Heizung auf Knopfdruck auf eine definierte Spartemperatur. Deaktiviert sich auf Wunsch nach X Tagen automatisch.
* **Intelligentes Auto-Reset für manuelles Heizen:** Der manuelle Modus kann sich vollautomatisch abschalten – nach einer festgelegten Dauer, zu einer bestimmten Uhrzeit oder sobald alle das Haus verlassen.
* **Dynamische Fenster-Absenkung:** Bestimme selbst, in welchen Betriebsmodi (z. B. Auto, Urlaub, Manuell) geöffnete Fenster die Heizung absenken dürfen.
* **Konfliktfreie Prioritäten-Logik:** Das System weiß jederzeit genau, was zu tun ist (Manuell > Sommer > Urlaub > Fenster > Extern > Abwesend > Auto). Manuelle Eingriffe überschreiben den Sommer-Modus, dieser überschreibt offene Fenster usw.
* **Regler vs. Entität:** Wähle für *jede* Zieltemperatur, ob du einen festen Wert im Blueprint einstellst oder sie dynamisch über eine Dashboard-Entität (z.B. einen Slider) steuern möchtest.
* **Extern-Modus:** Binde externe Heizquellen (wie einen Kamin) ein, um die Hauptheizung automatisch abzusenken.

---

## 🚀 Installation

Du kannst den Blueprint direkt in Home Assistant importieren. Dieser Link greift immer auf die aktuellste Version im `main`-Branch zu:

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FSyncNetOps%2FSNO-perfekt-Heating-V2%2Fblob%2Fmain%2Fsno_perfekt_heating_V2.yaml)

*(Alternativ: Lade die Datei `sno_perfekt_heating_V2.yaml` aus dem GitHub-Repository herunter und speichere sie manuell in deinem Ordner `config/blueprints/automation/`.)*

---

## 📚 Dokumentation & Hilfe

Wir haben umfangreiche Dokumentationen erstellt, um dir die Einrichtung so einfach wie möglich zu machen:

* **[Interaktive FAQ & Guide (HTML)](https://sno.mb222.de/ph-faq/):** Unsere webbasierte Wissensdatenbank mit detaillierten Erklärungen, Diagrammen und Antworten auf alle gängigen Fragen.
* **[Benutzerhandbuch](./Benutzerhandbuch_SNO_perfekt_Heating.md):** Eine Schritt-für-Schritt-Anleitung von der Helfer-Einrichtung bis zur finalen Konfiguration, inkl. Praxisbeispielen zu allen V2.4.0 Features.
* **[Entwicklerdokumentation](./Entwickler-Dokumentation_V2.4.0.md):** Für alle, die die asynchrone State-Engine, die `expand()`-Logik und die Code-Architektur im Detail verstehen wollen.

---

## 🛠️ Voraussetzungen

* Home Assistant (aktuellste Version empfohlen)
* Mindestens eine steuerbare Klima-Entität (`climate`)
* *(Optional)* Helfer-Entitäten (Zahlen, Schalter, Text) für das Dashboard-Erlebnis
* *(Optional)* Präsenzmelder, Fenster-Sensoren oder externe Temperatursensoren

---

**Entwickelt von SyncNetOps für die Home Assistant Community.**
Heize klüger, nicht härter! 🌡️

*(Stand: 16.05.2026)*