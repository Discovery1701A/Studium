



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

Diese Prinzipien sind fundamental für die Erstellung von robustem, flexiblem und wartbarem Code. Sie helfen dabei, den Code modular zu halten und Änderungen oder Erweiterungen leichter durchzuführen.
