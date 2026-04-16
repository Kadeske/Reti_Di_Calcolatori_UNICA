### 1. Concetti Introduttivi

- **Reti di calcolatori:** Un insieme di computer distinti connessi tra loro da una singola tecnologia, il cui scopo principale è la condivisione di risorse, informazioni ed elaborazione.
    
- **Sistema distribuito:** Un software (o componente hardware) che gira su una rete di computer. I componenti comunicano scambiandosi messaggi per coordinare le proprie azioni, e agli occhi dell'utente tutto appare come un sistema unico.
    
- **Digital divide:** La mancanza o carenza di un metodo di connettività affidabile o di accesso alla rete in un determinato luogo.
    
- **Pacchetto:** Le informazioni vengono divise in blocchi più piccoli chiamati "pacchetti", che viaggiano sui canali di comunicazione per facilitare e parallelizzare la trasmissione.
    

---

### 2. Caratterizzazione delle Reti

Per Tecnologia Trasmissiva

- **Point-to-point (Punto a Punto):** Canale trasmissivo riservato tra due host (unicasting). I pacchetti possono attraversare nodi intermedi, richiedendo l'uso di algoritmi di "routing" per trovare il percorso migliore.
    
- **Broadcast:** Canale di comunicazione condiviso tra tutti i nodi. I pacchetti sono ricevuti da tutti, ma solo il nodo con l'indirizzo corrispondente li legge (gli altri li scartano). Richiede meccanismi per gestire le collisioni. Rientrano in questo gruppo:
    ![[Pasted image 20260415121327.png]]
    - _Broadcasting:_ Messaggio indirizzato a tutti i dispositivi della rete.
        
    - _Multicasting:_ Messaggio rivolto solo ad un gruppo specifico di destinatari.
        
    - _Unicasting (in rete broadcast):_ Messaggio inviato nel mezzo condiviso, ma indirizzato a un singolo destinatario.
	
        

Per Topologia La topologia è il modello geometrico dei collegamenti. Parametri per sceglierla: numero di nodi, canali trasmissivi e ridondanza.

- **Bus:**
    
    - _Pro:_ Semplice da realizzare e poco costosa.
        
    - _Contro:_ Facile intercettare le comunicazioni altrui, elevato traffico, sensibile ai guasti e difficile isolarli.
        
- **Anello:**
    
    - _Pro:_ Banda e tempi di attesa deterministici, non necessita amplificatori di segnale.
        
    - _Contro:_ Scarsamente diffusa, un guasto in un punto può far cadere l'affidabilità o l'intera rete.
        
- **Stella:**
    
    - _Pro:_ Componenti economici e diffusissimi, nessun blocco della rete se un host si scollega o guasta, comunicazioni sicure/isolate (se si usano gli switch).
        
    - _Contro:_ Serve molto cavo, blocco completo se il nodo centrale (hub o switch) si guasta.
        

**Per Scala di Interconnessione**
![[Pasted image 20260415121647.png]]
- **PAN (Personal Area Network):** Estensione massima di un metro (es. Bluetooth, dispositivi indossabili). Usa logica _master-slave_.
- **LAN (Local Area Network):** Rete per stanza/edificio (fino a 2km). Di solito usa broadcast. Metodi di _allocazione del canale_:
    
    - _Statica:_ Il tempo è diviso in slot discreti; se un host non trasmette, il suo slot viene sprecato.
    - _Dinamica:_ Il tempo/canale viene assegnato solo a chi richiede attivamente di trasmettere.
        
- **MAN (Metropolitan Area Network):** Estensione urbana. Solitamente basata su 2 bus broadcast(802.6).
- **WAN (Wide Area Network):** Estensione nazione/continente. Gli host sono collegati tramite una sottorete (subnet) formata da router e linee trasmissive. Non si ha mai una rete collettiva ma tante sottoreti composte da router connesse tra loro.
- **WLAN:** LAN senza fili.
- **Internetworks:** rete che si interpone tra due reti diverse tra loro. Permetta la comunicazione tra reti diverse attraverso un gateway.
    

---

### 3. Gli Standard IEEE 802

Dedicati a LAN e MAN con pacchetti a lunghezza variabile.

- **[[IEEE 802.3 -> CSMA-CD]]** I nodi ascoltano il canale (Carrier Sense). Mezzo condiviso (Multiple Access). Se due trasmettono insieme (Collision Detection), si attende un tempo casuale e si ritenta.
    
- **[[IEEE 802.4 -> Token Bus]]:** I nodi sono cablati a bus fisico, ma lavorano ad anello logico in cui circola un _Token_. Solo chi possiede il token può trasmettere.
    
- **[[IEEE 802.5 -> Token Ring]]:** Connessione sia fisica che logica ad anello. Il token circola, la stazione lo prende, invia il pacchetto, e quando questo finisce il giro rimuove il pacchetto e rilascia il token.
    
- **[[IEEE 802.6 -> DQBD]]:** Standard usato in passato per MAN ad altissima velocità.
    
- **[[IEEE 802.11 -> WLAN]]** LAN wireless. Usa un Access Point o una rete ad-hoc diretta. Frequenze e bande varie (a, b, g, n).
    

---

### 4. Architettura, Livelli e Funzionamento

- **Perché usare i livelli:** Serve a ridurre la complessità del problema di networking. Ogni livello ha funzionalità precise e ben delimitate.
    
- **[[Gerarchie di protocolli]]:** I nodi non comunicano tutti in blocco, ma il "livello N" di una macchina parla virtualmente con il "livello N" di un'altra. Le regole di questa conversazione virtuale sono i protocolli.

	- **Interfaccia:** Dato che la comunicazione in realtà avviene tramite mezzo fisico, tra livelli adiacenti c'è un *interfaccia* che definisce le operazioni e i servizi offerti al livello superiore.
    
	- **Architettura di rete:** L'insieme di tutti i livelli e dei protocolli utilizzati.
    
	- **Pila di protocolli:** La serie concreta di protocolli attivi usati livello per livello su una macchina.
    
- **[[Invio di un messaggio (come funziona fisicamente)]]:** All'Host 1, il messaggio scende i livelli. Ogni livello aggiunge le sue informazioni operative (Header) e talvolta suddivide il pacchetto. Raggiunto il livello fisico, i bit viaggiano sul cavo. Arrivati all'Host 2, i livelli processano il proprio Header e lo scartano, riassemblando i dati puliti fino all'applicazione.
    
--- 

-  **Progettazione dei Livelli:** Ogni strato fa solo il suo compito, fornisce tolleranza di guasto (es. controlli di errore ripetuti) per garantire che i livelli superiori ricevano dati intatti.
**Componenti e Compiti all'interno dei Livelli:**

- **[[Indirizzamento]]:**  *Meccanismo essenziale utilizzato da ogni livello di una rete al fine di identificare in modo specifico le sorgenti e le destinazioni delle comunicazioni*. I **SAP (Service Access Point)** sono i punti (gli indirizzi) in cui uno strato offre un servizio a quello superiore (es. porte per il Trasporto, IP per la Rete, MAC per il livello Datalink).
    
- **Regole di trasferimento:** determinano in quale senso possono viaggiare i dati.
	- **Simplex:** Comunicazione in una sola direzione (e in un unico canale).
    
    - _Half-duplex:_ Bidirezionale ma una sola macchina alla volta. Ad ogni lato viene dato un tempo in cui poter utilizzare il canale.
        
    - _Duplex:_ Bidirezionale contemporaneo. (Viene suddiviso in due parti)
        
- **[[Controllo d'errore]]:** Verifica la correttezza dei bit. Può agire per _Rilevamento e Ritrasmissione_ (se l'esito del calcolo indica un errore, si chiede di rimandare) oppure _Rilevamento e Correzione_ (tramite codifiche come Hamming per correggere errori lievi direttamente).
    
- **Controllo della sequenza:** Meccanismo che consente al destinatario di verificare e ricostruire i dati nell’ordine esatto in cui sono stati inviati dal mittente.
  A ciascun dato viene assegnata un etichetta indicante l'ordine originale.
	- con comunicazioni **orientate alla connessione** l'ordine di arrivo dei dati è garantito.
	- con comunicazioni **senza connessione** i dati potrebbero arrivare in maniera non sequenziale.
    
- **[[Controllo di flusso]]:** Evita che un mittente "veloce" anneghi e ingolfi un destinatario "lento". Regola la frequenza di invio o attende conferme (Ack).
    
- **Multiplexing/Demultiplexing:** Disassembla pacchetti troppo grandi per i mezzi fisici e riassembla pacchetti a destinazione; o accorpa flussi troppo leggeri per usarli in una sola connessione ad alta capacità.
    
- **Routing:** Scelta del miglior percorso, ad ogni istante, in una rete magliata o tramite nodi (router) intermedi.
	- **Router**: dispositivi che implementano solo i primi 3 livelli di una rete (fino al livello di rete).
	- **Algoritmo di routing**: ha l'obiettivo di trovare il miglior persorso.
    

---

### 5. [[Interfacce e Servizi]]

- **Passaggio dei Servizi:** L'informazione _n-PDU_ in un livello viene calata al livello $(n-1)$ tramite un'interfaccia (SAP). Diventa _$(n-1)$-SDU_, le viene aggiunto l'Header e si trasforma nella _$(n-1)$-PDU_.

- **[[Servizi orientati alla connessione e servizi privi di connessione]]:**
	- **Servizi orientati alla connessione:** Ordine dei dati garantito. Funziona in 3 stadi: instaurazione, trasferimento, rilascio (Es. telefonata, TCP).
	    
	- **Servizi privi di connessione (Datagramma):** Nessun canale precostituito, il percorso non è garantito e l'ordine d'arrivo nemmeno. Ogni pacchetto viaggia per conto suo. (Es. posta, UDP) .
    
- **[[Quality of Service]](QoS):** Determina i parametri di garanzia (affidabilità, ordine, latenza, banda). Molto costosa in termini di tempo se si vuole affidabilità al 100%.
    
- **[[Primitive]] (Routine di servizio):** Chiamate fondamentali, per es.: LISTEN (attesa passiva), CONNECT (chiama attivamente l'altro host), RECEIVE (riceve), SEND (invia), DISCONNECT (chiude connessione).
    
- **Relazione Servizi-Protocolli:** Sono disaccoppiati. 
	- Il _Servizio_ definisce le funzionalità offerte allo strato superiore (l'interfaccia). 
	- Il _Protocollo_ definisce le regole con cui entità equivalenti comunicano tra calcolatori diversi per implementare quel servizio.
	- L'*interfaccia* definisce le operazioni elementari e i servizi che lo strato inferiore offre a quello superiore.
    Le entità possono modificare o sostituire i protocolli a patto di mantenere lo stesso tipo di servizio.

---

### 6. Modelli di Riferimento

**[[Modello ISO-OSI (De jure)]]** Sette livelli concettuali standardizzati.

1. **Livello Fisico:** Invia i singoli bit sul canale (si occupa di cavi, segnali, voltaggi).
    
2. **Livello di Collegamento (Data Link):** Crea i Frame, calcola le sum e gli ack (es. schede di rete). Assicura il trasferimento tra nodi adiacenti.
    
3. **Livello di Rete:** Ruolo del routing, instradamento pacchetti da sorgente a destinazione ed evitare congestione.
    
4. **Livello di Trasporto:** Spezza i dati, ne assicura l'arrivo creando comunicazioni end-to-end perfette bilanciando velocità.
    
5. **Livello di Sessione:** Gestisce e sincronizza il dialogo (chi parla, turni, punti di ripristino per crash).
    
6. **Livello di Presentazione:** Gestisce formati, sintassi, codifica dei caratteri.
    
7. **Livello Applicazione:** Protocolli per software utente e l'interfaccia finale (es. visualizzazione risultato web).
    

**[[Modello TCP-IP (De facto)]]l** Quattro livelli molto più flessibili, creati per unire reti eterogenee (Internet).

1. **Livello Link:** Copre il ruolo dei livelli Fisico e Collegamento Dati dell'OSI.
    
2. **Livello Internet:** Equivalente al livello Rete. Ruolo: spedire il pacchetto (IP) in modo che viaggi autonomamente.
    
3. **Livello Trasporto:** Permette comunicazioni host-to-host. Usa TCP (affidabile e con connessione) o UDP (inaffidabile e veloce).
    
4. **Livello Applicazione:** Accorpa Applicazione, Presentazione e Sessione dell'OSI.
    

**Confronto tra ISO-OSI e TCP/IP (Punti chiave)**
Il modello TCP/IP è, ingenerale, più flessible.
![[Pasted image 20260415163051.png]]
![[Pasted image 20260415163130.png]]

---

### 7. Esempi di Reti

- **[[ARPANET]]:** Prima rete a pacchetto basata sui router (chiamati IMP). Obiettivo: resistere a guerre nucleari per non far cadere il sistema.
    
- **[[X.25]]** Rete europea degli anni 70 orientata alla connessione con un fortissimo controllo errori nodo per nodo. Robusta ma con alta latenza.
    
- **[[Frame Relay]]:** Erede dell'X.25. Usa connessioni virtuali per LAN distanti. Non fa controllo d'errore (scarta i pacchetti corrotti per guadagnare altissime velocità) e non ha livello di rete.
    
- **[[ATM]]:** Rete basata sulla "commutazione a celle" fisse (48 byte dati + 5 indirizzamento) a grandissima velocità per fonia, video e dati. Implementata specialmente nelle dorsali telefoniche.
    
- **IEEE 802.11 (WLAN):** Il Wi-Fi moderno. Le stazioni si servono di un Access Point che si collega a internet per far viaggiare pacchetti wireless.
    
- **[[RFID]]:** Sistemi per identificare oggetti a onde radio: composti da lettore (Reader) e tag (Etichette). _RFID attivi_ hanno una batteria, _RFID passivi_ no (vengono alimentati dal campo elettromagnetico del lettore).
    

---

### 8. Standardizzazione delle Reti

La **standardizzazione** è il processo fondamentale che permette a dispositivi prodotti da aziende diverse (come un PC Dell e un router Cisco) di comunicare tra loro senza problemi. Senza standard, il mercato delle reti sarebbe frammentato in sistemi proprietari chiusi e incompatibili.

Il termine **standard** indica una norma amministrativa che regola le caratteristiche e/o il funzionamento di un bene/servizio, **è costituito tipicamente da un insieme di documenti tecnici** in cui si perviene dopo un processo di normazione o standardizzazione.

- **De Facto (dalla realtà):** Nascono per emulazione senza una delibera vera e propria di un ente, ma s'impongono perché validi o famosi (Es. TCP/IP).
    
- **De Jure (dalla legge):** Elaborati tramite comitati di enti appositi in lunghi cicli di verifica formale prima di essere rilasciati (Es. Modello OSI).
    

**Gli Enti:**
![[Pasted image 20260415164102.png]]
- **[[ITU]] (International Telecommunication Union):** Agenzia ONU. Si divide in:
    
    - _ITU-R:_ Radio (assegna lo spettro radio e le orbite satellitari mondiali).
        
    - _ITU-T:_ Telecomunicazioni (linee, dati).
        
    - _ITU-D:_ Sviluppo per combattere il digital divide globale.
        
- **[[ISO]] (International Standard Organization):** Il colosso che unisce enti nazionali di quasi 160 paesi. Regola praticamente tutti gli ambiti tecnologici e manufatturieri.
    
- **[[IEEE]]:** Organizzazione per l'Ingegneria Elettrica e dei Computer. Si divide in vari Working Group (es. 802.1 architetture, 802.3 Ethernet, 802.11 WiFi, ecc.).
    
- **[[IAB]] (Internet Architecture Board):** Gestisce la supervisione e la ricerca del mondo Internet/TCP-IP.




--- 
Parte 2

# Livello fisico

Il livello fisico ha un solo e unico scopo: **trasmettere bit grezzi (0 e 1) da un nodo all'altro attraverso un canale di comunicazione**. Non sa cosa stia trasmettendo (se sia un video, un'email o un virus), si preoccupa solo dei voltaggi, della luce o delle onde radio necessarie per far arrivare il segnale.

### 1. Basi Teoriche e Segnali

- **Analisi di Fourier:** Dimostra matematicamente che qualsiasi segnale periodico (come un'onda quadra che rappresenta i bit) può essere scomposto in una somma infinita di onde sinusoidali (armoniche) di frequenze diverse.
    
- **[[Segnali a larghezza di banda limitata]]:** I mezzi trasmissivi reali non possono trasportare frequenze infinite. Tagliare le frequenze alte "arrotonda" il segnale, mentre le **frequenze più basse** trasportano la maggior parte dell'energia. Se il canale taglia le frequenze basse, il segnale si distrugge e diventa illeggibile.
    
- **Cos'è la Banda:**
    
    - _Analogica (Hertz - Hz):_ L'intervallo di frequenze che il cavo riesce a far passare senza attenuarle troppo (è una proprietà fisica del cavo).
        
    - _Digitale (Bit per second - bps):_ La quantità di bit trasferiti nell'unità di tempo (velocità).
        
    - _Regola d'oro:_ Una banda analogica più ampia permette di far passare più armoniche. Più armoniche passano, meno il segnale si distorce, e quindi possiamo inviare i bit più velocemente (maggiore banda digitale).
        
- **Limiti Teorici del Canale:**
    
    - **Teorema di Nyquist (Canale Ideale senza rumore):** 
    - Nyquist dimostrò che un segnale analogico, trasmesso lungo un canale dotato di ampiezza di banda pari a H, può essere ricostruito mediante una campionatura effettuata 2H volte per secondo.Definisce la capacità massima $C$ di un canale perfetto:
        
        $$\text{maxDataRate} = 2H \log_2(V)$$
        (dove H è la banda in Hz e V è il numero di livelli discreti del segnale, es. voltaggi diversi)
        
    - **Formula di Shannon (Canale Reale con rumore):**  ci dice come riusciamo a trasferire nonostante il rumore. Considera il rumore termico ineliminabile.
        
        $$\text{maxDataRate} = H \log_2(1 + \frac{S}{N})$$
        
        (dove $S/N$ è il rapporto tra la potenza del segnale e quella del rumore). Nessun trucco ingegneristico può superare il limite di Shannon.
        

---

### 2. Mezzi di Trasmissione a fili (Wired / *Guidati*)

Sono "**guidati**" perché il segnale (corrente o luce) è costretto fisicamente a viaggiare all'interno del mezzo.

Ogni mezzo fisico è caratterizzato da:
- banda passante 
- ritardo
- costo 
- installabiltà
- manutenibilità

- **[[Doppino telefonico]] (Twisted Pair):** Due fili di rame intrecciati. L'intreccio serve a cancellare le reciproche interferenze elettromagnetiche (diafonia). Le **Categorie** (Cat 5, Cat 6, ecc.) differiscono per il numero di intrecci per centimetro: più intrecci = banda maggiore. Può essere _UTP_ (non schermato) o _STP_ (con guaina metallica per proteggere dai rumori esterni). Limite: alta attenuazione sulle lunghe distanze.
    
- **[[Cavo coassiale]]:** Ha un'anima centrale in rame, isolante, maglia metallica (schermo) e guaina esterna. Differenza dal doppino: schermatura quasi perfetta, banda molto più ampia. Usato per vecchie LAN e TV via cavo.
    
- **[[Fibra ottica]]:** Sfrutta il vetro o il silicio per trasmettere luce.
    
    - _Come funziona:_ Basata sulla **riflessione totale interna**. Se il raggio di luce colpisce il bordo del vetro con un angolo superiore a un certo "angolo critico", non esce ma rimbalza all'infinito dentro il cavo.
        
    - _Tipi:_ **Multimodale** (core largo, la luce rimbalza creando vari percorsi/modi, usata per brevi distanze); **Monomodale** (core sottilissimo, la luce viaggia dritta come un laser, usata per lunghissime distanze/dorsali oceaniche).
        
    - _Componenti:_ Sorgente (LED o Laser) $\rightarrow$ Cavo $\rightarrow$ Ricevitore (Fotodiodo che ritraduce la luce in elettricità). I bit sono semplici: c'è luce = 1, buio = 0.
        
    - _Splicing (Giunzioni):_ Connettori meccanici (perdita 10-20%), incollaggio, o fusione ottica (si fonde il vetro a caldo, perdita vicina allo 0%).
        

---

### 3. Trasmissione senza filo (Wireless)

Il segnale viaggia nello spazio libero irradiando energia dallo ***[[Spettro elettromagnetico]]***.

- **[[Onde Radio]]:** Omnidirezionali, attraversano i muri. Soffrono di interferenze e attenuazione (soprattutto per rimbalzi multipli).
    
- **[[Microonde]]:** Altamente direzionali (servono parabole allineate "a vista"). Non attraversano ostacoli solidi e sono assorbite dalla pioggia.
    
- **Onde infrarosse e millimetriche:** sono a cortissimo raggio (es. telecomandi). Eccellenti per la sicurezza locale (*non possono essere intercettate dall'esterno*) e *non disturbano altre comunicazioni*. *Non attraversano i muri*. Viaggiano a frequenze THF (tremendamente alte), nell'ordine dei Ghz. Non richiedono nessuna licenza governativa.

- **Onde luminose**: Sono segnali ottici visibili ad occhio nudo.
	- Sono **unidirezionali** e **facilmente disturbabili**
	- Richiedono **grande precisione**
	- Sono **poco utilizzate**
    
- **[[Comunicazioni satellitari]]:** Funzionano come ripetitori a microonde nel cielo.
    
    - _GEO (Geostazionari):_ ~36.000 km. Sembrano fermi nel cielo. Latenza altissima (~250ms), ma bastano 3 satelliti per coprire il mondo (es. VSAT).
        
    - _MEO (Media orbita):_ ~10.000 km. Usati per il GPS.
        
    - _LEO (Bassa orbita):_ ~500-1500 km. Latenza minima (simile alla fibra), ma ruotano velocemente, quindi serve una costellazione di decine/centinaia di satelliti interconnessi (es. Iridium, Globalstar, Starlink).
    - **VSAT (Very Small Aperture Terminal)**: 
        
    - _Wired vs Sat:_ Il satellite è insostituibile per navi, aerei o zone remote, ma la fibra vince sempre per latenza e banda nelle comunicazioni terrestri punto-punto.
        

---

### 4. Sistema Telefonico e Multiplexing

La **PSTN** (Public Switched Telephone Network) è nata per trasportare la voce analogica umana, tagliando drasticamente le frequenze sotto i 300Hz e sopra i 3400Hz.

- **Problemi fisici:** _Attenuazione_ (il segnale perde potenza viaggiando), _Distorsione_ (le frequenze diverse viaggiano a velocità diverse, deformando il segnale d'arrivo), _Rumore_ (energia elettrica indesiderata).
    
- **Modem:** Dato che la rete PSTN è fatta per segnali analogici (onde continue), i computer (digitali) usano il MOdem (MOdulatore/DEModulatore) per "travestire" i bit in suoni.
    
- **Banda Larga:** * _xDSL (es. ADSL):_ Sfrutta le frequenze alte del doppino in rame (che la voce non usa) per inviare dati. È Asimmetrica (A-DSL) perché offre più banda per scaricare che per caricare dati.
    
    - _FTTH (Fiber to the Home):_ Sostituisce il vecchio doppino portando la fibra ottica pura fino dentro casa, garantendo velocità Gigabit.
        
- **Multiplexing:** Tecniche per far viaggiare più segnali contemporaneamente sullo stesso cavo.
    
    - **FDM (Frequency Division):** Divide la banda disponibile in diverse frequenze (es. radio FM o i canali TV).
        
    - **WDM (Wavelength Division):** È l'FDM applicato alla fibra ottica. Si inviano più segnali di luce di "colori" (lunghezze d'onda) differenti contemporaneamente.
        
    - **TDM (Time Division):** I segnali si alternano nel tempo. Il canale è usato a turno per brevissime frazioni di secondo.
        
