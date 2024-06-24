



1. **Single Responsibility Principle (SRP)**
    - **Name**: Single Responsibility Principle
    - **Beschreibung**: Eine Klasse sollte nur eine einzige Verantwortlichkeit haben.
    - **Vorteile**: Erhöht die Kohäsion und erleichtert die Wartung und Erweiterbarkeit des Codes.
    - **Beispiel**: Eine Klasse `Rechnung` sollte nur für die Verwaltung von Rechnungsinformationen verantwortlich sein und nicht für die Verwaltung von Kundendaten.

2. **Open/Closed Principle (OCP)**
    - **Name**: Open/Closed Principle
    - **Beschreibung**: Softwarekomponenten sollten offen für Erweiterung, aber geschlossen für Modifikation sein.
    - **Vorteile**: Erleichtert das Hinzufügen neuer Funktionalitäten ohne Änderungen am bestehenden Code.
    - **Beispiel**: Eine Klasse `Grafik` kann durch Unterklassen wie `Kreis` und `Rechteck` erweitert werden, ohne die Klasse `Grafik` selbst zu ändern.

3. **Liskov Substitution Principle (LSP)**
    - **Name**: Liskov Substitution Principle
    - **Beschreibung**: Objekte einer Basisklasse sollten durch Objekte ihrer Unterklassen ersetzt werden können, ohne dass sich das Verhalten des Programms ändert.
    - **Vorteile**: Stellt sicher, dass Unterklassen die Erwartungen an die Basisklasse erfüllen.
    - **Beispiel**: Eine Klasse `Vogel` mit einer Methode `fliegen` kann durch die Klasse `Spatz` ersetzt werden, ohne dass der Code, der `Vogel` verwendet, angepasst werden muss.

4. **Interface Segregation Principle (ISP)**
    - **Name**: Interface Segregation Principle
    - **Beschreibung**: Viele spezialisierte Schnittstellen sind besser als eine allgemeine.
    - **Vorteile**: Reduziert die Abhängigkeiten und macht den Code flexibler und wartbarer.
    - **Beispiel**: Anstatt einer großen Schnittstelle `Fahrzeug` mit vielen Methoden wie `fahren`, `fliegen`, und `schwimmen`, sollte es spezialisierte Schnittstellen wie `Auto`, `Flugzeug`, und `Boot` geben.

5. **Dependency Inversion Principle (DIP)**
    - **Name**: Dependency Inversion Principle
    - **Beschreibung**: Abhängigkeiten sollten von abstrakten Schnittstellen und nicht von konkreten Implementierungen abhängen.
    - **Vorteile**: Erhöht die Flexibilität und erleichtert das Testen des Codes.
    - **Beispiel**: Eine Klasse `DatenbankService` sollte von einer Schnittstelle `Datenbank` abhängen, nicht von einer konkreten Klasse `MySQLDatenbank`.


6. **Abstraktion**
    - **Beschreibung**: Konzentration auf die relevantesten Aspekte des Systems durch Vernachlässigung von unwesentlichen Eigenschaften. Es ermöglicht das Verstehen des Systems durch systematisches Vergröbern und Verfeinern.
    - **Vorteile**: 
        - Verstehen des Gesamtsystems ohne Kenntnis der Details von Teilsystemen.
        - Verstehen von Teilsystemen ohne Kenntnis des gesamten Systems.

7. **Modularisierung** 
    - **Beschreibung**: Definition beherrschbarer, abgegrenzter Einheiten (Module). Ein Modul ist in sich geschlossen, hat schwache Kopplung zu anderen Modulen, ist durch seine Schnittstellen verwendbar und besitzt intern eine starke Kohäsion.
    - **Vorteile**: 
        - Erleichtert die Wartung und Erweiterung des Systems.
        - Minimiert die Auswirkungen von Änderungen, da Module unabhängig voneinander entwickelt und getestet werden können.

8. **Kapselung**
    - **Beschreibung**: Die Schnittstelle eines Moduls beschreibt nur, was das Modul leistet (Vertrag zwischen Nutzer und Anbieter). Die Implementierung und der interne Zustand (Attribute) sind nach außen nicht bekannt.
    - **Vorteile**: 
        - Reduziert die Komplexität durch Verbergen der Implementierungsdetails.
        - Erhöht die Sicherheit und Integrität des Systems, da der Zugriff auf interne Zustände und Implementierungen kontrolliert wird.

9. **Wiederverwendung**
    - **Beschreibung**: Verwendung bestehender Software oder Module statt Neuentwicklung. Dies kann durch bestehende Software, Teilsysteme, Bibliotheken oder Frameworks erfolgen.
    - **Vorteile**: 
        - Reduziert die Entwicklungszeit und -kosten.
        - Erhöht die Zuverlässigkeit durch Verwendung erprobter Komponenten.

10. **Nebenläufigkeit**
    - **Beschreibung**: Gleichzeitige (parallele oder verzahnte) Ausführung von Anweisungen durch Prozesse oder Threads. Fragestellungen im Entwurf umfassen die Aufgabenverteilung auf Prozesse und die Kommunikation zwischen Prozessen.
    - **Vorteile**: 
        - Potenziell höhere Performance durch parallele Ausführung.
    - **Nachteile**: 
        - Erhöht die Komplexität des Systems.


Diese Prinzipien sind fundamental für die Erstellung von robustem, flexiblem und wartbarem Code. Sie helfen dabei, den Code modular zu halten und Änderungen oder Erweiterungen leichter durchzuführen.

- **Abstrakte Klassen**:
    - Eine abstrakte Klasse kann keine direkten Instanzen erzeugen.
    - Eine konkrete Klasse kann instanziiert werden.
- **Schnittstellen**:
    - Eine Schnittstelle definiert nur abstrakte Methoden und kann nicht instanziiert werden.
- **Sichtbarkeit**:
    - Bestimmt die Zugreifbarkeit eines Attributs bzw. die Aufrufbarkeit einer Operation.
    - Sichtbarkeiten: `private (-)`, `protected (#)`, `public (+)`, `package (~)`.
- **Parametrisierte Klassen**:
    - Klassen, die mit generischen Typen arbeiten, z.B. `ArrayList<E>`.
- **Algorithmusentwurf**:
    - Wahl und Optimierung von Algorithmen basierend auf Verarbeitungskomplexität, Implementierung, Verständlichkeit und Flexibilität.
- **Sequenzdiagramme**:
    - Geeignet zur Darstellung komplexer Abläufe und zur Dokumentation/Kommunikation komplexer Sachverhalte.
