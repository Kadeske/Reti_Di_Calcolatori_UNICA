Il protocollo **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) è la versione originale e classica di Ethernet.

È il protocollo che regola come i nodi trasmettono dati su un **mezzo condiviso** (come un cavo bus) per evitare che i segnali si sovrappongano e si distruggano.

Il nome stesso spiega il funzionamento in tre regole:

1. **CS (Carrier Sense):** Prima di trasmettere, il nodo **ascolta il canale**. Se è libero, invia; se è occupato, aspetta.
2. **MA (Multiple Access):** Più dispositivi sono collegati allo **stesso cavo**.
3. **CD (Collision Detection):** Mentre trasmette, il nodo continua ad ascoltare. Se rileva un segnale alterato, capisce che c'è stata una **collisione** (due nodi hanno trasmesso nello stesso istante).
    

**Gestione della Collisione (Cosa succede dopo lo scontro):**

- **Segnale di Jam:** Il nodo ferma la trasmissione e invia un segnale di disturbo per avvisare tutta la rete che i dati sul cavo sono corrotti e vanno scartati.
- **Backoff Esponenziale:** I nodi scontrati aspettano un **tempo di attesa casuale** prima di riprovare. Se collidono di nuovo, l'intervallo di tempo tra cui scegliere casualmente _raddoppia_, riducendo drasticamente le probabilità di un nuovo scontro.