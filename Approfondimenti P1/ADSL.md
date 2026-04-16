Questa è la conclusione perfetta del discorso sul DSL. L'**ADSL** (Asymmetric Digital Subscriber Line) è la variante che ha conquistato il mondo, e lo ha fatto sfruttando un trucco ingegneristico elegante che separa fisicamente la voce dai dati.

### **1. Il Trucco del DMT (Discrete MultiTone)**

Come fa l'ADSL a far passare voce e internet sullo stesso cavo senza interferenze?

Usa l'approccio DMT. Immagina la capacità totale del cavo di rame (che arriva fino a 1,1 MHz) come un'autostrada larghissima. Invece di usare un'unica corsia gigante, l'ADSL divide l'autostrada in **256 corsie strette e indipendenti** (chiamate canali).

Ecco come vengono assegnate queste corsie:

- **Canale 0 (POTS):** La primissima corsia, quella a frequenza più bassa, è riservata esclusivamente alla vecchia voce analogica (POTS).
    
- **Canali 1-5:** Corsie vuote. Fanno da "guardrail" (fascia di guardia) per evitare che il rumore di internet disturbi la telefonata.
    
- **I restanti 248 canali:** Vengono usati per i dati internet.
    

### **2. L'Asimmetria (Perché la "A" di ADSL?)**

Quei 248 canali per i dati non vengono divisi a metà tra caricamento e scaricamento. L'ADSL è _Asimmetrica_ perché rispecchia il comportamento tipico degli utenti (che scaricano film e pagine web molto più di quanto carichino file).

- **Upstream (Caricamento):** Si prendono solo **24 canali**.
    
- **Downstream (Scaricamento):** Si prende il blocco gigante di **224 canali**.
    

_Prestazioni (Il calcolo dell'esame):_ Ogni singolo canale usa la modulazione QAM (fino a 15 bit/baud) e viaggia a 4000 baud. Se moltiplichi $4000 \times 15 \times 224$ ottieni una velocità teorica in downstream di **13,44 Mbps**. (Nella realtà, a causa del rumore visto prima, gli standard ufficiali si fermavano a 8 Mbps).

### **3. L'Architettura Fisica (Cosa succede in casa e in centrale)**

La Figura 2.7 mostra esattamente i "pezzi" necessari per far funzionare questa divisione a corsie:

- **In Casa:**
    
    - Il segnale misto (voce + dati) entra in casa.
        
    - Incontra lo **Splitter** (quel piccolo filtro bianco che attaccavamo alle prese del muro). Lo splitter è un vigile urbano: prende le basse frequenze (Canale 0) e le manda al telefono fisso, mentre prende le alte frequenze e le manda al **Modem ADSL**.
        
    - Il Modem ADSL (che in realtà è come se fossero 250 vecchi modem messi in parallelo) decodifica i dati e li passa al PC tramite cavo Ethernet.
        
- **In Centrale Locale:**
    
    - Il doppino di rame arriva in centrale e incontra un altro Splitter gemello.
        
    - La voce viene filtrata e mandata ai vecchi commutatori per le telefonate.
        
    - I dati internet vengono mandati al **DSLAM** (Digital Subscriber Line Access Multiplexer). Questo macchinario enorme raccoglie i dati ADSL di tutto il quartiere, li impacchetta e li "spara" sulle dorsali in fibra ottica verso l'ISP.
        
