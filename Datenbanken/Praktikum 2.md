**Aufgabe 2.1**

Legen Sie eine Datenbank "Klausuren" mit folgenden Tabellen (inkl. Inhalt) an. Wählen Sie dabei geeignete Datentypen für die Attribute und beachten Sie die Primär- und Fremdschlüssel. Das Erstellen und Füllen der Tabellen soll komplett über SQL-Anweisungen erfolgen, die im Abgabedokument aufgeführt werden sollen.  
  
  
**_Tabelle STUDENT:_**

|   |   |
|---|---|
|**MatrNr**|**Name**|
|**1**|**Meier**|
|**2**|**Meyer**|
|**3**|**Maier**|

**_Tabelle KLAUSUR:_**

|   |   |   |   |
|---|---|---|---|
|**KNr**|**Name**|**Datum**|**Zeit**|
|**1**|**Java 1**|**2024-01-14**|**10:00:00**|
|**2**|**Einführung Inf.**|****2024**-01-16**|**08:00:00**|
|**3**|**Mathematik 1**|****2024**-01-20**|**13:00:00**|
|**4**|**Medieninformatik**|****2024**-01-20**|**08:00:00**|
|**5**|**Audio/Video**|****2024**-01-28**|**15:30:00**|

**_Tabelle ANMELDUNG:_**

|            |         |             |
| ---------- | ------- | ----------- |
| **MatrNr** | **KNr** | **Versuch** |
| **1**      | **2**   | **1**       |
| **1**      | **4**   | **2**       |
| **2**      | **1**   | **2**       |
| **3**      | **3**   | **3**       |
		`-- Erstellen der Tabelle STUDENT`
		`CREATE TABLE STUDENT (`
		    `MatrNr INT PRIMARY KEY,      -- Primärschlüssel`
		    `Name VARCHAR(10) NOT NULL    -- Name darf nicht leer sein`
		`);`
		
		`-- Daten in die Tabelle STUDENT einfügen`
		`INSERT INTO STUDENT (MatrNr, Name) VALUES`
		`(1, 'Meier'),`
		`(2, 'Meyer'),`
		`(3, 'Maier');`
		
		`-- Erstellen der Tabelle KLAUSUR`
		`CREATE TABLE KLAUSUR (`
		    `KNr INT PRIMARY KEY,        -- Primärschlüssel`
		    `Name VARCHAR(100) NOT NULL, -- Name der Klausur, darf nicht leer sein`
		    `Datum DATE NOT NULL,        -- Datum der Klausur`
		    `Zeit TIME NOT NULL          -- Zeit der Klausur`
		`);`
		
		`-- Daten in die Tabelle KLAUSUR einfügen`
		`INSERT INTO KLAUSUR (KNr, Name, Datum, Zeit) VALUES`
		`(1, 'Java 1', '2024-01-14', '10:00:00'),`
		`(2, 'Einführung Inf.', '2024-01-16', '08:00:00'),`
		`(3, 'Mathematik 1', '2024-01-20', '13:00:00'),`
		`(4, 'Medieninformatik', '2024-01-20', '08:00:00'),`
		`(5, 'Audio/Video', '2024-01-28', '15:30:00');`
		
		`-- Erstellen der Tabelle ANMELDUNG`
		`CREATE TABLE ANMELDUNG (`
		    `MatrNr INT,                  -- Matrikelnummer des Studenten`
		    `KNr INT,                     -- Klausurnummer`
		    `Versuch INT,                 -- Versuch (1. Versuch, 2. Versuch, etc.)`
		    `PRIMARY KEY (MatrNr, KNr),    -- Kombination aus MatrNr und KNr ist der Primärschlüssel`
		    `FOREIGN KEY (MatrNr) REFERENCES STUDENT(MatrNr), -- Fremdschlüssel, referenziert MatrNr aus STUDENT`
		    `FOREIGN KEY (KNr) REFERENCES KLAUSUR(KNr)        -- Fremdschlüssel, referenziert KNr aus KLAUSUR`
		`);`
		
		`-- Daten in die Tabelle ANMELDUNG einfügen`
		`INSERT INTO ANMELDUNG (MatrNr, KNr, Versuch) VALUES`
		`(1, 2, 1),`
		`(1, 4, 2),`
		`(2, 1, 2),`
		`(3, 3, 3);`

**Aufgabe 2.2**

Formulieren Sie weiterhin für die folgenden Aufgaben jeweils eine SQL-Anfrage:

1. Geben Sie die Namen aller Studierenden aus.

		`SELECT DISTINCT Name FROM STUDENT;`
		
2. Geben Sie die Namen aller Klausuren aus, die um 08:00 Uhr geschrieben werden.

		`SELECT DISTINCT Name, Zeit FROM KLAUSUR WHERE Zeit = '08:00';`
		
3. Geben Sie eine Liste aller Erstanmeldungen (nur 1. Versuch) für eine Klausur aus (Ausgabe: Name der Klausur, Name des Studierenden).

		`SELECT DISTINCT KLAUSUR.Name, STUDENT.Name` 
		`FROM KLAUSUR` 
		`JOIN ANMELDUNG` 
		`ON KLAUSUR.KNr = ANMELDUNG.KNr` 
		`JOIN STUDENT`
		`ON ANMELDUNG.MatrNr = STUDENT.MAtrNr`
		`WHERE Versuch = 1;`
		
4. Geben Sie die Namen aller Klausuren aus, für die sich die Studentin "Meier" angemeldet hat.
 
		`SELECT DISTINCT KLAUSUR.Name` 
		`FROM KLAUSUR` 
		`JOIN ANMELDUNG` 
		`ON KLAUSUR.KNr = ANMELDUNG.KNr` 
		`JOIN STUDENT`
		`ON ANMELDUNG.MatrNr = STUDENT.MAtrNr`
		`WHERE STUDENT.Name = 'Meier';`
		
5. Geben Sie die Namen aller Studierenden aus, die mindestens zwei Klausuren im letzten Versuch (3. Versuch) schreiben.

		`SELECT DISTINCT STUDENT.Name` 
		`FROM KLAUSUR` 
		`JOIN ANMELDUNG` 
		`ON KLAUSUR.KNr = ANMELDUNG.KNr` 
		`JOIN STUDENT`
		`ON ANMELDUNG.MatrNr = STUDENT.MatrNr`
		`WHERE ANMELDUNG.Versuch = 3`
		`GROUP BY STUDENT.MatrNr` 
		`HAVING COUNT(ANMELDUNG.KNr) >= 2;`
		