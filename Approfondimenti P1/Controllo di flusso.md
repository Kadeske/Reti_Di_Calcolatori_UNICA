È il meccanismo fondamentale che evita che un mittente troppo "veloce" sommerga di dati un destinatario "lento", saturando la sua memoria (buffer) e causando la perdita dei pacchetti.

Per regolare il traffico si usano tre strategie principali:

- **Cadenza concordata (Rate-based):** La velocità massima di trasmissione viene decisa a priori. Il mittente invia i dati a intervalli regolari e prestabiliti, garantendo che il destinatario abbia sempre il tempo di elaborarli.
    
- **Sistema a Feedback (ACK-based):** È il metodo più diffuso. Il mittente invia i dati e si ferma in attesa. Riprenderà a trasmettere solo quando riceverà un **ACK (Acknowledgement - Conferma di ricezione)** dal destinatario. Questo regola automaticamente il ritmo: se il destinatario è lento a elaborare, sarà lento a mandare l'ACK, frenando il mittente.
    
- **Riduzione dinamica della velocità:** Se il mittente rileva segnali di congestione nella rete o ritardi anomali, riduce attivamente e in autonomia la propria velocità di trasmissione per non peggiorare la situazione.
    

**Dove opera nel Modello OSI:**
Il controllo di flusso non avviene in un solo punto, ma è gestito principalmente su due livelli:

- **Livello 2 (Collegamento Dati):** Regola il flusso "nodo a nodo" (sul singolo cavo fisico tra due macchine adiacenti).
    
- **Livello 4 (Trasporto):** Regola il flusso "end-to-end" (tra l'applicazione del mittente originale e l'applicazione del destinatario finale, attraversando tutta la rete).