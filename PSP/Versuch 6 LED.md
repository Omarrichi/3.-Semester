### LED-Matrix
- 32 x 32 Pixel
	- eigene Steuerleitungen (RGB)
- 3072 Leitungen
	- Latch-Bausteine
	- Schiebregister
	- Decoder

#### Latch-Baustein:
- Zwischenspeichern mehrere Bits
- Dateneingänge = Datenausgänge
- Steuerleitung: $\textit{Latch enable}$ (LE)
	- LE = 1 $\Rightarrow$ Eingänge auf Ausgänge durchgeschaltet
	- LE = 0 $\Rightarrow$ Ausgangspins bleiben konstant 

#### Schiebregister: 
- n-Bit Schiebregister speichert n Bits.
- Jeden Bit $\Rightarrow$ Ausgangpin
- einen Eingangspin
- Steuerleitung $\textit{Clock}$ (CLK)
- Steigende Flanke:
	- Signal am Eingangspin in die erste Stelle des Schiebregisters eingelesen
	- jedes gespeicherte Bit wird um eine Stelle verschoben
	- das letzte Bit wird verworfen

#### Decoder:
- n Decoder
- n Eingangspins
- $2^n$ Ausgangspins
- Eingangspin x als Binärzahl
- x+1-ten Ausgangspin eine logische 1, Rest 0

#### Gesamtverschaltung:
- Zwei Zeilen gleichzeitig leuchten
- Vollbild bei sehr schnelle hintereinander ansteuerung von allen Zeilen
- Zwei leuchtende Zeilen müssen um 16 Zeilen verschoben werden.
- Insgesamt gibts es 16 Doppelzeilen $\Rightarrow 2^4$ also vier Eingänge
	- zum wählen der Doppelzeilen
	- 4-Bit Decoder verbindet die Kathoden der LEDs der Doppelzeile mit Ground
		- damit nur diese Leuchten.
- Beim Wählern von Doppelzeile:
	- 192 Leitungen werden beschaltet
		- 2 Zeilen 32 Pixel x 3 LEDs
	- mithilft von 12 MB15024-Chips
		- jeweils 16 Leitungen
- MB15024:
	- 16-Bit Schiebregister
	- Dateneingang (SDI)
	- Clockeingang (CLK)
	- 16 Ausgänge (OUT0 bis OUT15)
	- Ausgang (SDO)
	- Inhalte des Schiebregisters $\Rightarrow$ nicht direkt auf den Ausgängen ausgegeben, sondern sind mit einem 16-Bit Latch verbunden
		- LE von Latch ist verbunden am MB15024 als Eingangspin
		- Ausgänge des Latches sind verbunden mit einem Output Driver
		- passt die Spannungen für die LEDs an
		- Wird gesteuert von der invertierte Leitung $\overline{OE}$ (Output Enable)

### Aktualisierung einer Doppelzeile:
- 6 Dateneingänge (R1,G1,B1,R2,G2,B2)
	- RGB für Farben, 1 ist für Zeile von 0 bis 15 
	- 2 für Zeile von 16 bis 31
- Jeder Dateneingang mit SDI eines MB-Chips verbunden, der mit weiteren MB-Chip verkettet ist.
	- mit einem SDO-Ausgang
	- 16-Bits zweier Chips wie 32-Bit Schiebregister
	- Ausgänge der Chips sind mit dem LEDs der passende Hälfte und Farbe verbunden.
- Aktualisierung: 
	- Eine neue Doppelzeile auswählen
	- 6 Bits an die Ausgänge der Matrix anlegen
	- Clock und Schiebregister auf 1 und dann wieder auf 0
		- Bits einlesen damit
		- 32 mal wiederholen (für alle 192 bits )
	- Inhalts des Schiebregisters im Latchbaustein speichern.
		- LE = 1  danach wieder auf 0
	- aktivieren von $\overline{OE}$
		- gespeicherte Inhalte auf die LEDs geben
	- Eingänge: CLK, LE $\overline{OE}$ aller Chips sind zusammengeführt und Eingangspinsder Matrix

### Joystick:
- Druch zwei Potentiometer realisiert
	- Spannungsteiler zwischen $V_{CC} (5V)$ und Ground $(0V)$
	- Jeder liefert ein analoges Signal
	- Ruhe Position $\Rightarrow 2,5V$ Spannung am Ausgang

#### AD-Wandler:
- A-D-Wandlung ist kompliziert $\Rightarrow$  ATmega verfügt nur über einen internen ADC 
- Über einen Multiplexer mit mehreren Pins für mehrere Analoge Signale
- Multiplexer wird über ADMUX konfiguriert