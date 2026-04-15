Il protocollo **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) è la versione originale e classica di Ethernet.

Anche se il nome sembra uno scioglilingua tecnico, descrive in realtà un comportamento molto logico. L'analogia migliore per capirlo è pensare a **un gruppo di persone educate che conversano in una stanza completamente buia**, dove tutti possono sentire tutti, ma nessuno può vedere chi sta per parlare.
### 1. I Tre Pilastri del CSMA/CD

- **MA (Multiple Access - Accesso Multiplo):** È la condizione di partenza. *Tutti i computer (nodi) della rete sono collegati allo stesso "tubo"* o cavo condiviso (il mezzo trasmissivo). Se due computer inviano dati nello stesso esatto momento, i segnali elettrici si sovrappongono, si "scontrano" e diventano illeggibili. Questa è la _collisione_.
    
- **CS (Carrier Sense - Ascolto della Portante):** È la regola dell'educazione. Prima di trasmettere un pacchetto, la scheda di rete "ascolta" il cavo per sentire se c'è un segnale elettrico in corso (la portante).
    
    - _Se il cavo è occupato:_ Il nodo aspetta.
        
    - _Se il cavo è libero:_ Il nodo inizia a trasmettere.
        
- **CD (Collision Detection - Rilevamento della Collisione):** Dato che la luce e l'elettricità sono veloci ma non istantanee, due computer lontani potrebbero ascoltare il cavo nello stesso momento, trovarlo libero e iniziare a trasmettere contemporaneamente. I pacchetti si scontreranno a metà strada. Mentre trasmette, ogni nodo "ascolta" ciò che passa sul cavo. Se il segnale che legge è diverso da quello che sta inviando, capisce che è avvenuta una collisione.
    

### 2. Cosa succede quando c'è una collisione?

Questa è la parte cruciale (e spesso oggetto di domande all'esame). Quando viene rilevata una collisione, i nodi non si limitano a riprovare subito, altrimenti si scontrerebbero di nuovo all'infinito. Eseguono questa procedura:

1. **Segnale di Jamming:** Appena un nodo rileva la collisione, smette di inviare i suoi dati e trasmette per un breve istante una sequenza di bit "di disturbo" (Jam signal). Questo assicura che _tutti_ gli altri nodi sulla rete si accorgano inequivocabilmente che c'è stata una collisione e scartino i dati corrotti.
    
2. **L'algoritmo di Backoff Esponenziale Binario:** I nodi che si sono scontrati devono aspettare un tempo casuale prima di ritentare. L'algoritmo funziona così:
    
    - Alla **1° collisione**, il nodo sceglie a caso di aspettare 0 oppure 1 "slot" di tempo.
        
    - Se c'è una **2° collisione** (magari hanno scelto entrambi 0), il tempo di attesa casuale viene scelto tra 0, 1, 2 o 3 slot.
        
    - Alla **3° collisione**, l'intervallo si allarga da 0 a 7.
        
    - _In sintesi:_ Ad ogni scontro consecutivo, la "finestra" di tempo casuale si raddoppia ($2^n - 1$). Questo diluisce il traffico e abbassa drasticamente la probabilità di un nuovo scontro. Se dopo 16 tentativi fallisce ancora, il nodo si arrende e segnala un errore al livello superiore.
        

### 3. CSMA/CD oggi: un concetto "storico" ma fondamentale

È importante sapere che nelle reti cablate moderne (LAN in topologia a stella con Switch), il CSMA/CD **non entra quasi mai in azione**. Gli Switch moderni creano canali dedicati (_full-duplex_) per ogni computer, eliminando fisicamente la possibilità che i pacchetti si scontrino.

Tuttavia, studiarlo è vitale perché:

1. Spiega il fondamento filosofico di come i computer gestiscono le risorse condivise.
    
2. È la base da cui è nato il **CSMA/CA** (Collision _Avoidance_), che è invece il protocollo attualmente usato dalle reti Wi-Fi (IEEE 802.11), dove le collisioni nell'etere radio sono ancora un problema enorme.
    

Per capire visivamente la tempistica e le collisioni, ho preparato un simulatore. Prova a far trasmettere due nodi vicini e osserva come gestiscono l'attesa.

Mostrami la visualizzazione