
È uno standard nato specificamente per le **MAN (Reti Metropolitane)** per coprire le distanze di una città. Oggi è un protocollo **obsoleto** (superato dall'ATM e dalla fibra ottica moderna), ma il suo funzionamento logico è una pietra miliare.

I tre concetti chiave da memorizzare sono:

1. **Dual Bus (Doppio Bus):** Non usa un solo cavo, ma **due bus fisici paralleli e unidirezionali** che viaggiano in direzioni opposte (es. il _Bus A_ viaggia solo verso destra, il _Bus B_ viaggia solo verso sinistra). Tutti i computer sono attaccati a entrambi i bus.
    
2. **Celle di dimensione fissa:** A differenza del CSMA/CD che usa pacchetti di lunghezza variabile, il DQDB trita i dati in "slot" o "celle" tutti uguali e rigidissimi (da 53 byte).
    
3. **Coda Distribuita (Prenotazione):** È il meccanismo geniale per evitare le collisioni. Funziona a prenotazioni usando i bus incrociati.
    
    - _Esempio:_ Se il Nodo 3 vuole inviare dati al Nodo 5 (che sta alla sua destra), dovrà usare il _Bus A_ (che va a destra).
        
    - _La regola:_ Prima di poterlo fare, il Nodo 3 deve mandare un segnale di "Prenotazione" sul _Bus B_ (che va a sinistra). In questo modo, i Nodi 1 e 2 (che stanno "a monte") leggono la prenotazione e sanno che dovranno far passare una cella vuota sul _Bus A_ per permettere al Nodo 3 di riempirla senza scontrarsi.
        
