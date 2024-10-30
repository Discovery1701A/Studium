Das zur Erzeugung der Datenbank erforderliche SQL-Skript mhbdb.sql finden Sie im Moodle-Kurs unter [Datenbanken](https://moodle.hs-emden-leer.de/moodle/mod/url/view.php?id=323657 "Datenbanken").   

Beachten Sie folgende Randbedingungen:

- Die in der Tabelle Modul angegebene PID verweist auf den Modulverantwortlichen.
- Falls das Attribute Semester in der Tabelle Modulzuordnung NULL ist, handelt es sich um ein Wahlpflichtmodul, das keinem Zertifikat zugeordnet ist.

Formulieren Sie für folgende Anfragen SQL-Anweisungen:

1. Geben Sie aus, wie viele Module in der Datenbank gespeichert sind.
```SQL
SELECT DISTINCT COUNT( mid ) AS Anzahl FROM modul
```
2. Geben Sie alle Module (Name) aus, die weniger als 4 ECTS-Punkte haben.
3. 
4. Geben Sie alle Module aus, in denen eine Klausur als Prüfung möglich ist.  
    
4. Geben Sie die Namen der Module aus, bei denen als Modulverantwortlicher "F. Rump" angegeben ist.  
    
5. Geben Sie alle Studiengänge mit den zugehörigen Zertifikaten aus (Ausgabe: Studiengang, Zertifikat).
6. Geben Sie alle Lehrenden und die Veranstaltungen aus, die sie unterrichten.
7. Geben Sie alle Module aus, sofern die enthaltenen Veranstaltung in Summe mehr als vier SWS haben.  
    
8. Geben Sie nur die Veranstaltungen aus, denen mehrere Lehrende zugeordnet sind.  
    
9. Geben Sie alle Studiengänge absteigend nach der Anzahl der "reinen" Wahlpflichtmodule, die somit keinem Zertifikat zugeordnet sind, aus.
10. Geben Sie zu jedem Studiengang und jedem Zertifikat in dem jeweiligen Studiengang die Anzahl der zugehörigen Module aus, wobei die Studiengänge und Zertifikate alphabetisch sortiert sein sollen.
11. Geben Sie zu jedem Studiengang die Anzahl der Zertifikate aus, sofern der Studiengang mehr als drei Zertifikate hat.
12. Geben Sie die Studiengänge absteigend nach den daran beteiligten, unterschiedlichen Lehrenden sortiert aus.
13. Geben Sie für alle Lehrenden aus, wie viele Veranstaltungen sie lehren.
14. Geben Sie die Lehrbeauftragten aus, die nur genau eine Veranstaltung anbieten.  
    
15. Geben Sie für jeden Studiengang die Semester (sofern ungleich NULL) aufsteigend sortiert mit der Summe der ECTS der enthaltenen Module an.

Einen Ansatz zur Formulierung von SQL-Anfragen finden Sie u.a. in den Vorlesungsunterlagen am Ende von Kapitel "Gruppierungen in SQL".