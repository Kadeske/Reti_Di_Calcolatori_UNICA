È una tecnologia di rete a commutazione di pacchetto nata negli anni '90 per superare i limiti di lentezza di X.25. È stata progettata per sfruttare le nuove linee di trasmissione (come la fibra ottica), che erano molto più affidabili e meno soggette a errori rispetto ai vecchi cavi telefonici.

I punti fondamentali da ricordare sono:

- **Semplificazione e Velocità:** A differenza di X.25, Frame Relay **elimina il controllo degli errori nodo per nodo**. I router intermedi non controllano più se il pacchetto è integro e non inviano conferme (ACK) durante il tragitto. Questo riduce drasticamente i tempi di elaborazione e rende la rete molto più veloce.
    
- **Gestione degli Errori "End-to-End":** Se un pacchetto arriva corrotto a un nodo, viene semplicemente **scartato**. Il compito di accorgersi della perdita e chiedere la ritrasmissione è spostato interamente ai due host finali (livelli superiori, come il TCP).
    
- **Connessione:** Funziona principalmente tramite **Circuiti Virtuali Permanenti (PVC)**. È come se tra due sedi di un'azienda ci fosse un "tubo" logico sempre attivo, anche se la linea fisica è condivisa con altri utenti.
    
- **Assenza di controllo di flusso:** Non gestisce attivamente il ritmo tra i nodi; se la rete si intasa (congestione), inizia a scartare i pacchetti in eccesso.
    

**In sintesi:** Se X.25 era un "camion blindato" (sicuro ma lentissimo), Frame Relay è una "macchina sportiva": viaggia molto più veloce perché ha eliminato il peso dei controlli di sicurezza superflui, dando per scontato che la strada (il cavo) sia in buone condizioni.