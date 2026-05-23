
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