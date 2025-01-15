
#### **1. Einführung in Tabellen**
- **Definition**: Tabellen sind die Grundlage relationaler Datenbanken.
- **Eigenschaften einer Tabelle**:
  - Hat einen **Namen**.
  - **Spaltenüberschriften** (Attribute).
  - **Datentypen**: Jede Spalte hat einen einheitlichen Datentyp (z. B. Text, Zahl, Datum, Boolean).
  - **Einträge**: Zeilen, die n-Tupel des Attribut-Kreuzprodukts darstellen.
  
#### **2. Übersetzung von Entity-Relationship-Modellen (ERM) in Tabellen**
Die Übersetzung erfolgt schrittweise:

##### **Schritt 1: Entitätstypen**
- Jeder Entitätstyp wird in eine eigene Tabelle übersetzt.
- **Attribute des Entitätstyps** werden zu Spalten der Tabelle.
- Beispiel:

| **MiNr** | **Name** |
| -------- | -------- |
| 42       | Egon     |
| 43       | Erwin    |
| 44       | Erna     |


##### **Schritt 2: 1:1-Beziehungen**
- Enge Verbindung zwischen zwei Entitätstypen.
- Attribute der Beziehung werden in eine Tabelle integriert.
- Beispiel:

| **MiNr** | **Name** | **TelNr** | **Typ**   |
|----------|----------|-----------|-----------|
| 42       | Egon     | 01777     | Nokus     |
| 43       | Erwin    | 01700     | Erika     |
| 44       | Erna     | 01622     | Simen     |


##### **Schritt 3: 1:N-Beziehungen**
- Die Primärschlüssel der „1“-Seite werden als **Fremdschlüssel** in die Tabelle der „N“-Seite aufgenommen.
- Beispiel:

| **AbtNr** | **Titel** | **KNr** | **Auftragsdatum** |
|-----------|-----------|---------|-------------------|
| 1         | DBX       | 54      | 26.02.06          |
| 1         | Jovo      | 54      | 06.05.06          |
| 2         | DBX       | 55      | 27.02.06          |


##### **Schritt 4: M:N-Beziehungen**
- Für jede M:N-Beziehung wird eine zusätzliche Tabelle erstellt.
- Diese enthält:
  - **Primärschlüssel beider Entitätstypen** als Fremdschlüssel.
  - Eventuell zusätzliche Attribute der Beziehung.
- Beispiel:

| **MiNr** | **AbtNr** | **Titel** | **Rolle**  |
|----------|-----------|-----------|------------|
| 42       | 1         | DBX       | Design     |
| 42       | 1         | Jovo      | Review     |
| 43       | 2         | DBX       | Analyse    |
| 44       | 1         | Jovo      | Design     |
| 44       | 2         | DBX       | Review     |


---

#### **3. Prinzipien der Übersetzung**
1. **Redundanz vermeiden**: Keine mehrfach gespeicherten Daten.
2. **NULL-Werte minimieren**: Tabellen so gestalten, dass möglichst keine NULL-Werte notwendig sind.
3. **Minimale Anzahl von Tabellen**: So wenig Tabellen wie möglich, solange die obigen Ziele erfüllt werden.

---

#### **4. Komplexere Beziehungen**
1. **1:C-Beziehungen**:
   - Werden wie 1:N-Beziehungen behandelt.
   - Beispiel: Telefoniert-Beziehung zwischen Personen.

2. **Rekursive Beziehungen**:
   - Beziehung innerhalb eines Entitätstyps.
   - Beispiele:
     - Mitarbeiter → berichtet an → Vorgesetzter.
     - Produkt → hat Teil → Produkt.

3. **Komplexe Beziehungen (mehr als zwei Entitätstypen)**:
   - Neue Tabelle erstellen, die alle identifizierenden Attribute der beteiligten Entitätstypen enthält.
   - Beispiel: **Firma verkauft Produkt in Land**.

---

#### **5. Symmetrie der Übersetzung**
- **Von ERM zu Tabellen**: Eindeutig.
- **Von Tabellen zu ERM**: Nicht eindeutig, da Tabellen sowohl Entitäten als auch Beziehungen repräsentieren können.

---

### **Zusammengeführtes Beispiel**
1. **Mitarbeiter-Tabelle**:

| **MiNr** | **Name** | **TelNr** | **Typ**   |
|----------|----------|-----------|-----------|
| 42       | Egon     | 01777     | Nokus     |
| 43       | Erwin    | 01700     | Erika     |
| 44       | Erna     | 01622     | Simen     |

2. **Projekt-Tabelle**:

| **AbtNr** | **Titel** | **KNr** | **Auftragsdatum** |
|-----------|-----------|---------|-------------------|
| 1         | DBX       | 54      | 26.02.06          |
| 1         | Jovo      | 54      | 06.05.06          |
| 2         | DBX       | 55      | 27.02.06          |

3. **Bearbeitung-Tabelle**:

| **MiNr** | **AbtNr** | **Titel** | **Rolle**  |
|----------|-----------|-----------|------------|
| 42       | 1         | DBX       | Design     |
| 42       | 1         | Jovo      | Review     |
| 43       | 2         | DBX       | Analyse    |
| 44       | 1         | Jovo      | Design     |
| 44       | 2         | DBX       | Review     |


4. **Kunde-Tabelle**:

| **KNr** | **Name**   |
|---------|------------|
| 54      | Bonzo      |
| 55      | Collecto   |
