Nata negli anni '90, l'ATM è stata concepita come la rete "universale" definitiva, capace di trasportare contemporaneamente voce, dati e video (multimedia) garantendo una precisa Qualità del Servizio (**QoS**).

![[Pasted image 20260415163702.png]]
(ATM/B-ISDN)

I punti fondamentali da ricordare sono:

- **Commutazione di Celle:** A differenza delle altre reti che usano pacchetti di lunghezza variabile, ATM usa pacchetti piccoli e di lunghezza fissa chiamati **Celle**.
    
    - Ogni cella è lunga esattamente **53 byte** (5 byte di header + 48 byte di dati).
        
    - La lunghezza fissa permette ai router (switch ATM) di elaborare i dati tramite hardware molto velocemente, riducendo al minimo il ritardo (jitter).
        
- **Orientamento alla Connessione:** Anche ATM richiede l'instaurazione di un **Circuito Virtuale** prima di poter inviare i dati.
    
- **Qualità del Servizio (QoS):** Era il vero punto di forza. ATM permette di prenotare la banda. Ad esempio, puoi dire alla rete: "Voglio 2 Mbps costanti per questa telefonata", e la rete garantisce che quel flusso non verrà disturbato dal traffico dati (come il download di un file).
    
- **Velocità:** È stata progettata per lavorare a velocità elevate (da 155 Mbps fino a diversi Gbps), tipiche delle dorsali in fibra ottica.
    

**Confronto rapido per l'esame:**

- **X.25:** Sicuro ma lento (controllo errori nodo per nodo).
    
- **Frame Relay:** Veloce (controllo errori solo finale), pacchetti variabili.
    
- **ATM:** Velocissimo e multimediale (lunghezza fissa delle celle + garanzia di banda).
    

**In sintesi:** ATM è la tecnologia che ha provato a unificare il mondo della telefonia con quello dei computer, fallendo però nel mercato dei desktop a causa dell'elevato costo degli apparati, lasciando il posto alla più economica Ethernet.