In un'architettura a livelli, lo scopo del **livello N** è fornire servizi al livello superiore (**N+1**). Chi svolge materialmente questo compito è un'**Entità** (che può essere un processo software, una funzione o un dispositivo hardware). Le entità dello stesso livello su computer diversi si chiamano **Entità Paritetiche (Peer)**.

I concetti chiave del passaggio dei dati sono:

- **SAP (Service Access Point):** È la "porta" logica dotata di un indirizzo univoco. È il punto esatto in cui avviene il passaggio delle informazioni dal livello superiore a quello inferiore.
    

**Il Passaggio dei Dati (Come si forma il pacchetto)**

Quando le informazioni scendono la pila dei protocolli attraversando i SAP, cambiano nome e struttura seguendo questa precisa sequenza (dal livello _N_ al livello _N-1_):

1. **PDU (Protocol Data Unit):** È il "pacchetto finito" di uno specifico livello. L'informazione di partenza nel livello superiore si chiama **n-PDU**.
![[Pasted image 20260415144923.png]]
    
2. **SDU (Service Data Unit):** Quando l'_n-PDU_ attraversa il SAP e scende al livello inferiore, diventa una **(n-1)-SDU**. In parole povere, diventa il "carico utile" (payload) da trasportare, senza che il livello inferiore ne capisca il contenuto.
    
3. **PCI (Protocol Control Information):** È l'intestazione (Header o Trailer) di controllo che il nuovo livello genera e appiccica ai dati.
    
4. **Il Nuovo PDU:** Unendo i dati e l'intestazione si ottiene il nuovo pacchetto completo per quel livello:
    
    > **(n-1)-SDU** _[Dati]_ + **(n-1)-PCI** _[Header]_ = **(n-1)-PDU** _[Pacchetto Completo]_
    
5. Questo nuovo _(n-1)-PDU_ è ora pronto per essere passato al livello ancora inferiore _(N-2)_ attraverso il prossimo SAP, e il ciclo si ripete.
![[Pasted image 20260415144958.png]]

**I due tipi di Informazioni di Controllo (Da non confondere!)**

- **ICI (Interface Control Information):** Sono istruzioni scambiate _localmente_ tra due livelli sulla stessa macchina attraverso il SAP. Aiutano il livello inferiore a capire come formare l'header (PCI), ma **non viaggiano sulla rete**.
    
- **PCI (Protocol Control Information):** È l'header vero e proprio. Questo **viaggia sulla rete** e deve arrivare intatto all'entità _peer_ (paritetica) sull'altro computer per essere letto.