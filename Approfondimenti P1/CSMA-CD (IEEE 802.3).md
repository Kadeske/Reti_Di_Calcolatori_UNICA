Il protocollo **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) è la versione originale e classica di Ethernet.

Anche se il nome sembra uno scioglilingua tecnico, descrive in realtà un comportamento molto logico. L'analogia migliore per capirlo è pensare a **un gruppo di persone educate che conversano in una stanza completamente buia**, dove tutti possono sentire tutti, ma nessuno può vedere chi sta per parlare.
### Caratteristiche

- **MA (Multiple Access - Accesso Multiplo):** È la condizione di partenza. *Tutti i computer (nodi) della rete sono collegati allo stesso "tubo"* o cavo condiviso (il mezzo trasmissivo). Se due computer inviano dati nello stesso esatto momento, i segnali elettrici si sovrappongono, si "scontrano" e diventano illeggibili. Questa è la _collisione_.
    
- **CS (Carrier Sense - Ascolto della Portante):** È la regola dell'educazione. Prima di trasmettere un pacchetto, la scheda di rete "ascolta" il cavo per sentire se c'è un segnale elettrico in corso (la portante).
    
    - _Se il cavo è occupato:_ Il nodo aspetta.
        
    - _Se il cavo è libero:_ Il nodo inizia a trasmettere.
        
- **CD (Collision Detection - Rilevamento della Collisione):** Dato che la luce e l'elettricità sono veloci ma non istantanee, due computer lontani potrebbero ascoltare il cavo nello stesso momento, trovarlo libero e iniziare a trasmettere contemporaneamente. I pacchetti si scontreranno a metà strada. Mentre trasmette, ogni nodo "ascolta" ciò che passa sul cavo. Se il segnale che legge è diverso da quello che sta inviando, capisce che è avvenuta una collisione.
    
