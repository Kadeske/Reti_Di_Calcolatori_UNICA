In una rete con milioni di computer e migliaia di processi in esecuzione, l'indirizzamento è il meccanismo necessario per identificare in modo univoco chi invia i dati (sorgente) e chi o cosa deve riceverli (destinazione).

La cosa fondamentale da capire è che **non esiste un solo tipo di indirizzo**. Dato che le reti funzionano a livelli sovrapposti, il pacchetto viene "indirizzato" più volte man mano che sale o scende nella gerarchia.

1. **Il concetto di SAP (Service Access Point):** È letteralmente il "Punto di Accesso al Servizio". Immaginalo come una **porta logica** (un'interfaccia) attraverso cui il Livello inferiore _N_ offre i suoi servizi al Livello superiore _N+1_.


**Esempi pratici di Indirizzamento e SAP:**

Per capire il concetto astratto, pensa a cosa succede quando ricevi un dato sul tuo computer:

- **Al Livello di Collegamento (Data Link):** Il SAP usa l'**Indirizzo MAC** (es. la tua scheda di rete) per capire se il pacchetto fisico sul cavo era destinato proprio al tuo PC.
    
- **Al Livello di Rete:** Il SAP usa l'**Indirizzo IP** per capire se il pacchetto logico è arrivato alla destinazione finale corretta.
    
- **Al Livello di Trasporto:** Questo è l'esempio più chiaro. Il SAP usa il **Numero di Porta**. Se il pacchetto indica "Porta 80", il Livello Trasporto sa che deve passarlo attraverso quel SAP specifico verso il tuo Browser Web. Se indica "Porta 25", lo passerà attraverso un altro SAP verso il tuo programma di posta elettronica. Questo processo di smistamento finale si chiama _Demultiplexing_.
 