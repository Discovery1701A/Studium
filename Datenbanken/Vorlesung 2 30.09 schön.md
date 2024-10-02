# Relationen und Mengen in der relationalen Algebra

## Eigenschaften von Relationen:

- **Relationen** können als **Tabellen** betrachtet werden, die auf **Mengen** basieren.
- **Mengen** enthalten **keine doppelten Datensätze** (keine Duplikate).
- Relationen sind **vereinigungsverträglich**, wenn bestimmte Bedingungen erfüllt sind.
- **Vereinigungsverträglichkeit** liegt vor, wenn:
  - Die **Datentypen** der zu verknüpfenden Relationen übereinstimmen.
  - Die **Struktur** (Anzahl und Reihenfolge der Attribute) identisch ist.

### Mengenoperatoren:

Diese Operatoren werden verwendet, um Relationen auf Mengenebene zu kombinieren.

1. **Vereinigung**:
   $$ R \cup S $$
   - Kombiniert zwei Relationen, wobei doppelte Datensätze entfernt werden.
   - **Beispiel**:
     ```sql
     SELECT * FROM R
     UNION
     SELECT * FROM S;
     ```
     - **Ergebnis**: Alle Tupel, die entweder in Relation \( R \) oder in Relation \( S \) (oder in beiden) vorkommen.

2. **Schnittmenge**:
   $$ R \cap S $$
   - Gibt nur die Tupel zurück, die in beiden Relationen \( R \) und \( S \) vorhanden sind.
   - **Beispiel**:
     ```sql
     SELECT * FROM R
     INTERSECT
     SELECT * FROM S;
     ```

3. **Differenz**:
   $$ R - S $$
   - Liefert alle Tupel, die in Relation \( R \) vorkommen, aber nicht in Relation \( S \).
   - **Beispiel**:
     ```sql
     SELECT * FROM R
     EXCEPT
     SELECT * FROM S;
     ```

### Anforderungen an Mengenoperatoren:
- Der Operator muss **vereinigungsverträglich** sein.
- Das Ergebnis der Operation ist immer eine **Relation**.

---

## Relationale Operationen:

Diese Operatoren beziehen sich auf spezielle Operationen in der relationalen Algebra, die auf Relationen angewendet werden.

### Projektion:
$$ \pi_{\text{Attribut(e)}}(Relation) $$
- Wählt bestimmte Spalten (Attribute) einer Relation aus.
- **Beispiel**:
  ```sql
  SELECT name, age FROM Personen;
  ```
  - In der relationalen Algebra:  
    $$ \pi_{\text{name, age}}(Personen) $$
  
### Umbenennen:
$$ \rho_{\text{Neuer Name}}(Relation) $$
- Gibt einer Relation oder einem Attribut einen neuen Namen.
- **Beispiel**:  
  $$ \rho_{\text{NeuePersonen}}(Personen) $$
  Dies benennt die Relation "Personen" in "NeuePersonen" um.

### Auswahl:
$$ \sigma_{\text{Bedingung}}(Relation) $$
- Wählt bestimmte Zeilen (Tupel) einer Relation anhand einer Bedingung aus.
- **Beispiel**:
  ```sql
  SELECT * FROM Personen WHERE age > 30;
  ```
  - In der relationalen Algebra:  
    $$ \sigma_{\text{age > 30}}(Personen) $$

---

## Verknüpfungsoperatoren:

Diese Operatoren verknüpfen Tupel aus verschiedenen Relationen miteinander.

### Kreuzprodukt:
$$ R \times S $$
- Kombiniert alle Tupel aus Relation \( R \) mit allen Tupeln aus Relation \( S \).
- **Beispiel**:
  ```sql
  SELECT * FROM R, S;
  ```

  - **Ergebnis**: Jede Zeile von \( R \) wird mit jeder Zeile von \( S \) kombiniert, was eine große neue Tabelle erzeugt.

---

### Zusammenfassung:
In der relationalen Algebra ist es wichtig, dass die Operatoren **vereinigungsverträglich** sind. Die Ergebnisse der Operationen sind stets wieder Relationen. Die gängigsten Operatoren sind **Mengenoperatoren** (Vereinigung, Schnittmenge, Differenz) und **relationale Operationen** (Projektion, Umbenennung, Auswahl). Durch **Verknüpfungsoperatoren** wie das Kreuzprodukt können Tupel aus verschiedenen Relationen kombiniert werden.

---

## Beispiel 1: Relationen `R` und `S`

### Relation `R`

| ID  | Name   | Alter |
| --- | ------ | ----- |
| 1   | Alice  | 30    |
| 2   | Bob    | 25    |
| 3   | Carol  | 35    |

### Relation `S`

| ID  | Name    | Stadt   |
| --- | ------- | ------- |
| 2   | Bob     | Berlin  |
| 3   | Carol   | München |
| 4   | Dave    | Hamburg |

---

## Mengenoperatoren

### 1. **Vereinigung**  
$$ R \cup S $$  
Hierbei werden die Tupel von beiden Relationen zusammengeführt, aber doppelte Einträge werden entfernt.

| ID  | Name  | Alter | Stadt   |
| --- | ----- | ----- | ------- |
| 1   | Alice | 30    |         |
| 2   | Bob   | 25    | Berlin  |
| 3   | Carol | 35    | München |
| 4   | Dave  |       | Hamburg |

### 2. **Schnittmenge**  
$$ R \cap S $$  
Nur die gemeinsamen Tupel werden zurückgegeben. Hier würde das Tupel von Bob und Carol zurückkommen, aber nur für die gemeinsame Spalte.

| ID  | Name   | Alter | Stadt   |
| --- | ------ | ----- | ------- |
| 2   | Bob    | 25    | Berlin  |
| 3   | Carol  | 35    | München |

### 3. **Differenz**  
$$ R - S $$  
Hier werden die Tupel angezeigt, die in `R`, aber nicht in `S` vorkommen.

| ID  | Name   | Alter |
| --- | ------ | ----- |
| 1   | Alice  | 30    |

---

## Relationale Operationen

### Projektion  
$$ \pi_{\text{Name, Alter}}(R) $$  
Nehmen wir an, wir möchten nur die **Name**- und **Alter**-Spalten von `R` auswählen:

| Name   | Alter |
| ------ | ----- |
| Alice  | 30    |
| Bob    | 25    |
| Carol  | 35    |

---

### Auswahl  
$$ \sigma_{\text{Alter > 30}}(R) $$  
Wenn wir nur die Tupel haben möchten, wo das Alter größer als 30 ist:

| ID  | Name   | Alter |
| --- | ------ | ----- |
| 3   | Carol  | 35    |

---

## Verknüpfungsoperatoren

### Kreuzprodukt  
$$ R \times S $$  
Das Kreuzprodukt kombiniert alle Tupel von `R` mit allen Tupeln von `S`. Hierbei handelt es sich um eine Kombination aller möglichen Tupel aus beiden Relationen. Dies ist in der Praxis oft weniger nützlich, kann aber für die Verknüpfung von Relationen verwendet werden.

**Anfrage**:  
$$ R \times S $$

| R.ID | R.Name | Alter | S.ID | S.Name | Stadt   |
| ---- | ------ | ----- | ---- | ------ | ------- |
| 1    | Alice  | 30    | 2    | Bob    | Berlin  |
| 1    | Alice  | 30    | 3    | Carol  | München |
| 1    | Alice  | 30    | 4    | Dave   | Hamburg |
| 2    | Bob    | 25    | 2    | Bob    | Berlin  |
| 2    | Bob    | 25    | 3    | Carol  | München |
| 2    | Bob    | 25    | 4    | Dave   | Hamburg |
| 3    | Carol  | 35    | 2    | Bob    | Berlin  |
| 3    | Carol  | 35    | 3    | Carol  | München |
| 3    | Carol  | 35    | 4    | Dave   | Hamburg |


