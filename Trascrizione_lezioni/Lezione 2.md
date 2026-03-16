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

