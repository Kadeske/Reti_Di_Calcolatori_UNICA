
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
    

**Attenzione al dettaglio:** Perché ci sono dei grandi "buchi" vuoti tra i 5.000-10.000 km e tra i 15.000-20.000 km?

