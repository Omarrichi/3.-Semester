#### Lernziele:
- Verschiedene Speicherarten von Atmega 644
- dynamische Speicher *Heap*

##### Grundlagen:

- 64 kByte Flashspeicher:
	- nicht flüchtig
	- elektrisch
	- begrenzt schreibar
		- 10k Schreib und Löschzykeln (Atmega)
	- Über Sektoren (Blöcke mit vielen Bits)
		- Position der Bits entscheidet Dauer
	- Speichert mehrere Programme
		- Daten die sich während der ausführung nicht geändert werden
- 4 kByte SRAM:
	- flüchtig
	- wahlfreiem Zugriff
	- unbegrenzt schreib und lesbar
		- konstante Zeit
	- sehr schnell
	- Speichert häufig zugegriffene Daten und häufig veränderte Daten

### Dynamische Speicher:

- Speicherbereich im RAM
- Bietet Speicherblöcke für Prozesse (beliebige Größe)
- Alle Blöcke sind zusammen in einem großen Speicher
- Benötigt eine Speicherverwaltung 
- **Memory Leak**: Prozesse geben Blöcke nicht wieder ab (speicher verringert sich)

##### Allokationstrategien:
- Bits in einem Array
- First Fit

##### Dynamsiche Speicher in SPOS:

- **Heap Map:**
	- Allokationstabelle (im Heap)
		- Nibbles oder Halbbytes (vier Bytes)
	- Ein Tabellen Byte $\rightarrow$ 2 Nutzdaten Bytes
		- Tabellengröße * 2 = Nutzdatengröße
	- Jeder Byte Nutzdaten kann 16 verschiedene Zustände zugeordnet werden
	- Hochwertige Nibbles in der Tabelle $\rightarrow$ niedrigeste Adresse in den Nutzdaten
- Speicherblöcke werden von einem Protokoll an Prozessen zugewiesen.
- Es gibt 8 Prozesse (7+Idel)
- Nibble Wert:
	- 0: Frei
	- i: zugewiesen an Prozess i
	- F Fortlaufen der Speicher von davor
- **__heap_start:** liegt am Am Anfang der Dynamischen Speicher.
	- mit ihrer Adresse kann man den Anfang des Heaps vergleichen
- damit überprüfen ob genug Sicherheitsabstand liegt
	- nicht direkt prüfen, da LCD auch init werden muss noch

##### Speicherverwaltung:

- Obere Schicht:
	- bearbeitet Speicheranfragen durch Memory Funktionen
- Untere Schicht:
	- Treiber für direkter Zugriffe auf das Speichermedium
	- Für jedes Medium eigens Speicher
	- Teil des Haupttreibers (sind parameter; Funktionen der obere Schicht übergegeben werden)
- Speichertreiber:
	- Instanzen der untere Schicht
	- enthalten Informationen über das verwendete Speichermediums
		- Größe von SM
		- verfügbaren Speicherräume
		- Funktionen zur Initialisirung des Mediums
		- Funktionen zum direkten Schreiben und Lesen von Bytes

**Treiber:**
- Eine Struktur
	- enthält: Funktionszeiger und char. Werte des Mediums
	- jedes Medium muss eine Instanz davon haben
	- Zeiger ist 16 Bits (MemAddr) (Speicheratome)
		- MemValue ist 8 Bits (für einzelne Speicheratome)

**Heaptreiber:**
- überliegende Speicher Verwaltung des Speichermedium
- Unterscheidliche Speicherverwaltungen auf einem gemeinsamen Speichermedium realisiert werden
- Startadresse und größe von Map und Use-Bereich