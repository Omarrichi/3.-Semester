### Grundlagen der Mikrocontrollerprogrammierung:
- Microcontroller sind Halbleiterchips, die neben dem Prozessor weitere Peripheriefunktionen auf einem Chip vereinen
- main-Methode: Programmseinstiegpunkt
- Programm auf den Mikrocontroller zu übertragen und debuggen (JTAG)

### ATmega 644
- EEPROM
- AD/DA-Wandler
- I/O-Ports
- eine USART schnittstelle
- drei Timer
- Intruppt-Controller


```ad-note
title: 40 Pins -> 32 Ein-/Ausgabe
Vier Organisationseinheiten:
- Ports: A, B, C, D
- von 0 bis 7 durchnummeriert
- Data Direction-Register (DDR)
- Port Output-Register (PORT)
- Port Input-Register (PIN)
	- Konfiguration der Pins
```


##### Data Direction Register:
- Port A: Data Direction Register (DDRA)
- Welche Pins eines Ports zur Ein-/Ausgabe verwendet werden.
- DDRA0 : ist erste Stelle als Eingang 
	- Analog mit DDRA1 für Ausgang

##### Data Register:
- Port A: Data Register
- Falls Pin Ausgabe:  PORTA: welche Signale ausgegeben werden
- Falls Pin Eingabe:  PORTA um Pullup-Wiederstand zu kontrollieren

##### Input Pins:
- Port A Input Pins-Register PINA: Auslesen externer Signale

---

- *Zur Änderung einzelner Bits benötigt man Bitmasken*
	- werden in hex oder bin eingegeben
	- mit führenden Nullen (Größe)
	- Binäre Operatoren | und & werden einzelen Bits geändert

*Button gedruckt Zustand 0*
*Button nicht gedruckt Zustand 1*

---

**Pin D1 als Eingang:**

- Pin D1 als Eingang konfigurieren (also bit 1 von DDRD auf 0 setzen)
```C
DDRD &= 0b11111101;
```

-  Pullup -Widerstand an Pin D1 aktivieren (Bit 1 von PORTD auf 1 setzen)
```C
PORTD |= 0b00000010;
```

-  Pin D1 auslesen (Bit extrahieren und nach rechts verschieben)
```C
uint8_t pinState = (PIND & 0b00000010) >> 1;
```

**Pin D1 als Ausgang:**

-  Pin D1 als Ausgang konfigurieren (Bit 1 von DDRD auf 1 setzen)
```C
DDRD &= 0b00000010;
```

- Logische 1 an Pin D1 ausgeben (Bit 1 von PORTD auf 1 setzen)
```C
PORTD &= 0b00000010;
```