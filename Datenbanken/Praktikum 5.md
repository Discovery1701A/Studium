Vorbereitung: [Installation Eclipse und Webanwendung Projektverwaltung](https://pad.gwdg.de/s/N_Lj1VRGJ)

**Aufgabe**

Die vorgegebene Webanwendung zur Projektverwaltung speichert aktuell alle Daten (Personen, Projekte) in einer In-Memory-Datenbank ([EclipseStore](https://eclipsestore.io/)). Die Daten werden dabei in dem Verzeichnis "dataea3" im Home-Verzeichnis des Benutzers persistiert, dieses kann bei Bedarf auch wieder gelöscht werden, um die Daten in den Ursprungszustand zu bringen.

Ihre Aufgabe besteht nun darin, die Daten über eine PostgreSQL-Datenbank (über JDBC) verfügbar zu machen. Folgende Teilaufgaben sind dazu umzusetzen:

1. Erstellen Sie eine Datenbank und entsprechende Tabellen, um alle für die Projektverwaltung relevanten Daten dort speichern zu können. Richten Sie für die Tabellen Primär- und Fremdschlüssel ein. Ihre Tabellenstruktur sollte dazu folgende Daten bereitstellen, die hier mit den passenden Java-Datentypen aufgeführt sind (siehe auch Paket model):  
    - Person: Personennummer (int), Vorname (String), Nachname (String), Position (String)
    - Projekt: Projektnummer (int), Name (String), Kunde (String)
    - Projektmitarbeit: Personennummer (int), Projektnummer (int), Aufgabe (String)

```SQL

-- Erstellen der Tabelle 'Person'
CREATE TABLE Person (
    Personennummer SERIAL PRIMARY KEY,  -- generiert fortlaufende Zahl
    Vorname VARCHAR(100) NOT NULL,
    Nachname VARCHAR(100) NOT NULL,
    Position VARCHAR(100) NOT NULL
);

-- Erstellen der Tabelle 'Projekt'
CREATE TABLE Projekt (
    Projektnummer SERIAL PRIMARY KEY, -- generiert fortlaufende Zahl
    Name VARCHAR(200) NOT NULL,
    Kunde VARCHAR(200) NOT NULL
);

-- Erstellen der Tabelle 'Projektmitarbeit'
CREATE TABLE Projektmitarbeit (
    Personennummer INT NOT NULL,
    Projektnummer INT NOT NULL,
    Aufgabe VARCHAR(255) NOT NULL,
    PRIMARY KEY (Personennummer, Projektnummer),
    CONSTRAINT fk_person FOREIGN KEY (Personennummer) REFERENCES Person(Personennummer) ON DELETE CASCADE, -- wenn Person gelöscht wird wird auch der Eintrag hier gelöscht
    CONSTRAINT fk_projekt FOREIGN KEY (Projektnummer) REFERENCES Projekt(Projektnummer) ON DELETE CASCADE -- wenn das Projekt gelöscht wird wird auch der Eintrag hier gelöscht
);
```

1. Aktuell wird die Datenverwaltung der Anwendung über die Klasse Database durchgeführt. Machen Sie sich mit den dort implementierten Methoden vertraut, indem Sie sich die JavaDoc-Kommentare anschauen.
2. Redefinieren Sie alle Methoden der Klasse Database in der bereits vorhandenen Klasse SQLDatabase. Die Methoden sind dort bereits vorhanden, rufen aber bislang nur die Methoden der Superklasse (Database) auf. Alle Methoden sollen dabei die jeweiligen Operationen über JDBC auf der in Teilaufgabe 1 erstellten Datenbank ausführen.

**Hinweis:** Bei dieser Webanwendung ist es erforderlich, den JDBC-Treiber explizit über Class.forName(...) vor dem Verbindungsaufbau zu laden (siehe Vorlesungsunterlagen)!