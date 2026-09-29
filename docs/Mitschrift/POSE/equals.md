# Java – equals()

## 1. Was ist `equals()`?

`equals()` prüft, ob zwei Objekte **logisch gleich** sind.

> **`equals()` = Sind diese beiden Objekte inhaltlich/logisch gleich?**

`equals()` gibt einen `boolean` zurück:

```java
true
false
```

---

## 2. `equals()` vs. `==`

Diese beiden Vergleiche sind **nicht dasselbe**.

### `==`

Prüft, ob zwei Variablen auf **dasselbe Objekt im Speicher** zeigen.

```java
a == b
```

> Sind es exakt dieselben Objekte?

### `equals()`

Prüft, ob zwei Objekte **inhaltlich gleich** sind.

```java
a.equals(b)
```

> Haben die Objekte dieselben relevanten Werte?

---

## 3. Beispiel

```java
Person original = new Person("Max", date, location);

Person copy = new Person("Max", date, location);
```

Obwohl beide Personen dieselben Daten haben:

```java
original == copy
```

ist:

```text
false
```

weil es zwei verschiedene Objekte sind.

Wenn `equals()` richtig implementiert wurde:

```java
original.equals(copy)
```

kann:

```text
true
```

sein.

---

## 4. `equals()` überschreiben

Die Standardimplementierung von `Object` prüft grundsätzlich die Objektidentität.

Wenn zwei `Person`-Objekte aufgrund ihrer Attribute gleich sein sollen, muss `equals()` überschrieben werden.

Beispiel:

```java
@Override
public boolean equals(Object obj) {

    if (this == obj) {
        return true;
    }

    if (obj == null || getClass() != obj.getClass()) {
        return false;
    }

    Person other = (Person) obj;

    return name.equals(other.name)
        && birthDate.equals(other.birthDate)
        && location.equals(other.location);
}
```

---

## 5. `this == obj`

```java
if (this == obj) {
    return true;
}
```

Prüft, ob beide Referenzen auf **dasselbe Objekt** zeigen.

Wenn ja, müssen die Attribute nicht mehr einzeln verglichen werden.

---

## 6. `obj == null`

```java
if (obj == null) {
    return false;
}
```

Ein Objekt ist nicht gleich `null`.

---

## 7. `getClass()`

```java
if (getClass() != obj.getClass()) {
    return false;
}
```

Damit wird überprüft, ob beide Objekte zur **gleichen Klasse** gehören.

Danach kann das Objekt gecastet werden:

```java
Person other = (Person) obj;
```

---

## 8. Welche Attribute werden verglichen?

Das hängt davon ab, was für die Klasse als **logische Gleichheit** definiert wurde.

Beispiel:

Eine `Person` ist gleich, wenn:

- `name` gleich ist
- `birthDate` gleich ist
- `location` gleich ist

Dann werden diese Attribute in `equals()` verglichen.

---

## 9. `equals()` und `compareTo()`

Die beiden Methoden haben unterschiedliche Aufgaben:

| Methode | Frage | Rückgabe |
|---|---|---|
| `equals()` | Sind die Objekte logisch gleich? | `boolean` |
| `compareTo()` | Welches Objekt kommt bei der Sortierung zuerst? | `int` |
| `==` | Ist es dasselbe Objekt im Speicher? | `boolean` |

### Beispiel

```java
a.equals(b)
```

prüft die **logische Gleichheit**.

```java
a.compareTo(b)
```

prüft die **Sortierreihenfolge**.

```java
a == b
```

prüft die **Referenz/Identität**.

---

## 10. Wichtig: `equals()` und `compareTo()` müssen nicht dasselbe vergleichen

Beispiel:

```java
@Override
public int compareTo(Person other) {
    return birthDate.compareTo(other.birthDate);
}
```

Hier wird nur das Geburtsdatum für die Sortierung verwendet.

`equals()` könnte dagegen vergleichen:

```text
Name + Geburtsdatum + Ort
```

Deshalb kann gelten:

```java
a.compareTo(b) == 0
```

aber:

```java
a.equals(b) == false
```

### Beispiel

```text
Person A:
Name: Max
Geburtsdatum: 01.01.2008
Ort: Linz

Person B:
Name: Anna
Geburtsdatum: 01.01.2008
Ort: Wien
```

Dann:

```java
a.compareTo(b) == 0
```

weil beide am selben Tag geboren wurden.

Aber:

```java
a.equals(b) == false
```

weil Name und Ort unterschiedlich sind.

---

## 11. Wichtige `equals()`-Regeln

`equals()` sollte folgende Eigenschaften erfüllen:

### Reflexivität

Ein Objekt ist gleich sich selbst:

```java
a.equals(a) == true
```

### Symmetrie

Wenn `a` gleich `b` ist, muss auch `b` gleich `a` sein:

```java
a.equals(b) == b.equals(a)
```

### Transitivität

Wenn:

```text
a = b
b = c
```

dann muss auch gelten:

```text
a = c
```

### Konsistenz

Solange sich die relevanten Daten nicht ändern, sollte das Ergebnis gleich bleiben.

### `null`

Für `null` muss gelten:

```java
a.equals(null) == false
```

---

## 12. `equals()` und `hashCode()`

Wenn `equals()` überschrieben wird, sollte **auch `hashCode()` überschrieben werden**.

Grundregel:

> Wenn zwei Objekte laut `equals()` gleich sind, müssen sie denselben `hashCode()` haben.

Beispiel:

```java
@Override
public int hashCode() {
    return Objects.hash(name, birthDate, location);
}
```

Dafür benötigt man:

```java
import java.util.Objects;
```

### Warum?

Das ist besonders wichtig bei Collections wie:

- `HashSet`
- `HashMap`

---

## 13. Kurz gesagt

```text
==          → gleiche Referenz?
equals()    → logisch gleich?
compareTo() → Sortierreihenfolge?
```

### Merksatz

> **`==` prüft Identität, `equals()` prüft Gleichheit und `compareTo()` prüft Reihenfolge.**