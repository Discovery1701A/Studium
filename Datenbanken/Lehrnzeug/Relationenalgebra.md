
#### **Grundlagen der Relationenalgebra**
- Formale Grundlage der Datenbanktheorie.
- Beinhaltet Operatoren für das Arbeiten mit Relationen (Tabellen).

---

### **Elementare Operatoren**
1. **Mengenoperatoren** (für vereinigungsverträgliche Relationen):
   - **Schnittmenge (R ∩ S)**: Einträge, die in beiden Relationen vorkommen.
   - **Vereinigung (R ∪ S)**: Alle Einträge aus beiden Relationen.
   - **Differenz (R − S)**: Einträge, die nur in der ersten, aber nicht in der zweiten Relation vorkommen.

2. **Projektion (Proj(R, [Attr1, Attr2, ...]))**:
   - Auswahl bestimmter Spalten aus einer Relation.
   - Entfernt nicht benötigte Attribute.

3. **Umbenennung (Ren(R, T))**:
   - Gibt einer Relation einen neuen Namen, um Verknüpfungen mit sich selbst zu ermöglichen.

4. **Auswahl (Sel(R, Bedingung))**:
   - Filtert Zeilen basierend auf Bedingungen.
   - Bedingungen können Vergleichsoperatoren wie `=`, `<>`, `<`, `>` etc. enthalten.
   - Kombination von Bedingungen:
     - `AND`: Beide Bedingungen müssen erfüllt sein.
     - `OR`: Mindestens eine Bedingung muss erfüllt sein.
     - `NOT`: Bedingung darf nicht erfüllt sein.

---

### **Verknüpfungsoperatoren**
1. **Kreuzprodukt (R × S)**:
   - Kombiniert jede Zeile der ersten Tabelle mit jeder Zeile der zweiten.
   - Kann durch Auswahloperatoren gefiltert werden, um sinnvolle Verknüpfungen herzustellen.

2. **Verknüpfung (R ∘ S)**:
   - Kombiniert Zeilen aus beiden Relationen zu neuen Tupeln.

---

### **Beispiele**
1. **Auswahl eines Attributs:**
   - `Sel(VK, VK.Verkaeufer = 'Meier')`: Wählt alle Verkäufe von "Meier".
   
2. **Kreuzprodukt gefiltert:**
   - `Sel(VK × PL, VK.Produkt = PL.Produkt AND VK.Kaeufer = 'Schmidt')`: Preise aller Produkte, die "Schmidt" gekauft hat.

3. **Projektion:**
   - `Proj(Sel(...), [Attribut])`: Wählt nur die benötigten Spalten aus dem Ergebnis aus.

---

### **Typische Vorgehensweise bei Anfragen**
1. **Bestimme relevante Relationen.**
2. **Kombiniere Relationen durch Kreuzprodukt.**
3. **Filtern durch Auswahloperatoren.**
4. **Ergebnis auf benötigte Attribute reduzieren (Projektion).**

---

### **Übungsaufgaben (basierend auf Beispielrelationen)**
1. **Gebe die Namen aller möglichen Arbeiten aus.**
2. **Bestimme zu jedem Projektnamen die zugehörigen Arbeiten.**
3. **Welche Maschinen werden für das "Knicken" genutzt?**
4. **Welche Maschinen werden für jedes Projekt genutzt?**
5. **Gebe alle Projekte aus, bei denen "Knicken" und "Färben" vorkommen.**

---
