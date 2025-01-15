
**Aufgabe: Datenbank „Bibliotheksverwaltung“ erstellen**

  

Legen Sie eine Datenbank „Bibliotheksverwaltung“ mit folgenden Tabellen an:

1. **BUCH**

• **Attribute**: ISBN, Titel, Erscheinungsjahr, Preis, KategorieNr

• **Beschreibung**: Speichert Informationen zu Büchern in der Bibliothek.

• **Hinweis**: Die KategorieNr ist ein Fremdschlüssel zu der Tabelle **KATEGORIE**.

2. **KATEGORIE**

• **Attribute**: KategorieNr, Bezeichnung

• **Beschreibung**: Enthält Kategorien, denen Bücher zugeordnet werden können, z. B. „Roman“, „Fachbuch“, „Kinderbuch“.

3. **LESER**

• **Attribute**: LeserID, Name, Geburtsdatum, Adresse

• **Beschreibung**: Enthält Informationen zu Lesern, die Bücher ausleihen können.

4. **AUSLEIHE**

• **Attribute**: AusleihNr, Ausleihdatum, Rückgabedatum, LeserID, ISBN

• **Beschreibung**: Speichert Informationen über ausgeliehene Bücher.

• **Hinweis**: Die LeserID und ISBN sind Fremdschlüssel zu den Tabellen **LESER** und **BUCH**.

  

**Aufgabe**

1. **Erstellen Sie die Tabellen mit den angegebenen Attributen**:

• Wählen Sie geeignete Datentypen für die Attribute (z. B. VARCHAR, DATE, DECIMAL).

• Achten Sie darauf, Primär- und Fremdschlüssel korrekt zu definieren.

• Gewährleisten Sie, dass:

• jedes Buch zu einer Kategorie gehört,

• jede Ausleihe einem Leser und einem Buch zugeordnet ist,

• der Preis eines Buches immer positiv ist.

2. **Fügen Sie einen beispielhaften Datensatz in jede Tabelle ein**:

• **BUCH**: z. B. ein Buch mit der ISBN 978-3-16-148410-0, Titel Programmieren lernen, Erscheinungsjahr 2020, Preis 19.99, KategorieNr 1.

• **KATEGORIE**: z. B. eine Kategorie mit KategorieNr 1 und Bezeichnung Fachbuch.

• **LESER**: z. B. ein Leser mit LeserID 101, Name Max Mustermann, Geburtsdatum 1990-05-15, Adresse Musterstraße 1, 12345 Musterstadt.

• **AUSLEIHE**: z. B. eine Ausleihe mit AusleihNr 1, Ausleihdatum 2025-01-01, Rückgabedatum 2025-01-15, LeserID 101, ISBN 978-3-16-148410-0.

3. **Definieren Sie Einschränkungen**:

• Der Preis in der Tabelle **BUCH** muss größer als 0 sein.

• Geburtsdaten in der Tabelle **LESER** dürfen nicht in der Zukunft liegen.

4. **SQL-Befehle**: Geben Sie die SQL-Befehle für das Erstellen der Tabellen, das Einfügen der Daten und die Festlegung der Einschränkungen an.

  

**Punktevergabe (10 Punkte):**

• **4 Punkte**: Erstellen der Tabellen mit korrekten Attributen, Primär- und Fremdschlüsseln.

• **3 Punkte**: Hinzufügen der Beispiel-Datensätze.

• **2 Punkte**: Festlegen von Einschränkungen (z. B. Preis > 0, gültige Geburtsdaten).

• **1 Punkt**: Korrekte und sinnvolle Benennung der Tabellen und Attribute.

  
CREATE TABLE Buch(
ISBN INTEGER PRIMARY KEY,
Titel VARCHAR(255),
Erscheinungsjahr DATE,
Preis DECIMAL(5,2) CHECK (Preis > 0),
CONSTRAINT FK_Kategorie
FOREIGN KEY (KategorieNr)
REFERENCES Kategorie(KategorieNr)
);

CREATE TABLE Kategorie(
KategorieNr INTEGER PRIMARY KEY,
Bezeichnung VARCHAR(255)
);

CREATE TABLE Leser(
LeserID INTEGER PRIMARY KEY,
Name VARCHAR(255),
Geburtsdatum DATE Check (Geburtsdatum <= CURRENT_DATE),
Adresse VARCHAR(255)
);

CREATE TABLE Ausleihe(
AusleihNr INTEGER PRIMARY KEY,
Ausleihdatum DATE,
Rückgabedatum DATE,
CONSTRAINT FK_Leser
FOREIGN KEY (LeserID)
REFERENCES Leser(LeserID),
CONSTRAINT FK_Buch
FOREIGN KEY (ISBN)
REFERENCES Buch(ISBN)
);

INSERT INTO Kategorie(KategorieNr, Bezeichnung) VALUES (1, 'Fachbuch');

INSERT INTO Leser (LeserID, Name, Geburtsdatum, Adresse) VALUES (101, 'Max Mustermann', '1990-05-15', 'Musterstraße 1, 12345 Musterstadt');

INSERT INTO Buch VALUES(44434235535, 'Programmieren lernen', 2020-1-1, 19.99, 1);
)

INSERT INTO Ausleihe VALUES(1, '2025-01-01', '2025-01-15', 101, 44434235535);
)



**Aufgabe: SQL-Anfragen für eine Datenbank „Universitätsverwaltung“**

  

Die folgende Datenbank „Universitätsverwaltung“ enthält die Tabellen:

1. **Student**:

• **Attribute**: MatrNr, Name, Studienrichtung, Semester

• **Beschreibung**: Speichert Informationen über Studenten an einer Universität.

2. **Kurs**:

• **Attribute**: KursNr, Name, Leistungspunkte, Semester

• **Beschreibung**: Speichert Informationen zu angebotenen Kursen.

3. **Belegt**:

• **Attribute**: MatrNr, KursNr, Note

• **Beschreibung**: Verknüpft Studenten mit den von ihnen belegten Kursen.

4. **Dozent**:

• **Attribute**: PersNr, Name, Abteilung

• **Beschreibung**: Enthält Informationen über Dozenten, die Kurse unterrichten.

5. **Hält**:

• **Attribute**: PersNr, KursNr

• **Beschreibung**: Verknüpft Dozenten mit den Kursen, die sie unterrichten.

  

**Aufgaben (jeweils 3 Punkte)**

  

a) Geben Sie die Namen aller Studenten im ersten Semester aus, alphabetisch sortiert.
```SQL
SELECT Name
FROM Student
WHERE Semester = 1
ORDER BY Name ASC;
```

b) Welche Studenten (Ausgabe der Namen) haben Kurse mit mehr als 10 Leistungspunkten belegt?
```SQL
SELECT Student.Name
FROM Student
WHERE Student.MatrNr IN (SELECT Belegt.MatrNr FROM Belegt, Kurs
WHERE Belegt.Kurs.Nr = Kurs.Nr AND Kurs.Leistungspunkte > 10);
```
  

c) Wie viele Studenten studieren Informatik?
```SQL
SELECT COUNT(*) AS ANZAHL
FROM STUDENT 
WHERE Studienrichtung = 'Informatik';
```
  

d) Wie viele Kurse im aktuellen Semester (Semester = 2025) werden nicht unterrichtet (kein Eintrag in der Tabelle Hält)?
```SQL
SELECT COUNT(*) AS ANZAHL
FROM Kurs
WHERE Semester = 2025
WHERE Kurs.NR NOT IN (SELECT KursNr FROM Hält);
```

  

e) Geben Sie die Namen der Dozenten aus, die keine Kurse unterrichten.
```SQL
SELECT Dozent.Name
FROM Dozent
WHERE Dozent.PersNr NOT IN (SELECT PersNr FROM Hält);
```

  

f) Geben Sie den Namen des Kurses mit den meisten Teilnehmern aus.
```SQL
SELECT Kurs.Name
FROM Kurs 
WHERE Kurs.Nr = 
(SELECT KursNr 
 FROM Belegt 
 GROUP BY KursNr 
 ORDER BY COUNT(*) DESC LIMIT 1);
```

  

**Hinweise für die Lösung:**

• Verwenden Sie sinnvolle SQL-Abfragen mit SELECT, JOIN, GROUP BY, HAVING, und ORDER BY.

• Prüfen Sie auf leere Einträge (z. B. mit IS NULL) bei Aufgaben wie e) oder d).

• Nutzen Sie Aggregatfunktionen wie COUNT() oder MAX() bei den Aufgaben c), d), und f).

  

**Aufgabe: SQL-Anfragen für eine Datenbank „Buchhandlung“**

  

Die folgende Datenbank „Buchhandlung“ enthält die Tabellen:

1. **Buch**:

• **Attribute**: ISBN, Titel, Preis, Kategorie, Bestand

• **Beschreibung**: Enthält Informationen über Bücher, die in der Buchhandlung verfügbar sind.

2. **Kunde**:

• **Attribute**: Kundennr, Name, Adresse, Telefonnummer

• **Beschreibung**: Speichert Informationen über die Kunden der Buchhandlung.

3. **Bestellung**:

• **Attribute**: BestellNr, Datum, Kundennr

• **Beschreibung**: Verknüpft Bestellungen mit Kunden und speichert das Bestelldatum.

4. **Bestellposition**:

• **Attribute**: BestellNr, ISBN, Menge

• **Beschreibung**: Gibt die Bücher und deren Mengen an, die zu einer Bestellung gehören.

  

**Aufgaben (jeweils 3 Punkte)**

  

a) Geben Sie die Titel aller Bücher aus, die mehr als 50 Exemplare im Bestand haben, alphabetisch sortiert.

  

b) Welche Kunden (Name und Kundennr) haben mindestens eine Bestellung aufgegeben?

  

c) Wie viele Bestellungen wurden im Jahr 2024 aufgegeben?

  

d) Welche Kategorien von Büchern (nur die Namen der Kategorien) wurden bestellt, und wie oft kam jede Kategorie vor?

  

e) Geben Sie die Namen der Kunden aus, die noch keine Bestellung aufgegeben haben.

  

f) Welches Buch wurde in der höchsten Menge (über alle Bestellungen hinweg) bestellt? Geben Sie die ISBN, den Titel und die Gesamtanzahl der bestellten Exemplare aus.

  

**Hinweise für die Lösung:**

• Verwenden Sie JOIN, GROUP BY, HAVING, ORDER BY, und COUNT() für die Lösungen.

• Achten Sie bei Summen oder Maxima auf die Verwendung von SUM() oder MAX().

• Nutzen Sie LEFT JOIN oder NOT EXISTS, um Ergebnisse wie e) zu berechnen.

  

Falls du Unterstützung bei der Lösung oder Visualisierung der Tabellen benötigst, lass es mich wissen!