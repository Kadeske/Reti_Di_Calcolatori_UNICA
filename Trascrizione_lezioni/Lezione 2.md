![[Pasted image 20260316164446.png]]...
Nel terzo livello di rete, collega tutte le macchine a livello globale, è l'ultimo livello di gestione tra macchine/host, l'ultimo che gestisce il p. tpc/ip.
Vedremo fino al livello di trasporto.

Questi livelli seguono la stessa regola: ciascuno ha un compito ben definito, offre servizi ai livelli adiacenti.
E' come avere un'architettura software all'interno di una macchina.
Posso cambiare tutto della macchina, basta che usi lo stesso protocollo.

I router: dispositivi che "lavorano fortemente fino al livello 4", il loro compito è instradare.

Le colonne a destra e sinistra rappresentano due host, quel quadro centrale in basso rappresenta il lavoro dei router.
Gli host sono macchine normali che conoscono i protocolli di quella rete.

Packet Data Unit (PDU): porzione di dati che viene passata da un livello all'altro, venendo "incapsulata" ad ogni livello.

Segment è un pezzo di informazione del livello di sessione. (?)

"Qual'e la struttura del livello bla bala?" -> APDU (Application PDU), PPDU(Presentazione), SPDU(segmento (livello di sessione))

Un livello ha più di un protocollo.

Il mezzo deve avere delle standardizzazioni chiare: voltaggio da utilizzare, tipo di connettori, tempo per ogni segnale, etc..

"Perchè ho necessità di limitare i bit nel livello inferiore?" "Perchè in caso io perda un pezzo non saprei quale ripetere"
Quindi divido in trame.

Trasmissione veloce e ricezione lenta vs T lenta e R lenta
Chi regolamenta la velocità della comunicazione? Il protocollo: Analizza e decide la velocità massima della trasmissione.

Nella parte iniziale della trama sarà presente il destinatario. Nella rete locale potrebbero essere più di uno.
Come identifico il destinatario?

