Meccanismo fondamentale che consente di individuare e/o correggere gli errori che si verificano durante la trasmissione dei dati.

Il **controllo d’errore** viene svolto applicando all’informazione un polinomio generatore, il quale restituisce un determinato valore. All’arrivo il ricevente ricalcola questo polinomio, e se il risultato ottenuto è lo stesso allora non si è verificato nessun errore durante la trasmissione.

Ci sono due modi di gestire gli errori: 
### 1. Codici a Rilevamento d'Errore (Error Detection)

È la strategia "leggera" e più diffusa. Il mittente aggiunge in coda ai dati una piccola stringa di bit di controllo (calcolata tramite formule matematiche, come la _Parità_ o il _CRC_).

- **RIlevamento:** Il destinatario riceve i dati e rifà lo stesso calcolo matematico. Se il suo risultato non combacia con i bit di controllo allegati dal mittente, significa che c'è stato un errore.
    
- **Ritrasmissione:** Il destinatario scarta il pacchetto danneggiato e **chiede al mittente di ritrasmetterlo** (questo meccanismo si chiama _ARQ - Automatic Repeat reQuest_).


### 2. Codici a Correzione d'Errore (Error Correction / FEC)

È la strategia "pesante" (nota anche come _Forward Error Correction_). Il mittente aggiunge una quantità enorme di bit di ridondanza (usando algoritmi complessi come il _Codice di Hamming_).

- **Come funziona:** Quando il destinatario riceve i dati, usa questa forte ridondanza matematica non solo per capire _se_ c'è stato un errore, ma per calcolare con precisione millimetrica **quale esatto bit è sbagliato e correggerlo da solo** invertendolo.
    
- **Cosa succede dopo (Correzione automatica):** Nessuna ritrasmissione. Il dato viene riparato al volo.
    