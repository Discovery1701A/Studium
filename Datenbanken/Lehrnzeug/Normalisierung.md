
#### **1. Funktionale Abhängigkeit**
- **Definition**: Attribut B ist funktional abhängig von Attribut A (A → B), wenn es für jeden Wert von A maximal einen Wert von B gibt.
- **Beispiel**:

| MiNr | Name  |
|------|-------|
| 1    | Egon  |
| 2    | Erna  |
| 3    | Uwe   |


  - **Abhängigkeit**: `{MiNr} → {Name}`

---

#### **2. Volle funktionale Abhängigkeit**
- **Definition**: B ist voll funktional abhängig von A, wenn B von der gesamten Attributmenge A und keiner Teilmenge von A abhängt.
- **Beispiel**: `{MiNr, ProNr} → {Name}` ist nicht voll funktional, da `{MiNr} → {Name}` gilt.

---

#### **3. Schlüsselkandidaten**
- **Definition**: Ein Schlüsselkandidat ist eine Attributkombination, aus der alle anderen Attribute der Tabelle abgeleitet werden können.
- **Beispiel:**
  - Tabelle **Projektmitarbeit**:
   
| **MiNr** | **ProNr** | **Name** | **AbtNr** | **Abteilung** | **Projekt** |
| -------- | --------- | -------- | --------- | ------------- | ----------- |
| 1        | 1         | Egon     | 42        | DB            | Infra       |
| 2        | 2         | Erna     | 42        | DB            | Portal      |

    - Schlüsselkandidat: `{MiNr, ProNr}`

---

### **Normalformen**

#### **4. Erste Normalform (1NF)**
- **Definition**: Alle Attributwerte sind atomar (keine Listen oder verschachtelten Werte).
- **Beispiel:**
  - Nicht in 1NF:
    
| MiNr | Name  | Projekte                   |
|------|-------|----------------------------|
| 1    | Egon  | {(1, Infra), (2, Portal)}  |
| 2    | Erna  | {(2, Portal), (3, Frame)}  |
| 3    | Uwe   | {(1, Infra), (3, Frame)}   |


  - In 1NF:
    
| MiNr | Name  | ProNr | Projekt |
|------|-------|-------|---------|
| 1    | Egon  | 1     | Infra   |
| 1    | Egon  | 2     | Portal  |
| 2    | Erna  | 2     | Portal  |
| 2    | Erna  | 3     | Frame   |
| 3    | Uwe   | 1     | Infra   |
| 3    | Uwe   | 3     | Frame   |


---

#### **5. Zweite Normalform (2NF)**
- **Definition**: Tabelle ist in 1NF, und alle Nichtschlüsselattribute sind voll funktional abhängig von jedem Schlüsselkandidaten.
- **Beispiel**: Tabelle **Projektmitarbeit** (nicht in 2NF):
  | **MiNr** | **ProNr** | **Name**  | **AbtNr** | **Abteilung** | **Projekt** |
  |----------|-----------|-----------|-----------|---------------|-------------|

  - Umwandlung in 2NF:
    - Tabelle **Mitarbeiter**:
    
| MiNr | Name  | AbtNr | Abteilung |
|------|-------|-------|-----------|
| 1    | Egon  | 42    | DB        |
| 2    | Erna  | 42    | DB        |
| 3    | Uwe   | 43    | GUI       |


    - Tabelle **Projekt**:
    
| ProNr | Projekt |
|-------|---------|
| 1     | Infra   |
| 2     | Portal  |
| 3     | Frame   |


    - Tabelle **Projektmitarbeit**:
     
| MiNr | ProNr |
|------|-------|
| 1    | 1     |
| 1    | 2     |
| 2    | 2     |
| 2    | 3     |
| 3    | 1     |
| 3    | 3     |


---

#### **6. Dritte Normalform (3NF)**
- **Definition**: Tabelle ist in 2NF und enthält keine funktionalen Abhängigkeiten zwischen Nichtschlüsselattributen.
- **Beispiel**: Tabelle **Mitarbeiter** (nicht in 3NF):

| **MiNr** | **Name** | **AbtNr** | **Abteilung** |
| -------- | -------- | --------- | ------------- |
|          |          |           |               |

  - `{AbtNr} → {Abteilung}` verletzt die 3NF.
  - Umwandlung:
    - Tabelle **Abteilung**:

| AbtNr | Abteilung |
|-------|-----------|
| 42    | DB        |
| 43    | GUI       |


    - Tabelle **Mitarbeiter**:
    
| MiNr | Name  | AbtNr |
|------|-------|-------|
| 1    | Egon  | 42    |
| 2    | Erna  | 42    |
| 3    | Uwe   | 43    |


---

#### **7. Boyce-Codd-Normalform (BCNF)**
- **Definition**: Tabelle ist in 3NF, und jede Determinante ist ein Schlüsselkandidat.
- **Beispiel:**
  - Tabelle **Betreuung** (nicht in BCNF):
    
| Schüler | Lehrer  | Fach     | Note |
|---------|---------|----------|------|
| Erkan   | Müller  | Deutsch  | 2    |
| Leon    | Müller  | Deutsch  | 4    |
| Lisa    | Schmidt | Sport    | 1    |
| David   | Mess    | Deutsch  | 4    |


  - `{Lehrer} → {Fach}` verletzt die BCNF.
  - Umwandlung:
    - Tabelle **Fachgebiet**:
    
| Lehrer  | Fach     |
|---------|----------|
| Müller  | Deutsch  |
| Schmidt | Sport    |
| Mess    | Deutsch  |


    - Tabelle **Betreuung**:

| Schüler | Lehrer  | Note |
|---------|---------|------|
| Erkan   | Müller  | 2    |
| Leon    | Müller  | 4    |
| Lisa    | Schmidt | 1    |
| David   | Mess    | 4    |


---

#### **8. Vierte Normalform (4NF)**
- **Definition**: Tabelle ist in BCNF, und keine mehrwertigen Abhängigkeiten existieren.
- **Beispiel:**
  - Tabelle **Sprachkenntnisse** (nicht in 4NF):
    
| Mitarbeiter | Programmiersprache | Fremdsprache |
|-------------|--------------------|--------------|
| Heinz       | Java               | Englisch     |
| Heinz       | Java               | Spanisch     |
| Heinz       | C#                 | Englisch     |
| Heinz       | C#                 | Spanisch     |
| Erwin       | Cobol              | Englisch     |
| Erwin       | Mumps              | Englisch     |
| Erwin       | C#                 | Englisch     |

  - Umwandlung:
    - Tabelle **Programmierkenntnis**:
    
| Mitarbeiter | Programmiersprache |
|-------------|--------------------|
| Heinz       | Java               |
| Heinz       | C#                 |
| Erwin       | Cobol              |
| Erwin       | Mumps              |
| Erwin       | C#                 |

    - Tabelle **Fremdsprachenkenntnis**:

| Mitarbeiter | Fremdsprache |
|-------------|--------------|
| Heinz       | Englisch     |
| Heinz       | Spanisch     |
| Erwin       | Englisch     |


