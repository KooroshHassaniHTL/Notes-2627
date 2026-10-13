# Netzwerktechnik – Subnetting

## 1. Was ist Subnetting?

**Subnetting** bedeutet, dass man ein großes Netzwerk in mehrere **kleinere Netzwerke (Subnetze)** aufteilt.

Beispiel:

```text
192.168.1.0/24
```

Dieses Netzwerk kann in kleinere Netzwerke aufgeteilt werden, zum Beispiel:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

### Warum macht man Subnetting?

- Netzwerke übersichtlicher machen
- Broadcast-Verkehr reduzieren
- verschiedene Abteilungen trennen
- IP-Adressen sinnvoll verteilen
- Sicherheit und Verwaltung verbessern

---

# 2. Grundaufbau einer IPv4-Adresse

Eine IPv4-Adresse besteht aus **32 Bit**.

Sie wird in **4 Oktette** mit jeweils 8 Bit aufgeteilt.

Beispiel:

```text
192.168.1.10
```

Binär:

```text
11000000.10101000.00000001.00001010
```

Jedes Oktett kann Werte von

```text
0 bis 255
```

haben.

---

# 3. Netzwerkanteil und Hostanteil

Eine IP-Adresse besteht aus:

```text
Netzwerkanteil | Hostanteil
```

Der **Netzwerkanteil** sagt, zu welchem Netzwerk die IP gehört.

Der **Hostanteil** identifiziert das Gerät innerhalb dieses Netzwerks.

Beispiel:

```text
192.168.1.10/24
```

Bei `/24` sind:

```text
24 Bit = Netzwerk
8 Bit  = Host
```

Also:

```text
192.168.1 | 10
 Netzwerk   Host
```

---

# 4. Was bedeutet `/24`?

Die Zahl hinter dem `/` nennt man **Präfixlänge** oder **CIDR-Präfix**.

```text
192.168.1.10/24
```

bedeutet:

> Die ersten 24 Bit gehören zum Netzwerk.

IPv4 hat insgesamt 32 Bit.

Also:

```text
32 - 24 = 8 Host-Bits
```

---

# 5. Subnetzmaske

Zu jedem Präfix gehört eine **Subnetzmaske**.

Wichtige Beispiele:

| Präfix | Subnetzmaske |
|---|---|
| `/8` | `255.0.0.0` |
| `/16` | `255.255.0.0` |
| `/24` | `255.255.255.0` |
| `/25` | `255.255.255.128` |
| `/26` | `255.255.255.192` |
| `/27` | `255.255.255.224` |
| `/28` | `255.255.255.240` |
| `/29` | `255.255.255.248` |
| `/30` | `255.255.255.252` |

### Merke

```text
/24 → 24 Netzwerk-Bits
/25 → 25 Netzwerk-Bits
/26 → 26 Netzwerk-Bits
/27 → 27 Netzwerk-Bits
```

Je **größer** der Präfix ist, desto **kleiner** wird das Subnetz.

---

# 6. Host-Bits berechnen

Die Formel ist sehr wichtig:

```text
Host-Bits = 32 - Präfix
```

Beispiele:

```text
/24 → 32 - 24 = 8 Host-Bits
/26 → 32 - 26 = 6 Host-Bits
/27 → 32 - 27 = 5 Host-Bits
/28 → 32 - 28 = 4 Host-Bits
```

---

# 7. Anzahl der Adressen berechnen

Die Anzahl aller IP-Adressen in einem Subnetz berechnet man mit:

```text
2^Host-Bits
```

Beispiel `/24`:

```text
32 - 24 = 8 Host-Bits

2^8 = 256 Adressen
```

Beispiel `/26`:

```text
32 - 26 = 6 Host-Bits

2^6 = 64 Adressen
```

Beispiel `/27`:

```text
32 - 27 = 5 Host-Bits

2^5 = 32 Adressen
```

---

# 8. Wie viele Hosts sind möglich?

Bei normalen IPv4-Subnetzen sind jeweils:

- **1 Adresse = Netzwerkadresse**
- **1 Adresse = Broadcastadresse**

für normale Hosts nicht verwendbar.

Deshalb:

```text
Hosts = 2^Host-Bits - 2
```

Beispiel `/26`:

```text
2^6 = 64 Adressen

64 - 2 = 62 Hosts
```

Beispiel `/27`:

```text
2^5 = 32 Adressen

32 - 2 = 30 Hosts
```

---

# 9. Die wichtigsten Adressen eines Subnetzes

Jedes Subnetz hat:

### Netzwerkadresse

Die **erste Adresse** des Subnetzes.

Sie bezeichnet das gesamte Netzwerk.

### Broadcastadresse

Die **letzte Adresse** des Subnetzes.

Sie wird verwendet, um alle Geräte im Subnetz gleichzeitig anzusprechen.

### Hostbereich

Alle Adressen zwischen Netzwerkadresse und Broadcastadresse.

---

# 10. Beispiel `/24`

Nehmen wir:

```text
192.168.1.0/24
```

Dann:

```text
Netzwerkadresse:
192.168.1.0

Erster Host:
192.168.1.1

Letzter Host:
192.168.1.254

Broadcast:
192.168.1.255
```

Insgesamt:

```text
256 Adressen
254 nutzbare Hosts
```

---

# 11. Was passiert beim Subnetting?

Wir nehmen:

```text
192.168.1.0/24
```

und wollen daraus **4 kleinere Subnetze** machen.

Dafür müssen wir Host-Bits in Netzwerk-Bits umwandeln.

---

# 12. Wie viele Bits brauche ich?

Wir wollen:

```text
4 Subnetze
```

Wir suchen also:

```text
2^n >= 4
```

Mit:

```text
2^2 = 4
```

brauchen wir **2 zusätzliche Netzwerk-Bits**.

Aus:

```text
/24
```

wird:

```text
/26
```

Denn:

```text
24 + 2 = 26
```

---

# 13. `/26` verstehen

Bei `/26`:

```text
32 - 26 = 6 Host-Bits
```

Anzahl der Adressen:

```text
2^6 = 64
```

Nutzbare Hosts:

```text
64 - 2 = 62
```

Subnetzmaske:

```text
255.255.255.192
```

---

# 14. Wie finde ich die einzelnen Subnetze?

Hier kommt eine der wichtigsten Formeln:

```text
Blockgröße = 256 - relevante Maskenzahl
```

Bei `/26` ist die Maske:

```text
255.255.255.192
```

Also:

```text
256 - 192 = 64
```

Die Subnetze springen deshalb immer um **64**.

```text
0
64
128
192
```

Daraus entstehen:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

---

# 15. Die 4 Subnetze vollständig berechnen

## Subnetz 1

```text
Netzwerk:
192.168.1.0

Erster Host:
192.168.1.1

Letzter Host:
192.168.1.62

Broadcast:
192.168.1.63
```

---

## Subnetz 2

```text
Netzwerk:
192.168.1.64

Erster Host:
192.168.1.65

Letzter Host:
192.168.1.126

Broadcast:
192.168.1.127
```

---

## Subnetz 3

```text
Netzwerk:
192.168.1.128

Erster Host:
192.168.1.129

Letzter Host:
192.168.1.190

Broadcast:
192.168.1.191
```

---

## Subnetz 4

```text
Netzwerk:
192.168.1.192

Erster Host:
192.168.1.193

Letzter Host:
192.168.1.254

Broadcast:
192.168.1.255
```

---

# 16. Übersicht der `/26`-Subnetze

| Subnetz | Netzwerkadresse | Hostbereich | Broadcast |
|---|---|---|---|
| 1 | `192.168.1.0` | `192.168.1.1 - 62` | `192.168.1.63` |
| 2 | `192.168.1.64` | `192.168.1.65 - 126` | `192.168.1.127` |
| 3 | `192.168.1.128` | `192.168.1.129 - 190` | `192.168.1.191` |
| 4 | `192.168.1.192` | `192.168.1.193 - 254` | `192.168.1.255` |

---

# 17. So berechnest du ein Subnetz Schritt für Schritt

Bei einer typischen Prüfungsaufgabe kannst du immer so vorgehen:

### Schritt 1: Präfix anschauen

Beispiel:

```text
192.168.1.77/26
```

---

### Schritt 2: Host-Bits berechnen

```text
32 - 26 = 6
```

---

### Schritt 3: Anzahl der Adressen berechnen

```text
2^6 = 64
```

---

### Schritt 4: Subnetzmaske bestimmen

```text
/26 = 255.255.255.192
```

---

### Schritt 5: Blockgröße berechnen

```text
256 - 192 = 64
```

---

### Schritt 6: Subnetze aufschreiben

```text
0
64
128
192
```

---

### Schritt 7: Prüfen, in welchem Bereich die IP liegt

Die IP ist:

```text
192.168.1.77
```

Die Bereiche sind:

```text
0 - 63
64 - 127
128 - 191
192 - 255
```

`77` liegt zwischen `64` und `127`.

Also:

```text
Netzwerkadresse = 192.168.1.64
```

---

### Schritt 8: Broadcast bestimmen

Das nächste Subnetz beginnt bei:

```text
128
```

Also ist die Adresse davor der Broadcast:

```text
127
```

Damit:

```text
Broadcast = 192.168.1.127
```

---

### Schritt 9: Hostbereich bestimmen

```text
Erster Host = 192.168.1.65
Letzter Host = 192.168.1.126
```

---

# 18. Beispiel komplett

Gegeben:

```text
192.168.1.77/26
```

Gesucht:

- Netzwerkadresse
- Broadcast
- erster Host
- letzter Host
- Anzahl der nutzbaren Hosts

### Lösung

```text
/26

Host-Bits:
32 - 26 = 6

Adressen:
2^6 = 64

Nutzbare Hosts:
64 - 2 = 62

Maske:
255.255.255.192

Blockgröße:
256 - 192 = 64
```

Subnetzbereiche:

```text
0 - 63
64 - 127
128 - 191
192 - 255
```

Die `77` liegt im Bereich:

```text
64 - 127
```

Deshalb:

```text
Netzwerkadresse:
192.168.1.64

Erster Host:
192.168.1.65

Letzter Host:
192.168.1.126

Broadcast:
192.168.1.127

Nutzbare Hosts:
62
```

---

# 19. Weitere wichtige Präfixe

| Präfix | Adressen | Nutzbare Hosts | Maske |
|---|---:|---:|---|
| `/24` | 256 | 254 | `255.255.255.0` |
| `/25` | 128 | 126 | `255.255.255.128` |
| `/26` | 64 | 62 | `255.255.255.192` |
| `/27` | 32 | 30 | `255.255.255.224` |
| `/28` | 16 | 14 | `255.255.255.240` |
| `/29` | 8 | 6 | `255.255.255.248` |
| `/30` | 4 | 2 | `255.255.255.252` |

### Merke

Je größer der Präfix:

```text
/24 → /25 → /26 → /27 → /28
```

desto:

- kleiner wird das Subnetz
- weniger Hosts sind möglich
- mehr Subnetze entstehen

---

# 20. Subnetze aus einem `/24` Netzwerk

Aus:

```text
192.168.1.0/24
```

kann man machen:

### `/25`

```text
2 Subnetze
```

```text
192.168.1.0/25
192.168.1.128/25
```

---

### `/26`

```text
4 Subnetze
```

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

---

### `/27`

```text
8 Subnetze
```

```text
192.168.1.0/27
192.168.1.32/27
192.168.1.64/27
192.168.1.96/27
192.168.1.128/27
192.168.1.160/27
192.168.1.192/27
192.168.1.224/27
```

---

# 21. Die Zweierpotenzen, die man kennen sollte

Beim Subnetting sind diese Zahlen besonders wichtig:

| Potenz | Ergebnis |
|---|---:|
| `2^0` | 1 |
| `2^1` | 2 |
| `2^2` | 4 |
| `2^3` | 8 |
| `2^4` | 16 |
| `2^5` | 32 |
| `2^6` | 64 |
| `2^7` | 128 |
| `2^8` | 256 |

Diese Zahlen helfen beim schnellen Rechnen.

---

# 22. Subnetting mit benötigten Hosts

Manchmal lautet die Aufgabe nicht:

> "Erstelle 4 Subnetze"

sondern:

> "Wir brauchen mindestens 50 Hosts pro Subnetz."

Dann musst du herausfinden, wie viele Host-Bits notwendig sind.

Gesucht:

```text
2^h - 2 >= 50
```

Probieren:

```text
2^5 - 2 = 30
```

Zu wenig.

```text
2^6 - 2 = 62
```

Genug.

Also brauchen wir:

```text
6 Host-Bits
```

Damit bleiben:

```text
32 - 6 = 26 Netzwerk-Bits
```

Ergebnis:

```text
/26
```

Ein `/26`-Netz kann also **62 Hosts** aufnehmen.

---

# 23. Subnetting mit benötigten Subnetzen

Beispiel:

> Aus einem `/24`-Netz sollen mindestens 8 Subnetze entstehen.

Gesucht:

```text
2^n >= 8
```

Da:

```text
2^3 = 8
```

benötigen wir **3 zusätzliche Bits**.

Also:

```text
/24 + 3 = /27
```

Ergebnis:

```text
/27
```

---

# 24. Unterschied: Subnetze vs. Hosts

Das ist sehr wichtig:

### Anzahl der Subnetze

```text
2^entliehene Bits
```

### Anzahl der Hosts pro Subnetz

```text
2^Host-Bits - 2
```

Beispiel:

```text
/24 → /27
```

Wir haben 3 Bits ausgeliehen:

```text
2^3 = 8 Subnetze
```

Es bleiben 5 Host-Bits:

```text
2^5 - 2 = 30 Hosts pro Subnetz
```

---

# 25. Binärdarstellung der Subnetzmaske

Um Subnetting richtig zu verstehen, hilft die Binärdarstellung.

Beispiel `/26`:

```text
11111111.11111111.11111111.11000000
```

Das bedeutet:

```text
26 Netzwerk-Bits
6 Host-Bits
```

In Dezimal:

```text
255.255.255.192
```

---

# 26. Wichtige Bitwerte eines Oktetts

Ein Oktett besteht aus 8 Bit:

```text
128 64 32 16 8 4 2 1
```

Beispiel:

```text
11000000
```

Rechnung:

```text
128 + 64 = 192
```

Also:

```text
11000000 = 192
```

Deshalb ist:

```text
/26 = 255.255.255.192
```

Denn im letzten Oktett stehen:

```text
11000000
```

---

# 27. Schnellmethode für Subnetting

Bei vielen Aufgaben musst du nicht jedes Mal alles in Binär umwandeln.

Nutze diese Reihenfolge:

```text
1. Präfix bestimmen
2. Host-Bits berechnen
3. 2^Host-Bits berechnen
4. Subnetzmaske bestimmen
5. Blockgröße berechnen
6. Subnetzgrenzen aufschreiben
7. IP einem Bereich zuordnen
8. Netzwerkadresse bestimmen
9. Broadcast bestimmen
10. Hostbereich bestimmen
```

---

# 28. Häufige Fehler

### Fehler 1: Netzwerkadresse als Host verwenden

Falsch:

```text
192.168.1.64
```

als Host in einem `/26`-Netz.

Das ist die **Netzwerkadresse**.

---

### Fehler 2: Broadcast als Host verwenden

Falsch:

```text
192.168.1.127
```

Das ist die **Broadcastadresse**.

---

### Fehler 3: `2^Host-Bits` als nutzbare Hosts verwenden

Bei `/26`:

```text
2^6 = 64
```

Aber:

```text
64 - 2 = 62 nutzbare Hosts
```

---

### Fehler 4: Netzwerk- und Host-Bits verwechseln

Bei `/26`:

```text
26 Netzwerk-Bits
6 Host-Bits
```

Nicht umgekehrt.

---

# 29. Super-Merksätze

> **IPv4 = 32 Bit**

> **Host-Bits = 32 - Präfix**

> **Adressen = 2^Host-Bits**

> **Nutzbare Hosts = 2^Host-Bits - 2**

> **Mehr Netzwerk-Bits = kleinere Subnetze**

> **Weniger Host-Bits = weniger Hosts**

> **Netzwerkadresse = erste Adresse**

> **Broadcast = letzte Adresse**

> **Hostbereich = alles dazwischen**

---

# 30. Ein Beispiel zum Üben

Gegeben:

```text
192.168.10.145/27
```

Gesucht:

```text
- Subnetzmaske
- Blockgröße
- Netzwerkadresse
- Broadcastadresse
- erster Host
- letzter Host
- Anzahl der nutzbaren Hosts
```

### Lösung

`/27` bedeutet:

```text
32 - 27 = 5 Host-Bits
```

Adressen:

```text
2^5 = 32
```

Nutzbare Hosts:

```text
32 - 2 = 30
```

Maske:

```text
255.255.255.224
```

Blockgröße:

```text
256 - 224 = 32
```

Subnetzgrenzen:

```text
0
32
64
96
128
160
192
224
```

Die IP:

```text
192.168.10.145
```

liegt zwischen:

```text
128 - 159
```

Also:

```text
Netzwerkadresse:
192.168.10.128

Erster Host:
192.168.10.129

Letzter Host:
192.168.10.158

Broadcast:
192.168.10.159

Nutzbare Hosts:
30
```

---

# 31. Wichtigste Prüfungstabelle

| Präfix | Host-Bits | Adressen | Nutzbare Hosts | Blockgröße |
|---|---:|---:|---:|---:|
| `/24` | 8 | 256 | 254 | 256 |
| `/25` | 7 | 128 | 126 | 128 |
| `/26` | 6 | 64 | 62 | 64 |
| `/27` | 5 | 32 | 30 | 32 |
| `/28` | 4 | 16 | 14 | 16 |
| `/29` | 3 | 8 | 6 | 8 |
| `/30` | 2 | 4 | 2 | 4 |

---

# 32. Subnetting in einem Satz

> **Subnetting bedeutet, Host-Bits zu Netzwerk-Bits zu machen, um ein großes Netzwerk in kleinere Netzwerke aufzuteilen.**