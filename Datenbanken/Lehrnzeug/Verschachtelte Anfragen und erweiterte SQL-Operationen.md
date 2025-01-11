
#### **1. Mengenoperationen**
1. **Vereinigung (`UNION` und `UNION ALL`):**
   - **Beispiel: Gattungen in Gehege 2 oder 3**
     ```sql
     SELECT Gattung FROM Tier WHERE GNr = 2
     UNION
     SELECT Gattung FROM Tier WHERE GNr = 3;
     ```

   - **`UNION ALL`:** Beinhaltet doppelte Einträge.

2. **Schnittmenge (`INTERSECT`):**
   - **Beispiel: Gattungen, die in beiden Gehegen vorkommen**
     ```sql
     SELECT Gattung FROM Tier WHERE GNr = 2
     INTERSECT
     SELECT Gattung FROM Tier WHERE GNr = 3;
     ```

3. **Differenz (`EXCEPT`):**
   - **Beispiel: Gattungen in Gehege 2, aber nicht in Gehege 3**
     ```sql
     SELECT Gattung FROM Tier WHERE GNr = 2
     EXCEPT
     SELECT Gattung FROM Tier WHERE GNr = 3;
     ```

---

#### **2. Teilanfragen**
1. **In der `SELECT`-Zeile:**
   - **Beispiel: Gehege mit Gesamtfläche aller Gehege**
     ```sql
     SELECT Gehege.*, (SELECT SUM(Flaeche) FROM Gehege) AS Gesamtflaeche
     FROM Gehege;
     ```

2. **In der `WHERE`-Bedingung:**
   - **Beispiel: Größtes Gehege**
     ```sql
     SELECT Gname, Flaeche
     FROM Gehege
     WHERE Flaeche = (SELECT MAX(Flaeche) FROM Gehege);
     ```

3. **Mit `ANY` und `ALL`:**
   - **Beispiel: Gehege, die mindestens so groß sind wie alle Gehege mit Hasen**
     ```sql
     SELECT Gname
     FROM Gehege
     WHERE Flaeche >= ALL (
         SELECT Flaeche
         FROM Gehege JOIN Tier ON Gehege.GNr = Tier.GNr
         WHERE Tier.Gattung = 'Hase');
     ```

---

#### **3. Abhängigkeiten zwischen äußeren und inneren Anfragen**
1. **Abhängige Unterabfragen:**
   - **Beispiel: Gehege mit Hasen**
     ```sql
     SELECT Gname
     FROM Gehege
     WHERE 'Hase' IN (
         SELECT Gattung
         FROM Tier
         WHERE Gehege.GNr = Tier.GNr);
     ```

---

#### **4. Joins**
1. **Standard-Joins:**
   - **Beispiel: Verknüpfung von Verkäufer und Verkäufen**
     ```sql
     SELECT *
     FROM Verkaeufer
     JOIN Verkauf ON Verkaeufer.VNr = Verkauf.VNr;
     ```

2. **Left Join:**
   - Zeigt alle Einträge der linken Tabelle, auch wenn keine Entsprechung in der rechten Tabelle vorhanden ist.

3. **Right Join:**
   - Zeigt alle Einträge der rechten Tabelle, auch ohne Entsprechung in der linken Tabelle.

4. **Full Join:**
   - Zeigt alle Einträge aus beiden Tabellen, unabhängig von Entsprechungen.

---

#### **5. Teilanfragen in der `FROM`-Zeile**
- **Beispiel: Fläche, die Hasen in jedem Gehege verbrauchen**
   ```sql
   SELECT Gehegename, COUNT(*) * Art.MinFlaeche AS Verbrauch
   FROM Gehege
   JOIN Tier ON Gehege.GNr = Tier.GNr
   JOIN Art ON Tier.Gattung = Art.Gattung
   WHERE Tier.Gattung = 'Hase'
   GROUP BY Gehegename, Art.MinFlaeche;
   ```

---

#### **6. Indizes**
1. **Index erstellen:**
   ```sql
   CREATE INDEX idx_customer_id ON orders(customer_id);
   ```

2. **Index löschen:**
   ```sql
   DROP INDEX idx_customer_id;
   ```

3. **Wann Indizes sinnvoll sind:**
   - Häufige Verwendung in `WHERE`, `JOIN`, oder Sortierungen.
   - Große Tabellen mit selektiven Abfragen.
   - Automatisch erstellt für Primärschlüssel.

---
