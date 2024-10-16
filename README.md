**Projektbeschreibung**
die Eingangsdatei wird mit dem Python Skript emobpy erstellt
-> https://emobpy.readthedocs.io/en/latest/index.html

Dieses Python-Skript modifiziert die Ladeprofile von Elektrofahrzeugen basierend auf Hochpreisphasen (HT-Phasen) und speichert die Ergebnisse in neuen CSV-Dateien. Die Hochpreisphasen sind vorgegeben, und die Ladeleistung in diesen Phasen wird verschoben, um die Netzlast zu optimieren. Werte aus den Hochpreisphasen werden in spätere, günstigere Zeiträume verschoben.

////////////**Funktionsweise**

Das Skript liest CSV-Dateien aus einem angegebenen Input-Ordner, die Ladeprofile enthalten. In den Dateien wird geprüft, ob bestimmte Zeiten in Hochpreisphasen (HT) fallen. Die Ladeleistung in diesen Phasen wird auf 0.0 gesetzt und in den folgenden Zeiträumen nach der HT-Phase eingefügt. Dabei werden alle Ladeleistungen, die mit 0,0 beginnen, übersprungen, um eine optimierte Verschiebung sicherzustellen.

Für jede ITEM_X-Spalte in den CSV-Dateien wird eine neue ITEM_X_Mod-Spalte erstellt, in die die verschobenen Werte eingetragen werden. Zusätzlich wird eine Sum-Spalte erstellt, die die Summe der ursprünglichen Werte und der verschobenen Werte enthält. Falls diese Summen einen definierten Maximalwert überschreiten (z.B. 2.5), wird die Differenz degressiv auf die folgenden Zeilen verteilt.

Verzeichnisse und Pfade

	•	Input-Ordner: /Users/florianliebenguth/Desktop/Programming/emobpy_modifyer/Input_Mod
	•	Output-Ordner: /Users/florianliebenguth/Desktop/Programming/emobpy_modifyer/Output_Mod

Das Skript liest alle Dateien im Input-Ordner, verarbeitet sie und speichert die modifizierten Dateien im Output-Ordner.

//////////////Eingabeformat

	•	Die Eingabedateien sind CSV-Dateien, die Semikolon als Trennzeichen und Komma als Dezimaltrennzeichen verwenden.
	•	Die CSV-Dateien enthalten keine Kopfzeilen (Spaltenüberschriften).
	•	Jede Datei besteht aus einer Datum-Spalte und mehreren ITEM_X-Spalten, die die Ladeprofile für verschiedene Zeitpunkte enthalten.

///////////////Beispiel einer Eingabedatei:
01.01.2024 00:00;0,5;0,7;0,6
01.01.2024 01:00;0,6;0,7;0,6
...
//////////////	1.	Abhängigkeiten installieren:
Stelle sicher, dass Python und Pandas installiert sind. Verwende ggf. den folgenden Befehl, um Pandas zu installieren:
pip install pandas
//////////////	2.	Ordnerstruktur einrichten:
	•	Erstelle die Verzeichnisse Input_Mod und Output_Mod in deinem Projektordner.
	•	Lege die zu verarbeitenden CSV-Dateien im Input_Mod-Ordner ab.
//////////////// Anpassungen

	•	Hochpreisphasen: Die Hochpreisphasen sind derzeit fest auf 06:00–09:00 und 18:00–20:00 Uhr eingestellt. Du kannst diese Zeiträume in der Funktion check_high_tariff anpassen, falls nötig.
	•	Maximale Summe: Das Skript begrenzt die Ladeleistung auf 2.5. Dies kann im Code angepasst werden, indem der Wert von max_value geändert wird.
