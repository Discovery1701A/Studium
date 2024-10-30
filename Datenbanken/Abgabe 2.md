**Aufgabe 2.1**

Legen Sie eine Datenbank "Klausuren" mit folgenden Tabellen (inkl. Inhalt) an. Wählen Sie dabei geeignete Datentypen für die Attribute und beachten Sie die Primär- und Fremdschlüssel. Das Erstellen und Füllen der Tabellen soll komplett über SQL-Anweisungen erfolgen, die im Abgabedokument aufgeführt werden sollen.

***Tabelle STUDENT:***

| **MatrNr** | **Name** |
|--------|------|
| **1** | **Meier** |
| **2** | **Meyer** |
| **3** | **Maier** |

**Tabelle KLAUSUR:**

| **KNr** | **Name** | **Datum** | **Zeit** |
|-----|------|-------|------|
| **1** | **Java 1** | **2024-01-14** | **10:00:00** |
| **2** | **Einführung Inf.** | **2024-01-16** | **08:00:00** |
| **3** | **Mathematik 1** | **2024-01-20** | **13:00:00** |
| **4** | **Medieninformatik** | **2024-01-20** | **08:00:00** |
| **5** | **Audio/Video** | **2024-01-28** | **15:30:00** |

**Tabelle ANMELDUNG:**

| **MatrNr** | **KNr** | **Versuch** |
|--------|-----|---------|
| **1** | **2** | **1** |
| **1** | **4** | **2** |
| **2** | **1** | **2** |
| **3** | **3** | **3** |

---

**Aufgabe 2.2**

Formulieren Sie weiterhin für die folgenden Aufgaben jeweils eine SQL-Anfrage:

1. Geben Sie die Namen aller Studierenden aus.
2. Geben Sie die Namen aller Klausuren aus, die um 08:00 Uhr geschrieben werden.
3. Geben Sie eine Liste aller Erstanmeldungen (nur 1. Versuch) für eine Klausur aus (Ausgabe: Name der Klausur, Name des Studierenden).
4. Geben Sie die Namen aller Klausuren aus, für die sich die Studentin "Meier" angemeldet hat.
5. Geben Sie die Namen aller Studierenden aus, die mindestens zwei Klausuren im letzten Versuch (3. Versuch) schreiben.

**Aufgabe 2.1 - Lösung**

**Erstellung der Tabellen**

```SQL
CREATE TABLE STUDENT(
MatrNr INTEGER,
Name Varchar(6),
PRIMARY KEY (MatrNr));

CREATE TABLE KLAUSUR(
KNr INTEGER,
Name Varchar(17),
Datum DATE NOT NULL DEFAULT CURRENT_DATE,
Zeit TIME,
PRIMARY KEY (KNr));

CREATE TABLE ANMELDUNG(
MatrNr INTEGER,
KNr INTEGER,
Versuche INTEGER,
PRIMARY KEY (MatrNr, KNr),
CONSTRAINT STUD_Anmeldung
	FOREIGN KEY (MatrNr)
	REFERENCES STUDENT(MatrNr),
CONSTRAINT Kl_Anmeldung
	FOREIGN KEY (KNr)
	REFERENCES Klausur(KNr)
);
```

**Füllen der Tabellen mit Inhalten**

```SQL
INSERT INTO STUDENT VALUES(1, 'Meier');
INSERT INTO STUDENT VALUES(2, 'Meyer');
INSERT INTO STUDENT VALUES(3, 'Maier');


INSERT INTO KLAUSUR VALUES(1, 'Java 1', '2024-01-14', '10:00:00');
INSERT INTO KLAUSUR VALUES(2, 'Einführung Inf. 1', '2024-01-16', '08:00:00');
INSERT INTO KLAUSUR VALUES(3, 'Mathematik 1', '2024-01-20', '13:00:00');
INSERT INTO KLAUSUR VALUES(4, 'Medieninformatik', '2024-01-20', '08:00:00');
INSERT INTO KLAUSUR VALUES(5, 'Audio/Video', '2024-01-28', '15:30:00');

INSERT INTO ANMELDUNG VALUES(1,2,1);
INSERT INTO ANMELDUNG VALUES(1,4,2);
INSERT INTO ANMELDUNG VALUES(2,1,2);
INSERT INTO ANMELDUNG VALUES(3,3,3)
```

**Aufgabe 2.2**

1. Geben Sie die Namen aller Studierenden aus.

   ```SQL
   SELECT Name FROM student
   ```
2. Geben Sie die Namen aller Klausuren aus, die um 08:00 Uhr geschrieben werden.

   ```SQL
   SELECT Name FROM klausur where Zeit='08:00:00'
   ```
3. Geben Sie eine Liste aller Erstanmeldungen (nur 1. Versuch) für eine Klausur aus (Ausgabe: Name der Klausur, Name des Studierenden).

   ```SQL
   SELECT KLAUSUR.Name AS Klausurname, STUDENT.Name AS Studentname 
   FROM anmeldung
   JOIN STUDENT ON ANMELDUNG.MatrNr = STUDENT.MatrNr
   JOIN KLAUSUR ON ANMELDUNG.KNr = KLAUSUR.KNr
   WHERE ANMELDUNG.Versuch = 1;  -- geht auch ohne Anmeldung sieht aber so schöner aus
   
   -- oder
   SELECT DISTINCT KLAUSUR.Name, STUDENT.Name
   FROM KLAUSUR , ANMELDUNG , STUDENT
   WHERE KLAUSUR.KNr = ANMELDUNG.KNr 
   AND ANMELDUNG.MatrNr = STUDENT.MatrNr 
   AND Versuch = 1;
   ```
4. Geben Sie die Namen aller Klausuren aus, für die sich die Studentin "Meier" angemeldet hat.

   ```SQL
   -- 1. Ansatz vor VL 24.0kt.2024
   SELECT KLAUSUR.Name AS Klausurname 
   FROM anmeldung
   JOIN STUDENT ON ANMELDUNG.MatrNr = STUDENT.MatrNr
   JOIN KLAUSUR ON ANMELDUNG.KNr = KLAUSUR.KNr
   WHERE STUDENT.Name = 'Meier';
   ```

   ```SQL
   SELECT Klausur.Name Klausurname
   FROM Klausur, Student, Anmeldung
   Where Student.MatrNr = Anmeldung.MatrNr
     AND Klausur.KNr = Anmeldung.KNr
     AND Student.Name = 'Meier'
   ```
5. Geben Sie die Namen aller Studierenden aus, die mindestens zwei Klausuren im letzten Versuch (3. Versuch) schreiben.

   ```SQL
   -- 1. Ansatz vor VL 24.0kt.2024
   SELECT STUDENT.Name AS Studierende
   FROM anmeldung
   JOIN STUDENT ON ANMELDUNG.MatrNr = STUDENT.MatrNr
   WHERE ANMELDUNG.Versuch = 3
   GROUP BY STUDENT.Name
   HAVING COUNT(ANMELDUNG.KNr) >= 2;
   ```

   ```SQL
 SELECT DISTINCT S.Name
FROM STUDENT S ,ANMELDUNG A1 ,ANMELDUNG A2
WHERE S.MatrNr = A1.MatrNr
AND S.MatrNr = A2.MatrNr
AND A1.KNr <> A2.KNr
AND A1.Versuch = 3
AND A2.Versuch = 3;
   ```

      