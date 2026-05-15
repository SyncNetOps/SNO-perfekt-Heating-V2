# **🛠️ Entwickler-Dokumentation: SNO-perfekt-Heating V2.4.0**

**Zweck:** Technische Referenz für zukünftige Entwickler, Contributor und Wartungsarbeiten am Blueprint. Dieses Dokument erklärt die architektonischen Designentscheidungen, die Logik-Engine und die spezifischen Neuerungen in V2.4.0.

## **1\. Architektur-Paradigma**

Der Blueprint nutzt bewusst den mode: restart. Um Netzwerk-Spam (insbesondere in Zigbee/Z-Wave Mesh-Netzwerken) zu verhindern und die Stabilität zu maximieren, nutzt die Automatisierung **keine verschachtelten Logikbäume (if/else) in den Actions**.

Stattdessen wird der zukünftige Soll-Zustand (Modus, Temperatur, Helper-Zustände) komplett im variables-Block vorausberechnet. Die action-Sequenz dient lediglich der "stumpfen" Ausführung (Push to Thermostat & Helfer), falls der *aktuelle* Zustand vom *berechneten Soll* abweicht.

## **2\. Kern-Upgrades in V2.4.0 (Multi-Select & Listen-Handling)**

Die wichtigste Neuerung in V2.4.0 ist die native Unterstützung von Listen (Arrays) für Thermostate (climate\_entity) und Fenstersensoren (window\_sensor) durch multiple: true in den UI-Selektoren.

### **2.1. Die expand() Funktion**

Um maximale Abwärtskompatibilität zu gewährleisten, wird die Jinja-Funktion expand() genutzt. Sie ist extrem mächtig, da sie verschiedene Datentypen nahtlos verarbeitet:

* Ein einzelner String (z.B. climate.wohnzimmer)  
* Eine Liste von Strings (z.B. \['climate.w1', 'climate.w2'\])  
* Eine Home Assistant Gruppe (Helfer)  
  Die Logik in is\_window\_open und in der Action-Condition für das Thermostat bricht die Inputs mittels expand() auf die atomaren Entitäten herunter und wertet diese aus.

### **2.2. Smarter Netzwerk-Schutz (Namespace Loop)**

Da state\_attr(climate\_entity, 'temperature') bei einer Liste fehlschlägt, wurde die Condition in Action 5 neu geschrieben. Es wird über alle ausgewählten Thermostate iteriert. Ein namespace wird genutzt, um den Scope der Variable innerhalb der Jinja-Schleife zu erhalten:

{% set target \= calc\_target\_temp | float(-99) %}  
{% set ns \= namespace(update\_needed=false) %}  
{% for state in expand(climate\_entity) %}  
  {% set curr \= state.attributes.temperature | float(-99) %}  
  {% if curr \!= target %}  
    {% set ns.update\_needed \= true %}  
  {% endif %}  
{% endfor %}  
{{ ns.update\_needed }}

**Ergebnis:** Der Funkbefehl wird nur gesendet, wenn *mindestens ein* Thermostat der Gruppe noch nicht den korrekten Zielwert hat.

## **3\. Die Prioritäten-Engine (Variables)**

Die Kette wird *strictly top-to-bottom* im variables-Block ausgewertet.

1. **base\_mode**: Prüft die Status-Variablen in fester Reihenfolge: is\_manual \-\> is\_summer \-\> is\_vacation \-\> is\_extern \-\> is\_away \-\> auto.  
2. **base\_temp**: Lädt die korrespondierende eff\_... (Effective) Temperatur für den festgestellten Modus.  
3. **calc\_target\_temp**: Die finale Instanz. Sie überschreibt base\_temp zwingend, falls is\_window\_open \== true UND der berechnete base\_mode in der User-Erlaubnisliste (window\_active\_modes) steht.

## **4\. Trigger & Auto-Reset Logik**

Timer (delay) in Automatisierungen mit mode: restart sind ein Anti-Pattern.

* **TemplateSyntaxError Fix:** Da HA verbietet, \!input direkt in Jinja-Triggern zu nutzen, werden im Block trigger\_variables sichere Kopien der Inputs erzeugt.  
* **Asynchrone Prüfung:** Die Auto-Reset-Funktionen prüfen asynchron über das Attribut last\_changed der Status-Entität, wie lange ein Schalter bereits aktiv ist.  
* **Execution:** Löst ein Reset-Trigger aus, schaltet Action 0 den Helper hart auf off und beendet den aktuellen Durchlauf mit stop:. Der Blueprint startet danach sofort neu, getriggert durch die Statusänderung des Helpers.

## **5\. Leitfaden für zukünftige Erweiterungen**

Wenn ein neuer Modus (z.B. "Party-Modus") hinzugefügt wird, müssen folgende Schritte zwingend eingehalten werden:

1. **UI-Inputs definieren:** In einer bestehenden oder neuen Sektion einkapseln.  
2. **Variablen registrieren:** Input im variables-Block mappen (Niemals \!input direkt in Jinja-Templates verwenden\!).  
3. **Effective Temp (eff\_party):** Variable für die Temperatur-Fallback-Logik erstellen (Input-Entität vs. statischer Regler).  
4. **Status Check (is\_party):** Variable für den Aktivitätsstatus des Schalters erstellen.  
5. **Logik-Kette anpassen:** In base\_mode, base\_temp und status\_string an der gewünschten hierarchischen Stelle einfügen.