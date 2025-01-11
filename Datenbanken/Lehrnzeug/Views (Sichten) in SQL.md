
#### **1. Was sind Views?**
- Eine **View** ist eine benannte Abfrage, die wie eine Tabelle behandelt werden kann.
- **Einsatzgebiete**:
  1. Reduktion der sichtbaren Datenmenge auf relevante Informationen.
  2. Zugriffskontrolle: Bearbeiter dürfen nur bestimmte Daten sehen.
  3. Wiederverwendbarkeit: Häufig benötigte Abfragen müssen nicht mehrfach geschrieben werden.

---

#### **2. Erstellen und Nutzen von Views**

- **Syntax**:
  ```sql
  CREATE VIEW <View_Name> AS
  SELECT ... FROM ... WHERE ...;
  ```
  
- **Beispiel**:
  ```sql
  CREATE VIEW Javaprogrammierer AS
  SELECT Mitarbeiter.MiNr
  FROM Mitarbeiter, Qualifikation
  WHERE Mitarbeiter.MiNr = Qualifikation.MiNr
    AND Qualifikation.Faehigkeit = 'Java';
  ```

- **Abfragen mit Views**:
  ```sql
  SELECT AVG(Mitarbeiter.Gehalt) AS Javaschnitt
  FROM Mitarbeiter, Javaprogrammierer
  WHERE Mitarbeiter.MiNr = Javaprogrammierer.MiNr;
  ```

- **Löschen einer View**:
  ```sql
  DROP VIEW <View_Name>;
  ```

---

#### **3. Materialized Views**
- Speichern nicht nur die Abfrage, sondern auch das Ergebnis.
- **Vorteile**:
  - Schnellere Abfragen, da keine erneute Berechnung erforderlich ist.
- **Nachteile**:
  - Müssen manuell oder automatisch aktualisiert werden, z. B. bei Änderungen der zugrunde liegenden Daten.
  
- **Syntax**:
  ```sql
  CREATE MATERIALIZED VIEW <View_Name> AS
  SELECT ... FROM ...;
  REFRESH MATERIALIZED VIEW <View_Name>;
  ```

- **Beispiel** (ohne Materialized View):
  ```sql
  CREATE TABLE Javakoenner (MiNr NUMBER);
  INSERT INTO Javakoenner
  SELECT Mitarbeiter.MiNr
  FROM Mitarbeiter, Qualifikation
  WHERE Mitarbeiter.MiNr = Qualifikation.MiNr
    AND Qualifikation.Faehigkeit = 'Java';
  ```

---

#### **4. Einschränkungen bei Änderungen**
- **Häufige Fehler bei Änderungen** (INSERT, UPDATE, DELETE):
  1. Keine Angabe für Primärschlüssel.
  2. Nicht alle NOT NULL-Spalten werden gefüllt.
  3. Berechnete Spalten in der View können nicht geändert werden.

- **Beispiel einer zulässigen Änderung**:
  ```sql
  CREATE VIEW Basisdaten AS
  SELECT Mitarbeiter.MiNr, Mitarbeiter.Name
  FROM Mitarbeiter;

  DELETE FROM Basisdaten
  WHERE MiNr < 44;

  INSERT INTO Basisdaten VALUES (46, 'Erna');
  ```

- **Überprüfung der Änderungen**:
  ```sql
  SELECT * FROM Basisdaten;
  SELECT * FROM Mitarbeiter;
  ```

---

#### **5. Vorteile von Views**
- Bessere **Datensicherheit**: Verhindern, dass sensible Daten wie Gehälter sichtbar sind.
- **Flexibilität**: Einfacher Zugriff auf gefilterte oder aggregierte Daten.
- **Reduzierung von Redundanz**: Komplexe Abfragen können zentral gespeichert werden.

---

#### **6. Einschränkungen von Views**
- **Keine Speicherung von Daten**: Views speichern nur die Abfrage, nicht die Daten.
- **Performance**: Bei jeder Nutzung wird die zugrunde liegende Abfrage erneut ausgeführt.
- **Änderungsbeschränkungen**: Änderungen über mehrere Basistabellen sind oft nicht möglich.

---
