# Java – Comparable

## 1. Was ist Comparable?

`Comparable<T>` wird verwendet, wenn Objekte einer Klasse eine **natürliche Sortierreihenfolge** bekommen sollen.

Beispiel:

> Personen sollen nach ihrem Geburtsdatum sortiert werden.

Dafür implementiert die Klasse `Comparable<Person>`:

```java
public class Person implements Comparable<Person> {

    @Override
    public int compareTo(Person other) {
        return this.birthDate.compareTo(other.birthDate);
    }
}
```

---

## 2. `compareTo()`

`compareTo()` vergleicht zwei Objekte und gibt eine `int` zurück.

| Rückgabewert | Bedeutung |
|---|---|
| `< 0` | `this` ist kleiner |
| `0` | Beide sind in der Sortierreihenfolge gleich |
| `> 0` | `this` ist größer |

Beispiel:

```java
return this.birthDate.compareTo(other.birthDate);
```

Damit werden Personen nach ihrem Geburtsdatum sortiert.

---

## 3. Beispiel

```java
Person a = new Person("Max", date1);
Person b = new Person("Anna", date2);

a.compareTo(b);
```

Wenn `date1` vor `date2` liegt:

```java
a.compareTo(b) < 0
```

Wenn beide dasselbe Geburtsdatum haben:

```java
a.compareTo(b) == 0
```

Wenn `date1` nach `date2` liegt:

```java
a.compareTo(b) > 0
```

---

## 4. Verwendung beim Sortieren

`Comparable` kann zum Beispiel mit `Collections.sort()` verwendet werden:

```java
List<Person> people = new ArrayList<>();

Collections.sort(people);
```

Java verwendet dabei automatisch:

```java
compareTo()
```

Alternativ:

```java
people.sort(null);
```

---

## 5. Wichtig: `compareTo() == 0`

Wenn

```java
a.compareTo(b) == 0
```

bedeutet das:

> `a` und `b` sind in der Sortierreihenfolge gleich.

Es bedeutet **nicht automatisch**, dass:

```java
a.equals(b)
```

`true` ergibt.

### Beispiel

`compareTo()` vergleicht nur das Geburtsdatum:

```java
@Override
public int compareTo(Person other) {
    return birthDate.compareTo(other.birthDate);
}
```

`equals()` könnte dagegen vergleichen:

- Name
- Geburtsdatum
- Ort

Dann können zwei Personen dasselbe Geburtsdatum haben, aber trotzdem nicht `equals()` sein.

---

## 6. Comparable vs. Comparator

### Comparable

Die Klasse selbst definiert ihre **natürliche Sortierung**.

```java
class Person implements Comparable<Person> {

    @Override
    public int compareTo(Person other) {
        return birthDate.compareTo(other.birthDate);
    }
}
```

### Comparator

Eine **externe Vergleichsregel** wird definiert.

```java
Comparator<Person> byName =
    (a, b) -> a.getName().compareTo(b.getName());
```

### Merke

> **Comparable = natürliche/Standard-Sortierung**

> **Comparator = alternative Sortierung**

---

## 7. Kurzvergleich

| Methode | Rückgabewert | Zweck |
|---|---|---|
| `compareTo()` | `int` | Objekte sortieren/vergleichen |
| `equals()` | `boolean` | Objekte logisch vergleichen |
| `==` | `boolean` | Gleiche Referenz prüfen |

---

## 8. Wichtig für die Prüfung

```java
public class Person implements Comparable<Person>
```

bedeutet:

> `Person` kann mit anderen `Person`-Objekten verglichen und natürlich sortiert werden.

Die Methode muss implementiert werden:

```java
@Override
public int compareTo(Person other) {
    ...
}
```

### Rückgabewerte

```text
< 0 → kleiner
= 0 → gleich in der Sortierreihenfolge
> 0 → größer
```

### Merksatz

> **Comparable bestimmt, wie Objekte standardmäßig sortiert werden.**