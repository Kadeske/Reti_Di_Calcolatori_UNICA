
Ecco una rielaborazione del testo e della tabella presenti nell'immagine, strutturata e formattata in Markdown per essere perfetta da inserire nei tuoi appunti:

## Quality of Service (QoS)

In tutti i servizi di rete è fondamentale garantire la **QoS (Quality of Service)**. I requisiti della QoS variano fortemente in base al tipo di applicazione:

- **Trasferimento FTP (File Transfer Protocol):** Richiede massima precisione; _non si possono assolutamente perdere informazioni_.
    
- **Conversazioni Voce/Video:** Sono più tolleranti; _si potrebbe perdere qualche informazione_ senza compromettere totalmente il servizio.
    

> **Nota bene:** Solitamente le reti _si misurano rispetto alla QoS che garantiscono_.

---

## L'Affidabilità nei Servizi di Rete

L'**affidabilità** di un servizio è un parametro critico. Si caratterizza per la garanzia di _non perdere alcun dato durante la trasmissione_.

Questa garanzia viene ottenuta tramite la conferma di ricevimento del messaggio, ovvero tramite un **ack (acknowledgement)**.

Nei servizi senza connessione, possiamo distinguere due categorie principali:

1. **Servizi datagramma:** Servizi **privi di connessione** e **non affidabili**.
    
2. **Servizi con messaggio di avvenuto ricevimento:** Servizi **privi di connessione ma affidabili**.
    

### Il Costo dell'Affidabilità

L'affidabilità ha un _costo molto rilevante_ in termini di risorse di rete. Poiché a ogni pacchetto inviato deve corrispondere un pacchetto di conferma (ack), si corre il rischio che **la rete venga saturata**. Nonostante questo costo, l'affidabilità è spesso essenziale per garantire un buon servizio.

---

## 1.3 Software delle reti: Tipologie di Servizio

Ecco una classificazione dei servizi in base al tipo di connessione:

|**Tipo di Connessione**|**Servizio**|**Esempio Pratico**|
|---|---|---|
|**Orientato alla connessione**|Flusso affidabile di messaggi|Sequenza di pagine|
|**Orientato alla connessione**|Flusso affidabile di byte|Scaricamento di filmati|
|**Orientato alla connessione**|Connessione inaffidabile|Voice over IP|
|**Senza connessione**|Datagram inaffidabile|E-mail spazzatura (spam)|
|**Senza connessione**|Datagram con conferma|Messaggistica istantanea|
|**Senza connessione**|Request-reply|Interrogazione di un database|

---

## Approfondimento: I Servizi Non Orientati alla Connessione

Nei servizi non orientati alla connessione, la gestione dei pacchetti richiede informazioni aggiuntive per funzionare correttamente.

**Indirizzamento dei pacchetti:**

- Ogni singolo pacchetto deve contenere non solo l'**indirizzo di destinazione**, ma anche l'**indirizzo sorgente** per poter essere riconosciuto dal destinatario.
    
- _Eccezione (Reti Locali):_ Nel caso di reti locali gestite in modalità _broadcast_, l'indirizzo di destinazione è dato da tutti gli indirizzi della rete.
    

**Parametri essenziali del pacchetto:**

Oltre agli indirizzi, il pacchetto deve includere:

- Un _percorso prestabilito_
    
- Il _tempo di vita (TTL)_
    
- Il _numero del pacchetto_
    
- L'_ack_ (acknowledgement)
    

> **Ottimizzazione dell'Ack:** Se l'ack viene inserito sin dall'inizio nel pacchetto, si evita di saturare il canale di comunicazione, poiché si rimanda indietro lo stesso pacchetto con la conferma di ricevuta inclusa.

**Integrità dei Dati:**

È teoricamente necessario garantire la _correttezza del pacchetto_ (ovvero la sua integrità). Tuttavia, essendo un'operazione molto costosa in termini di elaborazione e tempo, molti protocolli non implementano questo controllo, basandosi sull'assunto (e affermando) che il tasso di errore intrinseco del mezzo sia già molto basso.