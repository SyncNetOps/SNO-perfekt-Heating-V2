# 🌟 SNO-perfekt-Heating

**Die ultimative, intelligente Heizungssteuerung für Home Assistant.**

SNO-perfekt-Heating (Pro-Edition V2.3) ist ein fortschrittlicher Home Assistant Blueprint, der deine Heizungssteuerung auf ein neues Level hebt. Er kombiniert Tageszeitpläne, Anwesenheitserkennung, dynamische Fenster-Sensoren, Urlaubslogik und Jahreszeitensteuerung in einer einzigen, leistungsstarken Automatisierung. Anstatt starr nach Uhrzeit zu heizen, passt sich das System dynamisch an deinen Alltag an und maximiert den Komfort bei minimalem Energieverbrauch.

---

## ✨ Features & Vorteile (Neu in V2.3)

*   **Urlaubsmodus (Neu):** Setze die Heizung auf Knopfdruck auf eine definierte Spartemperatur. Deaktiviert sich auf Wunsch nach X Tagen automatisch.
*   **Intelligentes Auto-Reset für manuelles Heizen (Neu):** Der manuelle Modus kann sich nun vollautomatisch abschalten – nach einer festgelegten Dauer, zu einer bestimmten Uhrzeit oder sobald alle das Haus verlassen.
*   **Dynamische Fenster-Absenkung (Neu):** Bestimme selbst, in welchen Betriebsmodi (z. B. Auto, Urlaub, Manuell) geöffnete Fenster die Heizung absenken dürfen.
*   **Konfliktfreie Prioritäten-Logik:** Das System weiß jederzeit genau, was zu tun ist. Manuelle Eingriffe überschreiben den Sommer-Modus, dieser überschreibt offene Fenster (je nach Einstellung), und diese wiederum überschreiben den normalen Zeitplan. 
*   **Regler vs. Entität:** Wähle für *jede* Zieltemperatur, ob du einen festen Wert im Blueprint einstellst oder sie dynamisch über eine Dashboard-Entität (z.B. einen Slider) steuern möchtest.
*   **Multi-Fenster & Extern-Modus:** Bündle beliebig viele Fenstersensoren in einer Gruppe. Binde externe Heizquellen (wie einen Kamin) ein, um die Hauptheizung automatisch abzusenken.
*   **Batterieschonend:** Eine hochgradig optimierte Jinja2-State-Engine berechnet den Sollzustand und sendet nur dann Funkbefehle (Zigbee/Z-Wave), wenn sich die Zieltemperatur tatsächlich geändert hat.
*   **Aufgeräumtes Design:** Modernes UI durch in logische Sektionen unterteilte Eingabemasken.

---

## 🚀 Installation

Du kannst den Blueprint direkt in Home Assistant importieren. Dieser Link greift immer auf die aktuellste Version im `main`-Branch zu:

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FSyncNetOps%2FSNO-perfekt-Heating-V2%2Fblob%2Fmain%2Fsno_perfekt_heating_V2.yaml)

*(Alternativ: Lade die Datei `sno_perfekt_heating_V2.yaml` aus dem GitHub-Repository herunter und speichere sie manuell in deinem Ordner `config/blueprints/automation/`.)*

---

## 📚 Dokumentation & Hilfe

Wir haben umfangreiche Dokumentationen erstellt, um dir die Einrichtung so einfach wie möglich zu machen:

*   **[Interaktive FAQ & Guide (HTML)](https://sno.mb222.de/ph-faq/):** Unsere webbasierte Wissensdatenbank mit detaillierten Erklärungen, Diagrammen und Antworten auf alle gängigen Fragen (inklusive V2.3 Features).
*   **Benutzerhandbuch:** Eine Schritt-für-Schritt-Anleitung von der Helfer-Einrichtung bis zur finalen Konfiguration, inkl. Praxisbeispielen.
*   **Entwicklerdokumentation:** Für alle, die die asynchrone State-Engine, die `trigger_variables` und die Code-Architektur im Detail verstehen wollen.

---

## 🛠️ Voraussetzungen

*   Home Assistant (aktuellste Version empfohlen)
*   Mindestens eine steuerbare Klima-Entität (`climate`)
*   *(Optional)* Helfer-Entitäten (Zahlen, Schalter, Text) für das Dashboard-Erlebnis
*   *(Optional)* Präsenzmelder, Fenster-Sensoren oder externe Temperatursensoren

---

**Entwickelt von SyncNetOps für die Home Assistant Community.**
Heize klüger, nicht härter! 🌡️