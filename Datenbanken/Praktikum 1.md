
**Aufgabe 1.1**

Geben Sie ein sinnvolles Beispiel für die Verwendung des Ren-Operators (Umbenennung) der Relationenalgebra an.  
Der Ren-Operator (Umbenennung) in der Relationenalgebra wird genutzt, um entweder eine Ergebnistabelle für spätere Abfragen weiterzuverwenden oder um Namenskonflikte zu vermeiden, insbesondere bei Selbst-Joins. Dadurch kann man gleiche Attributnamen aus verschiedenen Relationen eindeutig unterscheiden und die Lesbarkeit der Abfragen verbessern.
  

**Aufgabe 1.2**

Gegeben seien folgende Tabellen zur Bewertung von Mensagerichten:

_Tabelle STUDENT_

|   |   |
|---|---|
|**MatrNr**|**Name**|
|1|Meier|
|2|Meyer|
|3|Maier|

_  
Tabelle GERICHT_

|   |   |   |
|---|---|---|
|**GNr**|**Name**|**Art**|
|1|Pizza|Haupt|
|2|Tomatensuppe|Vor|
|3|Schnitzel|Haupt|
|4|Reis|Beilage|
|5|Pudding|Nach|

_  
Tabelle BEWERTUNG_

|   |   |   |
|---|---|---|
|**MatrNr**|**GNr**|**Sterne**|
|1|2|3|
|1|4|2|
|2|1|4|
|3|3|3|

  
Formulieren Sie für die folgenden Aufgaben jeweils einen Ausdruck in der Relationenalgebra und geben Sie zusätzlich jeweils die Ergebnisrelation an:

1. Geben Sie alle Arten von Gerichten aus.
		SELECT DISTINCT "Art" FROM "GERICHT";
2. Geben Sie die Namen aller Hauptgerichte (mit der Art „Haupt“) aus.
		SELECT "Name", "Art" FROM "GERICHT" WHERE "Art" = 'Haupt';
3. Geben Sie eine Liste aller einzelnen Bewertungen aus (Ausgabe: Name des Gerichts, Sterne).
		SELECT "GERICHT"."Name", "BEWERTUNG"."Sterne" 
		FROM "BEWERTUNG" 
		JOIN "GERICHT" ON "BEWERTUNG"."GNr" = "GERICHT"."GNr";
4. Geben Sie die Namen aller Gerichte aus, die der Student Meier bewertet hat.
	1. SELECT "GERICHT"."Name"
		FROM "BEWERTUNG" 
		JOIN "STUDENT" ON "BEWERTUNG"."MatrNr" = "STUDENT"."MatrNr" 
		JOIN "GERICHT" ON "BEWERTUNG"."GNr" = "GERICHT"."GNr" 
		WHERE "STUDENT"."Name" = 'Meier';
5. Geben Sie alle Bewertungen aus (Name Student, Name Gericht, Sterne), die mindestens vier Sterne haben.
		SELECT "STUDENT"."Name" AS Studenten_Name, "GERICHT"."Name" AS Name_des_Gerichtes , "BEWERTUNG"."Sterne"
		FROM "BEWERTUNG" 
		JOIN "STUDENT" ON "BEWERTUNG"."MatrNr" = "STUDENT"."MatrNr" 
		JOIN "GERICHT" ON "BEWERTUNG"."GNr" = "GERICHT"."GNr" 
		WHERE "BEWERTUNG"."Sterne" >= 4;
6. Geben Sie aus, welche Studierenden das Schnitzel bewertet haben.
		SELECT "STUDENT"."Name" 
		FROM "BEWERTUNG" 
		JOIN "STUDENT" ON "BEWERTUNG"."MatrNr" = "STUDENT"."MatrNr" 
		JOIN "GERICHT" ON "BEWERTUNG"."GNr" = "GERICHT"."GNr" 
		WHERE "GERICHT"."Name" = 'Schnitzel';
7. Geben Sie aus, welcher Studierende mindestens zwei Bewertungen abgegeben hat.
		SELECT "STUDENT"."Name" 
		FROM "BEWERTUNG" 
		JOIN "STUDENT" ON "BEWERTUNG"."MatrNr" = "STUDENT"."MatrNr" 
		GROUP BY "STUDENT"."Name" 
		HAVING COUNT("BEWERTUNG"."GNr") >= 2;

  
  
**Aufgabe 1.3  
**Installieren Sie Docker gemäß der Anleitung. Jedes Gruppenmitglied muss diese Aufgabe erfüllen und im Praktikum das Ergebnis präsentieren. Sollten Sie keinen Laptop besitzen, besteht die Möglichkeit, die Rechner im Praktikumsraum zu verwenden.