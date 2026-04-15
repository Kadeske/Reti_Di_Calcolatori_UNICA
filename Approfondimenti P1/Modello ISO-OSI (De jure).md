Il modello **ISO-OSI** (Open Systems Interconnection) è il quadro di riferimento teorico per eccellenza nelle reti di calcolatori, standardizzato nel 1983 dall'ISO. Nasce per fornire una base comune per lo sviluppo di standard di interconnessione e per permettere a sistemi aperti di comunicare tra loro, riducendo la complessità della progettazione tramite una suddivisione in **7 livelli**.

Ogni livello offre servizi a quello superiore e nasconde i dettagli implementativi delle proprie funzionalità. La comunicazione è **logicamente orizzontale** (un livello comunica con il suo pari sull'altro host), ma **fisicamente verticale** (i dati scendono la pila sul mittente e risalgono sul destinatario).

![[Pasted image 20260415162748.png]]
Ecco la descrizione approfondita dei sette livelli, dal più basso al più alto:

---

### 1. Livello Fisico (Physical Layer)

È il livello responsabile della trasmissione dei singoli **bit** sul canale di comunicazione.

- **Compiti**: Gestisce i voltaggi elettrici per distinguere 0 e 1, stabilisce la durata dei bit (microsecondi), definisce i connettori fisici e i pin da utilizzare.
    
- **Dato**: Bit.
    

### 2. Livello di Collegamento (Data Link Layer)

Si occupa di rendere affidabile il mezzo fisico sottostante, trasformandolo in una linea priva di errori di trasmissione per il livello superiore.

- **Compiti**: Organizza i bit in **frame** (trame), rileva e corregge errori tramite checksum, gestisce il controllo di flusso per non sovraccaricare il ricevente e richiede la ritrasmissione dei frame danneggiati.
    
- **Dato**: Frame (Trama).
    

### 3. Livello di Rete (Network Layer)

Gestisce l'instradamento (**routing**) dei pacchetti all'interno della rete, decidendo quale percorso debbano seguire dalla sorgente alla destinazione.

- **Compiti**: Crea e consulta le tabelle di instradamento, controlla la congestione dei canali ed enumera i pacchetti per gestirne il flusso tra reti eterogenee.
    
- **Dato**: Pacchetto (Packet).
    

### 4. Livello di Trasporto (Transport Layer)

Fornisce una comunicazione end-to-end (da host a host) affidabile e trasparente per i livelli superiori.

- **Compiti**: Spezza i dati provenienti dall'alto in segmenti più piccoli, si assicura che arrivino tutti correttamente a destinazione e ottimizza l'uso delle connessioni di rete.
    
- **Dato**: Segmento (o Transport PDU).
    

### 5. Livello di Sessione (Session Layer)

Sincronizza e gestisce il dialogo tra le due parti che comunicano.

- **Compiti**: Tiene traccia del turno di trasmissione (controllo del dialogo), gestisce i token per operazioni critiche e inserisce punti di controllo per consentire di riprendere una lunga trasmissione in caso di crash.
    
- **Dato**: Session PDU.
    

### 6. Livello di Presentazione (Presentation Layer)

Si occupa della sintassi e della semantica delle informazioni trasmesse.

- **Compiti**: Traduce i dati tra diversi formati di rappresentazione (es. codifica dei caratteri), permettendo a computer con architetture differenti di comprendersi.
    
- **Dato**: Presentation PDU.
    

### 7. Livello di Applicazione (Application Layer)

È il livello più vicino all'utente finale e contiene i protocolli necessari per i programmi applicativi.

- **Compiti**: Fornisce i servizi di rete direttamente alle applicazioni (es. posta elettronica, trasferimento file, navigazione web) e ne visualizza i risultati sul terminale.
    
- **Dato**: Application PDU.
    

---

**Concetto di Incapsulamento:** Ogni livello aggiunge un proprio **Header** (intestazione) ai dati ricevuti dal livello superiore. Questi dati, una volta scesi al livello inferiore, diventano la sua **SDU** (Service Data Unit) alla quale verrà appiccicata una nuova **PCI** (Protocol Control Information) per formare la **PDU** di quel livello.