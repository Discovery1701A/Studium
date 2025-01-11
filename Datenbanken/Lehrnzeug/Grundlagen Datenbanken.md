
#### **Was ist eine Datenbank (DB)?**
- Sammlung von Daten, vergleichbar mit einem elektronischen Aktenschrank.
- Ermöglicht:
  - Anlegen von Datenschemata (Tabellen),
  - Einfügen, Ändern, Löschen von Datensätzen,
  - Strukturiertes Abrufen von Daten.

#### **Anforderungen an eine Datenbank**
1. **Persistenz**: Daten bleiben erhalten, auch nach Programmende.
2. **Datenschemata (Tabellen)**: Strukturierung der Daten (z. B. Artikelnummer, Bezeichnung, Anzahl).
3. **Datenmanipulation**: Einfügen, Ändern, Löschen von Datensätzen (Zeilen in Tabellen).
4. **Datenabruf**: Effiziente Abfragen wie z. B. „Welche Daten gehören zur Artikelnummer 12345?“
5. **Integrität & Redundanzfreiheit**:
   - Daten werden nur einmal gespeichert und bei Änderungen automatisch aktualisiert.
   - Beispiel: Verknüpfung von Artikel, Firma und Artikeleinkauf über Schlüsselwerte.
6. **Parallele Nutzung**: Mehrere Nutzer können gleichzeitig arbeiten, ohne Datenintegrität zu gefährden.
7. **Rechteverwaltung**: Rechte für das Erstellen, Löschen und Bearbeiten von Daten können individuell festgelegt werden.
8. **Datensicherung**: Regelmäßige Backups und Wiederherstellungsmöglichkeit.
9. **Katalog**: Übersicht über Struktur, Integritätsbedingungen und Nutzerrechte.

#### **Wichtige Begriffe**
- **Datenbankmanagementsystem (DBMS)**: Software zur Verwaltung der Datenbank.
- **Datenbanksystem (DBS)**: DBMS + Datenbanken.
- **Informationssystem (IS)**: DBS + Anwendungen.

#### **Ebenen des DBMS (ANSI-SPARC-Architektur)**
1. **Externe Ebene**: Benutzersicht (z. B. Eingabe- und Ausgabemasken).
2. **Logische Ebene**:
   - Zentrales Datenmodell (Datenobjekte, Integritätsregeln, etc.).
   - Unabhängig von konkreten Anwendungen.
3. **Physische Ebene**:
   - Speicherstruktur der Daten.
   - Einfluss auf Performance und Optimierung.

#### **Vorteile der ANSI-SPARC-Architektur**
- **Physische Datenunabhängigkeit**: Änderungen am Speicher haben keinen Einfluss auf die logische oder externe Ebene.
- **Logische Datenunabhängigkeit**: Änderungen der Datenstruktur wirken sich nicht auf externe Ebenen aus.
- **Robustheit gegenüber Änderungen**.

---
