
### **Aufgabe 1: ER-Diagramm**
Das Unternehmen „TechStore“ benötigt eine Datenbank, um folgende Informationen zu verwalten:
- Der Store verkauft verschiedene ==Elektronikgeräte== (z. B. Laptop „TechMate“, Handy „SmartX“).
- Jedes ==Gerät== hat eine ==Artikelnummer==, ===eine Bezeichnung==, ==einen Preis== und gehört zu ==einer Kategorie== (z. B. Laptop, Handy).
- ==Kategorien== haben ==eine Nummer== und ==eine Bezeichnung==0.
- ==Geräte== werden von ==Lieferanten== geliefert, die eine ==Lieferantennummer==, ==einen Namen== und ==einen Standort== haben.
- ==Bestellungen== umfassen ==mehrere Geräte== und werden von Kunden aufgegeben. Kunden haben eine Kundennummer, einen Namen und eine Adresse.

**Aufgabe**: Erstellen Sie ein ER-Diagramm mit Entitäten, Beziehungen, Attributen und Kardinalitäten. Markieren Sie Schlüssel und machen Sie ggf. Annahmen.

---

### **Aufgabe 2: Normalisierung**
Eine Tabelle enthält folgende Daten über ein Autohaus:
| **AutoNr** | **Modell** | **Hersteller** | **Preis** | **KäuferName** | **KäuferOrt** |
|------------|------------|----------------|-----------|----------------|---------------|
| 1          | Golf       | VW             | 20000     | Müller         | Berlin        |
| 2          | Passat     | VW             | 25000     | Meier          | München       |
| 3          | Focus      | Ford           | 22000     | Schmidt        | Hamburg       |

**Aufgabe**:
1. In welcher Normalform befindet sich die Tabelle?
		erste Normalform eine spalte enthält nur einfache werte und keine mehrfachwerte
1. Überführen Sie die Tabelle in die 3. Normalform. Geben Sie die resultierenden Tabellen an.

| Modell | Hersteller | Preis |
| ------ | ---------- | ----- |
| Golf   | VW         | 20000 |
| Passat | VW         | 25000 |
| Focus  | Ford       | 22000 |

| KäuferName | KäuferOrt | AutoNr |
| ---------- | --------- | ------ |
| Müller     | Berlin    | 1      |
| Meier      | München   | 2      |
| Schmidt    | Hamburg   | 3      |


| AutoNr | Modell |
| ------ | ------ |
| 1      | Golf   |
| 2      | Passat |
| 3      | Focus  |


---

### **Aufgabe 3: SQL-Abfragen**
Gegeben sind folgende Tabellen:
- **City(Name, Country, Province, Population)**
- **Country(Name, Code, Capital, Area, Population)**
- **Is_Member(Country, Organization, Type)**
- **Encompasses(Country, Continent, Percentage)**

**Aufgaben**:
a) Geben Sie die Namen aller Städte mit mehr als 500.000 Einwohnern alphabetisch sortiert aus.  
	Proj(Sel(City, City.population > 500000),[Name])
		Select Name
			From City
    Where Population > 500000
b) Welche Länder (Name) in der EU haben weniger als 1.000.000 Einwohner?  
	Proj(Sel(Country, Country.Population < 1000000 AND Country.Continent = 'EU'),[Name])
    Select Name
      From Country
    Where Population < 1000000 AND Continent = 'EU'
c) Geben Sie die Anzahl der Länder in Südamerika aus.  
Proj(Sel(Country x Encompasses, Country.Code = Encompasses.Country AND Encompasses.Continent = 'South America'),[Name])
SELECT COUNT(Country)
From Encompasses
Where Continent = 'South America'
d) Welche Länder (Name) haben keine Städte in der Tabelle **City**?  
Proj(Sel(Country x City, Country.Code = City.Country),[Name])
SELECT Country.Name
From Country
Where Country.Code NOT IN (Select Country From City)



---

### **Aufgabe 4: Java-Code Analyse**
Ein Java-Programm enthält folgenden Codeausschnitt:

```java
package datenbanken.jdbc;

import java.sql.*;

public class DBinsert {
    static String DBUrl = "jdbc:postgresql://localhost:5432/Store";

    public static void main(String[] args) {
        Connection con = null;
        Statement stmt = null;

        try {
            Class.forName("org.postgresql.Driver");
            con = DriverManager.getConnection(DBUrl, "admin", "1234");
            stmt = con.createStatement();
            stmt.executeUpdate("INSERT INTO Artikel VALUES (101, 'Laptop', 1200);");
            stmt.executeUpdate("INSERT INTO Artikel VALUES (102, 'Handy', 800);");
            stmt.close();
            con.close();
        } catch (SQLException | ClassNotFoundException ex) {
            System.err.println(ex);
        }
    }
}
```

**Aufgaben**:
1. Beschreiben Sie, was der Code macht.
		Der Code stellt eine verbindung zu einer Datenbank her und fügt zwei Artikel in die Tabelle Artikel ein.
		danache wird die verbindung geschlossen.
1. Finden Sie drei Fehler und schlagen Sie Verbesserungen vor.

---

### **Aufgabe 5: Transaktionen**
Ein Onlineshop möchte Bestellungen und Zahlungen in einer Transaktion verwalten. Folgende Aktionen sollen ausgeführt werden:
- Die Bestellung wird in die Tabelle **Bestellung** eingefügt.
- Die Zahlung wird in die Tabelle **Zahlung** eingefügt.
- Falls ein Fehler auftritt, sollen beide Aktionen rückgängig gemacht werden.

**Aufgabe**: Schreiben Sie den SQL-Code für die Transaktion.

Begin
  Insert into Bestellung values (101, '2022-01-01');
  Insert into Zahlung values (101, 100);
  RollBack
  Commit

---

### **Aufgabe 6: Views**
Gegeben ist die Tabelle **Mitarbeiter(MiNr, Name, Abteilung, Gehalt)**.

**Aufgabe**:
1. Erstellen Sie eine View, die nur Mitarbeiter der Abteilung „Verkauf“ und ihr Gehalt anzeigt.
		Create View Verkauf as
		    Select Name, Gehalt
    From Mitarbeiter
    Where Abteilung = 'Verkauf'
1. Schreiben Sie eine SQL-Abfrage, die den durchschnittlichen Gehalt der Mitarbeiter aus der View berechnet.
    Select AVG(Gehalt)
    From Verkauf



---

### **Aufgabe 7: Multiple Choice**
a) Welche der folgenden Aussagen zu Transaktionen ist korrekt?  
- [ ] Eine Transaktion wird durch `ROLLBACK` dauerhaft gespeichert.  
- [x] `COMMIT` speichert die Änderungen einer Transaktion.  
- [x] `SAVEPOINT` setzt einen Sicherungspunkt.  

b) Welche der folgenden Aussagen zu Normalisierung ist korrekt?  
- [ ] In der ersten Normalform dürfen Attribute Listen enthalten.  
- [x] Die dritte Normalform eliminiert funktionale Abhängigkeiten zwischen Nichtschlüsselattributen.  

---

Falls du weitere Aufgaben oder vertiefende Inhalte benötigst, lass es mich wissen!