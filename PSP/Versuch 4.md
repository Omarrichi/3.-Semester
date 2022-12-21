- Externerspeicher (23LC1024)
- 128 KiB extra SRAM
- Mit SPI verbunden (Serial Peripheral Interface)

**Lernziele:**
- Spezifikation des Serial Peripheral Interface
- Selbständiger Umgang mit Datenblättern
- Protokoll des 23LC1024
- Größenänderung dynamischer Speicherbereiche
- Weitere Strategien zur Allokation von Speicher

### Grundlagen
- SPI: Bussystem für den Seriellen Datenaustausch
- wird gestuert von einem Master:
	- Slaves sind Peripherie
	- Master entscheidet wer Kommunizieren darf
- In der Regel beliebig viele Slaves
	- hier nur der Speicher
- Busteilnehmer haben gemeinsame Steuerleitungen:
	- Clock (CLK)
	- Master-out-Slave-in (MOSI)
	- Master-in-Slave-out (MISO)
- Slaves: haben exclusive Leitungen zum master
	-  Chip Select (CS): ist active los $\overline{CS}$
- SPI ist Synchron und seriell
	- bits werden nacheinander gesendet
	- Clockleitung synchronisiert die Übertragung
- vom Master zur Slave (MOSI)
	- umgekehrt (MISO)
- Bei Übertragung werden stets vom beide Seiten Daten übermittelt (nicht sinnvoll)

#### Clock Timing

- Rechtsecksignale vom Master
	- Taktfrequence des Busses
- Datenleitungauslesen
	- nur bei Signalflanke des Clocks
- 4 SPI Modi:
	- aus zwei binären Einstellungen
	- Polarität
	- Phasenlage
- Polarität neutrale Signalzustand der Clockleitung
- Phasenlagen sagt wann ausgelesen werden soll
	- leading edge oder Trailing edge

#### Bitreihenfolge:
- muss spezifiziert werden ob der erste gesendete bit:
	- Least-Significant-Bit (LSB)
	- Most-Significant-Bit (MSB)

#### SPI-Modul im ATmega 644
- 3 Register:
	- SPI control Register (SPCR)
		- Konfiguration
	- SPI Status Register  (SPSR)
		- Konfiguration
	- SPI Date Register (SPDR)
		- Datenübertragung
- SPIE SPI Interrupt Enable
- DDRD Dataorder (Bitreihenfolge)
- CPOL Polarität
- CPHA Phasenlage
- SPR1, SPR0, SPI2X Clock Rate Select und Double Speed 
- SPIF SPI Interrupt Flag

#### SRAM-Baustein