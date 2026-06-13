
# Livello di rete 

Il livello di rete ha il compito fondamentale di trasferire i pacchetti, provenienti dal livello di trasporto, partendo dalla sorgente fino alla destinazione finale. Questo trasferimento avviene attraversando molteplici sistemi intermedi, che tipicamente sono i router, all'interno della sottorete di comunicazione.

Per portare a termine la sua responsabilità, il livello di rete deve assolvere a quattro compiti principali:
- Conoscere la topologia della sottorete di comunicazione.
- Scegliere di volta in volta il cammino migliore per i pacchetti, un'operazione nota come **routing**.
- Gestire il flusso dei dati e le eventuali congestioni (tramite _flow control_ e _congestion control_).
- Gestire le problematiche derivanti dalla presenza di reti diverse tra loro, ovvero l'**internetworking**.

Quando si progetta e si realizza il livello di rete di un'architettura, le decisioni ingegneristiche si basano essenzialmente su due parametri:
- I servizi che si intende offrire al livello superiore.
- L'organizzazione interna della sottorete di comunicazione.

##### Servizi offerti: Con e Senza Connessione
Le decisioni progettuali si traducono nella scelta di offrire un servizio affidabile orientato alla connessione, oppure un servizio non affidabile senza connessione.

**Servizi orientati alla connessione (Connection oriented)** Questo tipo di servizio è strutturato in tre fasi distinte: l'instaurazione della connessione, la trasmissione delle informazioni e infine il rilascio della connessione. Per poter creare questo servizio devono verificarsi precise condizioni:

- Le entità paritetiche (peer entities) stabiliscono una connessione negoziando i parametri, alla quale viene associato un identificatore univoco.
- Questo identificatore viene inserito in ogni singolo pacchetto inviato.
- La comunicazione è bidirezionale e i pacchetti viaggiano rigorosamente in sequenza lungo il cammino assegnato.
- Il controllo di flusso viene fornito in modo automatico dall'infrastruttura.
    

**Servizi non orientati alla connessione (Connectionless)** Questo servizio è molto più snello ed è inteso come un'operazione che si esaurisce in un'unica fase. Presenta condizioni operative completamente diverse:

- La sottorete è considerata inaffidabile alla base; per questo motivo, sono gli host stessi a dover provvedere per conto proprio alla correzione degli errori e al controllo del flusso.
- I pacchetti (che in questo contesto specifico prendono il nome di **datagram**) vengono inoltrati nella sottorete in maniera totalmente indipendente l'uno dall'altro.
- Poiché viaggiano in modo indipendente, ogni pacchetto deve contenere obbligatoriamente l'indirizzo di destinazione.
- Tutta la complessità viene demandata ai vari host periferici: saranno i loro livelli di trasporto a dover fornire la necessaria affidabilità e l'orientamento alla connessione se richiesto dall'applicazione.
## Principi di commutazione 

La **commutazione** è il processo fondamentale che permette di trasferire i dati da un computer sorgente (host di origine) a uno di destinazione.

La caratteristica chiave di questo processo è la sua **dinamicità**: le destinazioni non sono fisse o pre-cablate, ma variano di volta in volta per adattarsi alle specifiche esigenze del servizio richiesto in quel momento.

Dal punto di vista pratico, questo smistamento delle informazioni viene eseguito materialmente da dispositivi hardware dedicati, i quali sono strategicamente posizionati nei **nodi** (i punti di incrocio) della rete.

Quando si progetta una sottorete, la scelta di come implementare questa commutazione si restringe essenzialmente a tre tecniche principali, una scelta cruciale perché influenza direttamente la **Qualità del Servizio (QoS)**:

- **Commutazione di circuito**
- **Commutazione di messaggio**
- **Commutazione di pacchetto**

### Commutazione di circuito

È una tecnica rigorosamente orientata alla connessione (connection-oriented) e il suo intero ciclo di vita si articola in tre fasi obbligatorie: l'instaurazione (call setup), il trasferimento dei dati veri e propri e, infine, il rilascio della connessione (call clear-down).
![[Pasted image 20260612142334.png]]

**La fase di instaurazione e l'ostacolo del ritardo** Tutto inizia quando l'host chiamante invia alla sottorete le informazioni necessarie per individuare il destinatario. Affinché la comunicazione possa iniziare, il segnale di richiesta deve fisicamente attraversare i vari nodi intermedi della rete, ovvero i **router instradatori**.

Questo percorso iniziale non è istantaneo, ma genera un **ritardo di instaurazione** (call set-up delay). Come mostra il grafico temporale degli appunti, questo ritardo è la somma di due fattori fisici:

- Il tempo materiale di trasmissione delle informazioni di segnalazione lungo i cavi.
    
- I tempi di elaborazione interni dei router: un nodo intermedio non inoltra il segnale immediatamente, ma deve prima svolgere dei calcoli per selezionare il percorso corretto. Inoltre, il nodo finale a ridosso del destinatario richiede ancora più tempo, poiché deve confermare che l'intero percorso di trasmissione è valido e pronto.
    

**Il trasferimento dati e il limite del costo** Se la fase di instaurazione va a buon fine, la rete "blocca" quegli specifici router e cavi appena interpellati. In sostanza, viene resa disponibile una **connessione fisica dedicata** in via esclusiva per quei due host.

È qui che emerge il principale limite di questo sistema: impegna totalmente le risorse di rete lungo tutto il percorso per quel singolo collegamento. Questo vincolo rimane attivo per tutta la durata della chiamata, **anche nei momenti in cui i due host non si stanno scambiando alcun dato** (ad esempio, durante una pausa in una conversazione telefonica). Questo enorme spreco di risorse bloccate e inutilizzate rende il sistema della commutazione di circuito costosissimo da mantenere.

### Commutazione di messaggio 

In questo modello, non si crea più un "tubo" vuoto dedicato tra i due computer; si dà invece importanza prioritaria al messaggio stesso, che deve viaggiare in modo autonomo. Così facendo, un cavo di rete viene occupato e reso disponibile esclusivamente per il tempo strettamente necessario al passaggio dei dati. Scompare del tutto la fase iniziale di instaurazione del canale (sia fisico che logico), rendendo questa comunicazione orgogliosamente "senza connessione" (connectionless).

**La meccanica dello "Store and Forward"** Il cuore di questa tecnologia è il meccanismo di memorizzazione e inoltro, tecnicamente noto come **store and forward**.
Affinché funzioni, ogni nodo intermedio della rete (i router) viene equipaggiato con una propria memoria di massa (come un disco rigido). Quando il messaggio — che è un blocco dati molto ampio contenente sia le informazioni che un'intestazione — raggiunge un nodo, viene prima di tutto immagazzinato per intero al suo interno. Il nodo esamina l'intestazione, usa le sue strategie di instradamento per decidere la direzione migliore e controlla lo stato del segmento di linea successivo. Se quel canale è libero, inoltra il messaggio; se invece il canale è occupato da altre comunicazioni, il messaggio viene semplicemente messo in coda e attende il suo turno fermo nella memoria. Per garantire la sicurezza, il nodo cancella la sua copia locale del messaggio solo dopo aver ricevuto una conferma di corretta ricezione dal nodo successivo.
![[Pasted image 20260612142957.png]]

**Il prezzo da pagare: la latenza** Il grande vantaggio di questa tecnica è l'efficienza: la singola linea viene occupata solo per il tempo di trasferimento della porzione di dati, ottimizzando le risorse di rete.

![[Pasted image 20260612143125.png]]

Tuttavia, il difetto fatale risiede nel **ritardo di trasferimento**. Poiché ogni singolo nodo lungo il percorso deve ricevere, salvare su disco ed elaborare l'intero messaggio prima di farlo ripartire, il ritardo si accumula enormemente. Questo tempo dipende dalla lunghezza del messaggio, dalla velocità dei cavi e dai tempi di elaborazione dei nodi. A causa di questa latenza imprevedibile e dilatata, questo sistema **non può assolutamente supportare comunicazioni interattive** in tempo reale (come una telefonata o una videochiamata).

**L'evoluzione verso i pacchetti** Un'ulteriore criticità emerge quando i dati da spedire sono davvero immensi: far scaricare a ogni router un file gigantesco paralizza comunque il sistema, facendo crollare l'efficienza. Proprio per superare quest'ultimo ostacolo, si è capito che era molto meglio suddividere l'enorme messaggio in tanti frammenti più piccoli. Da questa intuizione nasce la **commutazione di pacchetto**, la tecnologia definitiva che permette di sfruttare i canali per mandare innumerevoli comunicazioni diverse contemporaneamente, ed è quella su cui si basa l'Internet di oggi.
Non c'è una connessione.


### Commutazione di pacchetto 

Informazione divisa in unità di lunghezza massima predefinita: pacchetti.

Queste reti possono funzionare in due modalità:
- datagramma;
- circuito virtuale

##### Datagramma 

È l'evoluzione diretta della commutazione di messaggio. L'informazione viene divisa in pacchetti chiamati datagrammi.
![[Pasted image 20260612143359.png]]

- **Indipendenza:** Ogni datagramma viaggia per conto proprio nella rete.
- **Intestazione necessaria:** Poiché viaggiano separati, ogni pacchetto deve avere un'intestazione con indirizzo di origine e destinazione.
- **Svantaggi:**
    
    - I pacchetti possono arrivare con un **ordine diverso** rispetto a quello di partenza; il destinatario deve riordinarli.
    - C'è un alto rischio di pacchetti persi o duplicati.
    - Si trasmette un **numero maggiore di informazioni** totali a causa delle ripetute intestazioni.

##### circuito virtuale

Per risolvere i problemi di disordine e perdita del datagramma, si usa il circuito virtuale.
![[Pasted image 20260612143533.png]]
- **Percorso fisso:** Tutti i pacchetti della stessa comunicazione seguono l'esatto stesso percorso logico. Questo percorso può differire per le due direzioni di trasferimento.
    
- **Vantaggio:** Garantisce la sequenzialità delle informazioni e l'integrità del messaggio.
    
- **Fasi operative:** Come la commutazione di circuito classica, è connection-oriented. Richiede tre fasi: instaurazione, trasferimento e rilascio.
    
- **Svantaggio:** L'uso continuo dello stesso circuito può portare al degrado delle prestazioni del percorso scelto, causando rallentamenti nell'attraversamento.

### Algoritmi di routing
Gli algoritmi di routing sono i protocolli responsabili di decidere il percorso migliore che un pacchetto deve seguire all'interno della rete per giungere a destinazione.

##### Statici vs Dinamici (Adattivi)
Gli algoritmi si dividono in due grandi categorie:
- **Statici:** Le decisioni di routing vengono prese a tavolino prima dell'avvio della rete. Sono adatti a reti piccole, permettendo al gestore un controllo totale.
- **Dinamici:** Le decisioni vengono costantemente riformulate in base a vari fattori. Sono indispensabili nelle reti di grandi dimensioni per la loro alta tolleranza agli errori.

**Differenze tra algoritmi dinamici** Gli algoritmi dinamici differiscono tra loro per tre aspetti chiave:
1. _Come ricevono le informazioni_ (solo dai router adiacenti, da tutti i router, ecc.).
2. _Quanto spesso rivedono le decisioni_ (a intervalli fissi, al variare del carico, al cambio della topologia).
3. _Quale metrica di valutazione adottano_ (es. distanza, salti, tempo stimato).

##### Algoritmo in base al tipo di sottorete

L'applicazione dell'algoritmo cambia drasticamente a seconda dell'architettura sottostante:
- **Sottorete Datagram:** L'algoritmo calcola un nuovo percorso per ogni singolo pacchetto (o piccola serie) in transito.
- **Sottorete a Circuiti Virtuali:** L'algoritmo viene eseguito una sola volta, esclusivamente durante la fase iniziale di creazione del circuito. Questo specifico caso prende il nome di **session routing**.

##### Cosa ci si aspetta da un algoritmo di routing (I 6 requisiti)

Un buon algoritmo deve garantire sei caratteristiche fondamentali:

1. **Correttezza:** Deve inoltrare il pacchetto alla destinazione giusta.
2. **Semplicità:** L'implementazione software non deve essere eccessivamente complicata.
3. **Robustezza:** Deve continuare a funzionare anche se cadono le linee o si bloccano dei router.
4. **Stabilità:** Deve convergere rapidamente verso una soluzione stabile.
5. **Equità:** Non deve favorire o privilegiare l'inoltro di pacchetti specifici a discapito di altri.
6. **Ottimalità:** Deve sempre scegliere la soluzione che risulti globalmente la migliore per l'intera rete.
##### Metrica

La metrica è lo strumento matematico utilizzato per misurare come si sta utilizzando la rete. Può basarsi su vari parametri, come il numero di pacchetti in coda, la capacità bidirezionale, il ritardo, o il numero di salti (hop) tra i nodi. Di regola, l'algoritmo seleziona sempre il percorso associato alla **metrica inferiore** (il "costo" minore). Alcuni protocolli avanzati riescono a combinare differenti metriche per calcolare un percorso ancora più ottimizzato.

##### Il Principio di Ottimalità e il Sink Tree

Questo principio stabilisce una regola logica fondamentale: se un router J si trova sul cammino ottimale per andare dal router I al router K, allora anche il cammino da J a K si troverà sulla stessa identica strada.
![[Pasted image 20260612143930.png]]
La logica è ferrea: se esistesse una strada migliore tra J e K, l'algoritmo l'avrebbe già scelta, modificando di conseguenza anche il percorso originale tra I e K. La conseguenza visiva e strutturale di questo principio è che l'insieme di tutti i cammini ottimali provenienti da ogni router verso una specifica destinazione assume sempre la forma di un albero senza cicli chiusi, chiamato **sink tree**.

![[Pasted image 20260612143946.png]]

##### Load Balancing (Bilanciamento del Carico)

È la capacità vitale di distribuire il traffico su percorsi differenti ma diretti verso la stessa destinazione. Serve ad aumentare l'efficienza e permette il re-instradamento automatico se un percorso fallisce. Le modalità principali sono due:

- **Equal-cost:** Distribuisce il traffico equamente solo su percorsi che hanno la stessa identica metrica (lo stesso "costo").
- **Unequal-cost:** Sfrutta anche percorsi con metriche peggiori. Il traffico viene diviso in maniera inversamente proporzionale: il percorso con il costo minore riceve più traffico, quello con il costo maggiore ne riceve meno.
##### Convergenza e Tempo di Consistenza

Nelle reti dinamiche, quando un cavo si rompe o si aggiunge un nuovo router (modifica della topologia), i router devono scambiarsi informazioni per aggiornare le loro mappe.

- La **convergenza** è proprio questo processo attraverso il quale tutte le tabelle di routing dei vari nodi vengono aggiornate fino a raggiungere un nuovo stato di "consistenza" globale (tutti hanno la stessa visione corretta della rete).
    
- Il **tempo di consistenza** è il tempo fisico necessario affinché questo aggiornamento sia completato su tutti i nodi. Ovviamente, ha senso parlare di convergenza solo riferendosi agli algoritmi dinamici.

### Principali Algoritmi di Routing Statici
sono 3: 
- Shortest Path Routing
- Flooding
- Flow-based Routing

#### Shortest Path Routing 

In questo modello, a ogni linea di collegamento della rete viene assegnato un **peso** (una metrica, tipicamente basata sulla velocità o sulla larghezza di banda). L'obiettivo è instradare i pacchetti lungo il percorso in cui la somma di questi pesi sia la minore possibile. Se si vuole scoraggiare il passaggio su una linea, le si assegna un peso molto alto; viceversa per favorirlo.

L'algoritmo calcola la rotta ottimale costruendo una mappa di **interdistanze** partendo da zero:
1. **Inizializzazione:** Al nodo di partenza si assegna un peso pari a zero. A tutti gli altri nodi della rete si assegna provvisoriamente un peso infinito.
2. **Selezione:** Si parte dal nodo con il peso più basso (all'inizio è la sorgente) e si osservano tutti i suoi vicini diretti.
3. **Calcolo:** Per ogni vicino, si somma il peso del nodo corrente al peso del collegamento per raggiungerlo.
4. **Aggiornamento (La regola d'oro):** Se il costo appena calcolato è _inferiore_ al costo attualmente registrato su quel vicino, si aggiorna l'etichetta del vicino inserendo il nuovo costo minore e il nodo di provenienza.
5. **Iterazione:** Si ripete il ciclo esplorando tutti i nodi finché l'intera rete non è stata esaminata. Il risultato finale è una tabella statica con i percorsi più brevi verso ogni destinazione.

![[Pasted image 20260612144151.png]]
Guardando la sequenza dei grafi, l'aspetto più importante da notare è come l'algoritmo "cambia idea" quando trova una strada migliore:
- Partendo da **A**, l'algoritmo vede che il costo diretto per raggiungere **G** è **6**. L'etichetta provvisoria di G diventa `(6, A)`.
- Successivamente, l'algoritmo esplora il percorso passando per la parte superiore della rete: va da **A a B** (costo 2), poi da **B a E** (costo 2). Arrivati in E, il costo cumulato è 4.
- Da **E**, c'è un collegamento verso **G** che costa solo 1.
- L'algoritmo fa la somma: 4+1=5. Poiché il costo **5** del percorso `A-B-E-G` è strettamente inferiore al costo **6** del percorso diretto `A-G`, il sistema aggiorna l'etichetta di G in `(5, E)`. Il percorso fisicamente più lungo si rivela essere quello "meno costoso".
#### Flooding

Il _flooding_ è una tecnica di instradamento in cui ogni pacchetto in arrivo viene duplicato e inoltrato su **tutte** le linee di uscita del router, eccetto quella da cui il pacchetto è provenuto.

Questa tecnica genera un numero enorme di pacchetti duplicati, saturando rapidamente la banda disponibile. Per questo motivo, è utilizzabile **solo in reti di dimensioni molto ridotte**.

Per evitare che il _flooding_ faccia collassare la rete, si possono adottare tre strategie correttive:
1. **Contatore di hop (TTL - Time To Live):** Ogni pacchetto contiene un contatore che viene decrementato a ogni salto (hop) tra i router. Quando il contatore raggiunge lo zero, il pacchetto viene scartato, evitando che giri all'infinito nella rete.
2. **Scarto alla seconda vista:** Ogni pacchetto riporta l'identificativo del router sorgente e un numero di sequenza unico. Ogni router mantiene traccia dei pacchetti visti: se un router riceve un pacchetto che ha già elaborato in precedenza, lo scarta immediatamente.
3. **Selective Flooding:** Il router non trasmette il pacchetto su _tutte_ le linee, ma solo su quelle che vanno orientativamente nella "giusta direzione" verso la destinazione. Questo richiede che i router mantengano apposite tabelle di instradamento a bordo.

#### Flow based routing

L'algoritmo stima il traffico atteso su ogni linea per prevederne il ritardo medio e basare su questi dati le scelte di instradamento.

Per applicare il metodo sono indispensabili:
- La **topologia** della rete.
- La **matrice delle quantità di traffico** T(i,j) stimate tra ogni coppia di router.
- Le **capacità** delle linee punto a punto.

**Assunzioni**:
1. Il traffico è **stabile** nel tempo e noto in anticipo.
2. Il ritardo su una linea aumenta con il traffico e diminuisce all'aumentare della velocità di linea (secondo la Teoria delle Code).


**Ritardo medio dell'intera rete**:
È espresso come una **somma pesata** dei ritardi delle singole linee. Il peso di ogni linea è calcolato così:
$$\text{ritardo singola linea}=\frac{\text{traffico sulla linea}}{\text{traffico totale della rete}}$$
(Come calcolare il ritardo medio dell'intera rete: somma pesata dei ritardi delle linee)

###### Metodo (basi su topologia nota)
Il sistema segue questi 6 passaggi:
1. Considera la matrice di traffico.
2. Determina i percorsi per ogni coppia di router.
3. Calcola il traffico incidente su ogni linea (somma di tutti i T(i,j) instradati su quella linea).
4. Calcola il ritardo di ogni singola linea.
5. Calcola il ritardo medio dell'intera rete.
6. Determina l'algoritmo di routing che minimizza tale ritardo medio.

### Principali algoritmi di routing dinamici 
Si adattano automaticamente alla rete.
Ne esistono principalmente 2:
- Distance Vector
- Link State Routing

#### Distance Vector

Ogni nodo della rete mantiene un **vettore dei ritardi**, ovvero una tabella che elenca, per ogni possibile destinazione:
- La distanza stimata (costo) per raggiungerla.
- La linea in uscita da utilizzare.

Per conoscere la distanza dai vicini immediati, il router invia speciali **pacchetti ECHO**. Misurando il tempo necessario affinché la risposta torni indietro, il router stima il tempo di raggiungibilità. Questa operazione è ripetuta più volte per ottenere un dato attendibile.

A intervalli regolari, ogni router invia la propria tabella a tutti i vicini. Ricevute le nuove informazioni, il router ricalcola la tabella scegliendo la concatenazione che minimizza la somma:
$$Distanza(Router stesso→Vicino)+Distanza(Vicino→Destinazione)$$

![[Pasted image 20260612145143.png]]

![[Pasted image 20260612145208.png]]


L'algoritmo è efficiente nel diffondere "buone notizie" (nuovi percorsi), ma è molto lento nel gestire le "brutte notizie" (guasti).

Si verifica il paradosso quando un nodo (es. A) smette di funzionare:
1. Il router B sa di non poter più raggiungere A direttamente.
2. Tuttavia, il router C (non ancora aggiornato) comunica a B: "Io posso raggiungere A in 2 passi".
3. B, basandosi su questa informazione, conclude: "Se C raggiunge A in 2 passi e io arrivo a C in 1, allora posso raggiungere A in 3 passi".
4. B aggiorna la sua tabella, poi C aggiornerà la sua basandosi su quella di B, incrementando ulteriormente il conteggio.

Questo ciclo continua indefinitamente (scambio all'infinito), poiché i nodi si scambiano informazioni obsolete senza rendersi conto che la destinazione non è più raggiungibile.
#### Link State Routing

In questo modello, invece di condividere l'intera tabella solo con i vicini, ogni router condivide lo stato dei suoi collegamenti diretti con _tutti_ gli altri nodi. In questo modo, ciascun router ricostruisce localmente la topologia completa della rete e calcola in autonomia il cammino minimo.

I protocolli moderni che sfruttano questa logica sono l'**OSPF** e l'**IS-IS**.


Il funzionamento si articola in cinque fasi precise:
1. **Scoperta dei vicini:** Il router invia pacchetti **HELLO** sulle linee in uscita per rilevare l'indirizzo dei nodi adiacenti.
2. **Misurazione del ritardo:** Invia pacchetti **ECHO** ai vicini, calcola il tempo di risposta e compila una _Neighbour Table_.
3. **Creazione del pacchetto (LSP):** Genera un **Link State Packet** che contiene: la propria identità, la lista dei vicini con i relativi ritardi, un **numero di sequenza** (per distinguere i pacchetti nuovi dai vecchi) e l'**Età** (un tempo di vita che scala fino a zero per evitare che i pacchetti vaghino all'infinito).
4. **Distribuzione (Flooding):** L'LSP viene inviato a tutti gli altri router della rete usando la tecnica del flooding, permettendo alla rete di convergere su tabelle coerenti.
5. **Calcolo del cammino minimo:** Con la topologia completa a disposizione, il router calcola le rotte migliori. Per gestire reti enormi senza creare tabelle infinite, l'algoritmo viene strutturato gerarchicamente (a livelli).

![[Pasted image 20260612220418.png]]

Per usare il flooding senza saturare la rete con pacchetti duplicati o infiniti, i router utilizzano una rigida struttura dati (un buffer) per gestire i pacchetti _non ancora elaborati_.
Ogni riga del buffer traccia l'Origine, la Sequenza, l'Età e usa dei bit di **Flag** per smistare il traffico:
- **Send Flags:** Indicano su quali linee il pacchetto deve essere inoltrato.

- **ACK Flags:** Indicano a quali nodi bisogna inviare la conferma di ricezione.
    
![[Pasted image 20260612220430.png]]
**Esempio pratico sul Router B (con vicini A, C, F):** Se il router B riceve un pacchetto proveniente da A, imposterà i Send Flag a 1 per le linee **C** e **F** (inoltrando il pacchetto al resto della rete) e imposterà l'ACK Flag a 1 per la linea **A** (inviando la conferma a chi glielo ha appena passato). Se lo stesso pacchetto dovesse arrivare da due strade diverse contemporaneamente, il router sa quali flag ha già soddisfatto ed evita invii superflui.

### Routing Gerarchico 

Per sottoreti molto grandi.

La rete viene divisa in regioni.

I router all'interno della stessa regione si conoscono.
Per comunicare con uno all'esterno, un router interno da da **router di confine**
Quindi si possono considerare due livelli di routing (interno e di confine/esterno)

![[Pasted image 20260612220449.png]]

![[Pasted image 20260612220459.png]]

### Broadcast Routing

4 metodologie per ottenere la trasmissione broadcast:
Invio pacchetti distinti : pro e contro 
flooding: pro e contro 
multidestination routing: lista di destinazioni, invio delle copie fino a raggiungere un solo destinatario
Il quarto utilizza il sink tree del routeer di trasmissioni e lo spanning tree per inoltrare i pacchetti. (pro, contro)

(ricorda definizione spanning tree CON IMMAGINE)
![[Pasted image 20260612220518.png]]

Utilizzo di **reverse path forwarding** al posto dello **spanning tree**
altra immagine con 3 topologie diverse: sottorete, sink tree, Albero realizzato dall'inoltro a percorso inverso.
![[Pasted image 20260612220542.png]]

### Multicast Routing 

Algoritmo per l'instradamento dei pacchetti multicast.

![[Pasted image 20260612220556.png]]

Necessita la divisione e gestione dei gruppi.
I router devono sapere quali host appartengono ad ogni gruppo. (host avvisano i router o router interrogano host).

Ogni router elabora uno spanning tree che copre tutti gli altri router.

### Internetworking

Per collegare reti che utilizzano protocolli differenti, passando attraverso una rete multiprotocollo con apposito router.

Il router consente di aprire un bridge o un tunnel a seconda dei casi.

![[Pasted image 20260612220610.png]]

- tunneling: cosa è e quando usarlo

![[Pasted image 20260612220623.png]]


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

![[Pasted image 20260612220657.png]]

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

![[Pasted image 20260612220723.png]]

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

![[Pasted image 20260612220742.png]]
RED vesione classica 

![[Pasted image 20260612220757.png]]
RED gentle-version

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

![[Pasted image 20260612220833.png]]

### Leaky bucket


![[Pasted image 20260612220844.png]]
**Scopo:** Trasformare un flusso di dati irregolare in un flusso costante e regolare (Traffic Shaping).

**Come funziona:** Immagina un secchio con un buco sul fondo. L'acqua (i pacchetti di dati inviati dall'host) può essere versata nel secchio a fiotti irregolari. Tuttavia, l'acqua uscirà dal buco sul fondo sempre a una velocità costante e fissa. Nella rete:

- L'host invia i pacchetti, che vengono temporaneamente immagazzinati in un buffer (il "secchio").

- Il sistema preleva i pacchetti dal buffer e li immette nella rete a una **velocità fissa e costante** (il "data rate fissato").

- **Gestione dei picchi:** Se l'host trasmette dati troppo velocemente e riempie completamente la capacità del buffer, i pacchetti in eccesso non trovano spazio e vengono **scartati (persi)**.


_In sintesi: Assicura un flusso di uscita rigido e costante, assorbendo piccole irregolarità ma non tollerando grossi picchi improvvisi._

### Token bucket

![[Pasted image 20260612220859.png]]

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
