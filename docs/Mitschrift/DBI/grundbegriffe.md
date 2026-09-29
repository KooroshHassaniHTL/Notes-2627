# DBI – Grundbegriffe

## 1. Datenbankmodelle

### 1.1 Hierarchisches Datenbankmodell (1960er)

- **Datenstruktur:** Baumstruktur mit Eltern- und Kindelementen (Parent-Child).
- **Verknüpfung:** Jedes Kind hat genau ein Elternteil. Beziehungen sind 1:n.
- **Vorteile:** Schneller Zugriff bei festen Datenpfaden, klare Struktur.
- **Nachteile:** Unflexibel, m:n-Beziehungen nur mit Redundanzen möglich.
- **Beispiele:** IBM IMS, Dateisysteme.

### 1.2 Netzwerkmodell (späte 1960er)

- **Datenstruktur:** Netzwerk aus Datensätzen (Records).
- **Verknüpfung:** Ein Datensatz kann mehrere übergeordnete Datensätze haben. m:n-Beziehungen sind möglich.
- **Vorteile:** Flexible Beziehungen, weniger Redundanzen als beim hierarchischen Modell.
- **Nachteile:** Komplexe Struktur, Verknüpfungen über Zeiger (Pointer), aufwendige Änderungen.
- **Beispiele:** UDS, IDMS.

### 1.3 Relationales Datenbankmodell (1970er)

- **Datenstruktur:** Tabellen mit Zeilen (Tupeln) und Spalten (Attributen).
- **Verknüpfung:** Primär- und Fremdschlüssel verbinden Tabellen.
- **Vorteile:** Einfach verständlich, flexibel, Abfragen mit SQL, Datenunabhängigkeit.
- **Nachteile:** Komplexe Abfragen mit vielen Tabellenverknüpfungen (JOINs) können langsam sein.
- **Beispiele:** PostgreSQL, MySQL, Oracle Database, Microsoft SQL Server.

---

## 2. Grundbegriffe

- **SQL (Structured Query Language):** Sprache zum Erstellen, Bearbeiten und Abfragen relationaler Datenbanken.
- **DBMS (Datenbankmanagementsystem):** Software zur Verwaltung von Datenbanken.
- **Redundanz:** Mehrfache Speicherung derselben Daten.
- **Datenintegrität:** Daten sind korrekt, vollständig und widerspruchsfrei.
- **Datenkonsistenz:** Daten befinden sich in einem gültigen und widerspruchsfreien Zustand.

---

## 3. Datenbankmanagementsystem (DBMS)

Ein DBMS bietet folgende Funktionen:

- **Integration:** Vermeidung unnötiger Datenredundanz.
- **Datenoperationen:** Daten einfügen, ändern, löschen und abfragen.
- **Katalog (Data Dictionary):** Speicherung von Informationen über die Datenbank.
- **Benutzersichten:** Benutzer sehen nur die für sie freigegebenen Daten.
- **Konsistenzüberwachung:** Sicherstellung der Korrektheit der Daten.
- **Datenschutz:** Schutz vor unberechtigtem Zugriff.
- **Transaktionen:** Zusammengehörige Operationen werden ganz oder gar nicht ausgeführt.
- **Synchronisation:** Gleichzeitige Zugriffe werden so koordiniert, dass sie sich nicht unzulässig stören.
- **Datensicherung:** Schutz vor Datenverlust, beispielsweise durch Backups und Wiederherstellung.

---

## 4. Data Dictionary (DD)

Das Data Dictionary ist ein Datenkatalog, der Informationen über die Struktur und Bedeutung der Datenbank enthält.

Typische Inhalte:

- **Feldname:** Name einer Spalte.
- **Datentyp:** Art der Daten, z. B. `VARCHAR`, `INTEGER` oder `DATE`.
- **Beschreibung:** Bedeutung des Datenfeldes.
- **Zulässige Werte:** Erlaubte Werte oder Wertebereiche.
- **Maßeinheit:** Einheit der Daten, z. B. kg oder Sekunden.
- **Beziehungen:** Verknüpfungen zu anderen Tabellen, z. B. über Primär- und Fremdschlüssel.

---

## 5. SQL-Sprachbereiche

### 5.1 DML – Data Manipulation Language

Dient zum **Bearbeiten von Daten**.

- `INSERT` – Daten einfügen
- `UPDATE` – Daten ändern
- `DELETE` – Daten löschen

### 5.2 DQL – Data Query Language

Dient zum **Abfragen von Daten**.

- `SELECT` – Daten abfragen

> **Merke:** DQL = Daten lesen, DML = Daten verändern.

### 5.3 DDL – Data Definition Language

Dient zum **Definieren und Ändern der Datenbankstruktur**.

- `CREATE` – Datenbankobjekte erstellen
- `ALTER` – Datenbankobjekte ändern
- `DROP` – Datenbankobjekte löschen

### Übersicht

| Bereich | Bedeutung | Befehle |
|---|---|---|
| **DQL** | Daten abfragen | `SELECT` |
| **DML** | Daten bearbeiten | `INSERT`, `UPDATE`, `DELETE` |
| **DDL** | Datenbankstruktur definieren | `CREATE`, `ALTER`, `DROP` |

---

## 6. Datenbanksysteme und Werkzeuge

| System | Hersteller / Lizenz |
|---|---|
| Oracle Database | Oracle |
| Microsoft SQL Server | Microsoft |
| PostgreSQL | Open Source |
| MySQL | Open Source, gehört zu Oracle |

### Werkzeuge

- **Oracle Database Free:** Kostenlose Edition der Oracle-Datenbank.
- **DataGrip:** Datenbank-Entwicklungsumgebung von JetBrains.
- **SQL Developer:** Datenbankwerkzeug von Oracle.