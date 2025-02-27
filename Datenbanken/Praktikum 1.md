
**Aufgabe 1.1**

Geben Sie ein sinnvolles Beispiel für die Verwendung des Ren-Operators (Umbenennung) der Relationenalgebra an.  

Der Ren-Operator (Umbenennung) in der Relationenalgebra wird genutzt, um entweder eine Ergebnistabelle für spätere Abfragen weiterzuverwenden oder um Namenskonflikte zu vermeiden, insbesondere bei Selbst-Joins. Dadurch kann man gleiche Attributnamen aus verschiedenen Relationen eindeutig unterscheiden und die Lesbarkeit der Abfragen verbessern.
  

**Aufgabe 1.2**

Gegeben seien folgende Tabellen zur Bewertung von Mensagerichten:

**_Tabelle STUDENT_**

|            |          |
| ---------- | -------- |
| **MatrNr** | **Name** |
| 1          | Meier    |
| 2          | Meyer    |
| 3          | Maier    |

**_Tabelle GERICHT_**

|   |   |   |
|---|---|---|
|**GNr**|**Name**|**Art**|
|1|Pizza|Haupt|
|2|Tomatensuppe|Vor|
|3|Schnitzel|Haupt|
|4|Reis|Beilage|
|5|Pudding|Nach|

**_Tabelle BEWERTUNG_**

|            |         |            |
| ---------- | ------- | ---------- |
| **MatrNr** | **GNr** | **Sterne** |
| 1          | 2       | 3          |
| 1          | 4       | 2          |
| 2          | 1       | 4          |
| 3          | 3       | 3          |

  
Formulieren Sie für die folgenden Aufgaben jeweils einen Ausdruck in der Relationenalgebra und geben Sie zusätzlich jeweils die Ergebnisrelation an:

1. Geben Sie alle Arten von Gerichten aus.

```SQL
		SELECT DISTINCT "Art" FROM "GERICHT";
```
		
Proj(GERICHT,[Art])

| Art     |
| ------- |
| Beilage |
| Vor     |
| Nach    |
| Haupt   |



2. Geben Sie die Namen aller Hauptgerichte (mit der Art „Haupt“) aus.

```SQL
		SELECT "Name", "Art" FROM "GERICHT" WHERE "Art" = 'Haupt';
```
		
Proj(Sel(Gericht,Gericht.Art = 'Haupt'),[Name,Art])

| Name      | Art   |
| --------- | ----- |
| Schnitzel | Haupt |
| Pizza     | Haupt |

3. Geben Sie eine Liste aller einzelnen Bewertungen aus (Ausgabe: Name des Gerichts, Sterne).

```SQL
		SELECT "GERICHT"."Name", "BEWERTUNG"."Sterne" 
		FROM "BEWERTUNG" 
		JOIN "GERICHT" ON "BEWERTUNG"."GNr" = "GERICHT"."GNr";
```
		
Proj(Sel(GERICHT X BEWERTUNG, GERICHT.GNr = BERWERTUNG.GNr),[Name,Sterne])


| Name         | Sterne |
| ------------ | ------ |
| Schnitzel    | 3      |
| Pizza        | 4      |
| Reis         | 2      |
| Tomatensuppe | 3      |


4. Geben Sie die Namen aller Gerichte aus, die der Student Meier bewertet hat.

```SQL
		SELECT "GERICHT"."Name"
		FROM "BEWERTUNG" 
		JOIN "STUDENT" ON "BEWERTUNG"."MatrNr" = "STUDENT"."MatrNr" 
		JOIN "GERICHT" ON "BEWERTUNG"."GNr" = "GERICHT"."GNr" 
		WHERE "STUDENT"."Name" = 'Meier';
```

Proj(Sel(STUDENT X GERICHT X BEWERTUNG, GERICHT.GNr = BEWERTUNG.GNr AND STUDENT.MatrNr = BEWERTUNG.MatrNr AND STUDENT.Name = 'Meier' ), [GERICHT.Name])

| Name         |
| ------------ |
| Reis         |
| Tomatensuppe |


5. Geben Sie alle Bewertungen aus (Name Student, Name Gericht, Sterne), die mindestens vier Sterne haben.

```SQL
SELECT "STUDENT"."Name" AS Studenten_Name, "GERICHT"."Name" AS Name_des_Gerichtes , "BEWERTUNG"."Sterne"
FROM "BEWERTUNG" 
JOIN "STUDENT" ON "BEWERTUNG"."MatrNr" = "STUDENT"."MatrNr" 
JOIN "GERICHT" ON "BEWERTUNG"."GNr" = "GERICHT"."GNr" 
WHERE "BEWERTUNG"."Sterne" >= 4;
```
		
Proj(Sel(STUDENT X GERICHT X BEWERTUNG, GERICHT.GNr = BEWERTUNG.GNr AND STUDENT.MatrNr = BEWERTUNG.MatrNr AND BEWERTUNG.Sterne >= 4 ), [STUDENT.Name, GERICHT.Name, BEWERTUNG.Sterne])

| STUDENT.Name | GERICHT.Name | Sterne |
| ------------ | ------------ | ------ |
| Meyer        | Pizza        | 4      |

6. Geben Sie aus, welche Studierenden das Schnitzel bewertet haben.

```SQL
SELECT "STUDENT"."Name" 
FROM "BEWERTUNG" 
JOIN "STUDENT" ON "BEWERTUNG"."MatrNr" = "STUDENT"."MatrNr" 
JOIN "GERICHT" ON "BEWERTUNG"."GNr" = "GERICHT"."GNr" 
WHERE "GERICHT"."Name" = 'Schnitzel';
```
		
Proj(Sel(STUDENT X GERICHT X BEWERTUNG, GERICHT.GNr = BEWERTUNG.GNr AND STUDENT.MatrNr = BEWERTUNG.MatrNr AND GERICHT.Name = 'Schnitzel' ), [STUDENT.Name])

| Name  |
| ----- |
| Maier |

7. Geben Sie aus, welcher Studierende mindestens zwei Bewertungen abgegeben hat.

```SQL
SELECT "STUDENT"."Name" 
FROM "BEWERTUNG" 
JOIN "STUDENT" ON "BEWERTUNG"."MatrNr" = "STUDENT"."MatrNr" 
GROUP BY "STUDENT"."Name" 
HAVING COUNT("BEWERTUNG"."GNr") >= 2;
```

Proj(Sel(Sel Ren(BEWERTUNG ,B1) X Ren(BEWERTUNG,B2), B1.MatrNr = B2.MatrNr AND B1.GrNr <> B2.GrNr )X STUDENT , STUDENT.MatrNr = B1.MatrNr),[Name])

| Name  |
| ----- |
| Meier |

  
  
**Aufgabe 1.3**
*Installieren Sie Docker gemäß der Anleitung. Jedes Gruppenmitglied muss diese Aufgabe erfüllen und im Praktikum das Ergebnis präsentieren. Sollten Sie keinen Laptop besitzen, besteht die Möglichkeit, die Rechner im Praktikumsraum zu verwenden.*