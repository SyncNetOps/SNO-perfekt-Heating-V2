# **📖 Benutzerhandbuch: SNO-perfekt-Heating V2.4.0**

Willkommen beim **SNO-perfekt-Heating** Blueprint\! Diese Pro-Edition bietet dir eine extrem smarte, dynamische und vollständig konfigurierbare Heizungssteuerung für dein Home Assistant.

## **🧠 Das Konzept: Die Prioritäten-Kette**

Die Steuerung funktioniert nach einem strikten "Wer gewinnt?"-Prinzip. Wenn mehrere Situationen gleichzeitig eintreten, gewinnt immer die Situation, die weiter oben in der Liste steht:

1. ✋ **Manuell:** Du drückst einen Knopf? Die Automatisierung gehorcht dir (bis zum Auto-Reset).  
2. ☀️ **Sommer:** Es ist warm genug. Die Heizung geht aus (Fenster werden ignoriert).  
3. 🌴 **Urlaub:** Du bist länger weg. Eine feste Spartemperatur wird gehalten.  
4. 🪟 **Fenster Offen:** Ein Fenster geht auf? Die Heizung wird sofort abgesenkt (konfigurierbar, in welchen Modi das erlaubt ist\!).  
5. 🔥 **Extern (Kamin):** Der Kamin brennt? Die normale Heizung schaltet ab.  
6. 🚶 **Abwesend:** Niemand ist im Haus.  
7. 🕒 **Auto:** Der normale Alltag (Zeitpläne & Raum-Präsenz).

## **🚀 Installation & Einrichtung**

1. **Blueprint importieren:** Lade den Blueprint in dein Home Assistant.  
2. **Automatisierung erstellen:** Gehe zu *Einstellungen \> Automatisierungen*, klicke auf "Automatisierung erstellen" und wähle "SNO-perfekt-Heating".  
3. **UI ausfüllen:** Arbeite dich von oben nach unten durch die Sektionen. Keine Sorge: Alles bis auf die "Klima-Entität" (Sektion 1\) ist optional\!

*(Hinweis: Sektion 1 lässt sich erst einklappen, wenn du mindestens ein Thermostat ausgewählt hast. Das ist ein Sicherheitsfeature von Home Assistant).*

## **⚙️ Die Sektionen im Detail & Praxisbeispiele**

### **1️⃣ Kern-Konfiguration**

Hier legst du das Fundament.

* **Klima-Entität(en):** Wähle ein oder gleich mehrere Thermostate (z.B. Heizkörper & Fußbodenheizung im Wohnzimmer) aus.  
* **Haus- / Raumanwesenheit:** Nutze Bewegungsmelder oder Ping-Sensoren.  
* *Praxisbeispiel:* Wenn dein "Haus-Präsenz"-Helfer auf "Abwesend" (off) schaltet, wartet das System die eingestellte Zeit (z.B. 5 Minuten) und senkt dann die Temperatur auf die "Abwesenheits-Temperatur" (z.B. 16.5°C) ab.

### **2️⃣ Manueller Modus & Auto-Reset**

Manchmal möchte man die Temperatur einfach per Knopfdruck am Dashboard überschreiben.

* **Manueller Schalter:** Lege dir einen "Input Boolean" (Helfer-Schalter) an und wähle ihn hier aus.  
* **Auto-Reset:** Vergessen, den manuellen Modus auszuschalten? Kein Problem.  
* *Praxisbeispiel:* Dir ist kalt. Du aktivierst den manuellen Modus auf 24°C. Dank *Auto-Aus nach Dauer* deaktiviert sich dieser Schalter nach 120 Minuten völlig von selbst und das normale Auto-Programm greift wieder.

### **3️⃣ Urlaubsmodus**

Perfekt für längere Reisen.

* *Praxisbeispiel:* Du fliegst in den Urlaub und aktivierst den Schalter. Die Heizung fällt auf 15°C. Mit *Auto-Aus nach Tagen* (z.B. 14 Tage) ist die Wohnung automatisch wieder warm, wenn du aus dem Flieger steigst, ohne dass du von unterwegs eingreifen musst.

### **4️⃣ Fenster-Erkennung**

Die Heizung soll beim Lüften nicht umsonst feuern.

* **Fenster-Sensor(en):** Wähle hier alle Fensterkontakte des Raumes aus (Mehrfachauswahl möglich\!).  
* **Fenster-Absenkung zulassen in:** Ein genialer Filter\!  
* *Praxisbeispiel:* Im Hochsommer (Sommer-Modus) lüftest du. Ohne diesen Filter würde das System versuchen, auf die "Fenster Offen"-Temperatur zu regeln. Da "Sommer" aber standardmäßig *nicht* in der Erlaubnisliste steht, ignoriert das System im Sommer die Fensteröffnungen komplett\!

### **5️⃣ Sommer & Extern (Kamin)**

Spare Energie in der warmen Jahreszeit oder wenn alternative Wärmequellen aktiv sind.

* **Sommer-Sensor & Schwellwert:** Nutze deinen Außentemperatur-Sensor. Steigt dieser über z.B. 22°C, schaltet das System in den Sommermodus (Heizung aus).  
* **Extern (Kamin):** Wenn dein Temperatursensor an der Wohnzimmerdecke über 28°C meldet (oder du einen Schalter drückst), wird die normale Heizung ausgesetzt, bis der Kamin aus ist.

### **6️⃣ Zeitpläne (Auto)**

Dein digitaler Alltag, aufgeteilt in Morgen, Tag, Abend und Nacht.

* *Praxisbeispiel:* Du stellst "Startzeit Morgen" auf 06:00 Uhr und "Morgen Komfort" auf 21°C. Wenn du aufstehst und den Raum betrittst (*Raumanwesenheit \= on*), heizt das System auf 21°C. Verlässt du den Raum für die Arbeit (*Raumanwesenheit \= off*), fällt die Temperatur auf die "Morgen Eco" Temperatur (z.B. 19°C).

### **7️⃣ Dashboard Status & Helper**

Mache sichtbar, was im Hintergrund passiert\!

* **Status-Text Ausgabe:** Erstelle einen Helfer "Text input" in HA. Der Blueprint schreibt dir hier exakt hinein, was er gerade tut (z.B. 🕒 Auto (Tag | ECO) \- Soll: 19.0 °C oder 🪟 2 Fenster (links, rechts) offen \- Soll: 5.0 °C). Das kannst du dir wunderbar auf deinem Dashboard anzeigen lassen\!