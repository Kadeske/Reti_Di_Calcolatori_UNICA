
# reti cellulari
Le reti cellulari sono considerate la parte terminale di una rete più complessa.
Usano una parte dello spettro assegnato dalla ITU-R.

Queste reti devono essere dei sistemi di comunicazione aperti che condividono la stessa chiave comune per comunicare.

Le reti radio su radiofrequenze utilizzano **comunicazioni diffuse**(broadcast), ovvero inviano il segnale nell'aria e solo il ricevende (in possesso della chiave) lo riceve. 
Questo principio è utilizzato anche per le comunicazioni radio e televisive.
In passato si utilizzava una sola frequenza, ora usiamo frequenze multiple per evitare uno spreco di risorse.

Il limite di velocità è determinato dalla porzione di spettro elettromagnetico disponibile. Per fornire servizi ad un grande numero di utenti è possibile **suddividere il territorio in celle**. Ad ogni *cella* viene assegnato un insieme di frequenze e canali, questi possono essere utilizzati da più celle ma *distanti tra loro*, altrimenti si ottengono delle **interferenze co-canale**.

Le celle hanno idealmente una forma esagonale, ma data la conformazione del terreno queste saranno in realtà irregolari.
Quando la *connessione si sposta da una cella ad un altra (handover)* la comunicazione deve essere mantenuta senza interruzioni.
Per far si che possa accadere, il raggi di azione di queste celle sono **sovrapposte** tra loro. 
Durante l'handover l'utente non deve accorgersi di questo fenomeno e la connessione deve rimanere invariata. Quindi **trasparenza** e **continuità**.

Dato che ogni cella ha un limite di utenti servibili: al diminuire della grandezza delle celle, aumenterebbero gli utenti connessi simultaneamente, ma ciò richiederebbe più celle e numerose operazioni di handover.
Le frequenze utilizzate non percorrono lunghe distanze, quindi la grandezza delle celle, e quindi la distanza tra loro vengono ristrette.

**soft handover**: Elimina la discontinuità durande il passaggio da una cella all'altra. In pratica ci si connette a più celle e si interrogano per capire quale sia la più vicina.

Un **cluster** è un gruppo di n celle che ricoprono tutta la banda disponibile. Devono essere costruiti in modo tale che siano autonomi e che garantiscano l'intera copertura geografica.

fenomeno del **fading**: 
- **lento**: le frequenze vengono assorbite 
- **veloce**: le frequenze rimbalzano sulle superfici

Per affrontare il problema del fadin si utilizzano 2 tecniche:
- **Antenna diversity**: utilizza **2 antenne riceventi**: se un antenna non riceve segnale o è guasta, ci penserà l'altra antenna.
- **Frequency hopping**: il segnale viene **trasmesso su fequenze diverse**, saltare da una frequenza all'altra riduce gli effetti delle interferenze

Le celle sono dotate di **BTS (Bse Transceiver Station)**.
La **distanza di riuso** è la distanza tra due antenne di celle diverse che operano alla stessa frequenza.

Le frequenze cengono assegnate ai singoli operatori e ognuno genera il proprio cluster.


## Generazioni delle reti radiocellulari

- Prima generazione (1G): **voce analogica**
	- AMPS
	- **TACS**
- Seconda generazione (2G): **voce digitale**
	- D-AMPS
	- **GSM**
	- CDMA
	- PDC
- Terza generagione (3G): **vocee dati digitali**
	- UMTS
	- W-CDMA
- Quarta (4G) e quinta (5G) generazione:
	- maggiore di 3 (incredibols)


### Sistemi cellulari analogici

Ad ogni utente viene assegnata una frequenza per l'intera durata della conversazione. La frequenza rimane bloccata agli altri.

Oggi si utilizza un sistema misto tra FDM e TDM che suddivide la stessa frequenza in slot temporali in modo da avere più comunicazioni.

Svantaggi:
- nessun sistema di crittografia
- nessun riconoscimento dell'utente
- non trasmette dati (solo voce)

#### TACS (Total Access Communication System)

Introdotto negli Stati Uniti nel 1983.

Chiamato anche **modello 900 MHz**.
Ha un range tra 890 e 960 Mhz, diviso in 1000 canali (da 70 kHz l'uno).
Ampiezza di banda: 
- upload: 25 KHz
- download: 45 KHz

Vantaggi:
- Segnale robusto: avendo frequenza dedicata

Limitazioni: 
- I dispoditivi di uno stato non funzionano in un altro (stati geografici)
- numero limitato di chiamate contemporanee
- Non può fornire altri servizi (es. no fax, no mail, no sms)
- I terminali erano soggetti a clonazione e falsificazione 
- le chiamate erano facilmente intercettabili

## Voce digitale

### Sistema GSM (Global System Mobile Communication)

E' stato sviluppato come un approccio globale e completo per la comunicazione mobile, è quindi uno standard consolidato.

Detto anche **1G**.
E' stato introdotto in 2 fasi.

E' un sistema numerico che ha sostituito il precedente sistema analogico.
Usa frequenze assegnate dall'ITU.

Nel GSM sono presenti due tipi di canali riservati:
- **up-link**: frequenze tra 890 e 915 MHz
- **down-link**: frequenze tra 935 e 960 MHz

E' completamente compatibile con OSI e ISDN.

Possibilità di trasmettere dati oltre alla voce.
Ha garantito il roaming internazionale.

Utilizza FDM e TDM per la creazione di più canali.
Implementa algoritmi di codifica direttamente nelle SIM.


### DCS 1800 (DIgital Cellular System)

Noto come GSM 1800 o GSM DCS.

E' uno standard di comunicazione mobile.
Opera nella banda di frequenza di 1800 MHz.

Ha consentito una maggiore capacità di trasmissione rispetto al GSM.

Principali miglioramenti:
- Utilizzo del protocollo PCN a frequenze più alte
- 1800 MHz > 900, quindi offre una maggiore capacità di trasmissione
- Le sue celle con portata inferiore sono vantaggiore nelle aree urbane.
- Ampiezza di banda triplicata (da 25 a 75 MHz)
- Potenza di trasmissione ridotta: meno interferenze, durata della batteria migliorata.

Nonostante cià il numero di connessioni contemporanee possibili era ancora insufficiente per il mercato.


### Telefoni mobili multistandard

Sono telefoni in grado di utilizzare due standard di comunicazione differenti contemporaneamente.
E' possibile avere 2 SIM nello stesso apparecchio:
- *dual band*: stesso standard ma due frequenze diverse.
- *dual mode*: diversa tecnologia

## Ritardo di propagazione tra BS-MS-BS e massima dimensione delle celle

BTS = Base Transceiver Station (ANTENNA)
ME = Mobile Equipment (CELLULARE)

Si vuole che il tempo massimo di comunicazione tra antenna e cellulare sia di al massimo di **33 microsecondi**, otttendo una distanza massima ideale di **70 km**.

la **distanza massima effettiva** è la metà, circa **35km**

All'aumentare del numero di celle e alla riduzione delle dimensioni delle celle, aumenta il rischio di interferenza co-canale.
All'aumentare della distanze tra l'antenna e il cellulare a alla diminuzione ella potenza di trasmissione di riduce la qualità del servizio (QoS).

## SIM e IMEI 

**GSM** prevede che i dispositivi mobili siano composti da:
- *ME* (Mobile Equipment): rappresenta il dispositivo stesso e ha un codice **IMEI** univoco;
- *SIM* (Subscriber Identity Module): identifica l'utente dell'apparecchio.

L'**IMEI** è un codice da 15 cifre composto da:
- prime *6 cifre*: **modello** e **produttore**
- *2 cifre*: **luogo** di produzione
- *6 cifre*: numero **seriale** dell'apparecchio
- L'ultima cifra è riservata ad **usi futuri**

La **SIM** contiene un processore a 16 bit e una memoria con capacità variabile attualmente tra 128 e 512 KB.

Contiene diversi codici tra cui:
- codici di tipo **primario** (collegati al possessore della SIM):
	- **IMSI**: identifica l'utente univocamente nel GSM
	- $K_{i}$ : chiave di autenticazione
- codici di tipo secondario (specifici della SIM stessa):
	- **A8**: cifratura di dati
	- **A3**: autenticazione
	- **PIN** e **PIN2**: codici personali dell'utente
	- **PUK**: recuopero PIN
	- altri dati (es. rubrica telefonica)

## Schema della rete radio mobile

L'architetura delle **reti radio mobili** si inserisce in una archietettura già esistenste (ISDN e PSTN esistevano già), a abbiamo fatto in modo che le nuove tecnologie (da GSM a 5G) fossero compatibili con esse.

Seguiamo il percorso di una chiamata che parte da una **MS** (Mobile Station).
Quando avvio una chiamata il cellulare invia una richiesta alla prima BTS disponibile fornendosi di IMEI e SIM.
Le antenne **BTS**, che fanno parte di una **BS** (Base Station) sono collegate ad una **BSC** (Base station Controller) la quale appartiene al provider e collega le antenne **BTS**.

L'MSC (Mobile Switching Center) è ciò che instrada le chiamate, in italia ce ne sono poche poichè controllano diversi gruppi di BS.
VLR (Visitor Locator Register): contengono i nostri dati riguardo la rete.

L'MSC è collegato ad un sistema in grado di individuare la nostra posizione all'interno dell'area.
Quando ci spostiamo l'MSC interroga l'**HLR**(Home Locator Register) 

#### I Protagonisti della Rete
- **MSC** (Mobile Switching Center): È il "centralino" principale di una specifica zona geografica (es. uno per il Sud Sardegna, uno per Trieste). Gestisce materialmente lo smistamento delle chiamate.

- **VLR** (Visitor Location Register): È il "registro degli ospiti" di un MSC. Contiene l'elenco temporaneo di tutti i telefoni che si trovano fisicamente in quella specifica zona in quel momento.

- **HLR** (Home Location Register): È l'"anagrafe centrale" del tuo operatore telefonico. Questo database permanente contiene tutti i dati del tuo contratto e, soprattutto, sa sempre in quale "registro degli ospiti" (VLR) ti trovi attualmente. (Nota a margine: nel testo c'è un piccolo refuso, la sigla corretta è Home Location Register, non "Locator").

- **GMSC** (Gateway MSC): È la "porta d'uscita". Serve quando devi comunicare fuori dalla tua rete locale, ad esempio per chiamare un telefono fisso, un utente di un altro operatore o per navigare su internet.

- **Base Station**: Sono le antenne fisiche sparse sul territorio a cui il tuo cellulare si collega direttamente via radio.


#### **EIR** (Equipment Identity Register): Il "Buttafuori" dei telefoni
Se l'HLR visto in precedenza controlla chi sei tu (il tuo contratto SIM), l'**EIR controlla l'identità del dispositivo fisico che stai usando**, tramite il suo codice di serie unico (chiamato IMEI).
L'EIR funziona come un database diviso in tre liste:

**White** list (Lista bianca): Contiene i codici **IMEI dei telefoni certificati** e autorizzati a funzionare sulla rete.

**Grey** list (Lista grigia): Contiene i **telefoni non perfettamente omologati**, che possono funzionare ma magari vengono tenuti "sotto osservazione".

**Black** list (Lista nera): È la lista dei **telefoni denunciati come rubati**. Se il tuo IMEI finisce qui, la rete ti impedisce di telefonare.

(Il testo fa una precisazione pragmatica: dato l'enorme numero di telefoni nel mondo, il controllo capillare su ogni singola chiamata ruberebbe troppe risorse, quindi spesso questi controlli vengono attivati in modo mirato durante specifiche indagini).

#### **AuC** (Authentication Center)

Viene attivato durante ogni inizio di comunicazione ed opera su rete fissa.

Contiene:
- IMSI
- TMSI
- $k_i$ 
- A4
- A8

usa questi dati per identificare la persona che effettua la chiamata.

#### **OMC** (Operation and Maintenance Center): "L'officina locale"

L'OMC è il centro nevralgico per la gestione quotidiana. **È specifico per ogni singolo operatore** (es. TIM, Vodafone, ecc.) e si occupa di:

**Monitoraggio**: Controlla che tutti gli elementi visti finora (antenne BTS, MSC, HLR, AuC, ecc.) funzionino correttamente e siano configurati bene.

**Allarmi e Guasti**: Se un'antenna si rompe o c'è un malfunzionamento, l'allarme suona qui.

**Fatturazione** (Accounting): **Raccoglie i dati** su quanto traffico generano gli utenti e quali tariffe usano, informazioni fondamentali per poi inviare le bollette o scalare il credito.


#### **NMC** (Network Management Center): Il coordinamento generale
Se l'OMC è l'officina che gestisce una determinata zona o un gruppo di macchinari, l'NMC è la sala di controllo principale. **Il suo compito è supervisionare e gestire tutti i vari OMC**, avendo così una visione globale e centralizzata dell'intera rete nazionale.


## TDMA (Time Division Multiple Access)

Immagina una torta (la frequenza radio) che non viene tagliata a fette spaziali, ma a "fette di tempo". Ognuno ha il diritto di mangiare l'intera torta, ma solo per una frazione di secondo a turno.

### Time Slot e Frame

La rete suddivide lo spazio radio (il canale da 200 kHz) in pezzettini di tempo minuscoli:

- **Time Slot** (**0.577 ms**): È la fetta di tempo più piccola. Il tuo telefono riceve il permesso di trasmettere la tua voce solo per questo minuscolo istante (poco più di mezzo millisecondo).

- **Frame** (**4.616 ms**): È composto da 8 Time Slot. In pratica, su una singola frequenza, la rete fa parlare 8 telefoni diversi, uno dopo l'altro, a turno. Ogni 4 millisecondi e rotti, tocca di nuovo a te.

### Dai Frame all'Hyperframe

Per organizzare miliardi di chiamate, la rete raggruppa questi microscopici "Frame" in blocchi sempre più grandi, un po' come i secondi formano i minuti, che formano le ore, che formano i giorni.

1. **Multiframe** (**Traffico o Controllo**): I frame vengono raggruppati a pacchetti di 26 (per far viaggiare la tua voce, Traffico) o a pacchetti di 51 (per far comunicare i sistemi di rete tra loro, Controllo).

2. **Superframe** (**6.12 secondi**): Moltiplicando i Multiframe tra loro, si crea un blocco più grande che dura poco più di 6 secondi.

3. **Hyperframe** (**3 ore, 28 minuti, 53 secondi**): Mettendo insieme ben **2048 Superframe**, otteniamo il *blocco di tempo massimo gestibile dalla rete GSM*.

I time slot sono sfalsati di circa 3 slot. Perché? 
Perché **il telefono non è fisicamente in grado di trasmettere e ricevere nello stesso identico istante sulla stessa frequenza**. Questo sfasamento dà al dispositivo una microscopica "pausa" (pochi millisecondi) tra quando ascolta e quando parla. In quel preciso istante di vuoto, il telefono ha il tempo materiale di misurare il segnale delle antenne vicine e agganciarsi a una nuova antenna più potente, senza che tu o il tuo interlocutore percepiate alcun "buco" nella conversazione.



# Livello DataLink

Ricorda: *FISICO* <-> **DATALINK** <-> *NETWORK*

Il livello DataLink è anche detto **livello di collegamento**.

Questo livello ha diverse funzioni: 
- fornire un **servizio** ben definito al **livello network**
- **gestire gli errori di trasmissione**
- **regolare il flusso di dati** (per evitare che un ricevitore lento venga soprafatto)


Quando i dati arrivano dal livello sottostante (FISICO): riordina i bit in dei gruppi detti **trame**, li delimita da un inizio (**header**) e da una fine (**trailer**) seguendo delle regole di dimensione e codifica precisi, e li invia al livello successivo (NETWORK) mediande il suo **SAP** (DLSAP, DL: DataLink).

Quando i dati arrivano dal livello superiore (NETWORK): inserisce una **intestazione** che indica da quale punto iniziano i dati e la chiude con un **trailer**.

Organizzare i bit in gruppi è utile per identificare e sapere cosa reinviare in caso di trama non ricevuta o danneggiata. Altrimenti andrebbe rimandato tutto.

### Servizi offerti

- Servizio **senza conferma** e **senza connessione**: Non possiede un controlle d'errore e non crea nessuna connessione logica. Viene utilizzato quando la frequenza di errori è molto bassa.
- Servizio **con conferma** ma **senza connessione**: Per ogni frame inviato si deve ricevere un **ack di pervenimento**. Se il mittente non lo riceve, riinvia il frame. Continua a non creare connessioni virtuali.
- Servizio **con conferma** e **orientato alla connessione**: Le macchine sorgente e destinatario **stabiliscono una connessione** prima di trasferire dati. Ogni frame è numerato, lo strato DataLink garantisce l'ordine d'arrivo e la ricezione.


## Framing

Un frame (o pacchetto) è composto da:
- **header**: segna l'inizio del frame e contiene dati come l'indirizzo del destinatario
- **payload**: i dati veri da trasmettere
- **trailer**: segna il termine del frame

Il framing (o impacchettamento) è un operazione che si svolge al livello 2 (DataLink).

In base alla direzione dei dati:
- se **arrivano dal livello network** (quindi sto inviando al destinatario): impacchetta i dati.
- se **arrivano dal livello fisico** (quindi sto ricevendo dei dati): il livello 2 deve riconoscere dove inizia e dove finisce il pacchetto e dividerlo nei vari frame per poterli poi leggere e utilizzare.

E' possibile combinare due o più tecniche di framing per superare eventuali limiti ed offrire un servizio della comunicazione migliore (Qos).


Diversi metodi di **suddivisione**:
- conteggio dei caratteri
- Flag Byte con Byte Stuffing
- Flag Inizio/FIne con Bit Stuffing
- Violazione Codifica Livello FIsico

### Conteggio dei caratteri (o byte)

Nel primo byte si inserisce la lunghezza del campo, non si ha la necessità di un trailer.
Il problema si verifica se, a causa dell'alterazione del segnale, viene letto il numero sbagliato di lunghezza, sfalsando tutta la struttura del messaggio.


### Flag Byte con Byte Stuffing

Viene utilizzato un byte detto **flag byte** per delimitare inizio e fine di un frame.
Solitamente si usano i codici (ASCII):
- STX (Start) Flag
- ETX (End) Flag

Per indicare la fine di un frame e l'inizio del prossimo vengono usati due **flag byte** consecutivi.

Il problema è che questi valori potrebbero apparite in modo naturale nel contenuto del messaggio ed essere scambiati per un flag byte. Per evitare ciò viene introdotto un **byte di escape** (*ESC*) prima di ogni occorrenza accidendale di un flag byte.

Il limite di questo metodo è legato all'utilizzo di 8 bit, essendo basato su dei caratteri.

### Flag Inizio/Fine con Byte Stuffing 

Viene utilizzato un **byte indicatore**: 01111110
questo *byte indicatore* indica l'inizio e la fine della trama.

All'invio, il livello 2 (del mittente), quando trova 5 '1' di seguito ne aggiunge uno 0.
Al contrario, durante la ricezione, il livello 2 (del destinatario), quando incontra 5 '1' consecutivi rimuove lo 0 che ne segue.

In questo modo il confine tra due frame viene riconosciuto in modo inequivocabile.

Lo svantaggio principale è che se all'interno del mesaggio si trova una sequenza uguale a al byte indicatore, il byte stuffing avviene più spesso, aumnentando il numero di bit trasmessi.

### Violazioni della codifica del livello fisico

Consiste in una variazione di tensione utile a rafforzare gli altri metodi di framing.

Ogni bit logico viene commutato in 2 corrispettivi bit fisici.
0 logico = 01
1 logico = 10

In questo modo, se si incontra una coppia di bit identica (00 o 11) si è in presenza di un errore di trasmissione.

Presenta comunque dei problemi se si verificano numerosi errori.

## Controllo degli errori

E' tipico delle trasmissioni con conferma.
Il controllo può essere *immediato*, quindi richiede un ack subito dopo la ricezione, o *distribuito nel tempo*, quindi l'ack di riscontro può venire richiesto più avanti.

Il **controllo del flusso** si occupa di evitare che un mittente veloce 'intasi' di messaggi un destinatario lento.

**Problemi** dei servizi con conferma:
- **perdita di frame:** il mittente rimane in attesa di un ack senza riceverlo (si aggira impostando un tempo limite o timeout)
- **perdita di riscontro**: il mittente ritrasmetti il frame credendo che sia stato perso (si aggira numerando i frame)

Gli **errori** possono essere: 
- **corretti**: oltre a madare la trama si aggiungono dai in grado di ricostruire il messaggio danneggiato
- **rilevati**: si rilevano esclusivamente e si richiede l'invio

Nell'ultimo periodo il rilevamento è il più utilizzato essendo i mezzi fisici più affidabili (es. fibre ottiche).


### Codifica di Hamming

E' una procedura per generare codici ridondanti correttivi. L'obiettivo è inidividuare i bit errati in una parola binaria.

Si utilizzano dei **bit** detti di **parità** posti lungo le potenze del 2.
il bit di parità 1 controllerà le posizioni in cui appare 1 nella posizione meno significativa della parola binaria.


|     | BP 3 | BP 2 | BP 1 |
| --- | ---- | ---- | ---- |
| 1   |      |      | 1    |
| 2   |      | 1    |      |
| 3   |      | 1    | 1    |
| 4   | 1    |      |      |
| 5   | 1    |      | 1    |
| 6   | 1    | 1    |      |
| 7   | 1    | 1    | 1    |
|     |      |      |      |
Secondo la tabella il BP 1 controlla le posizioni 1,3,5,7.

i BP sono posti in modo da formare una parola pari insieme ai bit che controllano.

### Codifica ridondanza ciclica (CRC)

Inserisce delle informazione per capire se esiste un errore all'interno del messaggio ricevuto.

Utilizza un polinomio generatore e lo si applica ad una sequenza ottenendo un risultato.
Se il destinatario, effettuando lo stesso calcolo sui dati ricevuti, ottiene un risultato diverso sa che il messaggio è stato danneggiato. 

## Protocolli DataLink

### Protocolli elementari

- Simplex **non limitato**
- Simplex **stop and wait**
- simplex per **canale disturbato**

#### Protocollo simplex non limitato

Questo è un **modello teorico** di base che opera su assunzioni ideali per semplificare l'analisi della trasmissione dati.

**Assunzioni**: Il canale è strettamente **unidirezionale** (simplex) e **non prevede feedback**. Si ipotizza che i **nodi di rete siano sempre pronti**, con **tempi di elaborazione trascurabili**. Il **destinatario dispone di un buffer infinito**, escludendo congestioni. Infine, si assume un'assoluta assenza di errori (nessuna perdita di dati).

**Dinamica**: In queste condizioni, il mittente trasmette un flusso continuo di dati in un loop infinito, senza attese tra i pacchetti. Il destinatario riceve costantemente senza problemi. Il processo si interrompe solo per decisione unilaterale del mittente.

#### Protocollo Simplex "Stop and Wait"

Questo modello introduce un vincolo realistico: il **destinatario possiede un buffer finito**.

Il **problema**: Un invio continuo di dati, come nel modello precedente, porterebbe rapidamente al **riempimento del buffer in ricezione**, causando la perdita dei frame in eccesso.

La **soluzione** (ACK): Per evitare la saturazione, **il destinatario invia un messaggio di riscontro**, denominato ACK (Acknowledgment).

**Dinamica**: Il mittente trasmette un set di frame e si ferma (Stop), attendendo la ricezione dell'ACK (Wait) prima di inviare i dati successivi. Questo meccanismo sincronizza la velocità di trasmissione con la capacità di ricezione.

**Requisiti** del canale: Poiché i dati e gli ACK viaggiano in direzioni opposte, il traffico è tecnicamente bidirezionale. Tuttavia, data la rigida alternanza delle trasmissioni, è sufficiente un canale fisico half-duplex (una direzione alla volta).


#### Protocollo Simplex per Canale Disturbato

L'ultimo modello introduce il livello massimo di complessità reale: la **possibilità di errori sul canale**, che si traduce nella **potenziale perdita di frame o di ACK**.

**Meccanismo di Timer**: All'invio di ogni frame, **il mittente avvia un timer**. Se l'ACK non viene ricevuto prima della scadenza di tale timer, il mittente presume che il pacchetto o la risposta siano andati persi e procede automaticamente alla ritrasmissione del frame.

**Numeri di sequenza**: A causa delle ritrasmissioni, il destinatario potrebbe ricevere frame duplicati (ad esempio, se si perde l'ACK ma non il frame originale). Per risolvere questa ambiguità, è **necessario applicare un numero di sequenza ai frame trasmessi**. È sufficiente un solo bit (alternando 0 e 1) per distinguere univocamente un frame da quello immediatamente successivo.

**Classificazione formale**: Questa tipologia di protocolli, in cui la sorgente avanza nella trasmissione solo dopo aver ricevuto un riscontro positivo, prende il nome di PAR (Positive Acknowledgement with Retransmission) o ARQ (Automatic Repeat reQuest).


### Protocolli Sliding Window

I protocolli a **finestra scorrevole** (sliding window) sono meccanismi di controllo del flusso e degli errori utilizzati nelle reti di calcolatori per **gestire la trasmissione affidabile dei dati su canali bidirezionali (duplex)**. L'obiettivo principale è **massimizzare l'utilizzo della banda**, permettendo al mittente di inviare sequenze di pacchetti senza dover attendere il riscontro per ciascuno di essi.

(Utilizza lo stesso canale per ricezione e invio)
##### Parametri e Struttura

- **Numeri di Sequenza:** Ogni frame viene contrassegnato da un identificativo numerico progressivo inserito nell'intestazione (header). Solitamente, la numerazione utilizza un campo di $n$ bit, permettendo valori che ciclicamente vanno da $0$ a $2^n - 1$.
    
- **Finestra di Invio:** È l'**intervallo logico dei frame che il nodo sorgente è autorizzato a trasmettere**. La dimensione massima della finestra definisce quanti frame possono rimanere contemporaneamente in transito senza aver ancora ricevuto conferma.
    
- **Finestra di Ricezione:** È l'**intervallo corrispondente sul nodo di destinazione**, che indica *quali numeri di sequenza il ricevitore è in grado di accettare e processare in quel determinato istante*. I frame che arrivano con numeri fuori da questa finestra vengono automaticamente scartati.
    

##### Dinamica di Scorrimento (Sliding)

Il protocollo si basa sull'avanzamento dei limiti di queste finestre:

- **Trasmissione:** Quando lo strato network passa un nuovo pacchetto al livello data link, viene assegnato il numero di sequenza successivo. Il limite superiore della finestra di invio avanza di una posizione.
    
- **Riscontro (ACK):** Quando la destinazione riceve correttamente i dati, genera un messaggio di _Acknowledgment_.
    
- **Scorrimento:** Alla ricezione dell'ACK, la sorgente sposta in avanti il limite inferiore della sua finestra. I frame confermati escono dalla finestra e vengono cancellati dalla memoria locale, liberando spazio per nuovi invii.
    

##### Gestione della Memoria (Buffer)

Questo meccanismo impone vincoli hardware precisi. Il nodo mittente deve necessariamente mantenere in memoria (buffer) una copia di tutti i frame che si trovano all'interno della finestra di invio. Questo è fondamentale per garantire la tolleranza ai guasti: se un pacchetto viene perso nel canale fisico o scade il tempo massimo di attesa (timeout), la sorgente recupera il pacchetto dal buffer per effettuare la ritrasmissione.

##### Piggybacking

Per evitare lo spreco di banda dovuto all'invio continuo di piccoli pacchetti contenenti solo gli ACK, si utilizza la tecnica del _piggybacking_. Poiché il canale è bidirezionale, il destinatario attende che il proprio strato network debba inviare un pacchetto dati verso il mittente originale. A quel punto, inserisce il numero di ACK direttamente nell'intestazione di quel pacchetto dati. Solo se scade un determinato intervallo di attesa e non ci sono dati da inviare, viene generato un frame di controllo dedicato esclusivamente al trasporto dell'ACK.


#### Sliding Window a 1 bit

Una _sliding window_ configurata a 1 bit ($n=1$) è operativamente equivalente a un protocollo **Stop-and-Wait**.

- **Meccanismo:** La sorgente è autorizzata a mantenere in transito **un solo frame alla volta**. La trasmissione del frame successivo è strettamente subordinata alla ricezione dell'ACK relativo al frame precedente.
    
- **Inefficienza (Spreco di banda):** Questo vincolo **genera periodi di inattività** (idle time). Il trasmettitore rimane in attesa per l'intera durata necessaria all'invio del frame e alla propagazione dell'ACK (Round Trip Time), non sfruttando la capacità trasmissiva del canale.


#### Protocollo go back n (sliding window)

- **Finestra di Ricezione:** La caratteristica fondamentale del Go-Back-N è l'utilizzo di una finestra di ricezione di **dimensione 1**. Questo implica che *il livello Data Link del nodo destinatario è programmato per accettare esclusivamente il frame successivo in ordine sequenziale* esatto rispetto a quello precedentemente consegnato al livello di Rete.
    
- **Finestra di Invio:** La sorgente possiede una finestra di dimensione $N > 1$, permettendo la *trasmissione continua di pacchetti in attesa di riscontro* (pipeline), fino al riempimento del buffer di invio.
![[Pasted image 20260515125342.png]]

- **Ricezione corretta:** I frame 0 e 1 vengono ricevuti, validati e riscontrati (Ack0, Ack1). Il destinatario aggiorna la sua finestra aspettandosi il frame 2.
    
- **Errore (E):** Il frame 2 viene danneggiato o perso durante il transito. Non giungendo al destinatario o non superando i controlli di integrità, non viene generato alcun ACK.
    
- **Scarto sistematico (D - Discard):** La sorgente, ignara della perdita, continua a trasmettere i frame successivi presenti nella sua finestra di invio (frame 3, 4, 5, 6, 7, 8). Il destinatario riceve questi frame integri, ma poiché si aspetta rigorosamente il frame 2 (avendo finestra pari a 1), **rifiuta e scarta** automaticamente *tutti i frame fuori sequenza*, omettendo l'invio dei relativi ACK.

- **Ritrasmissione:** L'assenza dell'Ack2 impedisce l'avanzamento della finestra di invio della sorgente. Allo scadere dell'intervallo di **timeout** associato al frame 2, la sorgente rileva l'anomalia.
    
- **Go-Back-N:** Il protocollo impone alla sorgente di "tornare indietro" al frame non riscontrato (il frame 2) e di **ritrasmettere in ordine tutti i frame** inviati successivamente, ricominciando l'intera sequenza (2, 3, 4, 5, 6, 7, 8...).

### Protocolo con ripetizione selettiva (sliding window)

Il protocollo a **Ripetizione Selettiva** (Selective Repeat) è un'evoluzione progettata per superare l'inefficienza e lo spreco di banda caratteristici del protocollo Go-Back-N in presenza di canali soggetti a errori.

- **Finestra di Ricezione:** A differenza del Go-Back-N, la ripetizione selettiva utilizza una finestra di ricezione di **dimensione maggiore di 1**. Questo permette al livello Data Link del destinatario di *accettare frame fuori sequenza*.
    
- **Meccanismo di Buffer:** Se un frame risulta danneggiato o perso, viene scartato. Tuttavia, i frame successivi ricevuti correttamente **non vengono rifiutati**, ma allocati in un buffer di memoria locale in attesa del recupero del frame mancante.

![[Pasted image 20260515130421.png]]

Il diagramma illustra la sequenza operativa in caso di errore:

1. **Errore e Salto:** I frame 0 e 1 sono riscontrati. Il frame 2 va perso.
    
2. **Buffering e NAK:** Arriva il frame 3. Il destinatario rileva il salto, genera un **NAK 2** e posiziona il frame 3 nel buffer. I successivi frame 4 e 5 in arrivo subiscono lo stesso trattamento di buffering.
    
3. **Ritrasmissione Selettiva:** La sorgente riceve il NAK 2 e trasmette immediatamente una nuova copia **solo** del frame 2 (non ritrasmette il 3, 4 o 5).
    
4. **Consegna Sequenziale:** Il destinatario riceve il frame 2. Ora la sequenza in memoria (2, 3, 4, 5) è continua e completa. Il livello Data Link scarica il buffer, passando i pacchetti nell'ordine corretto al livello di rete superiore, e fa avanzare la propria finestra generando i relativi ACK cumulativi o singoli.

Se dovesse perdere il NAK la soergente andrebbe comunque in timeout per il frame 2, e lo ritrasmetterebbe, ma se ne accorgerebbe più tardi.

### Esempi reali 

#### La famiglia HDLC (Protocolli storici)

Questi protocolli, derivati originariamente da IBM, rappresentano la base orientata ai bit per il controllo del data link.

- **Struttura del Frame:** Utilizzano il _bit stuffing_ e sono delimitati da un flag di inizio/fine `01111110`. Contengono campi per indirizzo, controllo, dati (payload) e un checksum (CRC) per gli errori.
    
- **Tipologie di Frame:** Il campo di controllo definisce tre tipi di frame:
    
    1. _Informazioni:_ trasportano dati e numeri di sequenza per gli ACK (piggybacking).
        
    2. _Supervisione:_ gestiscono il flusso e gli errori (es. ACK positivi o negativi/rifiuti).
        
    3. _Senza numero:_ gestiscono la connessione (es. disconnessione o reset della linea).

![[Pasted image 20260515131024.png]]![[Pasted image 20260515131054.png]]


#### SLIP (Obsoleto):

Protocollo basilare che utilizza il _byte stuffing_. 
Non effettua correzione degli errori, non supporta l'assegnazione dinamica degli IP e non prevede autenticazione.
Può risparmiare spazio comprimendo intestazioni di pacchetti consecutivi.


#### PPP (Point-to-Point Protocol):

È lo standard moderno, **orientato al carattere**, ampiamente usato per le connessioni WAN e ADSL. A differenza di SLIP, gestisce gli errori, supporta IP dinamici e permette l'autenticazione.

Il PPP si basa su due sotto-protocolli fondamentali:

- **LCP (Link Control Protocol):** Gestisce l'apertura, il test, la negoziazione dei parametri (come la lunghezza massima del frame) e la chiusura della linea fisica.
    
- **NCP (Network Control Protocol):** Subentra dopo LCP per configurare le opzioni specifiche del livello di rete sovrastante (come l'IP).

**Fasi della connessione PPP:** La linea parte dallo stato `DEAD`, passa a `ESTABLISH` (negoziazione LCP), poi ad `AUTHENTICATE` (opzionale), entra in fase `NETWORK` (configurazione NCP), e infine arriva allo stato `OPEN` per la trasmissione dati, prima di terminare (`TERMINATE`).
![[Pasted image 20260515131342.png]]


#### ADSL 

Per le connessioni a banda larga su doppino telefonico (ADSL), l'architettura utilizza una pila di protocolli sovrapposti.

La gerarchia (dal livello di rete al livello fisico) è la seguente: **IP -> PPP -> AAL5 -> ATM -> ADSL**.

- **ADSL (Livello Fisico):** Utilizza la modulazione digitale **OFDM** (Multiplazione a divisione di frequenze ortogonali).
    
- **ATM (Data Link):** Trasmette l'informazione in celle a lunghezza fissa in modo "asincrono" (ovvero, invia dati solo quando ce ne sono effettivamente, senza un flusso continuo forzato).
    
- **AAL5 (ATM Adaptation Layer 5):** Fa da intermediario tra PPP e ATM. Si occupa di segmentare e riassemblare i pacchetti in celle. Aggiunge un trailer (non un header) con la lunghezza totale e un CRC di 4 byte, inserendo byte di riempimento (_padding_) per far sì che la lunghezza sia un multiplo esatto di 48 byte.
    
- **PPPoA (PPP over ATM):** È la specifica che definisce come incapsulare esattamente i frame PPP all'interno del payload di AAL5.


# Sottolivello **MAC** ('di accesso al mezzo')

Questo sottolivello comprendi i protocolli per allocare l'uso di un canale ad accesso multiplo.
E' molto importante nelle LAN (e WLAN) dato che preferiscono le connessioni ad accesso multiplo.

## Problemi i allocazione del canale


### Allocazione statica 


