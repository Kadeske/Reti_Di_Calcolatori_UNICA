Parla di cambio di frequenze per evitare interferenze (non c'entra un pisellazzo ora).


### 1. Basi Teoriche della Comunicazione dei Dati

Per comprendere come i dati viaggino su un mezzo trasmissivo, è necessario partire dai principi fisici e matematici che regolano i segnali. Qualsiasi segnale può essere matematicamente scomposto e analizzato per capirne i limiti fisici durante la trasmissione.

- **Analisi di Fourier:** Qualsiasi funzione periodica può essere ottenuta sommando funzioni seno e coseno (chiamate armoniche).
    
- **Limiti fisici dei mezzi:** Nessun mezzo trasmissivo è in grado di trasmettere un segnale senza alcuna perdita di potenza. Ogni singola componente di Fourier subisce infatti attenuazioni differenti a seconda del mezzo utilizzato.
    
- **Baud vs. Bit:** Il segnale trasmesso varia in base ai cambiamenti al secondo (come variazioni di voltaggio), misurati in baud. A seconda di quanti stati diversi può assumere il segnale, un singolo baud può trasportare più bit alla volta.

La somma delle onde (o armoniche) combina i valori con un approssimarsi successivo, fino ad arrivare a dei valori determinati.
![[Pasted image 20260331151617.png]]
![[Pasted image 20260331152134.png]]
![[Pasted image 20260331152145.png]]
- **Tasso massimo per un canale senza rumore (Teorema di Nyquist):** Il massimo tasso di dati è definito dalla formula $2H \log_2 V$ bit/s, dove $H$ è la larghezza di banda e $V$ sono i livelli discreti del segnale .
    
- **Tasso massimo per un canale con rumore (Formula di Shannon):** Il numero massimo di bit/s si calcola con la formula $H \log_2(1+S/N)$, dove $S/N$ è il rapporto segnale/rumore espresso solitamente in decibel (dB) calcolato come $10 \log_{10} S/N$ .
![[Pasted image 20260331152406.png]]
    

---

### 2. Mezzi di Trasmissione Guidati: Il Rame

I cavi in rame sono stati il primo e più diffuso mezzo di comunicazione, sfruttando l'elettricità per trasportare l'informazione. Ne esistono di diverse tipologie a seconda delle necessità di isolamento e larghezza di banda.
Sono intrecciati per elidere i segnali tra loro.

**Il Doppino Telefonico (Twisted Pair)**

- È costituito da fili di rame isolati, spessi circa 1 mm.
- I fili vengono intrecciati (da qui "twisted") perché dei fili diritti si comporterebbero come l'antenna di una radio, catturando interferenze esterne.
- La larghezza di banda dipende strettamente dalla sezione del conduttore e dalla distanza tra sorgente e destinatario (legge di Joule).
- Più viene avvolto, migliore è la qualità e il costo.

![[Pasted image 20260331152633.png]]

**Il Cavo Coassiale**

- **A banda base (50 $\Omega$):** Usato per le trasmissioni digitali. Su distanze di 1 km può raggiungere velocità fino a 2 Gbps.
    
- **A larga banda (75 $\Omega$):** Usato storicamente per le trasmissioni analogiche e la TV via cavo.
	- In genere si impiegano sottocanali a 6MHz (tipico del canale TV via cavo)
- Di norma esiste una comparazione tra frequenza e velocità: ad esempio 300MHz consentono velocità di 300 Mbps.
    
- In questo cavo, gli amplificatori fanno un refresh del segnale che è monodirezionale; per questo motivo le reti coassiali richiedono o un doppio cavo (uno per trasmettere, uno per ricevere) oppure un singolo cavo gestito assegnando bande di frequenza diverse per upload e download (subsplit o midsplit) .
	- subspliti: in 5.30MHz, out 40-300MHz
	- midsplit: in 5-116MHz out 168-300MHz
    

![[Pasted image 20260331152652.png]]

Tecnica in grado di consentire molte comunicazione temporanee.
Utile per unire due centrali molto distanti tra loro.
![[Pasted image 20260331154018.png]]

---

### 3. Mezzi di Trasmissione Guidati: La Fibra Ottica

Le reti in fibra ottica utilizzano la luce per trasmettere i dati, offrendo prestazioni nettamente superiori rispetto al rame, sebbene siano limitate dalla necessità di convertire i segnali elettrici in ottici.

- **Velocità:** La velocità teorica massima per le fibre monomodali è di 100.000 Gbps (100 Tbps), ma quella reale è limitata a circa 10 Gbps a causa dei limiti di conversione dei convertitori elettro-ottici.
    
- **Principio di funzionamento:** Il segnale è costituito da impulsi di luce (luce = bit 1, assenza di luce = bit 0). È un sistema intrinsecamente unidirezionale .
![[Pasted image 20260331154423.png]]
    
- **Modi di propagazione:** A seconda di come l'angolo di incidenza e la rifrazione agiscono all'interno del mezzo, le fibre si dividono in monomodali (più performanti, fino a 100 Gbps) e multimodali.
![[Pasted image 20260331154442.png]]
    
- **Giunzioni:** Non riscalda, non è sottoposta a campi elettromagnetici, e non consuma, tuttavia i collegamenti presentano diverse perdite di luce: connettorizzate (perdita del 10-20%), giunzione meccanica (perdita del 10%), giunzione a caldo (perdita del 5-10%).
![[Pasted image 20260331154318.png]]
Sia il nucleo che il cladding sono composti da silicio, ma il materiale del nucleo è nettamente più puro.
E' rappresentato da 3 sezioni interne anche se in europa ne usiamo 8 (non vengono usate tutte e 8).

**Sorgenti Luminose**

Esistono due principali tecnologie per generare la luce nella fibra:

- **LED:** Bassa cadenza dei dati, usata per fibre multimodali a breve distanza. Ha una lunga durata, scarsa sensibilità alla temperatura e un costo basso .
    
- **Laser a semiconduttore:** Alta cadenza dei dati, usata per fibre multimodali o monomodali a lunga distanza. Ha una breve durata, è sensibile alla temperatura e ha un costo alto.

Quali sono le principali differenze?
    ![[Pasted image 20260331155052.png]]

Interfacce:
- Passive (non interrompono il circuito)
	- trasmissione con led o laser, ricezione con fotodiodo
- attive (possono interrompere il circuito)
	- ingresso di rigenerazione e reinvio
![[Pasted image 20260331155347.png]]


#### Fibra multimodo e monomodo
![[Pasted image 20260331155500.png]]

#### Attenuazione della luce
Posso utilizzare solamente delle "finestre" di luce rappresentate nello schema.

![[Pasted image 20260331154242.png]]

---

### 4. Trasmissione Senza Fili (Wireless)

Quando non è possibile stendere cavi fisici, l'informazione viene fatta viaggiare attraverso lo spazio libero sfruttando le onde elettromagnetiche.

- **Principi Base:** Gli elettroni in movimento creano onde. La frequenza ($f$) è il numero di oscillazioni al secondo, mentre la lunghezza d'onda ($\lambda$) è la distanza tra due massimi consecutivi . Nel vuoto, tutte viaggiano alla velocità della luce ($c = 3 \times 10^8 m/s$) secondo l'equazione $\lambda f = c$.
	- Definizioni: 
		- **Spettro elettromagnetico**: elettroni in movimento
		- **Frequenza** (f): numero di oscillazioni al secondo in un'onda elettromagnetica (Hz)
		- **lunghezza d'onda** (l): distanza tra due massimi consecutivi
    
- **Onde Radio:** Hanno una grande facilità di generazione e diffusione, e sono onnidirezionali. Le basse frequenze seguono la curvatura terrestre ma subiscono un forte decadimento di potenza, mentre le alte frequenze rimbalzano sulla ionosfera e sugli edifici .
    
- **Microonde (100 MHz - 10 GHz):** Sono monodirezionali e richiedono un forte allineamento tra trasmettitore e ricevitore . Hanno limiti nell'attraversamento degli edifici e sono soggette a sfasamenti o perdite di segnale (fading), richiedendo riallocazione o algoritmi specifici se piove.
    
- **Onde Infrarosse e Millimetriche:** Lavorano nell'ordine dei GHz, sono monodirezionali e non attraversano oggetti solidi, limitandone l'uso agli ambienti interni (es. telecomandi) .
    
- **Onde Luminose (Laser):** Monodirezionali a vista, e perciò fortemente limitate da agenti atmosferici, calore o turbolenze dell'aria .
    

![[Pasted image 20260331160028.png]]

**Comunicazioni radio**
![[Pasted image 20260331160712.png]]
**Comuniczioni microonde**
![[Pasted image 20260331160759.png]]

**Onde infrarosse e millimetriche**
E' nell'ordine dei GHz, viene utilizzato per telecomandi ed elettrodomestici.
Utilizza delle onde monodirezionali (un ripetitore e un ricevitore) e non trapassa gli oggetti solidi.

**Trasmissione a onde luminose**
E' un laser monodirezionale 'a vista'. E' limitato da agenti atmosferici.
![[Pasted image 20260331161038.png]]

**Comunicazioni Satellitari**

- **GEO (Satelliti geostazionari):** Orbitano a 35.000 km, ne bastano 3 per coprire la Terra ma hanno un'elevata latenza (270 ms) .
	- Se ne mandano pochi in orbita perchè costa molto mandarli a quella distanza ed è difficile manutenzionarli.
    
- **MEO (Orbite medie):** Orbitano a circa 10.000 km, tra le due fasce di Van Allen.
    
- **LEO (Orbite basse):** Orbitano molto vicino alla Terra, richiedono reti di molti satelliti (es. sistemi Iridium o Globalstar, 50 satelliti, latenza 1-7 ms) .
	- Come quelli utilizzati per starlink a circa 5 km posti all'altezza dell'equatore. Ne utilizza molti per evitare il sovraccarico del singolo satellite e averne di backup in caso di guasto.
    
- **Bande satellitari:** Si dividono in L, S, C (che soffre l'interferenza terrestre), Ku e Ka (che soffrono l'attenuazione dovuta alla pioggia) .
    
![[Pasted image 20260331161122.png]]
![[Pasted image 20260331161144.png]]
![[Pasted image 20260331161247.png]]

---

### 5. Il Sistema Telefonico e le reti dati

Il sistema telefonico globale è la più vasta rete di cavi esistente, originariamente pensata solo per la voce e poi riadattata per trasmettere enormi flussi di dati informatici.

- **PSTN e ISDN:** La PSTN nasce per la trasmissione vocale analogica, mentre la ISDN nasce per la trasmissione dati numerica.
    
- **Il Local Loop:** È il circuito locale che connette l'abitazione dell'utente alla centrale. Per far viaggiare i dati digitali dei computer su linee analogiche si utilizza un "modem" (modulatore/demodulatore).
    
- **Modulazione:** Può agire sull'ampiezza, sulla frequenza o sulla fase del segnale. Nelle trasmissioni avanzate si usano tecniche miste come la QAM (Quadrature Amplitude Modulation), come QAM-16 o QAM-64 .
    
- **Banda larga (DSL/ADSL):** Nelle linee DSL la velocità decade drasticamente all'aumentare della distanza in metri dalla centrale . L'ADSL, in particolare, utilizza la tecnologia DMT dividendo lo spettro in 256 canali da 4-kHz ciascuno (dedicando canali diversi a voce, upstream e downstream) .
    

> **[INSERIRE QUI: Schemi sulle tecniche di modulazione QPSK e QAM-16/64, grafico decadimento del segnale DSL e schema interno di una centrale ADSL con filtri Splitter e DSLAM]**

---

### 6. Dorsali e Multiplexing

Le dorsali telefoniche e dati necessitano di raggruppare migliaia di conversazioni o flussi dati all'interno di un unico grande collegamento per ottimizzare i costi e l'infrastruttura. Questa operazione si chiama multiplexing.

- **FDM (Frequency Division Multiplexing):** L'intero spettro di frequenza del mezzo viene diviso in "fette", e ogni canale ne occupa una contemporaneamente .
    
- **WDM (Wavelength Division Multiplexing):** È l'equivalente del FDM ma applicato alla luce all'interno delle fibre ottiche, combinando e poi separando diverse lunghezze d'onda .
    
- **TDM (Time Division Multiplexing):** Utilizza dei time-slot (slot temporali) che si ripetono ciclicamente nel tempo (frame). Esempi sono le modulazioni PCM come il carrier T1 americano (1,544 Mbps) o l'E1 europeo (2,048 Mbps) .
    
- **Gerarchie Digitali (SONET/SDH):** Per le fibre ottiche sono stati standardizzati i formati SONET e SDH, che multiplexano i dati in frame sincronizzati e raggiungono velocità altissime come la STM-64 (quasi 10 Gbps) .
    

> **[INSERIRE QUI: Schemi di FDM, WDM (con combinatore e separatore ottico), TDM e disegno del frame SONET da 87 colonne]**

---

### 7. Principi di Commutazione

Infine, l'infrastruttura di rete deve instradare (commutare) il traffico dalle sorgenti alle destinazioni corrette.

- **ISDN a banda stretta (N-ISDN):** Utilizza condotti digitali ("digital bit pipe") e definisce punti di riferimento come NT1, NT2 (interfacce per apparati cliente e centralino) e un accesso base (BRI) composto da 2 canali B (per i dati a 64 Kbps) e un canale D (per la segnalazione) .
    
- **B-ISDN e ATM:** La Broadband ISDN utilizza il protocollo ATM, che si differenzia dal normale PCM perché non utilizza frame ripetitivi, ma invia "celle" di dimensione fissa (53 byte) su circuiti virtuali commutati o permanenti .
    

> **[INSERIRE QUI: Schemi delle connessioni NT1/NT2 in ISDN e il confronto grafico tra l'invio ciclico PCM (Synchronous) e l'invio asincrono a celle dell'ATM]**