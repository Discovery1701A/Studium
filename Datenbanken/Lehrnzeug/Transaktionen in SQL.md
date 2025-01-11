
#### **1. Was ist eine Transaktion?**
- **Definition**: Eine Transaktion ist eine Menge von SQL-Befehlen, die zusammen ausgeführt werden und bei Bedarf vollständig rückgängig gemacht werden können.
- **Beispiel**:
  - **BEGIN**: Startet eine Transaktion.
  - **COMMIT**: Speichert alle Änderungen der Transaktion dauerhaft in der Datenbank.
  - **ROLLBACK**: Macht alle Änderungen der Transaktion rückgängig.

---

#### **2. Transaktionsbefehle in PostgreSQL**

| **Befehl**              | **Beschreibung**                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| `BEGIN`                 | Startet eine Transaktion.                                                        |
| `COMMIT`                | Übernimmt die Änderungen der Transaktion dauerhaft.                              |
| `SAVEPOINT <name>`      | Setzt einen Sicherungspunkt innerhalb der Transaktion.                           |
| `ROLLBACK TO <name>`    | Setzt die Transaktion auf den Sicherungspunkt zurück.                            |
| `ROLLBACK`              | Macht alle Änderungen seit `BEGIN` rückgängig.                                   |

**Beispiel:**
```sql
BEGIN;
INSERT INTO Gehege VALUES (4, 'Freiland', 100);
SAVEPOINT freiland;
INSERT INTO Gehege VALUES (5, 'Käfig', 10);
ROLLBACK TO freiland;  -- Rückgängig bis zum SAVEPOINT
COMMIT;  -- Speichert alle verbleibenden Änderungen
```

---

#### **3. Probleme bei parallelem Zugriff**
1. **Lost Update**: Änderungen gehen verloren, wenn zwei Transaktionen gleichzeitig dieselben Daten ändern.
2. **Dirty Read**: Eine Transaktion liest unbestätigte Änderungen einer anderen Transaktion.
3. **Unrepeatable Read**: Wiederholtes Lesen derselben Daten liefert unterschiedliche Ergebnisse.
4. **Phantom Read**: Eine Abfrage liefert unterschiedliche Ergebnisse, weil andere Transaktionen neue Daten einfügen.

---

#### **4. ACID-Prinzip**
- **Atomicity**: Eine Transaktion ist unteilbar (alles oder nichts).
- **Consistency**: Nach der Transaktion ist die Datenbank konsistent.
- **Isolation**: Transaktionen beeinflussen sich nicht gegenseitig.
- **Durability**: Änderungen sind nach einem erfolgreichen `COMMIT` dauerhaft gespeichert.

---

#### **5. Isolationsgrade**

| **Isolationsgrad**        | **Mögliche Probleme**                   | **Beschreibung**                                                 |
|---------------------------|-----------------------------------------|-------------------------------------------------------------------|
| `READ UNCOMMITTED`        | Dirty Read, Unrepeatable Read, Phantom Read | Zugriff auf unbestätigte Änderungen möglich.                     |
| `READ COMMITTED`          | Unrepeatable Read, Phantom Read        | Standard. Nur bestätigte Daten werden gelesen.                   |
| `REPEATABLE READ`         | Phantom Read                           | Daten sind innerhalb der Transaktion konstant.                   |
| `SERIALIZABLE`            | Keine                                  | Transaktionen wirken vollständig isoliert, aber mit höheren Wartezeiten. |

---

#### **6. Transaktionssteuerung in JDBC**
- **Standard:** Jede Anweisung führt automatisch ein `COMMIT` aus.
- **Methoden des Interface `Connection`:**

| **Methode**                | **Beschreibung**                                                     |
|----------------------------|---------------------------------------------------------------------|
| `setAutoCommit(boolean b)` | Schaltet automatisches `COMMIT` ein/aus.                            |
| `commit()`                 | Speichert die Änderungen der Transaktion.                          |
| `rollback()`               | Macht alle Änderungen der Transaktion rückgängig.                  |
| `setSavepoint()`           | Setzt einen Sicherungspunkt innerhalb der Transaktion.             |
| `rollback(Savepoint s)`    | Springt zu einem spezifischen Sicherungspunkt zurück.              |

**Beispiel:**
```java
Connection con = DriverManager.getConnection(...);
con.setAutoCommit(false);  // Automatisches COMMIT deaktivieren
Statement s = con.createStatement();
s.executeUpdate("INSERT INTO Gehege VALUES (6, 'Savanne', 200);");
con.commit();  // Änderungen speichern
```

---

#### **7. Tipps und Hinweise**
1. **Schattenspeicher-Verfahren**:
   - Änderungen werden vor einem `COMMIT` nur lokal gespeichert und erst danach in die Datenbank übernommen.
   - Andere Transaktionen sehen die Änderungen nicht.
   
2. **Deadlocks**:
   - Treten auf, wenn zwei Transaktionen aufeinander warten.
   - Lösung: Abbruch einer Transaktion nach einer Zeitschranke.

3. **Wahl des Isolationsgrades**:
   - Für hohe Performance und Konsistenz sollte der Isolationsgrad an die Anforderungen der Anwendung angepasst werden.

---
