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

|   |   |   |
|---|---|---|
|**MatrNr**|**KNr**|**Versuch**|
|**1**|**2**|**1**|
|**1**|**4**|**2**|
|**2**|**1**|**2**|
|**3**|**3**|**3**|

**Aufgabe 2.2**

Formulieren Sie weiterhin für die folgenden Aufgaben jeweils eine SQL-Anfrage:

1. Geben Sie die Namen aller Studierenden aus.
2. Geben Sie die Namen aller Klausuren aus, die um 08:00 Uhr geschrieben werden.
3. Geben Sie eine Liste aller Erstanmeldungen (nur 1. Versuch) für eine Klausur aus (Ausgabe: Name der Klausur, Name des Studierenden).
4. Geben Sie die Namen aller Klausuren aus, für die sich die Studentin "Meier" angemeldet hat.
5. Geben Sie die Namen aller Studierenden aus, die mindestens zwei Klausuren im letzten Versuch (3. Versuch) schreiben.