
### **Comunicazioni Satellitari: Concetti Generali**

Nate negli anni '60, queste reti sfruttano satelliti artificiali posizionati ad altitudini estreme. Di base, funzionano come degli immensi "specchi" o ripetitori a radiofrequenza sospesi nel vuoto:

- **Come funzionano:** Creano un **ponte radio** tra due o più stazioni ricetrasmittenti a terra che, a causa della curvatura terrestre o della distanza, non potrebbero mai "vedersi" direttamente.
    
- **Ambiti di applicazione:** Telefonia, televisione, telematica (internet), navigazione marittima (GPS) e campo militare.
    
- **Il vero vantaggio:** Spesso sono **l'unica soluzione possibile** quando mancano infrastrutture terrestri (es. in mezzo agli oceani, nei deserti, in volo, o in zone colpite da disastri naturali dove i cavi sono interrotti).
    

### **La classificazione delle Orbite (Il cuore del discorso)**

Il grafico nei tuoi appunti è fondamentale per l'esame. Ci mostra che non tutti i satelliti sono uguali, ma vengono classificati in base all'**altitudine** a cui orbitano.

C'è una regola ingegneristica d'oro che lega queste tre variabili: **Più il satellite è alto, maggiore è il ritardo del segnale (latenza), ma meno satelliti servono per coprire l'intera Terra.**

Ecco i dati della tua immagine riassunti in una tabella da memorizzare:

| **Tipo di Orbita**            | **Altitudine**        | **Latenza (Ritardo)** | **Satelliti per copertura globale** | **tempo di vita** |
| ----------------------------- | --------------------- | --------------------- | ----------------------------------- | ----------------- |
| **LEO** (Low Earth Orbit)     | Fino a ~5.000 km      | **20-34ms**           | **~50**                             | tra 5 e 8 anni    |
| **MEO** (Medium Earth Orbit)  | tra 5.000 e 15.000 km | **110-130ms**         | **~10**                             |                   |
| **GEO** (Geostationary Orbit) | **~35.000 km**        | **250-280 ms**        | **3**                               | ~15 anni          |

### **Analisi delle Orbite e le Fasce di Van Allen**

1. **GEO (Satelliti Geostazionari):** Sono posizionati a ben 35.000 km di altezza. A questa distanza esatta, il satellite ruota alla stessa identica velocità con cui la Terra gira su se stessa. Risultato? **Il satellite sembra immobile nel cielo**. È comodissimo perché basta puntare la parabola fissa sul tetto una sola volta (come per Sky). Bastano 3 satelliti per coprire tutto il pianeta. _Il difetto?_ La luce deve fare 70.000 km di andata e ritorno: questo crea un fastidiosissimo ritardo (latenza di quasi 300 millisecondi), pessimo per le videochiamate o i videogiochi.
    
2. **MEO (Media Orbita):** Stanno in una via di mezzo (~10.000 km). Non sono fermi nel cielo, quindi le antenne a terra devono "inseguirli". Il loro uso principale oggi è per i sistemi di navigazione satellitare come il **GPS** o il Galileo europeo.
    
3. **LEO (Bassa Orbita):** Sono vicinissimi alla Terra. Il segnale ci mette un attimo ad arrivare (latenza bassissima, simile a quella della fibra ottica). _Il problema?_ Essendo così vicini, vedono solo una piccolissima porzione di Terra e sfrecciano a velocità folli, scomparendo dietro l'orizzonte in pochi minuti. Per avere una connessione continua serve una "costellazione" immensa di decine (o migliaia, come Starlink) di satelliti che si passano la connessione l'un l'altro.


### **VSAT: Le Microstazioni Satellitari**

Il termine VSAT indica dei terminali satellitari caratterizzati da dimensioni molto ridotte. (**Very Small Aperture Terminal**)

![[Pasted image 20260416154604.png]]
**1. Caratteristiche Fisiche e Prestazioni**

- **Antenne minuscole:** Hanno un diametro di 1 metro o anche meno (da qui il nome _Very Small Aperture_).
    
- **Bassa potenza:** Essendo piccole ed economiche, generano appena **1 Watt** di potenza per trasmettere verso lo spazio.
    
- **Velocità asimmetrica:** Sono progettate principalmente per "ricevere" dati più che per inviarli. Hanno un _uplink_ (caricamento verso il satellite) lento, intorno ai 19,2 kbps, e un _downlink_ (scaricamento dal satellite) molto più veloce, superiore a 512 kbps. (Nota: i valori numerici dei tuoi appunti si riferiscono ai primi sistemi VSAT storici, oggi le velocità sono in Megabit, ma il principio di asimmetria rimane identico).

	

**2. Il Problema: Troppo deboli per parlarsi direttamente**

Se l'utente A (con una VSAT) vuole inviare un file all'utente B (con un'altra VSAT) attraverso il satellite, sorge un problema fisico. La parabola A ha solo 1 Watt di potenza: il suo segnale arriva al satellite molto debole. Il satellite lo rimbalza verso la parabola B, ma essendo anche l'antenna B molto piccola, **non riesce a captare un segnale così debole in arrivo dallo spazio profondo**.

**3. La Soluzione: L'architettura a HUB (Il Doppio Salto)**

Per far parlare due VSAT tra loro, si inserisce un intermediario terrestre chiamato **HUB**.

L'HUB è una gigantesca e potentissima stazione terrestre (con parabole enormi ad alto guadagno). Ecco come funziona la comunicazione (illustrata perfettamente nel disegno dei tuoi appunti):

1. La **VSAT A** invia il suo piccolo segnale al satellite.
    
2. Il satellite non lo manda a B, ma lo manda giù all'**HUB**.
    
3. L'HUB riceve il segnale debole, lo **elabora e lo amplifica** a grandissima potenza, e lo spara di nuovo verso il satellite.
    
4. Il satellite, ricevendo un segnale ora fortissimo, lo rimbalza finalmente verso la **VSAT B**, che essendo piccola riesce a captarlo solo grazie alla potenza che ci ha messo l'HUB.
    

**4. Pro e Contro all'esame**

- **Vantaggio:** Il costo per l'utente finale crolla. Puoi comprare una parabola VSAT con poche decine di euro.
    
- **Svantaggio (Il tempo di propagazione):** Questo percorso (A $\rightarrow$ Satellite $\rightarrow$ HUB $\rightarrow$ Satellite $\rightarrow$ B) costringe il segnale a fare la strada Terra-Spazio per ben **4 volte**! Se un satellite GEO ha già una latenza altissima di ~270 ms, con questo "doppio salto" il ritardo raddoppia superando il mezzo secondo (>540 ms). È il cosiddetto _incremento del tempo di propagazione_.
    
### **Iridium (La complessità nello spazio)**

- **Il nome e i numeri:** Inizialmente doveva avere 77 satelliti (77 è il numero atomico dell'elemento Iridio), ma alla fine ne bastarono **66**. (Oggi aggiornato a _Iridium Next_ con 81 satelliti).
    
- **Copertura totale:** È uno dei pochissimi sistemi a coprire il 100% del pianeta, **comprese le aree polari** (dove i satelliti GEO non arrivano bene).
    
- **Utilizzi:** Indispensabile in mare aperto, nei deserti e durante i disastri naturali (quando le antenne terrestri crollano).
    
- **Come gestisce il segnale (Diagramma A):** Iridium usa la **commutazione satellitare nello spazio**. Questo significa che i satelliti si passano la telefonata l'un l'altro lassù in orbita. Se chiami dall'Italia all'Australia, il tuo segnale sale al satellite 1, passa al satellite 2, poi al satellite 3, e infine scende in Australia.
    
    - _Il difetto:_ Costringe a mettere router e computer potentissimi (e pesanti) a bordo di ogni satellite. Se un componente si rompe, non puoi mandare un tecnico nello spazio a ripararlo.
        

### **Globalstar (La semplicità nello spazio)**

- **I numeri:** È un progetto alternativo e più economico, basato su **48 satelliti** LEO.
    
- **Come gestisce il segnale (Diagramma B):** Utilizza un modello tradizionale chiamato **"Bent pipe"** (tubo piegato) con **commutazione a terra**.
    
- **Cosa significa "Bent pipe"?** Il satellite Globalstar è "stupido": non sa a chi è diretta la chiamata. Si limita a prendere il segnale radio e a rifletterlo immediatamente verso il basso (come un tubo piegato) verso la stazione terrestre più vicina. Sarà poi la stazione terrestre a capire dove deve andare la chiamata e a instradarla, magari facendola rimbalzare su un altro satellite.
    
    - _Il grande vantaggio:_ Mantiene tutta la tecnologia complessa (i computer, i commutatori) **sulla Terra**, dove è infinitamente più facile, economico e veloce fare manutenzione o aggiornare i software.
        
![[Pasted image 20260416154704.png]]


## **Confronto satellite vs fibra/doppino**

La fibra ottica, ormai "liberalizzata", offre notevoli vantaggi, sebbene il satellite sia di ancora maggiormente impiegato in alcune situazioni, come ad esempio:

- **Luoghi poco accessibili**: difficile stendere la fibra ovunque, ma chiunque posizioni un'antenna sul tetto riesce a comunicare con il satellite;
    
- **Comunicazioni in mobilità**: auto, camion, barche;
    
- **Broadcasting**: trasmissione di dati ad una vasta gamma di riceventi;
    
- **Comunicazioni temporanee**: comunicazioni militari in periodo di guerra oppure durante i gran premi della Formula 1.