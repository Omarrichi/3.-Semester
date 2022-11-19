### Scheduler / Stack:
- Verwaltung von Programm und Prozessen
- Prozess-Scheduling
- Verwaltung des verfügbaren Speichers 

#### Scheduler:
- In regelmäßigen Zeitabständen:
	- unterbricht Prozessen und Prozessorziet neutilen

**Beriebsystem: SPOS**
- Kern:
	- Scheduling und Speicherverwaltung
- Treiber:
	- Steuerung eines LCDs
- Anwendungen:
	- Systemfunktionen benutzen


## Scheduler implementieren:
- quasi-gleichzeitige ausführen von mehreren Prozessen
- grundlegende Funktionalitäten und Datenstrukturen

---
### Programme und Prozesse:

- Programm: Endliche Folge von Operationen
- Prozess: Instanz eines Programms
	- durch Laufzeitkontext verwaltet
- Laufzeitkontext: Summe der Prozessorregister
	- zu einem Zeitpunkt den Ausfürhrungszustand eines Prozesses abbilden.
- Multitasking Betriebsystem: 
	- jede Programminstanz hat eigene Prozess und Laufzeitkontext
		- Jedes Programm kann seperat ausgeführt werden.

### Scheduler: 
- transparent Prozessorzeit verwalten und Stackspeicher zuteilen
- Prozess erkennt nicht, dass er unterbrochen wurde
- Leerlaufprozess


### Schedulingstrategien:

- Even:
	- Läuft alle Prozesse aufsteigend, und sorgt dafür, dass alle gleichmäßig Prozessorzeit bekommen
- Random:
	- Zufällig auswählen, trotzdem Gleichverteilung
- RunToCompletion:
	- Prozess läuft bis er terminiert (Aufsteigend)
- RoundRobin: 
	- Jede Prozess bekommt einen Priority, bei jedem Durchlauf dekremntieren der Priority
- InactiveAging:
	- Neben Prio bekommen die auch eine inactive counter
	- Bei jedem inactive erhöht sich der counter, sodass niedriger Prio trotzdem ausgeführt werden
	- Initiale Alter ist entsprechend der Prio


### Kritische Bereiche:

- Exclusiver Zugriff auf bestimmte Betriebsmittel

### Stack:

- LIFO
- PUSH, POP

##### Prozessstacks:

- Speicherung lokaler Variablen und Rücksprungsadressen 
- Prozessregister PC (Programm Counter ... Programmzähler):
	- Pointer auf die nächste Instruktion
- Stack Overflows: 
	- Stackinkonsistenzen, zuviele Werte überschreiben andere Stacks oder Datenbereiche.
	- Erkennen durch Prüfsumme

### Speicherverwaltung

- globale Variablen
- Heap
- Systemstacks
- Prozessstacks