
# Livello di rete 

Di cosa si fa carico 

Compiti principali

In base a cosa si realizza il livello di rete (principi/decisioni)

Servizi con e senza connessione

## Principi di commutazione 

Definizione commutazione 

Scelta della tecnica in base a: ...

### Commutazione di circuito

img con spiegazione : 
da spiegare meglio

- router instradatori
- ritardo di instaurazione


## Commutazione di messaggio 

- Store and forward 

img da spiegare 

Non c'è una connessione.

Altra img da spiegare 

- Ritardo di trasferimento 

Il servizio di trasferimento non può consentire una comunicazione interattiva.

Non va bene per grandi file, quindi si divide in pacchetti.

## Commutazione di pacchetto 

Informazione divisa in unità di lunghezza massima predefinita: pacchetti.

Modalità: datagramma; circuito virtuale

### Spiegazione datagramma con immagine

Conto proprio, intestazione con dati aggiuntivi

ordine sparso, persi, duplicati.
Molte cose insieme ma si possono perdere

### Spiegazione circuito virtuale con immagine 

Problema del continuo utilizzo di un percorso

#### Algoritmi di routing
Cosa fanno 
Statici e dinamici (o adattivi) -> in base a cosa differiscono tra loro

Algoritmo in base al tipo di sottorete 
- sessione di routing 

Cosa ci si aspetta da un algoritmo di routing  (6 punti)

- metrica -> cosa è, cosa utilizza.
	- metrica inferiore

- Principio di ottimalità (CON IMG e spiegazione)

- bilanciamento del carico
	- modalità di load balancing (equal-cost e unequal-cost)

- termine **convergenza**
	- tempo di consistenza (ha senso solo per alg. dinamici)


### Principali Algoritmi di Routing Statici
sono 3

#### Shortest Path Routing 

Con immagine da commentare (migliora di molto il commento, è troppo specifico all'esempio e mancano dei dettagli generali)

- interdistanze 

#### Flooding

cosa fe 
perche non conviene con molti pacchetti 

Tecniche per migliorarne il traffico generato 
(contatore di hop, scarta alla seconda vista, selective flooding)

#### Flow based routing

calcolo in anticipo

Informazioni necessarie per applicarlo

Assunzioni (2)

$$\text{ritardo singola linea}=\frac{\text{traffico sulla linea}}{\text{traffico totale della rete}}$$
Come calcolare il ritardo medio dell'intera rete: somma pesata dei ritardi delle linee  
Su cosa si basa questo metodo (flow based routing) considerata una topologia nota(6 punti)

### Principali algoritmi di routing dinamici 
sono 2 

#### Distance Vector

Ho un vettore di ritardi per ciascun nodo che ho a disposizione.
Quindi ciascun nodo avrà un vettore.
(controlla poi, può confondere)

Router stima i vicini con **pacchetti ECHO**, contando quanto ci mettono a tornare indietro. (viene fatto più volte come test)

Ad ogni intervallo i router condividono le loro tabelle con i vicini. Ogni router ricalcola la propria in base alle nuove informazioni 

Immagini con spiegazione (sono 3 tabelle, 2 simili tra loro)

- Paradosso dello scambio all'infinito
#### Link State Routing

Ogni tot i router testano i loro vicini e condividono le info con gli altri.
Ogni router ricostruisce localmente la topologia completa della rete.

E' suddiviso in 5 passaggi: 
Chi c'è vicino -> pacchetti HELLO
Quanto sono lenti i vicini -> pacchetti ECHO (Costruisce la **Neighbour Table**)
Viene costruito un pacchetto LSP (Link State Packet) che contiene ...
Invio dell'LSP con flooding.
Calcolo del cammino minimo tra tutti i router avendo ricevuto gli LSP.


### Routing Gerarchico 

Per sottoreti molto grandi.

La rete viene divisa in regioni.

I router all'interno della stessa regione si conoscono.
Per comunicare con uno all'esterno, un router interno da da **router di confine**
Quindi si possono considerare due livelli di routing (interno e di confine/esterno)

### Broadcast Routing

4 metodologie per ottenere la trasmissione broadcast:
Invio pacchetti distinti : pro e contro 
flooding: pro e contro 
multidestination routing: lista di destinazioni, invio delle copie fino a raggiungere un solo destinatario
Il quarto utilizza il sink tree del routeer di trasmissioni e lo spanning tree per inoltrare i pacchetti. (pro, contro)

(ricorda definizione spanning tree CON IMMAGINE)

Utilizzo di **reverse path forwarding** al posto dello **spanning tree**
altra immagine con 3 topologie diverse: sottorete, sink tree, Albero realizzato dall'inoltro a percorso inverso.

### Multicast Routing 

Algoritmo per l'instradamento dei pacchetti multicast.

(immagine con 4 grafi)

Necessita la divisione e gestione dei gruppi.
I router devono sapere quali host appartengono ad ogni gruppo. (host avvisano i router o router interrogano host).

Ogni router elabora uno spanning tree che copre tutti gli altri router.

### Internetworking

Per collegare reti che utilizzano protocolli differenti, passando attraverso una rete multiprotocollo con apposito router.

Il router consente di aprire un bridge o un tunnel a seconda dei casi.

(immagine con vari nomi di protocolli conosiuti che passano attraverso una rete multiprotocollo)

- tunneling: cosa è e quando usarlo

(immagine più generica con rete X <-> rete Y <-> rete X)


### Struttura generica di un pacchetto 

sorgente e destinazione 
lunghezza 
protocollo
percorso 
versione-servizi
frammentazione 
Time To Live 
checksum
campo dati 
(a volte anche timestamp)

## Congestione 

Va limitato il numero di collisioni tra pacchetti. (genera congestione)

Agli alg. di routing si affiancano gli **Algoritmi di controllo della congestione**

Buffer contenente pacchetti arrivati ma non ancora spediti/reinoltrati.

(img con grafico pacchetti inontrati X pacchetti inviati)

Peggioramento a causa del **Timeout and Retrasmission**
- Congestion Collapse 

Fattori di congestionamento di un router 

Politica di congestion avoidance (riscrivila, può confondere)

Come agiscono gli alg. di controllo della congestione
L'approccio al problema della congestione si può ricondurre a 2 categorie (open loop, closed loop)

### Choke Packet 

Da riformulare meglio.
Il router che sta ricevendo troppi pacchetti chiede al router più vicino alla sorgente di aumentare il buffer della sua linea e rallentare l'invio.

E' quindi previsto che un router tenga d'occhio il gradi di utilizzo delle sue linee in uscita.
U = utilizzo istantaneo
M = Media esponenziale
a = peso della storia passata (compreso tra 0 e 1)
(1-a) = peso dato dall'informazione più recente

$$M_{nuovo}=a*M_{vecchio}+(1-a)*U$$

Alla ricezione di un **choke packet** il router diminuirà la velocità di invio dei pacchetti.
Ogni router attende un intervallo di tempo prima di ricontrollare se è arrivato un nuovo choke packet.

#### HOP-BY-HOP Choke Packet 
Consiste nell'inviare un pacchetto di rallentamente su ogni router intermedio fino a raggiungere la fonte.
All'arrivo alla fonte il flusso sarà già rallentato.

Permette di sbloccare rapidamente la congestione nel punto in cui ha avuto origine.
Richiede un maggiore utilizzo del buffer nei router lungo il percorso.

### Drop Tail 

Cancella i pacchetti in eccesso dal buffer.

Non reagisce dinamicamente alle condizioni di traffico della rete.
Ha diversi svantaggi:
pessima sincronizzazione dei flussi
non equa distribuzione della perdita di pacchetti tra connessioni
scarso utilizzo delle risorse di rete 

### Load Shedding

Quando il buffer è pieno, scarta i pacchetti secondo delle regole.

Regola del **wine**: vecchio meglio del nuovo, scarta i pacchetti nuovi e serve i primi arrivati (FIFO).

Regola del **milk**: nuovo migliore del vecchio, scarca i pacchetti vecchi e serve quelli nuovi (LIFO).

### Active Queue Management (AQM)

E' una famiglia di tecniche usate dai router per gestire le congestioni in maniera dinamica.

Controlla costantemente la coda del buffer, quando si sta riempiendo troppo, inizia ad intervenire. Tutto PRIMA che il buffer si riempia.
E' quindi un metodo **pre-attivo**.

Utilizza il **Dynamic Buffer Limiting (DBL)** per tenere traccia della lunghezza della coda per ogni flusso dei traffico entrante.
Quando la lunghezza della coda è preoccupante, il DBL comincia a cancellare pacchetti o a impostare i bit **Explicit Congestione Notification (ECN)** nell'intestazione dei pacchetti a 1 (true).

#### Random Early Detection (RED)

Più popolari AQM utilizzati in TCP/IP.
Misura la dimensione media con un filtro pesaso.
Cancella pacchetto con una determinata probabilità

**Packet-marking-probability** in base:
valore aq,
tempo trascorso ultima cancellazione 
prob massima cancellazione

(immagine grafico) -> RED vesione classica 

(immagine grafico) -> RED gentle-version

Quando la lunghezza media della coda cresce proporzionalmente al numero di connessioni attive nel sistema, l'algoritmo non riesce ad evitare la congestione.

Con RED solitamente la coda viene misurata in byte, non in pacchetti.

RED può essere modificato per rendere la *packet marking probability* proporzionale alla grandezza del pacchetto.

Non agisce sulle **congestioni temporanee** le quali aumentano solo la *Queue lenght* per poco tempo, ma agisce sulle **congestioni a lunga durata** che aumentano invece la dimensione media della coda (quindi monitorata da RED).  


tanti calcoli e 2 immagini (di calcoli)


## Qualità del servizio 

connessione: seguono lo stesso percorso 
senza connessione: percorsi differenti per ogni pacchetto

Parametri QoS:
- affidabilità
- ritardo 
- jitter
- banda

Dipende dalla tipologia delle reti:
- reti a velocità costante 
- a velocità variabile in tempo reale
- a velocità variabile non in tempo reale 
- velocità disponibile 

tecniche per ottenere un buon Qos:
- bufferizzazione 
- leaky bucket
- token bucket
- flow specification
- routing adattivo
- sovradimensionamento

### Bufferizzazione 

Produco una quantità di pacchetti che memorizzo in un buffer. Quando avrò prodotto un buon numero di pacchetti, inizierò ad inviarli.
Così facendo il destinatario li riceverà in maniera costante nel tempo.

Il limite è il costo delle risorse (?)

### Leaky bucket


(img leakybucket) 
**Scopo:** Trasformare un flusso di dati irregolare in un flusso costante e regolare (Traffic Shaping).

**Come funziona:** Immagina un secchio con un buco sul fondo. L'acqua (i pacchetti di dati inviati dall'host) può essere versata nel secchio a fiotti irregolari. Tuttavia, l'acqua uscirà dal buco sul fondo sempre a una velocità costante e fissa. Nella rete:

- L'host invia i pacchetti, che vengono temporaneamente immagazzinati in un buffer (il "secchio").

- Il sistema preleva i pacchetti dal buffer e li immette nella rete a una **velocità fissa e costante** (il "data rate fissato").

- **Gestione dei picchi:** Se l'host trasmette dati troppo velocemente e riempie completamente la capacità del buffer, i pacchetti in eccesso non trovano spazio e vengono **scartati (persi)**.


_In sintesi: Assicura un flusso di uscita rigido e costante, assorbendo piccole irregolarità ma non tollerando grossi picchi improvvisi._

### Token bucket

(img token bucket) 

**Scopo:** Limitare la velocità media del traffico, ma consentendo dei picchi di trasmissione improvvisi (Traffic Policing / Shaping elastico).

**Come funziona:** In questo caso, il "secchio" non contiene i pacchetti, ma dei **gettoni (token)**. Nella rete:

- Il sistema genera nuovi gettoni a una velocità costante e li inserisce nel secchio, fino al raggiungimento di una capacità massima.

- Quando l'host vuole inviare un pacchetto, deve "pagare" prelevando un gettone dal secchio.

- Se ci sono gettoni disponibili, il pacchetto viene inviato immediatamente.

- Se l'host non ha trasmesso nulla per un po' di tempo, i gettoni si accumulano nel secchio.

- **Gestione dei picchi:** Grazie ai gettoni accumulati, se l'host deve inviare improvvisamente una grande mole di dati (un picco o _burst_), può farlo consumando tutti i gettoni presenti in un colpo solo. Una volta finiti i gettoni, dovrà aspettare che ne vengano generati di nuovi al ritmo prestabilito prima di inviare altri pacchetti.
    
Come la stamina nei guochiuoi.

### Flow specification

Molto efficace se sorgente, sottorete e destinazione si accordano in merito.
Ci si può accordare su: 
- caratteristiche che si vuole inviare 
- qualità del servizio 

Questo accordo viene chiamato **flow specification** e consiste in una struttura dati che descrive le grandezze in questione.

Il controllo della congestione è più semplice in reti 'in accordo'.

Admission control: negare l'attivazione di nuovi circuiti virtuali quando non si hanno le risorse per gestirli.

### Routing Adattivo 

Si basa sulla suddivisione dei dati in percorsi differenti.

### Sovradimensionamento

Consiste nell' aumentare la capacità di calcolo, la dimensione del buffer e l'ampiezza di banda in singole tratte della sottorete.
'Prevede un totale necessario e ne richiede di più per sicurezza'

## Servizi integrati 

Quando si trasmettono flussi di dati multimediali o _real-time_ (come voce o video), la rete deve garantire prestazioni elevate e tempi di consegna certi. Per fare questo, la Quality of Service (QoS) utilizza architetture specifiche, tra cui i **Servizi Integrati (IntServ)**, orientati alla gestione del singolo flusso di dati per applicazioni unicast e multicast.

### protocollo RSVP

![[Pasted image 20260523151844.png]]  

Il suo scopo è **prenotare in anticipo le risorse di rete** lungo tutto il percorso tra sorgente e destinazione.

- **Come funziona (l'esempio dei nodi):** Immagina una rete in cui l'Host 1 sta già comunicando con l'Host 4 occupando molta banda sul percorso (es. passando per i nodi A-E-H-J). Se l'Host 3 volesse iniziare a comunicare con l'Host 4, potrebbe trovare il percorso congestionato, subendo rallentamenti o perdite di pacchetti.
    
- **La soluzione di RSVP:** Prima di iniziare a inviare i dati veri e propri, l'Host 3 invia un messaggio RSVP di "prenotazione". I router lungo il percorso verificano se hanno abbastanza risorse libere. Se la risposta è sì, allocano (mettono da parte) una porzione di banda dedicata esclusivamente a quella comunicazione. In questo modo si ottimizza l'uso della rete e si prevengono le congestioni.

### protocollo MPLS

Un'altra metodologia estremamente efficiente per gestire il traffico e le risorse di rete è il **Label Switching** (commutazione di etichette), il cui standard di riferimento creato dall'IETF è l'**MPLS**.

Invece di far decidere ai router l'instradamento analizzando ogni volta il lungo indirizzo IP di destinazione, l'MPLS **aggiunge una breve etichetta (label)** al pacchetto. I router (chiamati LSR - Label Switching Routers) inoltrano il traffico basandosi unicamente sulla lettura di questa etichetta, rendendo l'operazione molto più rapida ed efficiente.

**Collocazione nella pila ISO/OSI** L'intestazione (header) MPLS viene inserita tra l'header di Livello 2 (Collegamento Dati, es. Ethernet) e l'header di Livello 3 (Rete, es. IP). Per questo motivo, l'MPLS viene spesso definito un protocollo di **Livello 2.5**. Questa flessibilità è una delle ragioni del suo enorme successo nelle reti moderne.

![[Pasted image 20260523151823.png]]
**I campi dell'intestazione MPLS (32 bit totali):** L'header MPLS è composto da 4 campi specifici:

- **Etichetta (Label - 20 bit):** È l'indice vero e proprio utilizzato dai router per capire su quale linea di uscita inoltrare il pacchetto.

- **QoS / EXP (3 bit):** Indica la classe di servizio o la priorità del pacchetto (Traffic Class), utile per gestire la Quality of Service.

- **S (Stack - 1 bit):** L'MPLS permette di impilare (incapsulare) più etichette una sull'altra (creando percorsi virtuali annidati). Questo bit indica se l'etichetta corrente è l'ultima in fondo allo stack (se vale 1) o se ce ne sono altre sotto (se vale 0).

- **TTL (Time To Live - 8 bit):** Funziona esattamente come il TTL dell'IP. Viene decrementato di 1 a ogni passaggio in un router. Se arriva a 0, il pacchetto viene scartato per evitare cicli infiniti nella rete.

**Forwarding Equivalence Class (FEC)** Nell'MPLS, **pacchetti diversi che richiedono lo stesso identico trattamento** (stesso percorso, stessa priorità) possono essere **raggruppati e associati alla medesima etichetta**. Questo gruppo di pacchetti prende il nome di **FEC (Forwarding Equivalence Class)**. Questo permette di creare circuiti virtuali sovrapposti alla normale infrastruttura IP, separando logicamente i flussi di traffico.

## Service Level Agreement (SLA)

Nelle reti di telecomunicazioni, la Quality of Service (QoS) non dipende solo dagli algoritmi usati, ma richiede che la rete e l'host (l'utente) si accordino su quali siano le prestazioni desiderate e quali risorse la rete possa effettivamente erogare.

Per regolamentare questo rapporto nasce il **Service Level Agreement (SLA)** (Accordo sul Livello di Servizio). In pratica, l'SLA è un contratto che definisce delle **soglie di garanzia minima o massima** su parametri misurabili, assicurando che la rete fornisca all'host le prestazioni promesse.

### I Parametri Tipici di un SLA

Per misurare la qualità del servizio, un SLA standard prende in considerazione vari parametri:

- **Throughput per port:** È la "produttività" minima garantita. Indica la quantità di dati che il router garantisce di poter inoltrare attraverso una sua porta (si misura in bit/sec, frame/sec o pacchetti/sec).
    
- **Data Delivery Ratio (DDR):** È il tasso di consegna. Rappresenta la garanzia sul livello minimo di dati che arriveranno effettivamente a destinazione (senza essere persi nella rete).
    
- **Constant Bit Rate (CBR):** È la garanzia che la rete *manterrà una velocità di consegna minima e costante*. È fondamentale per applicazioni in tempo reale (come voce o video) che non tollerano variazioni di velocità (tipico delle reti ATM).
    
- **Back-up di linea:** È la garanzia che la connessione non cada se il collegamento principale si guasta.
    
    - _A caldo (dinamico):_ La linea di riserva è già attiva. Il passaggio (switch) è immediato e si perdono pochissimi pacchetti.
        
    - _A freddo (statico):_ La linea di riserva va attivata al momento del guasto, comportando dei tempi di inattività stimati e concordati.
        
- **Back-up router:** Stesso concetto del back-up di linea, ma si applica al guasto del dispositivo fisico (il router). Anche questo può essere previsto _a caldo_ o _a freddo_.
    
- **Uptime:** È il tempo di disponibilità del servizio. Viene espresso in percentuale (es. **99.9%**) e indica per quanto tempo il servizio deve rimanere attivo e funzionante in un mese o in un anno.
    
- **Report Service Unit (RSU):** È la garanzia che l'host abbia a disposizione degli strumenti (dashboard/report) per visualizzare e monitorare le prestazioni della rete.
    
- **Management Service Unit (MSU):** A differenza del RSU, questi sono strumenti _attivi_. Permettono all'host di configurare la rete in autonomia (es. modificare la banda a disposizione o creare circuiti virtuali).

### KPI (Key Performance Indicator)

Poiché monitorare ogni singolo parametro dell'SLA può essere molto complesso, si utilizzano i **KPI (Key Performance Indicator)**.

I KPI sono indicatori strutturati che raggruppano vari parametri in un unico set di dati più facile da leggere, offrendo una "fotografia" immediata dello stato di salute del servizio. L'ultima frase della slide (_"Se scende sotto 1, il servizio non sta funzionando come vorremmo"_) fa riferimento a un tipico indicatore a rapporto: se il rapporto tra il servizio _effettivamente erogato_ e quello _concordato_ nell'SLA scende sotto il valore di 1 (cioè sotto il 100% di quanto pattuito), significa che la rete sta violando il contratto.

# Livello rete in internet

Per far funzionare un'infrastruttura **globale** ed **eterogenea** come Internet, il protocollo di rete (IP) è stato progettato seguendo queste regole auree:

- **Semplicità del nucleo centrale:** I protocolli di base (di livello basso) devono rimanere semplici, leggeri e veloci. Man mano che si aggiungono nuove funzioni complesse, queste devono essere gestite dai livelli superiori o agli estremi della rete (secondo il _principio End-to-End_), per non appesantire il lavoro dei router centrali.
    
- **Modularità (Indipendenza dei livelli):** È il concetto alla base della pila protocollare (come il TCP/IP o l'ISO/OSI). Ogni livello fa il suo lavoro in modo indipendente. Questo permette di modificare, aggiornare o sostituire un protocollo a un certo livello (es. passare dal Wi-Fi al cavo Ethernet) senza dover cambiare nulla nei livelli superiori o inferiori.
    
- **Gestione dell'eterogeneità:** Internet deve essere il "collante" universale. Deve poter connettere tra loro hardware, sistemi operativi e dispositivi completamente diversi (smartphone, server, sensori). Il protocollo IP è la lingua franca che tutti devono comprendere per parlarsi, indipendentemente dall'infrastruttura fisica.
    
- **Preferenza per algoritmi dinamici:** Rispetto alle vecchie reti telefoniche basate su parametri statici, Internet deve usare algoritmi dinamici (come i protocolli di routing). Questo permette alla rete di adattarsi automaticamente in tempo reale ai guasti, ricalcolando i percorsi alternativi.
    
- **Principio di Robustezza (Legge di Postel):** Sintetizzato dalla famosa frase dell'informatico Jon Postel: _"Sii rigoroso in ciò che invii, sii tollerante in ciò che ricevi"_. Un nodo deve formattare i pacchetti in uscita in modo impeccabile, ma deve essere programmato per tollerare imperfezioni (pacchetti in ritardo, disordinati, duplicati o leggermente malformati) quando riceve dati da altri, senza bloccarsi.
    
- **Scalabilità assoluta:** L'architettura non deve avere colli di bottiglia strutturali. Le soluzioni scelte devono funzionare bene sia per poche decine di macchine (le origini), sia per svariati miliardi di host (oggi). L'evoluzione dagli indirizzi IPv4 a IPv6 ne è l'esempio perfetto.
    
- **Rapporto costo/prestazioni:** Internet non è nata per fornire un servizio di lusso infallibile, ma come rete "Best-Effort" (fa del suo meglio, ma non garantisce nulla). Questo compromesso è stato scelto per mantenere l'hardware (i router) economico e semplice, favorendo l'espansione capillare e globale della rete. Se serve un'affidabilità assoluta, il costo elaborativo viene spostato sui computer degli utenti finali.

### L'infrastruttura di Internet

Internet è un insieme di reti interconnesse.

![[Pasted image 20260523151658.png]]

Internet non è una singola rete, ma una **"rete di reti"**. La sua struttura è gerarchica e può essere divisa in livelli:

- **Dorsali (Backbone):** Sono le "autostrade" ad altissima velocità di Internet (gestite dai provider di livello 1 o _Tier 1_). Attraversano continenti e oceani tramite cavi sottomarini in fibra ottica (le _linee affittate transoceaniche_).
    
- **Reti Nazionali e Regionali:** Si collegano alle dorsali per distribuire la connettività su aree geografiche più piccole (i provider _Tier 2_ o _Tier 3_). Un esempio italiano citato (con un errore di battitura nella slide) è il **GARR**, la rete nazionale per l'università e la ricerca.
    
- **Reti di Accesso (Edge):** Sono i margini della rete, dove si trovano gli utenti finali. Possono essere:
    
    - _Reti Domestiche:_ Collegate tramite tecnologie come la **DSL** (nella slide c'è un refuso "DLS") o la Fibra (FTTH).
        
    - _Reti Aziendali:_ Spesso basate su infrastrutture **Ethernet**.
        
    - _Reti Mobili/Wireless:_ Utilizzano antenne (4G/5G, WiMAX) per connettere dispositivi in mobilità.
        

_Nota sui router:_ Il passaggio tra una rete e l'altra avviene tramite **Router di confine (Edge/Boundary Router)**, che fungono da "dogana" per i dati.

### Il Protocollo IP:

Come possono reti fisicamente così diverse (Fibra, Rete Mobile, Rame) comunicare tra loro? Grazie al protocollo **IP (Internet Protocol)** al Livello di Rete.

- **Universalità:** L'IP maschera le differenze fisiche sottostanti. Permette di trasportare dati da una sorgente a una destinazione senza preoccuparsi di quante e quali reti diverse ci siano in mezzo.
    
- **Servizio "Best-Effort":** L'IP fa "del suo meglio" per consegnare i pacchetti, ma **non garantisce nulla**. I pacchetti (chiamati _datagrammi_) possono essere persi, arrivare in ritardo o in disordine. Se serve affidabilità, se ne deve occupare il Livello di Trasporto (TCP).
### Dimensione dei Pacchetti (MTU)

Quando il Livello di Trasporto passa i dati al Livello di Rete, questi vengono divisi in pacchetti IP.

- In teoria, un pacchetto IP potrebbe pesare fino a **64 KB**.
    
- Nella pratica, la dimensione massima è quasi sempre limitata a **1500 byte**.
    
- _Perché?_ Perché i pacchetti IP devono essere inseriti all'interno dei frame **Ethernet** (che è lo standard dominante per i collegamenti locali), la cui capacità massima (chiamata _MTU - Maximum Transmission Unit_) è storicamente di 1500 byte.
### Ridondanza e Instradamento (Routing)

Tra il computer di casa tua e un server aziendale ci possono essere decine di router intermedi.

- Internet è progettata con un'alta **ridondanza**: le dorsali e i provider sono interconnessi tra loro in punti multipli.
    
- Se un cavo si rompe o un router si guasta, esistono molti percorsi alternativi. Spetta ai **protocolli di routing** (gli "algoritmi dinamici" citati nelle slide precedenti) calcolare costantemente la strada migliore e più veloce da far prendere ai pacchetti IP in quel preciso istante.


## IPv4 e IPv6

Non c'è una divisione netta basata sulla gerarchia. A causa dell'esaurimento degli indirizzi IPv4, il mondo sta passando a **IPv6 ovunque**, dalle dorsali fino agli smartphone dei singoli utenti.

Attualmente, la maggior parte delle reti globali e locali utilizza una tecnica chiamata **"Dual Stack"**, ovvero i dispositivi e i router "parlano" _contemporaneamente_ sia IPv4 che IPv6 a tutti i livelli della rete, in attesa che il vecchio IPv4 venga definitivamente spento.


#### DIFFERENZA TRA INTESTAZIONE E STRUTTURA 
L'**intestazione** (o header) è l'insieme dei dati posti davanti al pacchetto da inviare. Come una lettera contiene varie informazioni tra le quali il destinatario.

La **struttura** dell'indirizzo ip è la struttura del dato con cui si **identifica** una macchina o una rete.
### Intestazione IPv4

![[Pasted image 20260523151604.png]]

L'intestazione IPv4 ha una dimensione **minima di 20 byte** (se non ci sono opzioni) e una **massima di 60 byte** (aggiungendo fino a 40 byte di opzioni). I dati sono organizzati in blocchi da 32 bit (4 byte).

Possiamo dividere logicamente l'intestazione in 5 parti funzionali:

#### PARTE 1: Informazioni Generali

- **Version (4 bit):** Indica la versione del protocollo IP. In questo caso, conterrà il valore binario per "4" (0100). _Nota: IPv6 usa un formato di intestazione completamente diverso, non si usa questo campo per passare a IPv6._
    
- **IHL - Internet Header Length (4 bit):** Indica la lunghezza totale dell'intestazione. Poiché misura in "parole" da 32 bit (4 byte), il valore minimo è 5 ($5 \times 4 = 20$ byte) e il valore massimo è 15 ($15 \times 4 = 60$ byte).
    
- **Type of Service - ToS (8 bit):** Utilizzato per la Quality of Service (QoS). Serve a dare priorità ad alcuni pacchetti (es. voce o video) rispetto ad altri.
    
- **Total Length (16 bit):** Indica la lunghezza totale dell'intero pacchetto (Intestazione + Dati utili). Avendo 16 bit a disposizione, un pacchetto IP può teoricamente pesare fino a **65.535 byte**. _Attenzione alla slide:_ i 1500 byte citati sono il tipico limite fisico delle reti Ethernet (MTU), non una regola fissa del Total Length dell'IP.

#### PARTE 2: Controllo della Frammentazione

Se un pacchetto è troppo grande per passare in una specifica rete fisica (es. supera i 1500 byte), il router deve "spezzettarlo" in pacchetti più piccoli, chiamati frammenti. Questa riga dell'header gestisce proprio questo:

- **Identification (16 bit):** Un "codice a barre" univoco generato dal mittente. Tutti i frammenti che derivano da uno stesso pacchetto originale avranno lo stesso numero di Identification, così il destinatario saprà quali rimettere insieme.
    
- **Flags (3 bit):**
    
    - _1° bit (Nullo/Riservato):_ Attualmente non usato, deve essere 0.
        
    - _DF (Don't Fragment):_ Se impostato a 1, ordina ai router di **non frammentare**. Se il pacchetto è troppo grosso per passare, il router lo scarta e manda un messaggio di errore al mittente.
        
    - _MF (More Fragments):_ Se impostato a 1, significa "attenzione, ci sono altri frammenti dopo di me". Nell'ultimo frammento della serie, questo bit viene messo a 0.
        
- **Fragment Offset (13 bit):** Indica la posizione esatta di quel frammento all'interno del pacchetto originale. Serve al destinatario per rimettere i pezzi in ordine corretto, come in un puzzle.
#### PARTE 3: Vita e Protocollo

- **TTL - Time to Live (8 bit):** _Attenzione qui:_ storicamente si misurava in secondi, ma oggi **rappresenta il numero di salti (hops) massimi**. Ogni router che il pacchetto attraversa sottrae 1 a questo valore. Se il TTL arriva a 0, il pacchetto viene scartato. Serve a evitare che un pacchetto vaghi all'infinito per Internet a causa di un errore di instradamento.
    
- **Protocol (8 bit):** Dice al livello di rete a chi deve consegnare i dati una volta arrivati a destinazione. Ad esempio, indicherà se il carico utile (payload) è un segmento TCP, un datagramma UDP o un messaggio ICMP.
    
- **Header Checksum (16 bit):** Una somma di controllo matematica usata per verificare che _solo l'intestazione_ (non i dati) non abbia subito corruzioni durante il viaggio.
    

#### PARTE 4: Indirizzamento

Questa è la parte fondamentale per il recapito:

- **Source Address (32 bit):** L'indirizzo IP di chi spedisce il pacchetto.
    
- **Destination Address (32 bit):** L'indirizzo IP di chi deve ricevere il pacchetto.
    

#### PARTE 5: Options (Opzionale, max 40 byte)

Vengono usate raramente per scopi di test o sicurezza. _Correzione importante rispetto alla tua slide:_

- **Security:** Specifica livelli di sicurezza o classificazione (usato in ambito militare).
    
- **Strict Source Routing:** Il mittente impone **tutti** i router esatti che il pacchetto deve attraversare. Se un router intermedio salta, il pacchetto viene scartato.
    
- **Loose Source Routing:** ⚠️ _ERRORE NELLA SLIDE:_ La slide dice "Elenco dei router dove non passare". È **Sbagliato**. Il Loose Source Routing contiene un elenco di router per i quali il pacchetto **DEVE obbligatoriamente passare**, ma lascia la libertà di attraversare _anche altri_ router intermedi non presenti in lista.
    
- **Record Route:** Ogni router attraversato scrive il proprio indirizzo IP in questo spazio, tracciando il percorso reale.
    
- **Timestamp:** Come il Record Route, ma ogni router aggiunge anche l'orario esatto del passaggio.

### Indirizzi IP (RFC 791)

##### Cosa significa RFC 791 
**RFC** sta per **Request for Comments** (letteralmente: _Richiesta di commenti_). È il nome ufficiale che viene dato a tutti i documenti tecnici, le specifiche e gli standard che descrivono come funziona Internet. Questi documenti sono gestiti e pubblicati dall'**IETF** (Internet Engineering Task Force), l'organizzazione mondiale che si occupa di sviluppare e promuovere gli standard di rete.

L'**RFC 791**, pubblicato nel settembre del **1981** (e curato dal famoso Jon Postel che abbiamo citato nella slide sui principi di Internet), è letteralmente **il documento fondativo del protocollo IPv4**.

#### La Struttura dell'Indirizzo IPv4

A differenza degli indirizzi MAC (Ethernet) che sono "piatti" (identificano solo la macchina fisica), gli indirizzi IP sono **gerarchici**. Un indirizzo IPv4 è **composto da 32 bit** ed è sempre diviso logicamente in due parti:

- **Network ID (Parte di Rete):** Identifica la rete a cui appartiene il dispositivo (come il CAP o il nome della via in un indirizzo postale). Tutti gli host sulla stessa rete locale (LAN) condividono questo stesso blocco di bit, chiamato _prefisso_.
    
- **Host ID (Parte Host):** Identifica univocamente il singolo dispositivo all'interno di quella specifica rete (come il numero civico).
    

**Notazione Decimale Puntata:** Per comodità umana, i 32 bit non si leggono di seguito, ma vengono divisi in 4 blocchi da 8 bit (chiamati _ottetti_ o byte). Ogni blocco viene convertito in un numero decimale da 0 a 255 e separato da un punto (es. `128.208.2.151`).

#### L'Indirizzamento per Classi (Classful Addressing)

![[Pasted image 20260523151529.png]]

Prima del 1993, gli indirizzi IP venivano assegnati seguendo un rigido schema "a classi", in cui la dimensione della rete era fissa e determinata dai primissimi bit dell'indirizzo. I router capivano subito a quale classe apparteneva un IP semplicemente guardando **i primi bit del primo ottetto**:

- **Classe A (Grandi reti):**
    
    - **Bit iniziali bloccati:** `0` (Gli indirizzi del primo ottetto vanno da 1 a 126).
    - **Struttura:** 8 bit per la Rete, 24 bit per gli Host.
    - **Capacità:** Pochissime reti disponibili a livello globale, ma ciascuna può contenere oltre **16 milioni di host**. Assegnate solo a governi o multinazionali enormi.
        
- **Classe B (Reti medie):**
    
    - **Bit iniziali bloccati:** `10` (Da 128 a 191).
    - **Struttura:** 16 bit per la Rete, 16 bit per gli Host.
    - **Capacità:** Permette circa 65.000 host per rete.
        
- **Classe C (Piccole reti):**
    
    - **Bit iniziali bloccati:** `110` (Da 192 a 223).
    - **Struttura:** 24 bit per la Rete, 8 bit per gli Host.
    - **Capacità:** Tante reti disponibili, ma ciascuna può avere al massimo **254 host** utilizzabili.
    
- **Classi D ed E:** La D (inizia con `1110`) è riservata al traffico Multicast (comunicazioni uno-a-molti), mentre la E (inizia con `1111`) era riservata per usi sperimentali futuri.

### 3. La Crisi degli Indirizzi e il "Problema dei Tre Orsi"

Lo schema Classful aveva un difetto fatale: **lo spreco enorme di indirizzi**.

La slide cita il simpatico _"Three Bears Problem"_ (ispirato alla fiaba di Riccioli d'Oro):

- La Classe A è _troppo grande_.
- La Classe C è _troppo piccola_ (spesso le aziende avevano più di 250 dipendenti/computer).
- La Classe B sembrava _"quella giusta"_ (perfetta per le aziende).


Il risultato? Tutte le aziende chiedevano (e ottenevano) un indirizzo di Classe B. Tuttavia, un'azienda media aveva magari 500 computer, ma ricevendone una Classe B intera bloccava per sé 65.536 indirizzi, **sprecandone 65.000**. Questo portò, nei primi anni '90, al rischio di un collasso prematuro di Internet per esaurimento degli indirizzi IP.

### Le Soluzioni all'Esaurimento

Per tamponare la crisi prima di inventare sistemi moderni (come il NAT, il CIDR o l'IPv6), si intervenne su tre fronti:

1. **Ripulitura:** Verificare e revocare le doppie assegnazioni o gli indirizzi assegnati per errore.
2. **Requisizione:** Riprendersi interi blocchi di Classe A o B assegnati ad enti che in realtà non li stavano utilizzando (o li stavano sottoutilizzando) per riassegnarli in modo più intelligente. (In Italia il GARR ha avuto un ruolo in queste gestioni accademiche).
3. **Subnetting ("Superfetazione" nelle slide):** Creare delle **Sottoreti**. Si prende la porzione Host di un indirizzo IP e le si "ruba" qualche bit per creare delle reti più piccole all'interno dell'azienda, frammentando in modo efficiente lo spazio a disposizione senza dover chiedere nuovi blocchi alla rete pubblica globale. _(Nota: "superfetazione" è un termine biologico, in ambito informatico e all'esame usa il termine "Subnetting" o "Sottoreti")._


### Indirizzi IP speciali 

Le assegnazioni degli indirizzi non seguono regole fisse, infatti esistono degli indirizzi IP speciali:

![[Pasted image 20260602141623.png]]

**"Questo Host" (Indirizzo Sconosciuto)**
- **Come è fatto:** Tutti i 32 bit sono a `0` (In decimale: **`0.0.0.0`**).
- Viene utilizzato _esclusivamente_ come indirizzo sorgente da un computer che si è appena acceso, è collegato alla rete, ma non ha ancora un indirizzo IP assegnato. In pratica dice: "Sono io, ma non so ancora chi sono". Lo si usa tipicamente mentre si sta chiedendo un indirizzo valido a un server DHCP. Non può mai essere usato come destinazione.

"**Un host su questa rete"** 

- **Come è fatto:** La parte Network (Net-ID) ha tutti i bit a `0`, mentre la parte Host ha un numero specifico.
- Significa "Voglio contattare l'Host X che si trova nella mia stessa identica rete". Oggi questa forma è obsoleta e raramente utilizzata, ma storicamente serviva per riferirsi a una macchina sulla rete locale senza dover specificare qual era l'indirizzo della rete stessa.
    

**Broadcast Locale (Limited Broadcast)**
- **Come è fatto:** Tutti i 32 bit sono a `1` (In decimale: **`255.255.255.255`**).
- È l'equivalente di urlare in una stanza. Quando invii un pacchetto a questo indirizzo, **tutti** i computer collegati alla tua stessa rete locale lo riceveranno e lo leggeranno.
- _Nota importante:_ I router sono programmati per "fermare" questi pacchetti. Non li fanno mai uscire dalla rete locale, altrimenti un singolo urlo inonderebbe l'intera Internet.

**Broadcast Diretto (Directed Broadcast)**

- **Come è fatto:** La parte Network (Net-ID) contiene l'indirizzo di una rete specifica, mentre la parte Host ha tutti i bit a `1` (Esempio: in una rete di classe C `192.168.1.X`, l'indirizzo sarebbe **`192.168.1.255`**).
- Serve a inviare un pacchetto a **tutti** gli host di una specifica rete lontana. Il router recapita il pacchetto fino alla rete di destinazione, e l'ultimo router lo "esplode" inviandolo a tutti i computer di quella LAN.

**Indirizzo di Loopback (Localhost)**

- **Come è fatto:** Qualsiasi indirizzo in cui il primo byte è **`127`** (L'indirizzo usato universalmente è **`127.0.0.1`**).
- È un indirizzo "specchio". Se un computer invia un pacchetto a questo indirizzo, la scheda di rete non lo fa nemmeno uscire sul cavo fisico: lo rimanda immediatamente indietro al computer stesso.
- _Perché è utile:_ È fondamentale per gli sviluppatori o per i test di sistema. Ti permette di far comunicare due programmi sul tuo stesso computer usando i protocolli di rete (come se fossero su Internet), anche se non sei connesso al Wi-Fi o a un cavo.

### Indirizzi IP privati

Poiché gli indirizzi IPv4 pubblici scarseggiavano, l'IETF ha deciso di riservare tre blocchi specifici di indirizzi per l'uso **esclusivamente locale (LAN)**.

- Puoi usare questi indirizzi liberamente all'interno di casa tua o della tua azienda senza doverli chiedere a nessuno e senza pagarli.
- La regola d'oro è che **questi indirizzi non sono instradabili su Internet**. I router di confine (dei provider) sono programmati per "scartare" immediatamente qualsiasi pacchetto che abbia un indirizzo sorgente o destinazione privato, impedendo che escano all'esterno.

Il numeretto dopo la barra (es. `/8`) indica la **Subnet Mask (o Notazione CIDR)**. Rappresenta esattamente quanti bit (partendo da sinistra) sono "bloccati" per identificare la Rete (Net-ID).
(Gianni chiama "mascheramento" la subnet mask)

![[Pasted image 20260602142454.png]]
Ecco i tre blocchi spiegati bene:
- **Blocco a 24 bit (Derivato dalla Classe A):**
    - **Range:** Da `10.0.0.0` a `10.255.255.255`
    - **Notazione:** `10.0.0.0/8` (I primi 8 bit, cioè il `10`, sono fissi).
    - **Capacità:** Offre un'unica gigantesca rete con quasi **17 milioni di host** disponibili. È usata dalle grandissime reti aziendali.
        
- **Blocco a 20 bit (Derivato dalla Classe B):**
    - **Range:** Da `172.16.0.0` a `172.31.255.255`
    - **Notazione:** `172.16.0.0/12` (I primi 12 bit sono fissi).
    - **Capacità:** Raggruppa 16 reti di classe B contigue. Permette di indirizzare circa **1 milione di host**.
        
- **Blocco a 16 bit (Derivato dalla Classe C):**
    - **Range:** Da `192.168.0.0` a `192.168.255.255`
    - **Notazione:** `192.168.0.0/16` (I primi 16 bit, cioè `192.168`, sono fissi).
    - **Capacità:** Raggruppa 256 reti di classe C contigue. Offre oltre **65.000 host**.

Dato che questo indirizzo non può comunicare direttamente all'esterno, è necessario convertirlo in indirizzo ip pubblico all'uscita del router.

Il meccanismo di conversione si chiama **NAT (Network Address Translation)**. (Approfondito dopo)
Funziona così: il tuo router di casa possiede _un solo_ indirizzo IP Pubblico e valido su Internet (fornito da TIM, Vodafone, ecc.). Quando il tuo computer (con IP privato) vuole aprire una pagina web, manda la richiesta al router. Il router "strappa" il tuo indirizzo privato dall'intestazione del pacchetto, ci "incolla" il suo indirizzo pubblico e lo manda su Internet (questo processo si chiama _IP Masquerading_. Quando il server risponde, il router fa l'operazione inversa e consegna i dati al tuo computer.


### Subnetting 


Se un'azienda riceve un blocco di indirizzi (es. una Classe B), non le conviene avere migliaia di computer tutti sulla stessa immensa rete locale: ci sarebbe troppo traffico inutile (broadcast) e poca sicurezza.

La soluzione è il **Subnetting**: si prende la porzione dedicata agli "Host" e la si divide arbitrariamente in due parti:

1. **Subnet ID (Sottorete):** Bit rubati agli host per creare reti interne più piccole.
2. **Host ID:** I bit rimanenti, usati per i singoli computer di quella specifica sottorete.

 **La Subnet Mask (Maschera di Sottorete)**:
Per dire ai router esattamente _dove_ abbiamo fatto questo "taglio", si usa la **Subnet Mask**. È un numero a 32 bit composto rigorosamente da una sequenza ininterrotta di `1` seguita da una sequenza ininterrotta di `0`.



![[Pasted image 20260605125246.png]]
- Gli **`1`** indicano la porzione di Rete + Sottorete.
- Gli **`0`** indicano la porzione dedicata agli Host.

**L'operazione AND:** Quando un router riceve un pacchetto, prende l'IP di destinazione, gli applica un'operazione matematica (AND logico) con la Subnet Mask, e il risultato "azzera" la parte host, restituendo esattamente l'indirizzo della sottorete a cui il pacchetto deve essere consegnato.

**Visibilità: Interna vs Esterna**:
**Il subnetting è un affare privato**. Se l'università ha l'indirizzo `128.208.0.0/16` e lo divide in 50 dipartimenti diversi, ai router di Internet non interessa. Internet vede solo la "porta principale" (il `/16`). Solo i router _interni_ dell'università conoscono l'esistenza delle sottoreti e usano le maschere per smistare i dati nei vari uffici. Questo meccanismo tiene le tabelle di routing mondiali piccole ed efficienti.

### CIDR (Classless Interdomain Routing)

**Il Problema: L'esplosione delle Tabelle di Routing**:

- **Edge Router (Router di bordo):** I router delle università o delle aziende hanno un compito facile. Sanno come raggiungere le proprie sottoreti interne, ma per tutto il resto del mondo usano una _rotta di default_: "Se non conosci l'indirizzo, manda tutto al provider (ISP) e ci penserà lui".
- **Core Router (La zona "Default-Free"):** I router giganti al centro di Internet (le dorsali) _non possono_ avere una rotta di default. Loro **devono sapere** dove si trova ogni singola rete del pianeta.
    

Se ogni piccola aziendina o università annunciasse la propria piccola rete a questi Core Router, le loro tabelle di instradamento (Routing Tables) esploderebbero, diventando lente da consultare e impossibili da mantenere in memoria.


**Supernetting e CIDR**:
Per ridurre le dimensioni delle tabelle, si usa il processo opposto al Subnetting: la **Route Aggregation (Aggregazione dei percorsi)** o **Supernetting**.

Invece di annunciare su Internet 4 piccole reti separate (occupando 4 righe nella tabella del Core Router), le si "fonde" in un unico grande blocco, annunciando **un solo prefisso più corto** (occupando 1 sola riga).

Questo è possibile grazie al **CIDR (Classless Inter-Domain Routing)**, che elimina le rigide Classi A, B e C, permettendo maschere di sottorete di qualsiasi lunghezza (es. `/21`, `/22`).


**Come vengono assegnati gli indirizzi in base al fabbisogno:**
Il provider ha a disposizione un grosso blocco e lo divide "su misura" (VLSM) per le università, guardando di quante macchine hanno bisogno:

![[Pasted image 20260605130709.png]]
- **Cambridge:** Ha bisogno di ~2000 IP. La potenza del 2 più vicina è $2^{11}$ (2048).    
    - Bit per gli host: 11
    - Bit per la rete: $32 - 11 = 21$
    - **Assegnazione:** `192.24.0.0/21`
- **Edimburgo:** Ha bisogno di ~1000 IP. Serve $2^{10}$ (1024).
    - Bit per la rete: $32 - 10 = 22$
    - **Assegnazione:** `192.24.8.0/22`
- **Oxford:** Ha bisogno di ~4000 IP. Serve $2^{12}$ (4096).
    - Bit per la rete: $32 - 12 = 20$
    - **Assegnazione:** `192.24.16.0/20`

Il router di Londra è collegato direttamente alle università, quindi nella sua tabella ha **3 righe separate** (più una per il blocco rimasto disponibile). Ma quando Londra deve dire al router di New York come raggiungere queste università, _non gli manda 4 righe_. Si accorge che tutti questi indirizzi sono adiacenti e possono essere inglobati in un'unica maschera più corta: **`/19`**.

Londra invia a New York una sola informazione: **`192.24.0.0/19`**. New York salva **una sola riga** nella sua tabella. Qualsiasi pacchetto destinato a Cambridge, Oxford o Edimburgo farà "match" con quel `/19` e verrà spedito a Londra. Sarà poi Londra, che ha il dettaglio, a smistarlo all'università corretta. Questo salva la memoria dei router globali.

![[Pasted image 20260605130756.png]]


### NAT (Network Address Translation)

In realtà quello che nelle slide chiama NAT è più precisamente PAT (agisce sulle porte), lo chiamerò comunque NAT.

**Come funziona il NAT**:
L'idea di base è permettere a un'intera rete privata (es. `10.0.x.x`) di uscire su Internet presentandosi con **un solo indirizzo IP pubblico** (es. `198.60.42.12`).

Il problema sorge quando il server web risponde al router: come fa il router a sapere a quale dei 50 computer interni deve consegnare la pagina web? La soluzione sfrutta il Livello di Trasporto (Livello 4): le **Porte Sorgente TCP/UDP**.

![[Pasted image 20260605143128.png]]
Ecco il flusso esatto (basato sul grafico):

1. **In uscita:** Il PC interno (`10.0.0.1`) crea una connessione usando una porta a caso (es. `5544`). Il router intercetta il pacchetto, **cancella** l'indirizzo e la porta sorgente, e ci **scrive sopra** il proprio IP pubblico (`198.60.42.12`) e una nuova porta inventata da lui (es. `3344`).
2. **La Tabella NAT:** Il router si segna questa sostituzione in una tabella interna: _"Ricordati che la mia porta esterna 3344 corrisponde al PC interno 10.0.0.1 sulla sua porta 5544"_.
3. **In entrata:** Il Web Server risponde all'indirizzo pubblico del router sulla porta `3344`. Il router legge la porta, consulta la sua Tabella NAT, capisce che il pacchetto era per il PC `10.0.0.1`, fa la sostituzione inversa e glielo consegna.


Per poter funzionare, il NAT infrange diverse regole architetturali:

- **Viola l'autonomia dei livelli (Stratificazione):** Un router lavora al Livello 3 (Rete) e dovrebbe limitarsi a guardare gli indirizzi IP. Il NAT, invece, è costretto ad "aprire" la busta e curiosare nel Livello 4 (Trasporto) per leggere e modificare le porte TCP/UDP.
- **Rompe il modello End-to-End:** Su Internet, chiunque dovrebbe poter contattare chiunque in ogni momento. Con il NAT, le connessioni **devono** per forza partire dall'interno verso l'esterno per creare la riga nella Tabella NAT. Se uno dall'esterno prova a contattare il tuo PC, il router non sa a chi mandare il pacchetto e lo scarta. (Per risolvere questo serve il cosiddetto _Port Forwarding_).
- **Trasforma IP in un protocollo "Stateful" (Orientato alla connessione):** L'IP è nato per essere _connectionless_ (senza memoria delle connessioni). Il NAT costringe i router a mantenere in memoria una tabella di "Stato" di tutte le connessioni attive. Se il router NAT si riavvia e perde la tabella, tutte le connessioni di tutti i PC crollano.
- **Ci incatena a TCP e UDP:** Poiché il NAT per funzionare _ha bisogno_ di leggere il campo "Porta", se un domani inventassimo un protocollo di trasporto migliore del TCP che non usa il concetto di "porte", il NAT non saprebbe come gestirlo e bloccherebbe tutto il traffico.
- **Rompe alcune applicazioni (es. FTP):** Alcuni vecchi protocolli come l'FTP sono soliti scrivere il proprio indirizzo IP all'interno del "carico utile" (nei dati) del pacchetto. Il NAT cambia l'indirizzo sull'intestazione (sulla busta), ma non sa che dentro la lettera c'è scritto il vecchio indirizzo privato! Risultato: la comunicazione fallisce.
    
In sintesi: il NAT è un "trucco sporco" che viola i principi fondamentali delle reti, ma è stato un male assolutamente necessario per impedire che Internet collassasse esaurendo gli indirizzi IPv4 negli anni '90.

### IPV6

**Il formato dell'Indirizzo IPv6 e la Compressione**
Gli indirizzi IPv6 passano da 32 a **128 bit**. Questo significa un numero di IP disponibili talmente vasto da poter assegnare un IP a ogni granello di sabbia sulla Terra. Essendo troppo lunghi (16 byte), non si usa più la notazione decimale, ma quella **esadecimale**, dividendo i numeri in 8 gruppi separati da due punti (`:`).

Per evitare di scrivere indirizzi lunghissimi pieni di zeri, esistono due regole di **compressione/ottimizzazione**:

1. **Omissione degli zeri iniziali:** In ogni gruppo, gli zeri a sinistra si possono togliere (es. `0123` diventa `123`, `0000` diventa `0`).
    
2. **Compressione dei blocchi nulli (`::`):** Una sequenza contigua di blocchi fatti solo di zeri può essere sostituita dal simbolo `::`. **Regola d'oro:** questa sostituzione può essere fatta _una sola volta_ all'interno di un indirizzo, altrimenti il router non saprebbe quanti zeri ripristinare per tornare a 128 bit!
    

_Nota sugli indirizzi "ibridi":_ Per facilitare la transizione, un vecchio indirizzo IPv4 può essere "mascherato" dentro un IPv6 mettendo tutti zeri iniziali e l'IP in fondo (es. `::192.167.148.11`).

***Intestazione (header) ipv6***
La vera rivoluzione dell'IPv6 non è solo la dimensione, ma **l'efficienza**. L'intestazione IPv6 è stata "ripulita" rispetto a quella caotica dell'IPv4. Passa da 13 campi a **soli 7 campi**, e ha una dimensione fissa di **40 byte**. Questo permette ai router centrali di processare i pacchetti a velocità inaudite.

![[Pasted image 20260610141847.png]]
Ecco i 7 campi dell'Header Base:

- **Version (4 bit):** Contiene il numero 6.
- **Traffic Class (8 bit):** L'equivalente del "Type of Service" in IPv4. Serve per la QoS (Quality of Service) per dare priorità a traffico come voce o video.
- **Flow Label (20 bit):** _Novità assoluta._ Serve a identificare un "flusso" specifico di pacchetti (es. uno streaming video). Permette ai router di applicare le stesse regole di instradamento a tutto il flusso senza dover ri-analizzare ogni singolo pacchetto. Crea una sorta di "corsia preferenziale" (pseudo-connessione).
- **Payload Length (16 bit):** A differenza dell'IPv4 (che indicava la lunghezza _totale_), qui si indica solo la dimensione dei dati utili (il payload) _esclusa_ l'intestazione fissa di 40 byte.
- **Next Header (8 bit):** Sostituisce il campo "Protocol" dell'IPv4. Dice al router cosa viene dopo: potrebbe essere l'intestazione TCP/UDP, oppure una delle nuove "Intestazioni Estese".
- **Hop Limit (8 bit):** Sostituisce il "TTL" (Time to Live) dell'IPv4. Il funzionamento è identico (viene decrementato a ogni router e se arriva a 0 il pacchetto muore), ma il nome è finalmente corretto: conta i "salti", non i secondi.
- **Source & Destination Address (128 bit ciascuno).**


***Intestazioni ipv6 ESTESE***
I campi mancanti di IPv4 sono ancora salutariamente necessari. Per introdurli nell'IPv6 si introduce il concetto di *intestazione estesa*.

L'header base a 40 byte c'è sempre. Se servono funzioni extra, si aggiungono "a catena" tra l'header base e i dati veri e propri. Ecco le principali:

![[Pasted image 20260610142054.png]]

- **Hop-by-hop options:** L'unica estensione che **deve** essere letta da _tutti_ i router attraversati. Viene usata ad esempio per i _Jumbogrammi_ (pacchetti giganti che superano i 65.536 byte, utili per i supercomputer).
    ![[Pasted image 20260610142119.png]]
- **Destination options:** Lette solo dal destinatario finale, i router in mezzo le ignorano.
    
- **Routing:** Simile al _Loose Source Routing_ dell'IPv4. Il mittente impone un elenco di router che il pacchetto deve obbligatoriamente visitare lungo il tragitto.
    ![[Pasted image 20260610142134.png]]
- **Autenticazione & Carico Utile Cifrato (ESP):** L'IPv6 integra in modo nativo i protocolli di sicurezza IPsec per garantire che il pacchetto non sia stato contraffatto e che i dati siano illeggibili a chi cerca di intercettarli.
    
- **Frammentazione:**  **DIFFERENZA CON IPV4 **
    
    - In IPv4, se un pacchetto è troppo grande, _il router in mezzo alla rete_ perde tempo a spezzettarlo.
        
    - **In IPv6, i router non frammentano mai.** Se un router riceve un pacchetto troppo grande per la sua linea, lo scarta immediatamente e manda un messaggio di errore ICMP al mittente ("Packet Too Big").
        
    - Sarà il **mittente originario (l'host)** a dover spezzettare i dati inserendo questa intestazione estesa di frammentazione. Questa regola ha alleggerito immensamente il carico di lavoro dei router globali.


## Protocolli di controllo Internet

La rete internet è complessa e sempre più grande, per tenerla sotto controllo abbiamo bisogno di **protocolli di controllo** con diverse funzioni:
- **ICMP**: è una suite di protcolli che verificano la correttezza interna della rete;
- **ARP e RARP**: risolvolo la corrispondenza tra scheda di livello 2 e indirizzi IP (collega MAC e IP)
- **Bootstrap** (BOOTP): Protocollo utilizzato per avviare un host alla rete. Successivamente sostituito da DHCP.
- **DHCP** (Dynamic Host Configuration Protocol): permette l'assegnazione manuale o dinamica di indirizzi IP a indirizzi ethernet.


### ICMP

Protocollo di controllo di messaggio che consente di avere diverse informazioni.
E' incapsulato nel pacchetto IP. Le informazioni riguardano:
- **Destination unreachable**: Viene inviato al mittente del messaggio avvisandolo di una nota irraggiungibilità del destinatario.
- **Time exceeded**: Viene inviato al mittente del pacchetto quando il contatore *TimeToLive* raggiunge lo 0.
- **Redirect**: Viene utilizzato da un router quando pensa di aver ricevuto un pacchetto formulato in modo errato. Invita l'host trasmittente ad aggiornare la sua tabella di routing.
- **Echo request, reply**: E' un meccanismo utilizzato per capire se una certa destinazione è raggiungibile. Si invia un messaggio ECHO e chi lo riceve deve rispondere con ECHO REPLY.
- **Timestamp request, reply**: come l'echo ma annota anche il timestamp di arrivo dei messaggi per misurare le prestazioni della rete.
- **Router Advertisement, solicitation**: Usati dagli host per trovare router vicini.

### ARP

In che modo gli indirizzi IP vengono associati agli indirizzi del livello data link?

**Indirizzi Logici != Indirizzi Fisici**
- **Il Livello di Rete (IP):** Parla usando indirizzi IP logici (es. `192.32.65.7`). Sono come i nomi e cognomi delle persone: servono per trovare qualcuno nel mondo, ma non dicono nulla sull'hardware fisico.
- **Il Livello Data Link (Ethernet):** Parla usando **Indirizzi MAC (o indirizzi Ethernet)** fisici (nella slide indicati per semplicità come `E1`, `E2`, ecc.). Sono indirizzi cablati fisicamente nella scheda di rete dal produttore.

Il problema sorge quando un computer deve inviare fisicamente un segnale sul cavo: **la scheda di rete non capisce gli indirizzi IP**. Capisce solo gli indirizzi MAC. Quindi, come fa un computer a sapere a quale scheda di rete fisica mandare i dati se conosce solo l'indirizzo IP del destinatario?

L'ARP è il protocollo che risolve questo problema. La sua unica funzione è rispondere a questa domanda: _"Conosco l'indirizzo IP X. Qual è l'indirizzo fisico (MAC) della scheda di rete associata a quell'IP?"_


Esempio riguardante la rete di una università con subnet mask /24:
![[Pasted image 20260610143954.png]]

Le reti *CS* e *EE* sono delle Ethernet commutate, quindi sono collegati ad uno switch ethernet. Queste sono connesse tra loro attraverso un router IP.
Gli indirizzi ethernet sono segnati come E1, E2, ...

L'Host 1 vuole inviare un messaggio all'Host 2, che si trova **sulla sua stessa rete locale (Rete CS)**:
1. **Verifica locale:** L'Host 1 guarda l'IP di destinazione (`192.32.65.5`), applica la sua Subnet Mask (`/24`) e capisce: _"Questo computer è sulla mia stessa rete, posso parlargli direttamente"_.
2. **L'Urlo (ARP Request):** L'Host 1 crea un pacchetto ARP speciale e lo invia in **Broadcast** su tutta la rete locale. È come se si affacciasse alla finestra e urlasse: _"Ehi a tutti! Chi di voi ha l'indirizzo IP 192.32.65.5? Per favore, mi dica qual è il suo indirizzo MAC!"_
3. **Il Silenzio e la Risposta:** Tutte le macchine sulla rete (incluso il router) ricevono l'urlo. Tutti tranne l'Host 2 guardano l'IP, vedono che non è il loro e scartano il pacchetto in silenzio. L'Host 2, invece, si riconosce e invia una **ARP Reply** (questa volta in formato Unicast, direttamente all'Host 1): _"Sono io! Il mio indirizzo Ethernet è E2"_.
4. **L'Incapsulamento e l'Invio:** Ora l'Host 1 ha tutto. Prende il suo pacchetto IP, lo "imbusta" dentro un _Frame Ethernet_, scrive `E2` come indirizzo di destinazione fisico e lo spedisce sul cavo. Lo switch leggerà `E2` e consegnerà il pacchetto fisicamente all'Host 2.

L'Host 1 vuole inviare un messaggio all'Host 4 che si trova su **un altra rete**:
- L'Host 1 guarda l'IP di Host 4 (`192.32.63.8`), usa la Subnet Mask e capisce: _"Non è sulla mia rete. Devo mandare questo pacchetto al mio Gateway (il Router E3)"_.
- L'Host 1 **NON** fa un ARP per l'Host 4 (l'urlo broadcast non supererebbe il router). L'Host 1 fa un ARP per chiedere **l'indirizzo MAC del Router**.
- Il Router risponde: _"Il mio MAC per questa interfaccia è E3"_.
- L'Host 1 crea il pacchetto. _Attenzione alle due intestazioni:_
    - **Intestazione IP (Il viaggio logico totale):** Sorgente: `IP1`, Destinazione: `IP4`.
    - **Intestazione Ethernet (Il salto fisico immediato):** Sorgente: `E1`, Destinazione: `E3` (Il Router).
- Il Router riceve il pacchetto, straccia la vecchia busta Ethernet e guarda l'IP. Capisce che deve mandarlo sulla Rete EE.
- Ora è il Router (tramite l'interfaccia E4) a fare una richiesta ARP sulla Rete EE chiedendo: _"Chi ha l'IP4?"_.
- L'Host 4 risponde con il MAC `E6`.
- Il Router crea una _nuova_ busta Ethernet (Sorgente `E4`, Destinazione `E6`) e recapita finalmente il pacchetto all'Host 4.

Altro esempio:
![[Pasted image 20260610145951.png]]


TODO: spiegazione esempio 


### RARP (Reverse Address Resolution Protocol)

RARP fa il processo inverso di ARP: dato un indirizzo ethernet restituisce il corrispondente indirizzo IP.
E' necessario un server RARP su ogni rete, dato che utilizza messaggi broadcast che non escono dalla rete stessa.

### Boot Prococol (BOOTP)

Utilizzato per risolvere i problemi dil RARP. A differenza di RARP, BOOTP utilizza messaggi UDP, spesso inoltrati attraverso i router, può quindi 'saltare' ad un altra rete locale.

Il problema  è che richiede una configurazione manuale delle tabelleche associano indirizi IP a indirizzi Ethernet. In pratica quando un utente si aggiunge alla LAN, BOOTP non lo conosce finchè non viene compilata la lista a mano (p.e. dall'amministratore).

### DHCP (Dynamic Host Control Protocol)

I protocolli come ARP suppongono che esista una configurazione che associa gli indirizzi IP a indirizzi ethernet.

Il DHCP si occupa di creare questa associazione. E' possibile farla in modo manuale o automatico.

![[Pasted image 20260610151215.png]]

Una volta acceso e collegato alla rete, un PC manda in broadcast un messaggio per richiedere il suo Indirizzo IP all'interno della rete. A rispondere sarà il server DHCP che gli fornirà un indirizzo IP privato.
Solitamente il DHCP affitta l'indirizzo per un tempo limitato.

Dato che i PC utilizzano messaggi broadcast (che non escono dal router) per cercare il DHCP, sorge un problema, in quanto il server DHCP potrebbe non essere nello stesso router. Per risolvere questo problema, e quindi utilizzare lo stesso server su reti distanti, si utilizza un agente di inoltre DHCP detto **DHCP Relay** il quale invierà il messaggio broadcast incapsulato alla rete distante.


## Protocolli Interni alle reti (IGP)
Con **Interior Gateway Protocol (IGP)** si intendono i protocolli di routing utilizzati all'interno di una rete autonoma.
Una rete autonoma (Autonomous System) è una porzione della rete amministrata da un unica entità (organizzazione, provider di servizi, etc.).

![[Pasted image 20260611121358.png]]

Gli IGP sono progettati per consentire il routing delle informazioni all'interno della rete.

Alcuni protocolli IGP:
- Routing Information Protocol (RIP)
- Open Shortest Path First (OSPF)
- Intermediate System to Intermediate System (IS-IS)

### Open Shortest Path First (OSPF)

Rappresenta la rete reale come un grafo ed elabora il percorso più breve da ogni router ad ogni altro router tramite un algoritmo di link state.
Se sono possibili più percorsi della stessa lunghezza, ricorda l'intero insieme dei percorsi più brevi e durante l'inoltro il traffico viene suddiviso tra espansione..

![[Pasted image 20260611121435.png]]
## Protocolli Esterni alle reti (EGP)

Il BGP è un **EGP (Exterior Gateway Protocol)** e serve a far parlare tra loro reti di aziende diverse, chiamate **AS (Autonomous System)**. A questo livello, **la velocità passa in secondo piano rispetto ai contratti commerciali**. Un router BGP non sceglie la strada più breve, ma sceglie la strada che _rispetta gli accordi economici_ presi dalla sua azienda con le altre aziende.

**Come comunicano economicamente gli AS tra loro?** Ci sono due modelli fondamentali:
- **Servizio di Transito (Il modello Cliente-Fornitore):** Un AS piccolo (es. la rete di un'università) paga un AS grande (il Provider, es. Telecom) per avere accesso a _tutta_ Internet.
    
    - _Regola:_ Il provider annuncia al cliente tutte le rotte del mondo. Il cliente annuncia al provider solo le proprie rotte interne (perché non vuole e non può fare da passacarte per il traffico di altri).
        
- **Peering (Il modello tra Pari):** Due AS (es. Netflix e Telecom) si scambiano tantissimo traffico. Invece di far passare questo traffico dai rispettivi provider (pagando il transito a caro prezzo), tirano un cavo diretto tra i loro router (spesso incontrandosi fisicamente in un **IXP - Internet Exchange Point**).
    
    - _Regola:_ Il traffico sul link di peering scambiato tra i due è **gratuito**.
        
    - **Il Peering non è transitivo:** Se l'AS2 fa peering con l'AS3, e l'AS3 è connesso ad AS4... l'AS2 **NON PUÒ** usare il link gratuito verso l'AS3 per raggiungere l'AS4! L'AS3 rifiuterà il traffico, dicendo: _"Facciamo peering gratis per i nostri dati, ma non faccio da provider gratuito per farti andare su Internet!"_
    
![[Pasted image 20260611122524.png]]

_"La diffusione del routing viaggia in direzione opposta ai pacchetti"_:
- Se l'AS4 vuole _ricevere_ traffico, deve "gridare" la sua esistenza verso sinistra (all'AS1, che lo dice all'AS2, ecc.).
    
- I pacchetti di dati veri e propri, poi, seguiranno le briciole di pane lasciate da quell'annuncio viaggiando da sinistra verso destra.

![[Pasted image 20260611122450.png]]

##### *Path vector*:
Il BGP viene definito una variante del Distance Vector, chiamata più precisamente **Path Vector Protocol (Protocollo a Vettore di Percorso)**.

- **La differenza:** Un protocollo distance vector normale dice solo "La rete X dista 3 salti". Il BGP invece si porta dietro un "diario di viaggio" completo, chiamato **AS-PATH**, che elenca esattamente nome e cognome di tutti gli AS attraversati (es. `AS1, AS2, AS3`).
- **Perché lo fa? (Prevenzione dei Loop):** Questo è cruciale! Registrando ogni singolo AS, si evitano i cicli infiniti. Se un router riceve un annuncio BGP e, leggendo l'AS-PATH, vede che il _proprio_ numero di AS è già presente nella lista, capisce che quell'annuncio ha fatto un giro a vuoto ed è tornato indietro. A quel punto, semplicemente, lo scarta.
- **Affidabilità:** Poiché le tabelle BGP del mondo intero pesano centinaia di megabyte, non vengono inviate a caso in broadcast. I router BGP stabiliscono delle connessioni **TCP** dirette tra loro per scambiarsi gli aggiornamenti in modo sicuro e affidabile.
## Internet multicasting

A differenza delle Classi A, B e C, gli indirizzi di Classe D **non hanno una maschera di sottorete (Subnet Mask)** e non sono divisi in "Rete" e "Host". I primi 4 bit sono sempre bloccati a `1110` (il che fa iniziare questi indirizzi da `224.0.0.0`), e i restanti **28 bit formano un "Group ID" (Identificativo di Gruppo)**.

- **`224.0.0.1` (All Systems):** Indirizza _tutti gli host_ (computer, stampanti, ecc.) presenti sulla rete locale.
- **`224.0.0.2` (All Routers):** Indirizza _solo i router_ presenti sulla rete locale.
- **`224.0.0.5` e `224.0.0.6` (OSPF):** Usati dal protocollo di routing OSPF. I router li usano per scambiarsi aggiornamenti sulle mappe di rete senza disturbare i computer degli utenti.
- **`224.0.0.251` (mDNS):** È il Multicast DNS. È quello che permette al tuo Mac o al tuo iPhone di trovare magicamente una stampante Wi-Fi o una Apple TV sulla rete domestica senza bisogno di configurazioni (tecnologia Bonjour/ZeroConf).

L’**IGMP** (Internet Group Management Protocol) è un protocollo legato al multi-casting che permette di eseguire ulteriori controlli interni. Il multi-casting usa algoritmi Spanning tree con protocollo **PIM** (Protocol Indipendent Multicast).

# Livello di trasporto 

