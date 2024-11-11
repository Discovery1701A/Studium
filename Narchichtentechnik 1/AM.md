# Amplitudenmodulation (AM): Umfassende Studiennotizen
## Grundkonzept der Modulation

### Ziel der Informationsübertragung

- **Anpassung der Informationsdarstellung an Kommunikationskanal**
    
- Verschiebung von Nachrichtenfrequenzen in höhere Frequenzbereiche
    
- **Hauptmerkmal**: Ausschließliche Änderung der Trägeramplitude
    

### Trägersignal

- Mathematische Darstellung: `s(t) = A sin(Ωt)`
    
- Komponenten:
    
    - A = mittlere Amplitude
        
    - Ω = Trägerkreisfrequenz
        
    

### Nachrichtensignal

- Mögliche Inhalte:
    
    - Sprache
        
    - Musik
        
    - Bildinformationen
        
    
- Bei Analyse oft **Eintonmodulation** verwendet
    
- Mathematische Darstellung: `n(t) = m cos(ωN t)`
    
    - m = Modulationsfaktor (0 ≤ m ≤ 1)
        
    - ωN = Nachrichtenkreisfrequenz
        
    

## Spektrale Eigenschaften

### Spektrumcharakteristiken

- **Frequenzverschobenes Spektrum**
    
- Unterscheidungskriterien:
    
    1. AM mit Träger
        
    2. AM ohne Träger
        
    

### Seitenbandmodulation

- **Zweiseitenband-Modulation (ZSB)**
    
- **Einseiten-Bandmodulation (ESB)**
    

## Modulationsverfahren

### Zweiseitenband-Modulation (ZSB) mit Träger

- Signalform: `s(t) = (1 + n(t))A sin(Ωt)`
    
- Bedingung: Nachrichtenamplitude ≤ 1
    
- **Spektrum**:
    
    - Träger
        
    - Oberes Seitenband
        
    - Unteres Seitenband
        
    

### Zweiseitenband-Modulation ohne Träger

- Signalform: `s(t) = mn(t)A sin(Ωt)`
    
- Energieeinsparung
    
- Charakteristisch: Phasensprung beim Träger
    

## Praktische Anwendungen

### Rundfunk

- **Wellenbereiche**:
    
    - Langwellen (LW)
        
    - Mittelwelle (MW)
        
    - Kurzwelle (KW)
        
    
- UKW: Frequenzmodulation (FM)
    
- Stereoübertragung: Amplitudenmodulation
    

### Elektronische Schaltungen

- **Signalmultiplikation**:
    
    - Ringmischer
        
    
- Empfängerschaltungen:
    
    1. Detektorempfänger
        
    2. Sekundär-Detektor-Empfänger
        
    3. Superheterodyn-Empfänger
        
    

### Digitale Übertragung

- **Pulse-Amplituden-Modulation (PAM)**
    
- Verwendung pulsförmiger Träger
    

## Wichtige Berechnungsgrundlagen

### Spektrumsberechnung

- Mathematische Identität:
    
    ```
    sin(α)cos(β) = 1/2 * [sin(α+β) + sin(α-β)]
    ```
    

### Bandbreitenbedarf

- Modulierter Träger: `B_Träger = 2 * B_Nachricht`
    

## Literaturhinweise

- Empfohlene Quellen:
    
    1. Steinbuch und Rupprecht
        
    2. Ohm und Lüke
        
    

## Prüfungsrelevante Aspekte

### Zu merkende Formeln

- Trägersignal: `s(t) = A sin(Ωt)`
    
- Nachrichtensignal: `n(t) = m cos(ωN t)`
    

### Typische Prüfungsaufgaben

- Blockschaltbilder zeichnen
    
- Spektren berechnen
    
- Modulationsverfahren unterscheiden
    
- Signalformen skizzieren