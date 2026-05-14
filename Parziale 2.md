
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
- lento: le frequenze vengono assorbite 
- veloce: le frequenze rimbalzano sulle superfici

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