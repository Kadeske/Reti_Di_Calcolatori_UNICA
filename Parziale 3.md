
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

(immagine con 2 schemi) e spiegazione 

Il suo scopo è **prenotare in anticipo le risorse di rete** lungo tutto il percorso tra sorgente e destinazione.

- **Come funziona (l'esempio dei nodi):** Immagina una rete in cui l'Host 1 sta già comunicando con l'Host 4 occupando molta banda sul percorso (es. passando per i nodi A-E-H-J). Se l'Host 3 volesse iniziare a comunicare con l'Host 4, potrebbe trovare il percorso congestionato, subendo rallentamenti o perdite di pacchetti.
    
- **La soluzione di RSVP:** Prima di iniziare a inviare i dati veri e propri, l'Host 3 invia un messaggio RSVP di "prenotazione". I router lungo il percorso verificano se hanno abbastanza risorse libere. Se la risposta è sì, allocano (mettono da parte) una porzione di banda dedicata esclusivamente a quella comunicazione. In questo modo si ottimizza l'uso della rete e si prevengono le congestioni.

### protocollo MPLS

Un'altra metodologia estremamente efficiente per gestire il traffico e le risorse di rete è il **Label Switching** (commutazione di etichette), il cui standard di riferimento creato dall'IETF è l'**MPLS**.

Invece di far decidere ai router l'instradamento analizzando ogni volta il lungo indirizzo IP di destinazione, l'MPLS **aggiunge una breve etichetta (label)** al pacchetto. I router (chiamati LSR - Label Switching Routers) inoltrano il traffico basandosi unicamente sulla lettura di questa etichetta, rendendo l'operazione molto più rapida ed efficiente.

**Collocazione nella pila ISO/OSI** L'intestazione (header) MPLS viene inserita tra l'header di Livello 2 (Collegamento Dati, es. Ethernet) e l'header di Livello 3 (Rete, es. IP). Per questo motivo, l'MPLS viene spesso definito un protocollo di **Livello 2.5**. Questa flessibilità è una delle ragioni del suo enorme successo nelle reti moderne.

(img intestazione)
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

(img infrastruttura)

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


### Intestazione IPv4

(img intestazione ipv4)

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

