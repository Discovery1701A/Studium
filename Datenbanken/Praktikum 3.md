Das zur Erzeugung der Datenbank erforderliche SQL-Skript mhbdb.sql finden Sie im Moodle-Kurs unter [Datenbanken](https://moodle.hs-emden-leer.de/moodle/mod/url/view.php?id=323657 "Datenbanken").   

Beachten Sie folgende Randbedingungen:

- Die in der Tabelle Modul angegebene PID verweist auf den Modulverantwortlichen.
- Falls das Attribute Semester in der Tabelle Modulzuordnung NULL ist, handelt es sich um ein Wahlpflichtmodul, das keinem Zertifikat zugeordnet ist.

Formulieren Sie für folgende Anfragen SQL-Anweisungen:

1. Geben Sie aus, wie viele Module in der Datenbank gespeichert sind.

```SQL
SELECT DISTINCT COUNT( MID ) AS Anzahl FROM Modul;
```

2. Geben Sie alle Module (Name) aus, die weniger als 4 ECTS-Punkte haben.

```SQL
SELECT DISTINCT Name FROM Modul WHERE ects < 4;
```
3. Geben Sie alle Module aus, in denen eine Klausur als Prüfung möglich ist.  

```SQL
SELECT DISTINCT Name FROM Modul WHERE Pruefung LIKE '%Klausur%';
```
    
4. Geben Sie die Namen der Module aus, bei denen als Modulverantwortlicher "F. Rump" angegeben ist.  

```SQL
SELECT DISTINCT Modul.Name FROM Person , Modul
WHERE Person.PID = Modul.PID AND Person.Name = 'F. Rump';
```
    
5. Geben Sie alle Studiengänge mit den zugehörigen Zertifikaten aus (Ausgabe: Studiengang, Zertifikat).

```SQL 
SELECT Studiengang.Name As Studiengangname, Zertifikat.Name AS Zertifikatsname
FROM Studiengang, Zertifikat, Zertifikatzuordnung
WHERE Studiengang.SID = Zertifikatzuordnung.SID AND Zertifikat.ZID = Zertifikatzuordnung.ZID;
```

6. Geben Sie alle Lehrenden und die Veranstaltungen aus, die sie unterrichten.

```SQL
SELECT Veranstaltung.Name AS Veranstaltungsname, Person.Name AS Lehrendername
FROM Veranstaltung, Person, Lehrende
WHERE Veranstaltung.VID = Lehrende.VID AND Person.PID = Lehrende.PID;
```

7. Geben Sie alle Module aus, sofern die enthaltenen Veranstaltung in Summe mehr als vier SWS haben.  

```SQL
SELECT Modul.Name AS Modulname, SUM(Veranstaltung.SWS) AS Gesamt_SWS
FROM Modul ,Veranstaltung
WHERE Modul.MID = Veranstaltung.MID
GROUP BY Modul.MID
HAVING SUM(Veranstaltung.SWS) > 4;
```

8. Geben Sie nur die Veranstaltungen aus, denen mehrere Lehrende zugeordnet sind.  

```SQL
SELECT Veranstaltung.Name AS Veranstaltungsname
FROM Veranstaltung, Lehrende
WHERE Veranstaltung.VID = lehrende.VID
GROUP BY Veranstaltung.VID
HAVING COUNT(lehrende.PID) >= 2;
```
    
9. Geben Sie alle Studiengänge absteigend nach der Anzahl der "reinen" Wahlpflichtmodule, die somit keinem Zertifikat zugeordnet sind, aus.

```SQL
SELECT DISTINCT Studiengang.Name AS Studiengang,
(SELECT DISTINCT COUNT(*)
FROM Modulzuordnung
WHERE Modulzuordnung.SID = Studiengang.SID
AND Modulzuordnung.Semester is  NULL)
AS Anzahl_Wahlpflichtmodule
FROM Studiengang
ORDER BY Anzahl_Wahlpflichtmodule DESC;
```

10. Geben Sie zu jedem Studiengang und jedem Zertifikat in dem jeweiligen Studiengang die Anzahl der zugehörigen Module aus, wobei die Studiengänge und Zertifikate alphabetisch sortiert sein sollen.

```SQL 
SELECT (SELECT Studiengang.Name FROM Studiengang WHERE SID = Zertifikatzuordnung.SID) AS Studiengang,
(SELECT Zertifikat.Name FROM Zertifikat WHERE ZID = Zertifikatzuordnung.ZID) AS Zertifikat,
(SELECT COUNT(*)
FROM Zertifikatsmodul, Modulzuordnung
WHERE Zertifikatsmodul.ZID = Zertifikatzuordnung.ZID
AND Modulzuordnung.SID = Zertifikatzuordnung.SID
AND Zertifikatsmodul.MID = Modulzuordnung.MID
) AS Anzahl_Module
FROM Zertifikatzuordnung
ORDER BY Studiengang ASC, Zertifikat ASC;
```

11. Geben Sie zu jedem Studiengang die Anzahl der Zertifikate aus, sofern der Studiengang mehr als drei Zertifikate hat.

```SQL 
SELECT (SELECT Studiengang.Name FROM Studiengang WHERE SID = Zertifikatzuordnung.SID) AS Studiengang,
COUNT(*) AS Anzahl_Zertifikate
FROM Zertifikatzuordnung
GROUP BY Zertifikatzuordnung.SID
HAVING COUNT(*) > 3
ORDER BY Studiengang;
```

12. Geben Sie die Studiengänge absteigend nach den daran beteiligten, unterschiedlichen Lehrenden sortiert aus.

```SQL  
SELECT Studiengang.Name AS Studiengang,
(SELECT COUNT(DISTINCT Lehrende.PID)
FROM Lehrende, Veranstaltung, Modulzuordnung
WHERE Lehrende.VID = Veranstaltung.VID
AND Veranstaltung.MID = Modulzuordnung.MID
AND Modulzuordnung.SID = Studiengang.SID) AS Anzahl_Lehrende
FROM Studiengang
ORDER BY Anzahl_Lehrende DESC;
```

13. Geben Sie für alle Lehrenden aus, wie viele Veranstaltungen sie lehren.

```SQL 
SELECT Person.Name AS Lehrendername, COUNT(Lehrende.VID) AS Anzahl_Veranstaltungen
FROM Person, Lehrende
WHERE Person.PID = Lehrende.PID
GROUP BY Person.PID;
```

14. Geben Sie die Lehrbeauftragten aus, die nur genau eine Veranstaltung anbieten.  

```SQL 
SELECT Person.Name AS Lehrendername, COUNT(Lehrende.VID) AS Anzahl_Veranstaltungen
FROM Person, Lehrende
WHERE Person.PID = Lehrende.PID
GROUP BY Person.PID
HAVING COUNT(Lehrende.VID) = 1;
```  



15. Geben Sie für jeden Studiengang die Semester (sofern ungleich NULL) aufsteigend sortiert mit der Summe der ECTS der enthaltenen Module an.

```SQL
SELECT DISTINCT Studiengang.Name AS Studiengangname, Modulzuordnung.Semester AS Semester, Sum(Modul.ECTS) AS ECTS
FROM Studiengang, Modulzuordnung, Modul
WHERE Modulzuordnung.SID = Studiengang.SID
AND Modulzuordnung.MID = Modul.MID
AND Modulzuordnung.Semester is NOT NULL
GROUP BY Studiengang.SID, Modulzuordnung.Semester
ORDER BY (Modulzuordnung.Semester) ASC;
``` 


Einen Ansatz zur Formulierung von SQL-Anfragen finden Sie u.a. in den Vorlesungsunterlagen am Ende von Kapitel "Gruppierungen in SQL".