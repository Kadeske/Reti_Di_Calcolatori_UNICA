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


### Livello fisico
Trasmissione veloce e ricezione lenta vs T lenta e R lenta
Chi regolamenta la velocità della comunicazione? Il protocollo: Analizza e decide la velocità massima della trasmissione.

### Livello di commegamento
Organizza i bit in frame, li invia, attende conferma di ricezione (ack)

Nella parte iniziale della trama sarà presente il destinatario. Nella rete locale potrebbero essere più di uno.
Come identifico il destinatario?

### Livello di rete

I pacchetti sono numerati, come le trame. 
Utilizza delle tabelle di instradamento (statiche e dinamiche)

### Livello di trasporto

Accetta dati dal livello superiore, li spezza in pacchetti più piccoli e li invia ai livelli superiori.

connessione di rete -> conn. di trasporto
n conn. di rete -> n conn. di trasporto

![[Pasted image 20260316171121.png]]
## Livello di sessione

![[Pasted image 20260316171151.png]]

## Livello di presentazione

![[Pasted image 20260316171245.png]]



## Livello di applicazione

![[Pasted image 20260316171316.png]]
"L'invio di un pacchetto avviene in modo tale che rimanga intonso, con le stesse dimensioni?" No.



![[Pasted image 20260316171449.png]]

# Modello TCP/IP

### Livello internet

SI basa su un livello privo di conessione.
E' analogo al sistema postale.
E' compito del destinatario riordinare i pacchetti ricevuti.
Compito: scegliere il cammino per evitare congestioni.


### Livello di trasporto
Serve a host per avere una conversazione:
- TCP -> orientato alla connessione affidabile, utilizza l'IP per consegnare i pacchetti
- UDP -> protocollo datagramma senza connessione e non affidabile. Utilizza l'IP.



### Livello applicativo

Esempi di applicazioni:
- TELNET: sviluppato per scopi militari, invia messaggi in modo stabile, ovvero se perde connessione è in grado di riconnettersi
- FTP -> scambio di file e archivi
- SMTP -> posta elettronica sicura
- DNS -> Associa indirizzi ip a nomi di dominio
- HTTP -> trasferimento dati ipertestuali
- SNMP -> gestione di rete
- NNTP -> 