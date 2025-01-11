
#### **Was ist JDBC(Java Database Connectivity)?**
- Schnittstelle für die Verbindung von Java-Programmen mit relationalen Datenbanken.
- SQL-Anfragen direkt aus Java ausführen.
- Unabhängig vom verwendeten Datenbank-Management-System (DBMS).

---

### **1. Verbindungsaufbau mit einer Datenbank**

1. **Laden des Treibers:**
   ```java
   Class.forName("org.postgresql.Driver");
   ```
   (Ab JDBC 4.0 automatisch, wenn der Treiber im CLASSPATH ist.)

2. **Verbindung herstellen:**
   ```java
   Connection con = DriverManager.getConnection(
       "jdbc:postgresql://localhost:5432/Zoo?user=root&password=myPassword");
   ```

3. **Verbindung beenden:**
   ```java
   con.close();
   ```

---

### **2. SQL-Anfragen ausführen**

1. **Statement-Objekt erstellen:**
   ```java
   Statement stmt = con.createStatement();
   ```

2. **Anfrage ausführen:**
   ```java
   ResultSet rs = stmt.executeQuery("SELECT * FROM Gehege");
   ```

3. **Ergebnisse verarbeiten:**
   ```java
   while (rs.next()) {
       System.out.println("Gehegename: " + rs.getString("GName"));
   }
   ```

4. **Metadaten auslesen:**
   ```java
   ResultSetMetaData rsmd = rs.getMetaData();
   int spaltenAnzahl = rsmd.getColumnCount();
   for (int i = 1; i <= spaltenAnzahl; i++) {
       System.out.println("Spalte " + i + ": " + rsmd.getColumnName(i));
   }
   ```

---

### **3. Daten ändern (INSERT, UPDATE, DELETE)**

1. **Daten einfügen:**
   ```java
   stmt.executeUpdate("INSERT INTO Gehege (GNr, GName, Flaeche) VALUES (4, 'Wald', 25)");
   ```

2. **Daten aktualisieren:**
   ```java
   stmt.executeUpdate("UPDATE Gehege SET Flaeche = 30 WHERE GNr = 4");
   ```

3. **Daten löschen:**
   ```java
   stmt.executeUpdate("DELETE FROM Gehege WHERE GNr = 4");
   ```

---

### **4. Verwendung von Prepared Statements**

- **Vorteile:**
  - Erhöhte Sicherheit (SQL-Injection vermeiden).
  - Wiederverwendbarkeit bei ähnlichen Anfragen.

1. **PreparedStatement erstellen:**
   ```java
   PreparedStatement prep = con.prepareStatement(
       "SELECT * FROM Tier WHERE Gattung = ? AND GNr = ?");
   ```

2. **Parameter setzen:**
   ```java
   prep.setString(1, "Baer");
   prep.setInt(2, 1);
   ```

3. **Anfrage ausführen:**
   ```java
   ResultSet rs = prep.executeQuery();
   ```

---

### **5. Bearbeiten von Ergebnismengen (ResultSet)**

1. **Typen von ResultSets:**
   - `TYPE_FORWARD_ONLY`: Nur vorwärts navigieren (Standard).
   - `TYPE_SCROLL_INSENSITIVE`: Navigieren in beide Richtungen, Änderungen in der Datenbank werden ignoriert.
   - `TYPE_SCROLL_SENSITIVE`: Navigieren in beide Richtungen, Änderungen werden berücksichtigt.

2. **Navigation:**
   ```java
   rs.next();        // Nächste Zeile
   rs.previous();    // Vorherige Zeile
   rs.absolute(3);   // Springt zur dritten Zeile
   rs.relative(-2);  // Springt zwei Zeilen zurück
   ```

3. **Daten ändern:**
   ```java
   rs.updateString("GName", "Savanne");
   rs.updateRow();   // Änderungen übernehmen
   ```

4. **Zeilen einfügen:**
   ```java
   rs.moveToInsertRow();
   rs.updateInt("GNr", 5);
   rs.updateString("GName", "Steppe");
   rs.updateInt("Flaeche", 50);
   rs.insertRow();
   rs.moveToCurrentRow();  // Zurück zur ursprünglichen Zeile
   ```

---

### **6. Generierte Schlüsselwerte**

1. **Automatische Schlüsselwerte:**
   ```sql
   CREATE TABLE Student (
       MatNr SERIAL PRIMARY KEY,
       Name VARCHAR(100)
   );
   ```

2. **Einfügen und Abfragen der generierten Schlüssel:**
   ```java
   Statement stmt = con.createStatement();
   stmt.executeUpdate("INSERT INTO Student (Name) VALUES ('Meier')", Statement.RETURN_GENERATED_KEYS);
   ResultSet rs = stmt.getGeneratedKeys();
   if (rs.next()) {
       int id = rs.getInt(1);
       System.out.println("Neue Matrikelnummer: " + id);
   }
   ```

---

### **7. Überblick über wichtige JDBC-Methoden**

| Methode                        | Zweck                             |
|--------------------------------|-----------------------------------|
| `DriverManager.getConnection()`| Verbindung zur Datenbank          |
| `Statement.executeQuery()`     | SQL-Abfrage ausführen             |
| `Statement.executeUpdate()`    | Änderungen ausführen (INSERT, ...)|
| `ResultSet.next()`             | Zur nächsten Zeile springen       |
| `ResultSet.getString()`        | Spaltenwerte auslesen             |
| `ResultSetMetaData`            | Informationen über Ergebnismenge  |
| `PreparedStatement.setString()`| Parameter für Abfragen setzen     |

---
