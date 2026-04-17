Il **Multiplexing (Multiplazione)** è la tecnica che permette di **far viaggiare più comunicazioni diverse contemporaneamente sullo stesso mezzo fisico** (che sia un cavo di rame, una fibra ottica o lo spazio aereo).

All'esame, ti chiederanno sicuramente di spiegare e confrontare le tre tecniche principali:

### **1. FDM (Frequency Division Multiplexing - Multiplazione a divisione di frequenza)**

Immagina la capacità del cavo come una grande autostrada. Con l'FDM, dividi l'autostrada in tante corsie strette (le bande di frequenza).

- **Come funziona:** Ogni utente riceve una specifica fascia di frequenza tutta per sé. I segnali viaggiano in parallelo, ognuno alla sua "altezza" nello spettro, separati da piccole fasce di guardia (bande vuote) per evitare che si scontrino.
    
- **Caratteristica chiave:** L'utente ha a disposizione **solo una frazione della banda totale**, ma ce l'ha per il **100% del tempo**.
    
- **Esempi pratici:** Le stazioni della radio FM (ognuna ha la sua frequenza fissa), i vecchi canali della TV analogica, e l'ADSL (che usa la variante DMT dividendo il cavo in 256 "corsie", come abbiamo appena visto).
    

### **2. TDM (Time Division Multiplexing - Multiplazione a divisione di tempo)**

Questa tecnica cambia completamente approccio. Invece di dividere la strada in corsie, si fa passare una macchina alla volta, ma velocissimamente.

- **Come funziona:** Il mezzo fisico viene concesso a un utente alla volta per una frazione di millisecondo (chiamato _time slot_ o slot temporale). Gli utenti si alternano in un ciclo continuo (round-robin: tocca ad A, poi a B, poi a C, poi di nuovo ad A, e così via).
    
- **Caratteristica chiave:** L'utente ha a disposizione **il 100% della banda (tutta la potenza del canale)**, ma solo per **una frazione del tempo**.
    
- **Esempi pratici:** È la base della telefonia digitale moderna (le reti PSTN digitali a lunga distanza) e delle reti cellulari 2G.
    

### **3. WDM (Wavelength Division Multiplexing - Multiplazione a divisione di lunghezza d'onda)**

È esattamente il principio dell'FDM, ma applicato alla **fibra ottica**.

- **Come funziona:** Invece di usare frequenze elettromagnetiche invisibili, si usano diversi "colori" di luce (lunghezze d'onda). Puoi sparare in un unico cavo di vetro un raggio laser rosso (con la connessione di Milano), un raggio verde (con quella di Roma) e uno blu (con quella di Napoli). Alla fine del cavo, un prisma di vetro separa di nuovo i colori, dirottando ogni flusso verso la sua destinazione.
