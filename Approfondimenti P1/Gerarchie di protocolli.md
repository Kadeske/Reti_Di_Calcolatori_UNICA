Le reti moderne sono estremamente complesse. Per renderne possibile la progettazione e la gestione, i progettisti non creano un unico software gigante che fa tutto, ma dividono il problema in parti più piccole chiamate **Livelli (o Strati)** sovrapposti.

![[Pasted image 20260415140626.png]]

Ecco i concetti e il vocabolario fondamentale da padroneggiare:

1. **Livelli (Strati):** Ogni livello ha un compito unico e specifico (es. instradare i pacchetti, oppure controllare gli errori). Lo scopo di ogni livello è **offrire un servizio al livello superiore**, nascondendogli i dettagli noiosi e complessi di come quel servizio viene tecnicamente realizzato.
    
2. **Il Protocollo:** È l'insieme di regole e convenzioni usate per la comunicazione. Attenzione alla regola d'oro: **il Livello _N_ della Macchina A parla virtualmente solo col Livello _N_ della Macchina B**. Le entità dello stesso livello su macchine diverse si chiamano **Entità Paritetiche (Peers)**.
    
3. **Flusso fisico dei dati:** Nella realtà, il Livello _N_ non manda quasi mai dati direttamente in orizzontale al suo corrispondente. I dati viaggiano **verticalmente**:
    
    - Sul mittente, il messaggio _scende_ attraverso i livelli. Ogni strato aggiunge le proprie informazioni di controllo (chiamate **Header** o intestazione), "incapsulando" il dato originale come in una matrioska.
        
    - Arrivati al livello 1 (Fisico), i bit viaggiano sul cavo.
        
    - Sul destinatario, i dati _risalgono_. Ogni livello legge il proprio Header, lo stacca (decapsulamento) e passa il pacchetto ripulito al livello superiore, fino all'applicazione finale.
        
4. **L'Interfaccia:** È il confine di separazione tra due livelli adiacenti (es. tra il Livello 3 e il Livello 2) sulla _stessa_ macchina. Definisce le operazioni primitive (i comandi) che il livello superiore può usare per sfruttare i servizi del livello inferiore.
    
5. **Architettura di rete:** È l'insieme teorico di tutti i livelli e dei relativi protocolli (es. il modello teorico ISO/OSI).
    
6. **Pila di protocolli (Protocol Stack):** È l'elenco _pratico_ e concreto dei protocolli effettivamente installati e funzionanti su un determinato computer in quel momento (es. HTTP per l'applicazione, TCP per il trasporto, IP per la rete).

Non fanno parte dell'architettura di rete:
- dettagli implementativi di ogni strato
- specifiche delle interfacce tra coppie di strati adiacenti
- dettagli e interfacce sono nascosti nell'host e variano da host a host