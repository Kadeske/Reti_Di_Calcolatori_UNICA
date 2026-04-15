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
- Servizi orientati alla connessione e servizi privi di connessione

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
    

**Modello TCP/IP (De facto** Quattro livelli molto più flessibili, creati per unire reti eterogenee (Internet).

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

Gli standard garantiscono che i dispositivi di diverse aziende possano dialogare tra loro.

- **De Facto (dalla realtà):** Nascono per emulazione senza una delibera vera e propria di un ente, ma s'impongono perché validi o famosi (Es. TCP/IP).
    
- **De Jure (dalla legge):** Elaborati tramite comitati di enti appositi in lunghi cicli di verifica formale prima di essere rilasciati (Es. Modello OSI).
    

**Gli Enti:**

- **ITU (International Telecommunication Union):** Agenzia ONU. Si divide in:
    
    - _ITU-R:_ Radio (assegna lo spettro radio e le orbite satellitari mondiali).
        
    - _ITU-T:_ Telecomunicazioni (linee, dati).
        
    - _ITU-D:_ Sviluppo per combattere il digital divide globale.
        
- **ISO (International Standard Organization):** Il colosso che unisce enti nazionali di quasi 160 paesi. Regola praticamente tutti gli ambiti tecnologici e manufatturieri.
    
- **IEEE:** Organizzazione per l'Ingegneria Elettrica e dei Computer. Si divide in vari Working Group (es. 802.1 architetture, 802.3 Ethernet, 802.11 WiFi, ecc.).
    
- **IAB (Internet Architecture Board):** Gestisce la supervisione e la ricerca del mondo Internet/TCP-IP.