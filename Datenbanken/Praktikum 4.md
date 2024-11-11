Legen Sie eine Tabelle der folgenden Form in einer neuen Datenbank an:

CREATE TABLE Student(  
  Matnr INTEGER,  
  Name VARCHAR(16),  
  Semester VARCHAR(10),  
  CONSTRAINT PK_Student PRIMARY KEY(matnr)  
);

Schreiben Sie ein Java-Programm, mit dem man

- einen Studierenden ergänzen (scheitert mit Fehlermeldung, wenn Matrikelnummer vorhanden)
- alle Studierenden ausgeben
- die Namen der Studierenden ändern
- alle Studierenden löschen
- das Programm beenden

kann. Semester stellt dabei das Semester der Einschreibung dar, also z.B. WS 2019/20. Für das Einlesen der Eingaben vom Benutzer können Sie die [Klasse Input](https://sync.academiccloud.de/index.php/s/mgtokLAhGFvsT54?path=%2Fjdbc) verwenden. In dem [Ordner](https://sync.academiccloud.de/index.php/s/mgtokLAhGFvsT54?path=%2Fjdbc) ist ebenfalls der JDBC-Treiber für PostgreSQL zu finden.

Wichtig: Änderungen am Datenbestand (Einfügen, Ändern, Löschen) sind nicht über ein ResultSet, sondern direkt über INSERT-, UPDATE- und DELETE-Anweisungen umzusetzen!  

Hier ein Beispieldialog für das Ändern des Namens, die Eingaben des Benutzers sind dabei fett und kursiv dargestellt:

Was wollen Sie?  
(0) Programm beenden  
(1) neuen Studierenden hinzufuegen  
(2) alle Studierenden zeigen  
(3) Namen eines Studierenden aendern  
(4) alle Studierenden loeschen  
_**3**_  
Matrikelnummer: _**72**_  
neuer Name: _**Susanne**_  
Erfolgreich geaendert!