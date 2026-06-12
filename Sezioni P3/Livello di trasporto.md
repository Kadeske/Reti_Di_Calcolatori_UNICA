# Livello di trasporto 

E' l'ultimo livello che governa le sessioni tra due host che comunicano tra loro.
Nel modello TCP/IP è sotto al livello applicativo, se fossimo nel modello ISO/OSI sarebbe sotto ai livelli sessione, presentazione, applicazione.

Si basa sul livello rete per fornire il trasporto dei dati tra 2 macchine con un livello di affidabilità desiderato e **indipendente dalle reti fisiche in uso**.

E' costituito da servizi orientati e non orientati alla connessione.
I dati prendono il nome di **Segmento**(TPDU) e abbiamo una connessione **END-TO-END**.


#### Servizi offerti ai livelli superiori 

L'hardware o il software che si occupa di far funzionare questo livello prende il nome di **Entità di Trasporto**. Nella maggior parte dei computer moderni, questo "motore" si trova direttamente integrato nel **Kernel del Sistema Operativo** (è lui che gestisce le connessioni TCP/IP), ma in casi specifici può risiedere in librerie separate o persino nell'hardware della scheda di rete.

![[Pasted image 20260611124316.png]]

Per passare i dati da un livello all'altro, si usano delle "porte comunicanti" logiche chiamate **SAP**.

- **N-SAP (Network SAP):** È il punto di contatto tra il Livello di Trasporto e il Livello di Rete (sottostante). Nella pratica di tutti i giorni, l'N-SAP corrisponde all'**Indirizzo IP**.
    
- **T-SAP (Transport SAP):** È il punto di contatto tra le Applicazioni e il Livello di Trasporto. Nel mondo di Internet, i T-SAP sono i **numeri di Porta**.
    

> Le porte vanno da **0 a 65535** (essendo un campo a 16 bit, i valori sono 65.536 ma si conta anche lo zero). 
> Inoltre, le porte standard (da 0 a 1023) si chiamano **well-known ports** (letteralmente "porte ben note").

Attenzione:
- Tutto ciò che sta dal Livello di Rete in giù dipende dall'infrastruttura fisica (i cavi, i provider, i router sparsi per il mondo).
- Il codice del Livello di Trasporto, invece, **gira esclusivamente sulle macchine terminali** (il tuo PC e il server di destinazione). È un protocollo strettamente _End-to-End_.

In un mondo utopico senza errori, questo livello sarebbe effettivamente inutile. Ma nel mondo reale i router perdono pacchetti, si intasano e li consegnano in disordine. 
Poiché **non abbiamo alcun controllo sui router di Internet** per correggere questi errori fisici, l'unica soluzione è delegare il controllo della qualità alle due macchine agli estremi della conversazione. Il Livello di Trasporto esiste per rimediare all'inaffidabilità della rete sottostante, garantendo (se richiesto) che i dati arrivino intatti e in ordine.

#### Primitive del servizio

Le quattro primitive astratte fondamentali sono:

- **LISTEN:** Il server dichiara di essere pronto a ricevere chiamate su una certa porta. È un'azione passiva (si mette in attesa).
- **CONNECT:** Il client tenta attivamente di "chiamare" il server per instaurare una sessione.
- **SEND / RECEIVE:** Sono le primitive usate per lo scambio vero e proprio dei dati.
- **DISCONNECT:** La richiesta di abbattere la connessione.


L'**Imbustamento** (spesso chiamato _Incapsulamento_) (come le matrioske):
- Il **Payload del Segmento** (i dati puri dell'applicazione) viene inserito in una "busta" a cui si aggiunge l'Intestazione del Trasporto (le Porte). Insieme formano la **TPDU** (Segmento).
    
- Questa TPDU viene calata nel Livello di Rete, che aggiunge la sua intestazione (gli IP). Tutto l'insieme diventa il **Pacchetto**.
    
- Il Pacchetto scende nel Livello Data Link, che aggiunge l'intestazione finale (i MAC Address). Diventa il **Frame (Trama)**.
![[Pasted image 20260611125050.png]]

Il passaggio da una primitiva all'altra fa muovere la **Macchina a Stati Finiti** (che abbiamo simulato in precedenza), passando da _IDLE_ (inattivo) a _ESTABLISHED_ (connesso), fino a tornare a _IDLE_.

Ma chi inizia la conversazione? Dipende dall'architettura:
- **Architettura Client-Server:** È asimmetrica. C'è un Server sempre acceso che fa da ascoltatore passivo, e tanti Client che iniziano la comunicazione attiva. (È il caso di quasi tutto il web moderno).
- **Architettura Peering (P2P):** È paritetica. Entrambi i computer sono allo stesso livello e possono scambiarsi i ruoli (come in BitTorrent), sarà uno scambio equilibrato.

![[Pasted image 20260611125331.png]]

#### Socket di Berkeley

Il Server è come un negoziante: deve aprire la saracinesca, mettere l'insegna e aspettare che entri qualcuno. Utilizza queste 4 primitive in sequenza:

- **SOCKET:** Crea l'oggetto astratto, la "presa" vera e propria. Specifica che userà internet (IPv4) e il TCP (flusso affidabile). Riceve in cambio un numero identificativo (il descrittore).
    
- **BIND (Associa):** La socket appena creata è anonima. Con la BIND, il server le "appiccica" un Indirizzo IP e un Numero di Porta (es. la porta 80). È come mettere l'insegna col numero civico fuori dal negozio, così i client sanno dove trovarlo.
    
- **LISTEN (Ascolta):** Il server dice al sistema operativo: _"Da questo momento accetto connessioni su questa porta"_. Questa funzione crea anche una coda (una "sala d'attesa") in memoria, nel caso arrivassero più client contemporaneamente. Non blocca il programma.
    
- **ACCEPT (Accetta):** Qui il server si **blocca** e si mette in attesa. Aspetta fisicamente che un client bussi alla porta.
    
    - _Concetto fondamentale da esame:_ Quando un client si connette, l'ACCEPT **crea una nuova socket** dedicata esclusivamente a quel client e la restituisce al server. La socket originale (quella creata con la BIND) rimane intatta e continua ad ascoltare per accettare altri futuri client!

Il Client è il cliente del negozio. Non ha bisogno di un'insegna, deve solo sapere dove andare. Il suo lavoro è molto più snello:

- **SOCKET:** Crea anche lui la sua "presa" vuota e anonima.
    
- **CONNECT (Connetti):** Il client punta direttamente all'Indirizzo IP e alla Porta del Server (che deve conoscere in anticipo).
    
    - _Perché il client non fa la BIND?_ Perché al server non interessa da quale porta specifica arrivi la richiesta. Quando il client fa la CONNECT, il sistema operativo gli assegna automaticamente e di nascosto una porta libera a caso (chiamata porta effimera, es. 54321) per gestire la comunicazione.
    
Una volta che la `CONNECT` del client ha incontrato l'`ACCEPT` del server, il "tubo" logico è instaurato.

- **SEND / RECEIVE:** I due programmi usano queste funzioni per scriversi e leggersi i dati a vicenda, proprio come se stessero scrivendo su un normale file di testo.
    
- **CLOSE:** Quando la comunicazione è finita, entrambi chiamano questa primitiva per chiudere la connessione e liberare la porta e la memoria RAM utilizzata.

## Elementi dei protocolli di trasporto 

Il servizio di trasporto è implementato da un **protocollo di trasporto**.
Per certi versi ricordano i protocolli data link.

### Indirizzamento

Quando un applicativo vuole creare una connessione verso un processo remoto deve **specificare a quale intente connettersi**.
Solitamente si definiscono degli indirizzi su cui i processi possono restare in ascolto delle richieste di connessione. Questo utilizza le **porte**, punti terminali.

Questo colloquio avviene tramite uno specifico endpoint, i **T-SAP**.

Per capire l'indirizzamento, l'analogia migliore è quella di un grande condominio:
- **N-SAP (Network SAP):** È l'**Indirizzo IP**. Corrisponde all'indirizzo fisico del palazzo (es. Via Roma 10). Serve per far arrivare il pacchetto dal tuo PC fino al router del computer di destinazione.
- **T-SAP (Transport SAP):** È la **Porta** (un numero a 16 bit). Corrisponde al numero dell'interno/appartamento dentro il palazzo. Serve per consegnare il pacchetto all'applicazione giusta (es. l'interno 80 è il server Web, l'interno 25 è il server Email). Su Internet, i T-SAP sono chiamati _Endpoint_ o _Porte_.

![[Pasted image 20260611142336.png]]
L'immagine mostra esattamente il viaggio di una richiesta:
1. **La Partenza (Host 1):** Il Processo Applicativo del Client vuole conoscere l'ora esatta. Il sistema operativo gli assegna una porta (T-SAP) casuale e libera, ad esempio la **1208**.
    
2. **Il Viaggio:** La richiesta scende al Livello di Rete (N-SAP), viaggia sui cavi fisici (Livello Fisico) e arriva all'N-SAP dell'Host 2 (il server).
    
3. **L'Arrivo (Host 2):** L'N-SAP del server fa da "portiere". Legge l'intestazione del trasporto, vede che il pacchetto è destinato al T-SAP **1522** (la porta standard per il servizio dell'ora esatta) e lo smista al "Server 1", che è il programma in ascolto su quella specifica porta. (Ignorando il "Server 2" che è in ascolto sulla porta 1836 per fare tutt'altro).

Se dovessimo seguire il modello classico in modo rigido, un Server aziendale dovrebbe avere 65.536 programmi diversi avviati contemporaneamente (uno per ogni porta), tutti bloccati in uno stato di `LISTEN` perenne, in attesa che magari qualcuno, un giorno, si connetta. Questo comporterebbe un **consumo enorme e inutile di memoria RAM e CPU**.

Per evitare questo spreco, i sistemi operativi moderni non tengono tutti i server attivi, ma usano dei "trucchi" architetturali:
- _Modello Process Server_
- _Modello Directory Server_


#### Modello Process Server 

Invece di avere tutti i possibili server costantemente in ascolto su un proprio TSAP (Porta) noto, si utilizza un'architettura diversa per i servizi che vengono richiesti raramente.
- Ogni macchina che offre servizi remoti esegue un singolo **process server** che agisce da _proxy_ (intermediario) per i servizi meno utilizzati.
- Nel mondo UNIX, questo specifico server prende il nome di **inetd** (Internet Daemon).
- Il suo compito è ascoltare **contemporaneamente su un insieme di porte** aspettando una richiesta di connessione.
- Il libro definisce questo meccanismo come **protocollo di connessione iniziale**.

Come avviene la comunicazione in pratica?
- I potenziali utenti (Client) iniziano facendo una richiesta utilizzando la primitiva **CONNECT**, specificando l'indirizzo TSAP (Porta) del servizio che desiderano.
- In questo primo momento, ottengono una connessione direttamente col _process server_ (che stava sorvegliando quella porta), non con il server finale.
- Dopo aver ricevuto la richiesta, il _process server_ **genera** (crea "al volo") il server specifico richiesto dall'Host 1.
- Il passaggio chiave è che il _process server_ permette al nuovo server appena generato di **ereditare la connessione** precedentemente instaurata con l'utente. Da quel momento, sarà il nuovo server a svolgere il lavoro richiesto, mentre _inetd_ torna ad ascoltare.


Cosa succede scendendo nei dettagli dei livelli:
- Quando i dati arrivano al Livello di Rete (identificato dal **NSAP**, l'indirizzo IP), questo interroga il Livello di Trasporto (il **TSAP**, la porta).
- Il TSAP non risponde con un proprio server sempre attivo e dedicato. Invece, invoca il _process server_ che è già attivo su più porte.
- Il _process server_ legge la richiesta, capisce quale servizio attivare (nell'esempio del diagramma: l'ora del giorno, ovvero il _Time-of-day server_) e "aggancia" quel servizio alla richiesta.

![[Pasted image 20260611142851.png]]

Questo modello permette di **sganciare** il momento della risposta (e l'attivazione del server che deve rispondere) dalla necessità di dover tenere tutti i server costantemente attivi in background.
- **Vantaggi:** Ottimizzazione della capacità elaborativa, grande risparmio di energia ed elevata efficienza della macchina.
- **Svantaggi:** Si perde "qualche frazione di secondo" nel passaggio in cui il _process server_ deve generare e avviare da zero il nuovo server.

#### Modello Directory Server 

Il "protocollo di connessione iniziale" (cioè il Process Server/`inetd`) funziona benissimo per quei server leggeri che possono essere creati o avviati solo in caso di effettiva necessità.
Tuttavia, si verificano molto spesso situazioni in cui i **servizi esistono indipendentemente dal process server**.

Per gestire le situazioni in cui i servizi sono già attivi ma le loro porte (TSAP) non sono note a priori al pubblico, si utilizza questo schema alternativo.

- In questo modello viene introdotto un processo speciale chiamato **server dei nomi (name server)**, noto anche come **directory server**.
- **La dinamica di ricerca:** Se un utente vuole scoprire l'indirizzo TSAP che corrisponde a un preciso nome di servizio, non tenta di collegarsi a caso.
- L'utente apre prima di tutto una connessione con il _server dei nomi_, il quale ascolta sempre su uno **TSAP noto** (una porta pubblica e famosa che tutti conoscono).
- L'utente invia quindi un messaggio al _server dei nomi_ specificando il nome testuale del servizio che sta cercando.
- Il _server dei nomi_ risponde al client fornendogli l'indirizzo TSAP esatto a cui collegarsi. A quel punto, l'utente chiude la chiamata col directory server e si connette direttamente alla porta appena ricevuta.

In questo modello, c'è una regola fissa: ogni **nuovo servizio appena creato si deve registrare** sul server dei nomi.


### Stabilire una connessione

Stabilire una connessione sembra un'operazione banale (basterebbe inviare una richiesta `CONNECTION REQUEST` e attendere una risposta), ma in realtà è sorprendentemente complessa.

La radice del problema risiede nell'inaffidabilità della rete sottostante, la quale **può perdere, memorizzare e duplicare i pacchetti**. Questo comportamento imprevedibile genera complicazioni serie, soprattutto legate ai pacchetti "fantasma" che rimangono intrappolati nei router e riappaiono quando meno ce lo si aspetta.


Il primo scoglio affrontato è capire come **distruggere i pacchetti obsoleti che sono ancora in circolo**. Se non si sa con certezza che un vecchio pacchetto è "morto", c'è il rischio che arrivi a destinazione scambiato per uno nuovo. Il testo elenca tre potenziali soluzioni, scartandone subito due:
1. **Avere una rete ristretta:** Su una rete piccola si potrebbe usare un clock unico per verificare se il pacchetto è defunto. Su una rete vasta, invece, servirebbe un metodo per impedire i cicli e contenere il ritardo massimo di attraversamento.
2. **Mettere un contatore di salto in ogni pacchetto:** Questo contatore verrebbe decrementato a ogni salto (è il principio del TTL in IPv4), assicurando che il pacchetto muoia dopo un tot di hop.
3. **Inserire un orario in ogni pacchetto:** Scartata, perché richiederebbe che i router di tutta Internet siano perfettamente sincronizzati, cosa praticamente impossibile da attuare.

È necessario garantire matematicamente che un pacchetto e i relativi acknowledgement (le ricevute di ritorno) siano defunti.
- Si definisce un **tempo T** (chiamato anche **area proibita**), che rappresenta il tempo massimo necessario per essere assolutamente certi che l'ultimo potenziale acknowledgement di un pacchetto non sia più in circolazione nella rete. Nella rete Internet, storicamente, questo tempo T è stato fissato a **120 secondi**.

Per risolvere il problema, si può utilizzare il metodo inventato da **Tomlinson**.

- L'idea centrale è che la sorgente deve etichettare i segmenti con **numeri di sequenza che non saranno riutilizzati per un numero di secondi pari a T**.
- In pratica, lo spazio dei numeri di sequenza disponibili e la velocità di trasmissione definiscono la **dimensione dei numeri di sequenza**. Con questo vincolo, non può mai capitare che un duplicato in ritardo "batta sul tempo" un pacchetto nuovo a cui è stato assegnato lo stesso numero.

Ipotizziamo lo scenario critico in cui un host subisce un malfunzionamento (crash) e perde la memoria dei numeri di sequenza che stava usando.
- Un metodo rudimentale sarebbe tenere l'host inattivo per il tempo T dopo il riavvio, ma per reti estese T è troppo lungo.
- L'alternativa proposta, sempre da Tomlinson, insieme a Sunshine e Dalai, prevede l'installazione di **orologi** sugli host. La particolarità è che funzionano come **contatori binari** e _non_ hanno bisogno di essere sincronizzati tra le varie macchine. L'unica assunzione vitale è che l'orologio continui a funzionare (magari a batteria) anche quando l'host crasha.

**Il Meccanismo dell'Orologio:**
- Quando viene instaurata una connessione, i **k bit di ordine più basso** del valore attuale dell'orologio vengono usati per definire il **primo numero di sequenza** (Initial Sequence Number).
- Questo significa che ogni nuova connessione inizia a contare i segmenti partendo da un numero diverso, legato all'istante temporale.
- Lo spazio della sequenza deve essere abbastanza grande da garantire che, quando i numeri si esauriscono e il conteggio ricomincia da zero, i vecchi segmenti con lo stesso numero siano spariti dalla rete da parecchio tempo.

![[Pasted image 20260611143903.png]]
La parte ombreggiata nei grafici rappresenta la **regione proibita**: un'area temporale in cui è assolutamente vietato riutilizzare un determinato numero di sequenza, per evitare confusioni letali.

Se un host subisce un crash (ad esempio al secondo 70), quando si riavvia userà l'orologio per scegliere un nuovo numero di partenza, garantendo che questo numero cada _al di fuori_ della regione proibita legata ai pacchetti inviati prima del crash. Una volta d'accordo sul numero di partenza, si usa un **protocollo a finestra scorrevole** per trasmettere i dati veri e propri.

**I due grandi pericoli per i numeri di sequenza:** Il testo impone due paletti matematici fondamentali per evitare che il ritmo di trasmissione finisca dentro la regione proibita:

1. **Evitare di spedire troppo velocemente:** Se l'host invia dati a una velocità folle appena aperta la connessione, i numeri di sequenza si consumeranno molto più rapidamente dell'avanzare del tempo (orologio). Questo farebbe "sbattere" la linea del conteggio contro il bordo superiore dell'area proibita.
    
    - _Regola:_ Il **massimo tasso di invio dei dati** per qualsiasi connessione è limitato a **un segmento per ogni ciclo di clock**. L'entità di trasporto _deve_ aspettare il successivo "tic" dell'orologio prima di aprire una nuova connessione dopo un crash.
        
2. **Il vincolo dello spazio di sequenza (S/C>T):** Entrambe le dinamiche richiedono che l'orologio faccia un "tic" (un ciclo) molto velocemente (il testo indica 1 ps o meno). Per evitare che l'orologio "doppi" troppo velocemente i numeri di sequenza impiegati, c'è un vincolo: data una velocità C dell'orologio e uno spazio totale di numeri di sequenza disponibili S, il tempo necessario per esaurire tutti i numeri (S/C) **deve essere rigorosamente maggiore** del tempo di vita massimo del pacchetto (T).


### Three-Way Handshaking

Nel 1975 (alla fine del periodo di ARPANET), **Tomlinson** inventò l'algoritmo _three-way handshaking_ per risolvere definitivamente il problema della duplicazione dei pacchetti. L'idea di base è geniale ma semplice: serve una **verifica reciproca da parte di entrambi i peer** per assicurarsi che l'attuale richiesta di connessione sia genuina e non un vecchio duplicato fantasma.



![[Pasted image 20260611144237.png]]

**A)** I tre passaggi fondamentali dell'instaurazione normale di una connessione:
- **Passo 1:** Il richiedente (Host 1) invia un TPDU di tipo `CONNECTION REQUEST` (CR). All'interno ci mette un numero di sequenza iniziale **`x`**.

- **Passo 2:** L'Host 2 riceve la richiesta e risponde con un TPDU contenente due cose:
    - Un `ACK.x` (che dice: _"Ti do l'ack di x, la tua richiesta è arrivata correttamente"_).
    - La proposta di un proprio **numero progressivo iniziale** (che il testo chiama **`y`**).
    - 
- **Passo 3:** Il richiedente (Host 1) riceve questa risposta e invia il terzo e ultimo TPDU. Questo pacchetto conterrà:
    - I primi dati reali del dialogo.
    - La **conferma di `y` (`ACK di y`)**.

I valori iniziali di `x` e `y` possono (e devono) essere generati sfruttando l'orologio di sistema (come visto nella lezione precedente), in modo da avere valori di partenza ogni volta diversi.

**B)** Cosa succede se un vecchio pacchetto `CONNECTION REQUEST` (con un vecchio numero `x`), rimasto incastrato nella rete, riappare all'improvviso e arriva all'Host 2?
- Questo è il caso in cui **il primo segmento è duplicato e ritardato**. Arriva all'Host 2 senza che l'Host 1 lo sappia o lo voglia.
- L'Host 2, credendo sia una nuova richiesta genuina, reagisce inviando all'Host 1 il segmento di risposta (`ACK = x`, propone il suo `y`).
- In pratica, l'Host 2 sta chiedendo: _"Mi confermi che vuoi davvero aprire questa connessione con me?"_
- L'Host 1 riceve questo pacchetto ma si accorge che non aveva mai iniziato questa conversazione (oppure l'aveva già chiusa da tempo). Quindi, **rifiuta il tentativo inviando un `REJECT`** (o _RST_ nel gergo TCP moderno).
- Leggendo il `REJECT`, l'Host 2 comprende di essere stato ingannato dal duplicato in ritardo e abbandona la connessione. Il duplicato non ha fatto danni.

**C)** Il caso peggiore: cosa succede se riappare non solo la vecchia richiesta, ma _anche_ il vecchio pacchetto dati contenente l'Ack?

- Si verifica la presenza duplicata di una **CR ritardata** e di un **Ack ritardato**.
- Come prima, l'Host 2 riceve la vecchia CR (`seq=x`) e risponde proponendo il suo nuovo numero di sequenza attuale (es. **`y`**), sapendo per certo che non ci sono in giro vecchi segmenti con il numero `y`.
- A questo punto, il secondo segmento duplicato "fantasma" (quello dei vecchi dati) giunge all'Host 2.
- _Il trucco che salva la rete:_ Questo vecchio segmento conteneva la conferma (`ACK`) per il numero di sequenza che l'Host 2 aveva usato _nella vecchia sessione_ (che il testo chiama **`z`**).
- L'Host 2 legge il pacchetto e ragiona: _"Io ti ho appena proposto il numero `y`, ma tu mi stai mandando la conferma per il numero `z`! Questo è chiaramente un vecchio duplicato"_.
- Il fatto che sia stato confermato `z` e non `y` suggerisce all'Host 2 l'inganno. La richiesta viene rigettata.

### Rilascio della connessione

Il rilascio al livello di trasporto deve essere un **rilascio netto**. Il motivo è puramente legato all'efficienza delle risorse: le due macchine non devono mantenere "nulla di pendente" che continui a caricare o occupare inutilmente la rete.

Quando avviene questo rilascio, l'entità di trasporto esegue due azioni obbligatorie:

1. **Rimuove le informazioni** sulla connessione dalle proprie tavole di stato interne (liberando memoria RAM).
2. **Informa l'utente** di livello superiore (ovvero il processo applicativo, come il browser) che la connessione è ufficialmente chiusa.

Questo modello permette due tipi di rilascio:
- **Rilascio Asimmetrico**: come se, mentre tu stai ancora parlando, l'altra persona riagganciasse di colpo il ricevitore.
- **Rilascio simmetrico**: un host non si "spegne" all'improvviso, ma dichiara: "Io ho finito di trasmettere". Tuttavia, continua a rimanere in ascolto finché anche l'altro host non dichiara a sua volta di aver finito, realizzando così un **rilascio completo** senza perdite.
![[Pasted image 20260611144935.png]]


#### Esempio dei due eserciti

Il problema teorico alla base del rilascio sicuro di una connessione è perfettamente illustrato dal celebre paradosso dei due eserciti. 

Immaginiamo un **esercito bianco** posizionato in una valle, con un **numero di soldati superiore a quello del singolo esercito blu 1 o dell'esercito blu 2**, i quali sono accampati sulle colline opposte.
![[Pasted image 20260611154048.png]]


La vittoria per i blu è sicura solamente se attaccano in modo simultaneo. Per coordinarsi, l'esercito 1 invia un messaggero proponendo di attaccare l'indomani alle 6, ma non si muoverà senza aver prima ricevuto una conferma. Se l'esercito 2 invia la conferma, a sua volta non attaccherà finché non saprà che l'esercito 1 ha effettivamente ricevuto tale conferma, innescando un processo iterativo senza fine. Nessuno ha mai la certezza assoluta che l'altro abbia ricevuto la comunicazione, arrivando al paradosso.

![[Pasted image 20260611154113.png]]

Proprio a causa di questa impossibilità logica, le tecniche elaborate per il rilascio evitano di imporre la necessità di un accordo perfetto. Il problema viene demandato a chi utilizza il livello di trasporto, facendo decidere i partecipanti in modo indipendente tramite l'uso di timer di sicurezza. Questo approccio si declina in quattro scenari principali:

- **a) Rilascio Normale (Three-way handshake di chiusura):** L'Host 1 decide di chiudere, invia una `DISCONNECTION REQUEST (DR)` e fa partire il suo timer. L'Host 2 riceve la richiesta, invia a sua volta una `DR` (facendo partire anche lui un timer di sicurezza) per confermare. Quando l'Host 1 riceve questa risposta, invia l'ultimo `ACK` e chiude definitivamente la connessione, cancellandola dalla memoria. Quando l'Host 2 riceve l'ACK, si chiude a sua volta. È lo scenario perfetto.
    
- **b) Perdita dell'ACK finale:** Tutto procede bene fino all'ultimo passaggio: l'Host 1 invia l'ACK finale e si spegne, ma questo pacchetto viene perso. L'Host 2 rimane in attesa. È qui che il timer salva la situazione: scaduto il tempo massimo senza aver ricevuto l'ACK, l'Host 2 rilascia comunque la connessione. Senza questo timer, l'Host 2 rimarrebbe bloccato all'infinito aspettando un messaggio che non arriverà mai.
    
- **c) Perdita della risposta intermedia (DR):** L'Host 1 invia la sua prima `DR`, l'Host 2 risponde con la sua `DR`, ma questa si perde nel tragitto. L'Host 1, non ricevendo nulla, attende fino allo scadere del suo timer. A quel punto, ipotizza che la sua prima richiesta sia andata persa e procede a ritrasmettere una nuova `DR`, permettendo al processo di sbloccarsi e andare avanti.
    
- **d) Il caso peggiore (Connessione aperta a metà):** I tentativi di trasmettere la `DR` falliscono ripetutamente (magari a causa di un cavo staccato temporaneamente). Dopo N tentativi a vuoto, l'Host 1 si arrende, chiude la sua parte di connessione e la considera terminata. L'Host 2, però, non ha mai ricevuto nulla e continua a credere che la comunicazione sia nel pieno del suo svolgimento. Si crea così una **connessione aperta a metà (Half-Open Connection)**.


### Controllo di flusso e gestione dei buffer

Il controllo del flusso al Livello di Trasporto affronta un problema molto simile a quello già visto nel Livello Data Link: evitare che un ricevitore lento venga letteralmente "affogato" da una macchina mittente che spedisce dati a velocità troppo elevate.

La grande particolarità del Livello di Trasporto, però, è che **i segmenti (TPDU) non sono sempre uguali**. La loro dimensione è estremamente variabile e dipende dall'applicazione. Se un terminale bancario invia un singolo comando, produrrà un traffico molto piccolo (magari di soli 8 bit), ma se un server avvia il trasferimento di un file, produrrà un traffico massiccio.

Questa estrema variabilità richiede una gestione molto intelligente della memoria (i buffer). Esistono due profili di traffico principali:

- **Traffico bursty ma poco gravoso:** Per sessioni leggere come l'emulazione di un terminale, non è necessario allocare grandi buffer a destinazione. Basta mantenere i dati nel buffer della sorgente.
- **Traffico gravoso:** Per i trasferimenti di file, è obbligatorio prevedere buffer cospicui a destinazione per poter sempre accettare la mole di dati in arrivo.


Un aspetto cruciale riguarda l'affidabilità della rete sottostante. Se il servizio di rete è inaffidabile, il mittente è obbligato a conservare nel proprio buffer una copia di ogni singola TPDU inviata finché non viene confermata. Tuttavia, anche se la rete è affidabile, il mittente non può abbassare la guardia. L'acknowledgement (ACK) proveniente dal Livello di Rete certifica soltanto che la TPDU è arrivata a destinazione, **non garantisce che il ricevitore l'abbia effettivamente accettata** ed elaborata. Se il ricevitore ha i buffer pieni, scarterà il pacchetto. Pertanto, a meno che il ricevitore non garantisca sempre spazio libero, il mittente deve continuare a fare buffering.

Per compensare queste differenze e gestire la memoria in arrivo, si utilizzano tre modelli architetturali per i buffer:

![[Pasted image 20260611154838.png]]

1. (a)**Buffer a dimensione fissa:** Se la maggior parte delle TPDU ha una grandezza simile, è naturale organizzare la memoria come un "pool" di blocchi tutti identici, allocando una TPDU per ogni blocco. È un metodo facilissimo da gestire, ma rischia di sprecare moltissimo spazio (frammentazione interna) se arrivano pacchetti molto più piccoli del blocco standard.
    
2. (b)**Buffer a dimensione variabile:** Utilizza porzioni di memoria modellate esattamente sulla grandezza del pacchetto in arrivo. Il vantaggio è un utilizzo perfetto della memoria senza sprechi interni, ma il prezzo da pagare è un algoritmo di gestione molto più complicato per il sistema operativo.
    
3. (c)**Buffer circolari per ogni tipo di connessione:** Si dedica un singolo buffer ad anello, molto grande, in via esclusiva per ogni connessione aperta. Questo sistema è formidabile e velocissimo quando tutte le connessioni sono sottoposte a un carico pesante e continuo. Diventa invece uno spreco inaccettabile se ci sono connessioni aperte ma inattive (o con pochissimo carico), poiché la memoria rimane bloccata e inutilizzabile per altri scopi.


### Multiplexing 

Nel livello di trasporto, l'esigenza del multiplexing nasce da un problema pratico di instradamento e di limiti della banda. Quando un computer possiede un solo indirizzo di rete (NSAP, che nel nostro mondo coincide con l'indirizzo IP), tutte le comunicazioni in entrata e in uscita devono obbligatoriamente passare per quell'unico punto di accesso. All'arrivo di un segmento, il sistema deve stabilire con precisione a quale processo o applicazione consegnarlo.

Questa gestione dei flussi prende il nome di multiplexing e si divide in due architetture diametralmente opposte.

**Upward Multiplexing (Multiplexing verso l'alto)** È la situazione più comune, quella che avviene costantemente sui nostri dispositivi. Hai a disposizione un solo collegamento fisico, un solo indirizzo MAC e un unico indirizzo IP (NSAP) fornito dal router. Tuttavia, stai richiedendo diversi servizi in simultanea: navighi sul web (HTTP, HTTPS), scarichi un file (FTP) e magari gestisci un terminale remoto (Telnet).

![[Pasted image 20260611155135.png]]

Per gestire tutto questo, da un singolo NSAP alla base, la connessione si "ramifica" verso l'alto. Il livello di trasporto applica il multiplexing prendendo l'unico flusso di dati in ingresso e smistandolo su molteplici porte di destinazione (TSAP). Una singola connessione di rete sostiene tante connessioni di trasporto.

**Downward Multiplexing (Multiplexing verso il basso)** Qui ci troviamo nello scenario inverso, causato da un collo di bottiglia fisico. Immagina di dover trasferire una quantità di traffico dati impressionante, come il backup di un hard disk da 500 GB. Stai usando una singola applicazione (una sola sessione FTP), il che significa che il traffico è destinato a un unico TSAP.

![[Pasted image 20260611155154.png]]

Se l'infrastruttura di rete è lenta, una singola connessione IP non basta per svolgere il compito in tempi utili. La soluzione è instaurare più connessioni IP per dividere il carico di lavoro in modo proporzionale. Se una singola linea (l'esempio utilizza le classiche linee ISDN) offre una banda di 64 kbps, il trasferimento sarà lentissimo. Attivando una seconda linea il carico si divide e la velocità sale a 128 kbps. Attivandone 4, si arriva a 256 kbps.

In pratica, si attivano 4 differenti indirizzi IP di connessione per dividere il carico da scaricare. La mole di dati viaggia frammentata sulle diverse linee di rete sottostanti (più NSAP) e, risalendo, converge in modo trasparente verso l'alto, riunendosi nell'unico TSAP che ha fatto la richiesta iniziale.


### Ripristino dopo un crash 

Un classico esempio per comprendere l'assoluta gravità della situazione è un trasferimento bancario: immagina di aver vinto 1.000.000 € alla lotteria e di avviare il trasferimento dal terminale verso il server della banca. Se durante il processo la linea crolla e il server della banca subisce un crash, al riavvio il server re-inizializza le proprie tabelle. Il problema drammatico è che il server non sa più precisamente a che punto del trasferimento si fosse arrivati.

In questo scenario di incertezza, il client (il mittente dei dati) può trovarsi in due stati fondamentali rispetto alla rete:

- **Stato S0:** Non ci sono segmenti in circolazione in attesa di conferma. Il client ha ricevuto l'Acknowledgement (ACK) per tutto ciò che ha spedito fino a quel momento.
- **Stato S1:** Ci sono uno o più segmenti ancora in circolazione per i quali non è stato ancora ricevuto l'ACK.

Per capire se e quando il client debba ritrasmettere i dati per recuperare il milione di euro, bisogna analizzare come è stato programmato il server. Esistono due strategie diametralmente opposte per gestire l'arrivo di un pacchetto sul server: eseguire prima l'invio dell'ACK e poi la scrittura (passaggio dei dati al livello applicativo, es. l'accredito sul conto), oppure eseguire prima la scrittura e poi l'invio dell'ACK. Inoltre, un crash (C) può interrompere brutalmente questa sequenza in vari momenti, annullando di fatto le azioni successive (che indicheremo tra parentesi).

Analizziamo la prima strategia del server: **Prima ACK, poi scrittura**. In questo caso, si aprono tre possibili finestre temporali in cui il crash può colpire: Se si verifica **AC(W)**, il server ha inviato l'ACK, ma è crashato prima di poter scrivere i dati sul conto. Il client riceve regolarmente l'ACK, passa allo stato S0 ed è convinto che tutto sia andato a buon fine. Se il client decide di non ritrasmettere, il milione di euro andrà irrimediabilmente perso (LOST), perché la banca non ha mai registrato l'operazione. Se il client ritrasmette per forza, si salva. Se si verifica **AWC**, il server ha fatto in tempo a inviare l'ACK e a scrivere i dati prima di spegnersi. L'operazione è perfettamente salva. Se in questo caso il client, non sapendo del crash avvenuto _dopo_, decidesse di ritrasmettere per sicurezza, la banca registrerebbe l'accredito una seconda volta generando un duplicato (DUP). Se si verifica **C(AW)**, il crash avviene subito, prima di fare qualsiasi cosa. L'unica salvezza è la ritrasmissione obbligatoria, altrimenti il messaggio viene perso (LOST).

Passiamo alla seconda strategia del server: **Prima scrittura, poi ACK**. Anche qui abbiamo tre scenari temporali: Se si verifica **C(WA)**, il crash avviene prima di intraprendere qualsiasi azione. È un caso identico al precedente: serve ritrasmettere per evitare la perdita (LOST). Se si verifica **WAC** (indicato anche come W AC), l'operazione è stata scritta sul conto e l'ACK è stato regolarmente inviato e ricevuto. Se il client decide di ritrasmettere, si genera un inutile duplicato (DUP). Se si verifica **WC(A)**, si entra nello scenario più insidioso. Il server ha effettivamente registrato l'accredito di un milione in banca, ma è crashato una frazione di secondo prima di inviare l'ACK. Il client, non ricevendo conferma, si trova nello stato S1. Se il client, allarmato dal silenzio, ritrasmette il pacchetto, la banca eseguirà una seconda volta la scrittura generando un clamoroso duplicato invisibile al livello applicativo. La soluzione perfetta in questo specifico caso sarebbe non ritrasmettere affatto, oppure avere una regola che vieta di ritrasmettere quando ci si trova nello stato S1.

![[Pasted image 20260611155814.png]]

Incrociando le strategie del client (ritrasmettere sempre, mai, solo in S0 o solo in S1) con le strategie e le tempistiche di crash del server, emerge una verità matematica e architetturale ineluttabile, nota come il problema del ripristino: **non esiste una singola strategia per l'host mittente che garantisca un risultato corretto (OK) in ogni singola situazione.** Qualsiasi scelta si faccia sul client, ci sarà sempre almeno una precisa combinazione temporale del crash sul server che porterà inevitabilmente a una perdita di dati (LOST) o a una duplicazione indesiderata (DUP).

## UDP (User Datagram Protocol) RFC768

L'UDP trasporta **datagrammi**. La sua caratteristica fondamentale è la velocità pura, ottenuta eliminando quasi completamente l'overhead di controllo. Non ha meccanismi di "conferma" e non perde tempo a instaurare una sessione prima di parlare. L'UDP si attiva, prende i dati e cerca di farli arrivare a destinazione nel modo più rapido possibile, sfruttando la disponibilità immediata delle linee di rete.

Per funzionare bene, queste caratteristiche presuppongono che ci sia alla base una rete fisica piuttosto efficiente. Tuttavia, si sceglie di usare l'UDP in due scenari ben precisi:
1. Quando ci si trova all'interno di **reti locali (LAN) già estremamente affidabili**, dove la perdita di pacchetti è quasi nulla.
2. Quando si ha a che fare con traffico in cui **la perdita di qualche dato non è considerata importante**. Il classico esempio sono le sessioni _real-time_ come le videochiamate VoIP o lo streaming in diretta: se un pacchetto contenente un fotogramma video va perso, è molto meglio subire un microscopico scatto a schermo piuttosto che bloccare l'intera telefonata in attesa che il protocollo ritrasmetta il dato mancante.

![[Pasted image 20260612114557.png]]

Proprio per garantire questa estrema snellezza, l'header (l'intestazione) dell'UDP è uno dei più piccoli esistenti nel mondo delle reti (è superato in piccolezza solo dall'intestazione delle celle ATM).

Osservando lo schema a blocchi da 32 bit, vediamo che l'header è composto da soli 8 byte totali, suddivisi in quattro campi semplicissimi da 16 bit ciascuno:
- **Source Port (Porta Sorgente - 16 bit):** Identifica la porta del processo applicativo che sta inviando i dati.
- **Destination Port (Porta Destinazione - 16 bit):** Identifica la porta del processo che deve ricevere i dati sul computer remoto.
- **UDP Length (Lunghezza - 16 bit):** Indica la dimensione totale del datagramma, calcolata in byte, comprendendo sia questa intestazione sia i dati trasportati (il payload).
- **UDP Checksum (Controllo errori - 16 bit):** È un valore matematico usato dal ricevitore per verificare se i dati si sono accidentalmente corrotti (cambiando gli 0 e gli 1) durante il viaggio sui cavi. L'aspetto più interessante di questo campo è che **può non essere considerato**. Proprio per assecondare la fame di prestazioni delle sessioni real-time, i programmatori possono decidere di disattivare il calcolo del checksum (impostandolo tutto a zero) per risparmiare preziosi millisecondi di elaborazione sulle macchine.

### RPC (Remote Procedure Call)

Un'altra applicazione perfetta per la velocità estrema dell'UDP sono le **RPC (Remote Procedure Call)**, ovvero le Chiamate di Procedura Remota.

L'idea alla base di questo modello consiste nel creare un'illusione perfetta di località. Quando un programmatore scrive il software per il client, vuole poter richiamare una funzione (ad esempio, farsi restituire dei dati da un database) esattamente come se quella funzione si trovasse sul suo stesso computer, ignorando completamente l'esistenza della rete. Il client non deve accorgersi che sta interrogando una macchina distante; tutto deve essere trasparente e immediato. Ci si serve dell'UDP proprio per la sua velocità nell'eseguire queste operazioni fulminee.

![[Pasted image 20260612114925.png]]

1. **La finta chiamata:** Il programma client chiama una procedura all'interno dello stub del client. Dal punto di vista del software, è una normalissima funzione locale: inserisce i parametri necessari nello stack della memoria e si mette in attesa del risultato.
    
2. **Il Marshalling:** Qui interviene la magia dello stub del client. Prende i parametri appena ricevuti e li "impacchetta" in un formato standard (un messaggio) adatto a viaggiare sui cavi. Questa delicata operazione di traduzione e impacchettamento prende il nome tecnico di **marshalling**. Subito dopo, lo stub effettua una chiamata di sistema per chiedere al sistema operativo di spedire il pacchetto.
    
3. **Il Viaggio (UDP):** Il messaggio viene affidato al kernel del sistema operativo, che lo spara velocemente sulla rete facendolo arrivare al server remoto.
    
4. **La Ricezione:** Il messaggio in ingresso viene intercettato dal kernel del server e passato allo stub del server.
    
5. **L'Esecuzione reale:** Lo stub del server esegue l'operazione inversa (l'unmarshalling): spacchetta i parametri, invoca la _vera_ procedura del server, le fa svolgere il lavoro e ne raccoglie il risultato. A questo punto, la risposta viene re-impacchettata e fa il percorso esatto a ritroso, tornando al client che è rimasto beatamente all'oscuro di tutta questa complessa macchinazione.

### Protocolli di trasporto real-time 
Sono protocolli che preferiscono la velocità.
E' preferibile perdere qualche segmento ma avere una continuità di dati.

#### RTP (Real-time Transport Protocol)

RTP lavora in stretta sinergia con UDP, ma con una differenza architetturale importante: mentre UDP risiede nel kernel del sistema operativo, RTP viene solitamente implementato direttamente nello spazio utente, all'interno dell'applicazione multimediale stessa.

Dato che sfrutta le fondamenta dell'UDP, i router della rete non fanno alcuna distinzione: trattano i pacchetti RTP esattamente come qualsiasi altro datagramma, senza riservare loro corsie preferenziali.

La funzione base di RTP è quella di eseguire il multiplexing di flussi di
dati real-time in un singolo flusso di pacchetti UDP.
L'applicazione genera i dati (ad esempio, un frammento di voce), RTP ci attacca la sua intestazione e tutto questo blocco diventa il _payload_ (il carico utile) che viene annegato all'interno di un normale segmento UDP. A sua volta, UDP viene inserito nel pacchetto IP e infine nel frame Ethernet.


![[Pasted image 20260612115523.png]]


#### RTCP (Real-Time Transport Protocol)

A supporto del protocollo RTP lavora sempre un protocollo gemello chiamato **RTCP (Real-time Transport Control Protocol)**. Se RTP si occupa di trasportare fisicamente i dati multimediali, RTCP fa da "supervisore": non trasporta media, ma gestisce le retroazioni (feedback) verso la sorgente. Invia costantemente report sullo stato della rete, sulle perdite di pacchetti e gestisce la sincronizzazione dei flussi.

Il problema più grande che RTCP aiuta a monitorare e mitigare è il **Jitter** (la variazione del ritardo o tremolio).

Immagina un server che invia un flusso audio spedendo un pacchetto esattamente ogni 10 millisecondi, con la precisione di un metronomo. A causa del traffico caotico sui router, questi pacchetti non arriveranno mai a destinazione con la stessa cadenza perfetta. Alcuni subiranno un ritardo di 12 ms, altri di 15 ms, altri arriveranno quasi accavallati. Questa continua variazione nei tempi di arrivo è il Jitter.

Se il ricevitore tentasse di riprodurre l'audio istantaneamente non appena un pacchetto arriva, il risultato sarebbe inascoltabile: la voce subirebbe continue accelerazioni, rallentamenti e micro-interruzioni.

La soluzione universale per colmare questo problema è l'utilizzo di un **Buffer di Jitter**. Il trucco consiste nel ritardare intenzionalmente l'inizio della riproduzione. Quando arriva il primo pacchetto, l'applicazione non lo riproduce subito, ma lo salva nel buffer e attende un certo periodo di tempo prefissato. Questa attesa permette ai pacchetti successivi, anche se in ritardo, di accumularsi in modo sicuro. Terminato il tempo di attesa, l'applicazione inizia a estrarre i pacchetti dal buffer a un ritmo perfettamente costante, garantendo all'utente una rappresentazione audiovisiva fluida e continua.

![[Pasted image 20260612115910.png]]

Il momento esatto in cui l'applicazione inizia a estrarre i dati dal buffer prende il nome di **Playback point** (Punto di riproduzione).

Scegliere il giusto Playback point è un gioco di delicati equilibri e dipende fortemente dall'entità del Jitter, come mostrano i grafici a campana:
![[Pasted image 20260612120013.png]]

- **Jitter Basso (curva stretta):** I pacchetti arrivano quasi tutti con un ritardo simile. Il Playback point può essere impostato molto vicino al tempo di arrivo. L'utente percepirà la comunicazione in tempo reale (bassa latenza).
    
- **Jitter Alto (curva larga):** I ritardi sono molto altalenanti. Per poter catturare il 99% dei segmenti ed evitare interruzioni, il Playback point deve essere spinto abbondantemente in avanti, creando un tempo di attesa molto lungo. Questo meccanismo di accumulo prolungato è il motivo per cui nelle classiche trasmissioni televisive via satellite, o nei collegamenti dei telegiornali intercontinentali, si nota quel fastidioso _delay_ di un paio di secondi prima che l'interlocutore risponda.
    

Se un pacchetto subisce un ritardo eccezionale e arriva quando il suo momento di riproduzione è ormai passato (come il pacchetto numero 8 nel diagramma dei tempi), l'applicazione non può fare altro che scartarlo e perderlo definitivamente. La sequenza temporale non perdona.

Le applicazioni moderne misurano costantemente il Jitter calcolando la differenza tra i timestamp RTP (quando il pacchetto è partito) e il tempo effettivo di arrivo. Grazie a queste misurazioni, i software **adattano dinamicamente il loro Playback point durante l'esecuzione**. Se la rete peggiora, aumentano il buffer (aumentando il ritardo per l'utente, ma salvando la fluidità); se la rete migliora, riducono il buffer. Se questo adattamento non viene fatto correttamente, l'utente subirà fastidiosi artefatti visivi o fastidiose interruzioni audio.


## TCP (Transmission Control Protocol) RFC 793, 1122 e 1323 


Il Transmission Control Protocol (TCP) è di gran lunga il protocollo di trasporto più utilizzato su Internet. Tutte le principali funzionalità di rete e le primitive fondamentali che permettono al web di esistere si appoggiano a lui.

Il suo compito inizia ricevendo i dati puri dal livello Application. Poiché questi dati possono essere enormi, il TCP li deve frammentare e inserire all'interno di segmenti (le TPDU). La dimensione massima teorica di un segmento TCP è di 64 Kb, ma nella pratica quotidiana si utilizza tipicamente una dimensione di 1500 byte per adattarsi perfettamente al limite fisico imposto dalle reti Ethernet sottostanti.

Una volta creato il segmento, il TCP lo consegna al livello di rete per la spedizione, ma ne conserva una copia nel proprio buffer locale. Se la rete perde il pacchetto o si verificano errori, il TCP utilizza questa copia per effettuare una ritrasmissione automatica. Solo quando riceve la conferma di corretta ricezione dall'altra parte, il buffer viene svuotato, liberando spazio per elaborare il segmento successivo.

Sul fronte opposto, il TCP ricevente svolge un lavoro speculare e altrettanto vitale. Accoglie i segmenti dal livello di rete, i quali spesso arrivano in disordine o addirittura duplicati a causa dei percorsi caotici di Internet. Il protocollo li riordina scrupolosamente: elimina i doppioni, attende i frammenti mancanti per tappare i "buchi" e, solo quando la sequenza numerica è perfetta, consegna i dati ordinati al livello applicativo superiore.

L'obiettivo ingegneristico del TCP è proprio questo: fornire un flusso di dati assolutamente affidabile partendo da una rete intrinsecamente inaffidabile come quella IP. Offre inoltre un servizio full-duplex, permettendo la trasmissione simultanea in entrambe le direzioni, ed è dotato di raffinati meccanismi per il controllo del flusso dei dati.

Per poter instaurare questa comunicazione, si crea una connessione logica identificata da punti di accesso chiamati socket (che costituiscono i TSAP del TCP). Un socket number non è altro che l'unione matematica di due elementi: l'Indirizzo IP della macchina (a 32 bit) e il Numero di Porta del servizio (a 16 bit). La formula è quindi semplicemente: **Socket number = IP address : Port Number**.

Il campo della porta, essendo a 16 bit, offre esattamente 65535 combinazioni possibili. È impossibile e inutile tenere attive decine di migliaia di porte contemporaneamente, ma alcune sono essenziali per il funzionamento della rete. Quasi tutti i servizi standard risiedono sotto la soglia della porta 1024. Questo blocco riservato prende il nome di **Well-known ports** (porte ben note). Le più famose, che rappresentano l'ossatura di Internet, includono la 20 e 21 per il trasferimento file (FTP), la 22 per l'accesso remoto sicuro (SSH), la 25 per la posta elettronica (SMTP), e ovviamente la 80 e la 443 per la navigazione web (HTTP e HTTPS).
![[Pasted image 20260612120807.png]]

Le connessioni TCP sono rigorosamente point-to-point (da un singolo punto a un altro singolo punto) e ogni specifica sessione è identificata in modo univoco da una **coppia di socket number** (uno all'estremità sorgente e uno all'estremità destinazione). Grazie a questa identificazione a coppie, è perfettamente normale che su un singolo computer ci siano più connessioni distinte che utilizzano localmente lo stesso socket number; ad esempio, un server web riesce a gestire migliaia di visitatori contemporaneamente usando sempre e solo la sua porta 80 locale, distinguendoli in base all'IP e alla porta di provenienza di ciascuno.

Infine, esiste un meccanismo per gestire le emergenze. Se c'è la necessità di interrompere bruscamente una computazione remota già avviata (l'equivalente di premere la combinazione CTRL-C sulla tastiera durante una sessione di emulazione terminale), il TCP permette di inserire nel segmento un **flag URGENT**. Questo segnale indica al ricevitore di ignorare le code e le attese standard, processando quel dato specifico con la massima priorità per fermare l'operazione in corso il più velocemente possibile.



#### panoramica del protocollo TCP

Una delle caratteristiche più distintive del TCP è che non si limita a numerare i segmenti interi (es. pacchetto 1, pacchetto 2), ma assegna un **proprio numero di sequenza a 32 bit a ogni singolo byte trasmesso**. Essendo un campo a 32 bit, ci sono oltre 4 miliardi di numeri a disposizione. In passato, con le vecchie connessioni lente, ci volevano ore per consumare tutti questi numeri e far ripartire il conteggio da zero. Oggi, con le connessioni in fibra ottica, questi numeri di sequenza vengono bruciati e riciclati molto rapidamente. Questi numeri sono essenziali perché indicano in ogni istante l'esatta posizione della _finestra scorrevole_ e permettono al ricevitore di confermare esattamente quale porzione di dati ha ricevuto.

Quando il TCP prepara i dati per la spedizione, crea un segmento composto da due parti:

- Un'**intestazione fissa di 20 byte** (il minimo sindacale per contenere le porte, i numeri di sequenza e i flag di controllo), a cui si possono aggiungere dei campi opzionali.
- Seguita da **zero o più byte di dati** (il payload). È possibile avere zero byte di dati se il pacchetto serve solo a trasportare un ACK di controllo.

Chi decide quanto fare grande il pacchetto? Il software TCP cerca di raggruppare i dati in modo efficiente, ma deve scontrarsi con i limiti fisici della rete, rappresentati dalla **MTU (Maximum Transfer Unit)**. L'MTU è la dimensione massima che un pacchetto può avere per attraversare un cavo senza essere "spezzettato". Se un segmento TCP è troppo grande e incontra un router con un'MTU più piccola lungo il suo percorso, subirà una **frammentazione**. In ambito di reti, la frammentazione è un'operazione costosa in termini di tempo ed elaborazione, che abbassa drasticamente le prestazioni generali. Per questo il TCP cerca sempre di calcolare preventivamente la dimensione ideale per evitarla.

Il protocollo base che governa questo flusso è la **finestra scorrevole con dimensione dinamica**, che sfrutta una logica di tipo _go-back-n con timeout_.
Il ciclo di vita di una trasmissione sicura funziona così:

1. Il mittente invia un segmento e, nello stesso identico istante, fa partire un cronometro interno (**Timer**).
2. Il segmento viaggia, arriva a destinazione e il ricevitore lo elabora.
3. Il ricevitore risponde inviando indietro un _acknowledgment_ (ACK). Questo ACK è intelligentissimo perché contiene due informazioni cruciali per il mittente:
    - Il **numero di sequenza successivo** che si aspetta di ricevere (in pratica dice: "Ho ricevuto tutto fino al byte 1000, ora mandami il 1001").
    - La **dimensione della finestra disponibile**, ovvero quanto spazio libero gli è rimasto nel suo buffer per accogliere nuovi dati. In questo modo la finestra è _dinamica_: se il PC ricevente è sovraccarico, ridurrà questo numero costringendo il mittente a rallentare.
        
4. **La regola d'oro del ripristino:** Se il timer del mittente scade prima di aver ricevuto questo prezioso ACK di ritorno (perché il pacchetto originale o l'ACK stesso si sono persi nel traffico), il mittente taglia la testa al toro e **ritrasmette immediatamente il segmento**.




### Header di un pacchetto TCP


A differenza del leggerissimo header UDP di soli 8 byte, l'intestazione TCP ha una dimensione fissa di base di **20 byte**, divisa in campi estremamente specifici.

![[Pasted image 20260612120715.png]]

I primi campi identificano chi parla e a che punto della conversazione ci si trova:

- **Source Port e Destination Port (16 bit ciascuno):** Identificano le porte delle applicazioni mittente e destinatario.
    
- **Sequence Number (32 bit):** Come abbiamo visto, numera il primo byte di dati trasportato in questo specifico segmento, garantendo il riordino.
    
- **Acknowledgement Number (32 bit):** Questo è cruciale. L'ACK del TCP è **cumulativo** e indica sempre il **successivo byte previsto**, non l'ultimo ricevuto. Se un computer riceve perfettamente tutti i byte da 0 a 1000, inserirà in questo campo il numero 1001. Significa: _"Ho ricevuto tutto fino a 1000 senza buchi, ora sto aspettando il 1001"_.

Subito dopo la lunghezza dell'intestazione, troviamo una sequenza di bit singoli (chiamati **Flag**). Sono interruttori logici (accesi a 1 o spenti a 0) che definiscono lo scopo esatto di quel segmento e guidano la Macchina a Stati Finiti:

- **CWR ed ECE:** Lavorano in coppia per gestire la congestione di rete (ECN). L'ECE segnala al mittente di rallentare perché i router si stanno intasando, mentre il CWR è la risposta del mittente che conferma di aver ridotto la sua finestra di trasmissione.
    
- **URG (Urgent):** Se impostato a 1, dice al ricevitore di guardare il campo _Urgent Pointer_, il quale indica a quale offset (a quanti byte di distanza) si trovano dei dati urgenti da elaborare immediatamente scavalcando la coda (es. il comando CTRL-C per interrompere un processo).
    
- **ACK:** Se vale 1, significa che il campo _Acknowledgement Number_ contiene un valore valido e deve essere letto. Nella pratica, a parte il primissimo messaggio di apertura, questo bit è sempre a 1.
    
- **PSH (Push):** È un ordine perentorio per il ricevitore: _"Non parcheggiare questi dati nel tuo buffer in attesa che si riempia, consegnali immediatamente all'applicazione soprastante!"_.
    
- **RST (Reset):** È il pulsante antipanico. Viene usato per abbattere istantaneamente una connessione diventata confusa, o per rifiutare categoricamente un tentativo di connessione non valido. Se arriva un RST, c'è un problema grave.
    
- **SYN (Synchronize):** È il bit usato esclusivamente per instaurare la connessione (il famoso Three-Way Handshake).
    
    - Un segmento con `SYN = 1` e `ACK = 0` è la **Richiesta di Connessione**.
        
    - Un segmento con `SYN = 1` e `ACK = 1` è la **Connessione Accettata**.
        
- **FIN (Finish):** Segnala il rilascio della connessione. Indica che il mittente ha finito i dati da trasmettere. La connessione può comunque rimanere "aperta a metà" per continuare a ricevere dati dall'altra parte.

Il campo **Window Size (16 bit)** è il cuore del controllo di flusso. Indica esattamente la quantità di byte che il mittente può inviare prima di doversi fermare ad aspettare un nuovo ACK. Il destinatario usa questo campo per comunicare in tempo reale quanto spazio libero gli è rimasto nel buffer. Il caso estremo è la **finestra di dimensione zero (Zero Window)**: se il ricevitore è ingolfato, invia un pacchetto con Window Size = 0. Il mittente è obbligato a congelare l'invio dei dati all'istante, finché non riceverà un nuovo pacchetto con una finestra allargata.

L'intestazione si chiude con il classico **Checksum** (16 bit) per verificare l'integrità dei dati contro le corruzioni fisiche, l'**Urgent Pointer**, e uno spazio per eventuali **Opzioni** aggiuntive prima di arrivare al _Payload_ (i Dati veri e propri).


### Instaurazione di una connessione TCP (Three-Way Handshake)

Tutto inizia con un server in attesa passiva. Il server esegue le primitive `LISTEN` e `ACCEPT`, mettendosi in ascolto su una porta specifica (es. la porta 80 per il web). Quando un client desidera connettersi, esegue una `CONNECT`. Sotto il cofano, questa azione genera il primo pacchetto TCP:

![[Pasted image 20260612122105.png]]

1. Il client invia un segmento con il bit **SYN a 1** e l'**ACK a 0** (poiché non c'è ancora nulla da confermare). Inserisce un proprio numero di sequenza iniziale x. Questa è la _Connection Request_.
    
2. Il pacchetto arriva al server. Qui avviene un controllo vitale: il server verifica se c'è un'applicazione effettivamente in ascolto su quella _Destination Port_.
    
    - Se la porta è chiusa, il server respinge la richiesta inviando un segmento con il bit **RST a 1** (Reset).
        
    - Se la porta è aperta, il server "aggancia" la richiesta e risponde con la _Connection Accepted_: un segmento con **SYN a 1**, **ACK a 1** (per confermare la ricezione di x, chiedendo x+1) e un proprio numero di sequenza iniziale y.
        
3. Il client riceve l'accettazione e chiude la stretta di mano inviando un ultimo segmento con **ACK a 1** (confermando la ricezione di y, chiedendo y+1). La connessione è stabilita.
    

**L'anomalia della richiesta simultanea:** Cosa succede se due computer, per una coincidenza temporale perfetta, decidono di inviarsi un pacchetto SYN a vicenda nello stesso esatto istante? I due pacchetti SYN si incrociano sulla rete. Si potrebbe pensare che vengano create due connessioni separate, ma il TCP è più intelligente. Poiché una connessione è identificata esclusivamente dalle sue estremità (la coppia esatta di Indirizzi IP e Porte), il sistema si accorge che le due richieste riguardano lo stesso canale logico. Il risultato è la creazione di **una sola connessione** e di una singola voce nella tabella delle connessioni aperte del sistema operativo.


##### **La Vulnerabilità: L'attacco SYN Flood**:
Questo elegante meccanismo a tre vie nasconde una debolezza architetturale profonda. Nel momento in cui il server riceve il primo pacchetto SYN dal client e risponde con il suo SYN+ACK, entra in uno stato di mezza-connessione (Half-Open). Per poter riconoscere il terzo e ultimo pacchetto ACK quando (e se) arriverà, il server **deve allocare una porzione della sua memoria RAM** per ricordarsi i numeri di sequenza x e y di quella specifica conversazione in sospeso.

Un malintenzionato può sfruttare questa necessità di memoria per compiere un attacco Denial of Service (DoS) chiamato **SYN Flood** (Inondazione di SYN). L'attaccante bombarda il server con migliaia di pacchetti SYN falsificati al secondo, ma si guarda bene dall'inviare mai il terzo pacchetto ACK finale. Il server alloca memoria per la prima richiesta, poi per la seconda, poi per la millesima, in attesa di risposte che non arriveranno mai. In pochissimo tempo, la tabella delle connessioni pendenti si riempie, la memoria si esaurisce e il server è costretto a ignorare le richieste di connessione dei clienti legittimi. Il server è di fatto paralizzato.

##### La soluzione: I SYN Cookie
Per difendersi da questo attacco letale senza modificare il protocollo TCP mondiale, gli ingegneri hanno inventato i **SYN Cookie**. L'obiettivo della difesa è semplice: il server deve rispondere al primo SYN _senza memorizzare assolutamente nulla_ nella propria RAM.

Ecco come funziona la magia crittografica: Quando arriva un SYN, il server non salva i dati in una tabella. Invece, prende l'Indirizzo IP del mittente, la Porta, e una "password" segreta (conosciuta solo al server) e li frulla insieme usando un **algoritmo di crittografia** (un hash). Il risultato di questa operazione matematica complessa diventa il numero di sequenza iniziale y del server. Il server impacchetta questo numero, lo spedisce al client e **se ne dimentica istantaneamente**. Memoria occupata: zero.

Se il client è un attaccante SYN Flood, la connessione muore lì e il server non ha sprecato un singolo byte di RAM. Se invece il client è legittimo, rispetterà le regole e invierà l'ultimo pacchetto ACK, che conterrà (per le regole del TCP) il numero y+1. Quando il server riceve questo ACK, prende di nuovo l'IP del client, la Porta e la sua password segreta, rifà il calcolo matematico, aggiunge 1 e controlla se il risultato coincide col numero contenuto nell'ACK. Se combaciano, il server ha la **prova matematica assoluta** che quel client aveva completato regolarmente il primo step, e instaura la connessione in totale sicurezza.


### Rilascio di una connessione TCP

Le connessioni TCP sono **full-duplex**, il che significa che i dati possono fluire simultaneamente e in modo del tutto indipendente in entrambe le direzioni. Per chiudere la comunicazione senza rischiare di tranciare i dati in volo, il protocollo tratta la disconnessione come se dovesse chiudere **due connessioni simplex indipendenti**. Non si stacca la spina all'improvviso, ma ogni lato deve dichiarare esplicitamente di aver finito il proprio lavoro.

Ecco la sequenza esatta del rilascio:

1. **La prima richiesta di chiusura:** Quando una delle due parti (ad esempio, il Client) non ha più alcun dato da trasmettere, genera e invia un segmento TCP con il **bit FIN (Finish) posto a 1**.
2. **La conferma e lo stato "Half-Close":** Il Server riceve il FIN e risponde con un normale **ACK** di conferma. In questo preciso istante, la connessione in uscita dal Client viene rilasciata. Il Client non può più inviare nuovi dati. Tuttavia, l'altra direzione rimane "pendente". Il Server potrebbe avere ancora file da finire di scaricare verso il Client, e il Client è ancora perfettamente in grado di riceverli. Questa situazione si chiama connessione "aperta a metà" (Half-Closed).
3. **La seconda richiesta di chiusura:** Quando anche il Server ha terminato definitivamente le sue operazioni di invio, innesca lo stesso identico procedimento: invia a sua volta un segmento con il **bit FIN a 1** verso il Client.
4. **La chiusura definitiva:** Il Client riceve l'ultimo FIN, risponde con un **ACK** finale e la connessione full-duplex termina definitivamente per entrambi.

Come abbiamo imparato studiando il "Paradosso dei due eserciti", l'ultimo ACK di conferma potrebbe perdersi nella rete, lasciando un host in un'attesa infinita. Per disinnescare questo pericolo, il TCP si affida a dei **Timer** di sicurezza. Nello specifico, il protocollo imposta un conto alla rovescia pari al doppio della vita massima stimata di un pacchetto nella rete. Se il timer scade senza che siano arrivate le conferme previste dalla macchina a stati finiti, la connessione viene comunque forzatamente abbattuta per liberare la memoria.


### Criterio di trasmissione a finestra scorrevole TCP

La gestione della finestra scorrevole in TCP disaccoppia due concetti fondamentali: la conferma di corretta ricezione dei dati (l'ACK) e la gestione dello spazio fisico nella memoria del ricevitore (l'allocazione del buffer).

La dimensione della finestra non è fissa, ma viene continuamente adattata attraverso un dialogo costante. Ogni volta che la destinazione invia un ACK di conferma, comunica contestualmente al mittente quanti ulteriori byte è in grado di accettare in quel preciso istante.

![[Pasted image 20260612122617.png]]

##### La Dinamica del Blocco (Finestra a 0)
Analizzando lo scambio di messaggi, emerge una dinamica cruciale legata alla velocità. Immaginiamo che il mittente scarichi dati molto velocemente (es. 2 KB alla volta) verso una macchina ricevente che ha un buffer totale di soli 4 KB ed è lenta a elaborarli. Il mittente invia i primi 2 KB, poi altri 2 KB. Il buffer del ricevente si satura istantaneamente. A questo punto, la velocità di trasmissione si dimostra superiore alla velocità di elaborazione.

Il ricevente è costretto a inviare un ACK confermando la ricezione, ma dichiara una **finestra di ricezione pari a 0 (WIN = 0)**. Questo è un segnale di stop assoluto: la macchina mittente si blocca completamente. Il mittente rimarrà bloccato finché l'applicazione sul ricevitore non deciderà di leggere i dati (svuotando il buffer) e il ricevitore non invierà un nuovo aggiornamento con una finestra maggiore di zero.

Cosa succede se questo messaggio di "sblocco" (aggiornamento della finestra) va perso nella rete? Per evitare uno stallo infinito (deadlock), il TCP prevede il **Window Probe (Pacchetto Sonda)**. Il mittente bloccato ha il diritto di inviare periodicamente un microscopico segmento di 1 byte. Questo pacchetto forza il ricevente a rispondere, annunciando nuovamente il successivo byte atteso e, soprattutto, la dimensione aggiornata della sua finestra.

##### L'Ottimizzazione del Flusso (I 4 Strumenti TCP)
Per evitare che la rete venga inondata da pacchetti minuscoli e inefficienti, il livello di trasporto utilizza quattro tecniche pratiche per gestire le finestre scorrevoli in modo intelligente:

**1. Delayed Acknowledgement (ACK Ritardati)** Se il ricevitore sta subendo una congestione, può decidere di non inviare l'ACK immediatamente, ma di ritardarlo fino a un massimo di **500 millisecondi** (un'eternità per una rete informatica). Questo ritardo studiato impedisce al mittente di inviare nuovi dati, dando all'applicazione ricevente il tempo vitale per "digerire" i dati nel buffer, liberare spazio e regolare la trasmissione.

**2. L'algoritmo di Nagle (Lato Mittente)** Se un'applicazione genera dati in frammenti piccolissimi (es. un utente che digita su una tastiera 1 byte alla volta), spedire un intero pacchetto TCP da decine di byte di intestazione per trasportare un solo byte di payload è uno spreco enorme di banda. L'algoritmo di Nagle risolve il problema: il mittente invia immediatamente il primo byte, ma **inserisce tutti i byte successivi nel buffer** finché non riceve l'ACK del primo invio. Solo a quel punto, raggruppa tutti i caratteri digitati nel frattempo e li spedisce in un unico, corposo segmento TCP.

**3. Silly Window Syndrome e la Soluzione di Clark (Lato Ricevente)** La "Sindrome della Finestra Stupida" si verifica quando il problema è sul lato del ricevitore. Se il buffer è pieno e l'applicazione legge i dati a una lentezza esasperante (es. **1 byte alla volta**), il ricevitore invierà al mittente un aggiornamento dicendo: _"Ho liberato 1 byte, la mia finestra è 1"_. Il mittente invierà 1 byte, riempiendo il buffer. L'applicazione leggerà un altro byte, generando un nuovo aggiornamento di 1 byte. Il ciclo continuerà all'infinito, paralizzando l'efficienza della rete. La **Soluzione di Clark** vieta esplicitamente questo comportamento: impedisce al ricevente di inviare un aggiornamento della finestra per 1 solo byte. Il ricevitore è obbligato a mentire (dichiarando WIN=0) e ad attendere finché non ha liberato una quantità di spazio significativa (es. metà del buffer vuoto o spazio sufficiente per un segmento massimo intero) prima di annunciare la disponibilità al mittente. Nagle e Clark lavorano in simbiosi perfetta: Nagle impedisce al mittente di inviare pacchetti piccoli, Clark impedisce al ricevente di richiederli.

**4. Cumulative Acknowledgement (ACK Cumulativo)** Come già anticipato, la rete può disordinare i pacchetti. Se il destinatario riceve i segmenti in ordine sparso (es. riceve i pacchetti 0, 1, 2, poi saltano il 3 e arrivano il 4, 5, 6, 7), memorizza tutto nel buffer ma **non conferma gli arrivi isolati**. Invia un ACK cumulativo solo fino all'ultimo byte ricevuto in sequenza ininterrotta (in questo caso, conferma tutto fino al segmento 2 incluso). Quando il mittente andrà in timeout per il segmento 3 e lo ritrasmetterà, il ricevitore lo incastrerà nel "buco" del buffer e potrà improvvisamente inviare un ACK cumulativo enorme, confermando in un colpo solo la ricezione perfetta di tutti i dati fino al segmento 7.


### Gestione del timer di TCP

Il protocollo TCP si affida a diversi **timer** per gestire correttamente il flusso dei dati. Il meccanismo centrale di questa architettura è il timer **RTO** (Retransmission Timeout), direttamente responsabile di far scattare le ritrasmissioni.

Il funzionamento pratico è scandito da logiche precise: al momento dell'invio di un segmento, parte un conto alla rovescia. Se la conferma di ricezione (l'acknowledgement) giunge a destinazione prima che questo tempo scada, il TCP provvede a fermare il cronometro. Al contrario, se l'attesa si prolunga oltre la scadenza prefissata senza alcun riscontro, il segmento viene considerato perso e spedito nuovamente, facendo ripartire il timer da zero.

Il vero dilemma ingegneristico consiste nello stabilire l'esatta durata di questo intervallo di attesa. Per risolvere la questione, si adotta una soluzione basata su un algoritmo dinamico, capace di adattare la durata del timeout in tempo reale analizzando le misurazioni continue delle prestazioni effettive della rete. Nello specifico, per ogni singola connessione viene costantemente aggiornata una variabile chiamata **SRTT**, la quale fornisce una stima accurata del tempo necessario a un pacchetto per compiere un viaggio completo di andata e ritorno, noto come **round trip time**.
##### Il Timer di Ritrasmissione (RTO - Retransmission Timeout)

È il motore pulsante dell'affidabilità del TCP. Ogni volta che il mittente invia un segmento, fa partire questo cronometro. Se l'ACK di conferma arriva prima che il timer scada, il cronometro viene fermato e azzerato. Se invece il timer scade prima dell'arrivo dell'ACK, il segmento è considerato perso e viene immediatamente ritrasmesso (e il timer riavviato).

La grande sfida ingegneristica è: **quanto deve durare questo intervallo di timeout?** Se è troppo breve, il mittente ritrasmetterà pacchetti che in realtà sono solo in leggero ritardo, intasando inutilmente la rete. Se è troppo lungo, il sistema reagirà con eccessiva lentezza a una vera perdita di dati, crollando in termini di prestazioni.

Dato che i tempi di attraversamento su Internet variano continuamente a causa del traffico, un timer fisso è inutile. La soluzione è un **algoritmo dinamico** che calcola una media mobile basata sulle misurazioni continue dei ritardi. Per ogni connessione, il TCP mantiene una variabile chiamata **SRTT (Smoothed Round Trip Time)**, ovvero la stima "ammorbidita" del tempo di andata e ritorno.

La formula matematica per aggiornare costantemente questo valore a ogni nuovo pacchetto inviato è:

$$SRTT=α⋅SRTT+(1−α)⋅R$$

Dove:

- **R** è il Round Trip Time misurato per il pacchetto appena inviato (il nuovo campione).
    
- **α** (alfa) è un fattore di perequazione (smoothing). Determina quanto peso dare allo storico passato rispetto al nuovo campione appena rilevato.
    
- **L'ottimizzazione:** Tipicamente, α viene impostato al valore di **7/8**. Questa non è una scelta casuale: usare potenze di 2 permette ai programmatori del kernel di sostituire le complesse operazioni di moltiplicazione con un semplice _scorrimento di bit_ (bit shift) a livello hardware, rendendo il calcolo istantaneo e leggerissimo per la CPU.
    

##### Il Timer di Persistenza (Persistence Timer)

Questo timer serve a prevenire uno stallo fatale (deadlock) legato alla gestione della finestra scorrevole. Immagina che il ricevente abbia il buffer pieno e invii un ACK con "Dimensione Finestra = 0". Il mittente si blocca. Poco dopo, il ricevente libera spazio e invia un aggiornamento della finestra per sbloccare la situazione, ma **questo pacchetto viene perso dalla rete**. Il risultato? Il mittente aspetta all'infinito un aggiornamento, e il ricevente aspetta all'infinito nuovi dati. Per spezzare questo stallo, il mittente usa il _timer di persistenza_. Quando scade, il mittente invia un pacchetto "sonda" (Window Probe). Il ricevente è obbligato a rispondere alla sonda comunicando la dimensione attuale della sua finestra. Se è ancora 0, il timer riparte; se è maggiore di 0, il flusso riprende.

##### Il Timer Keep Alive

È il timer del "sei ancora vivo?". Quando una connessione rimane inattiva e silenziosa per un lungo periodo, questo timer scade e spinge una delle due macchine a inviare un pacchetto di controllo per verificare se l'altra è ancora accesa e connessa. Se non si riceve alcuna risposta, la connessione viene terminata e le risorse liberate. È una funzionalità controversa: genera traffico di rete inutile e, peggio ancora, rischia di abbattere connessioni sanissime solo perché c'è stata una momentanea e temporanea interruzione fisica su un router intermedio.

##### Il Timed Wait (Il timer fantasma)

Questo è l'ultimo timer utilizzato nel ciclo di vita di una connessione. Come abbiamo visto studiando il rilascio a 4 vie, quando una connessione viene chiusa, il sistema entra nello stato `TIMED WAIT`. Questo cronometro ha una durata prestabilita pari al **doppio del tempo di vita massimo di un pacchetto**. Il suo scopo è congelare quella specifica combinazione di porte e IP, garantendo che tutti i pacchetti ritardatari o duplicati appartenenti a quella vecchia conversazione "muoiano" definitivamente nella rete prima che quel socket possa essere riutilizzato per una nuova chiamata.


### Controllo della congestione TCP

Quando la rete viene inondata da una quantità di dati superiore alla sua capacità fisica, i router intermedi iniziano a riempire i loro buffer. Se il carico non diminuisce, i buffer si saturano e i router sono costretti a scartare (distruggere) i pacchetti in arrivo. Questa è la congestione. La soluzione principale per affrontarla è una sola: i mittenti devono accorgersi del problema e **ridurre drasticamente la loro velocità di trasmissione**.

In passato, era difficile capire se un pacchetto fosse andato perso per un'interferenza elettrica sul cavo o per un router intasato. Nelle reti moderne, molto più affidabili fisicamente, la perdita di un pacchetto è quasi sempre sintomo di traffico eccessivo. Per questo motivo, gli algoritmi TCP adottano un presupposto fondamentale e insindacabile: **ogni timeout è causato da una congestione**.

##### Il Vincolo della Doppia Finestra
Come fa il mittente a sapere a che velocità trasmettere senza intasare nulla? Deve rispettare due limiti ben distinti: la memoria del computer ricevente e la capacità dei cavi di rete nel mezzo.

Per gestire questo equilibrio, il mittente mantiene attive e aggiornate **due finestre separate**:

1. La **finestra garantita dal ricevente (Receiver Window)**: indica quanto spazio libero c'è nel buffer del PC di destinazione.
    
2. La **finestra di congestione (Congestion Window)**: è una stima calcolata dinamicamente di quanta banda è attualmente libera sui router della rete.
    

La regola d'oro della trasmissione impone che il mittente possa inviare solo un numero di byte pari alla **dimensione minore tra queste due finestre**. Se il destinatario ha spazio per 32 KB, ma la rete è congestionata e può sopportare solo 4 KB, il TCP invierà 4 KB per proteggere i router. Viceversa, se la rete è libera e può viaggiare a 32 KB, ma il destinatario ha solo 8 KB di RAM libera, il TCP invierà 8 KB per non far "affogare" il ricevitore.

![[Pasted image 20260612123850.png]]

##### L'Algoritmo di Avvio Lento (Slow Start)
Mentre la finestra del ricevitore viene comunicata esplicitamente tramite l'header TCP, la capacità della rete è un mistero assoluto. Il mittente deve "tastare il terreno" per scoprirla. Lo fa utilizzando l'algoritmo di **Slow Start** (Avvio lento).

L'obiettivo dello Slow Start è aumentare la quantità di dati inviati fino a trovare il punto esatto in cui la rete inizia a congestionarsi, per poi assestarsi appena sotto quel limite.

La dinamica funziona in questo modo: Al momento della connessione, si parte con estrema cautela impostando la finestra di congestione a un valore minimo (ad esempio 1 KB). Se il pacchetto arriva a destinazione e il mittente riceve regolarmente l'ACK, significa che la rete ha retto. A questo punto, la velocità viene raddoppiata: si inviano 2 KB. Arrivano gli ACK, e si raddoppia ancora a 4 KB, poi 8 KB, 16 KB e così via.

Nonostante il nome "Avvio lento", la crescita di questo algoritmo segue in realtà un **andamento esponenziale**, utilizzando le potenze del 2. La finestra si allarga a dismisura e in pochissimo tempo satura la linea.

##### Il Crash e il Ricalcolo della Soglia
Questo raddoppio brutale continua finché la rete non ce la fa più. Raggiunto il limite fisico dei router (nel grafico dell'esempio, questo avviene quando la finestra raggiunge i 40 KB), un pacchetto viene scartato e si verifica il temuto **timeout**.

Di fronte al timeout, il TCP interviene con due azioni correttive immediate:

1. Abbassa brutalmente la finestra di congestione **riportandola al valore iniziale minimo** (1 KB). Il flusso di dati viene quasi azzerato per dare il tempo alla rete di smaltire le code.
    
2. Impara dal proprio errore impostando un limite di sicurezza per il futuro. Prende il valore in cui si è verificato il crash e lo riduce per calcolare una nuova **Soglia (Threshold)**. Nel grafico, il crash a 40 KB genera una soglia di sicurezza abbassata a 20 KB.
    

Da questo momento, il processo riparte da 1 KB e raddoppia di nuovo velocemente, ma **solo fino al raggiungimento della nuova soglia** di 20 KB. Superata questa soglia sicura, l'algoritmo abbandonerà la crescita esponenziale per passare a un aumento molto più cauto e lineare, evitando di causare immediatamente un nuovo disastro.