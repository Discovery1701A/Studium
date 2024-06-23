### Ampelschaltung

```mermaid
stateDiagram-v2
    [*] --> Rot
    Rot --> RotGelb : Timer abgelaufen
    RotGelb --> Grün : Timer abgelaufen
    Grün --> Gelb : Timer abgelaufen
    Gelb --> Rot : Timer abgelaufen

```

### Waschmaschinen
```mermaid
stateDiagram-v2
    [*] --> Inaktiv
    Inaktiv --> Befüllen : startKnopfGedrückt
    Befüllen --> Waschen : after(5min)/wasserstandÜberprüfen
    Waschen --> Spülen : after(30min)/wasserAblassen
    Spülen --> Schleudern : after(10min)/wasserEinfüllen
    Schleudern --> Fertig : after(5min)/schleudernStoppen
    Fertig --> Inaktiv : türGeöffnet

```


```mermaid
stateDiagram-v2
    [*] --> Warenkorb
    Warenkorb --> BestellungAufgegeben : [ArtikelImWarenkorb] bestellen
    BestellungAufgegeben --> ZahlungAusstehend : [BestätigungErhalten] zahlungInitiieren
    ZahlungAusstehend --> ZahlungErfolgreich : [ZahlungsInformationenKorrekt] zahlungBestätigen / [BestätigungsEmailSenden]
    ZahlungAusstehend --> ZahlungFehlgeschlagen : [ZahlungsInformationenFehlerhaft] zahlungFehlgeschlagen / [FehlerEmailSenden]
    ZahlungErfolgreich --> Versandt : [PaketVorbereitet] versenden
    Versandt --> Geliefert : [PaketUnterwegs] zustellungBestätigen
    Geliefert --> Abgeschlossen : [KundeHatBestätigt] bestätigungErhalten

```
 ### Fahrkarte
 ```mermaid
 stateDiagram-v2
    [*] --> Bereit
    Bereit --> Auswahl : startKnopfGedrückt
    Auswahl --> ZahlungAusstehend : [TicketGewählt] zahlungInitiieren
    ZahlungAusstehend --> ZahlungErfolgreich : [BetragKorrekt] zahlungBestätigen / [TicketDrucken]
    ZahlungAusstehend --> ZahlungFehlgeschlagen : [BetragFehlerhaft] zahlungFehlgeschlagen / [FehlerMeldung]
    ZahlungErfolgreich --> TicketAusgabe : [TicketGedruckt] ticketAusgeben
    TicketAusgabe --> Abgeschlossen : [TicketEntnommen] abschließen

 ```

### Ampel

```mermaid
stateDiagram-v2
    [*] --> Rot
    Rot --> RotGelb : after(60s) / [Vorbereitung für Grün]
    RotGelb --> Grün : after(5s) / [Grün Licht an]
    Grün --> Gelb : after(60s) / [Vorbereitung für Rot]
    Gelb --> Rot : after(5s) / [Rot Licht an]
   
   
    Grün --> Rot : resetKnopfGedrückt / [Reset]
  
    Gelb --> Rot : resetKnopfGedrückt / [Reset]
  
    Rot --> [*] : störungKnopfGedrückt / [Störung]
    RotGelb --> [*] : störungKnopfGedrückt / [Störung]
    Grün --> [*] : störungKnopfGedrückt / [Störung]
    Gelb --> [*] : störungKnopfGedrückt / [Störung]

```