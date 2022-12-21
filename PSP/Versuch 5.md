### Gemeinsame Speicher:
- Interprozesskommunikation
- Kommunikationsschnittstelle
	- gemeinsame Speicher
	- allozierte Speicherbereiche
	- konsistenz betreuen

#### Zugriffskonflikte bei gemeinsame Speicher:
- read-before-write
- write-before-read
- write-before-write
- aktive Bereiche: geöffnet
- inaktive Bereiche: geschlossen

#### Integration in SPOS:
- Allokationstabellen-Protokoll erweitern
- sh_malloc und sh_free: entsprechend für den gemeinsamenspeicher
- sh_read : kopiert Inhalt von gemeinsame Speicher in privaten Speicher
- sh_write : kopiert Inhalt von privaten Speicher in gemeinsame Speicher

#### Blockierte Prozess:
- Synchronisationsmechanismen
- Optionen:
	- Active waiting: verschwendet Rechenzeit
	- Critical Sections: Erlaubt nur einen Lese Vorgangs
- Scheduler bricht manuell blockierte Prozesse

#### Referenzierung von gemeinsame Speicher:
- Zugriffsfunktionen mit MemAddr*
- MemAddr: Address eines Speicherbereichs
- MemAddr*: Addresse wo MemAddr gespeichert ist
	- Vermeidet undefinierte Zustände beim Zugriff auf gemeinsame Speicher

#### Multilevel-Feedback-Queue
- Priotätsklassen
- Werteschlange für jede Klasse
- Round-Robin 
- höhe Prio = weniger Zeitscheiben
- jeder Aufruf = Zeitscheibe -1
- falls Zeitscheibe = 0
	- Dann verschieben eine Klasse runter

#### Implementation:
- os_yield: Ermöglicht einem Prozess, seine Rechenzeit früh abgeben
	- als kritischer Bereich
	- TIMER2_COMPA_vect() ruft den Scheduler durch einen Interruptserviceroutine
	- Dazu wird der Prozess blockiert. OS_PS_BLOCKED
	- anpassen beim Dispatcher (OS_kill zum Teil ersetzen)
