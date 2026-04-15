È stato il primo standard internazionale per le reti a commutazione di pacchetto, molto diffuso negli anni '70 e '80 (soprattutto in Europa). È nato in un'epoca in cui le linee telefoniche erano di bassa qualità e soggette a molti disturbi.

I punti chiave da ricordare sono:

- **Orientamento alla Connessione:** A differenza di ARPANET, X.25 è un servizio **orientato alla connessione**. Prima di inviare dati, è necessario stabilire una "chiamata virtuale".
    
- **Controllo d'Errore "Nodo per Nodo":** Questa è la sua caratteristica principale. Dato che i cavi dell'epoca erano inaffidabili, ogni singolo nodo (router) della rete controllava che il pacchetto fosse integro prima di mandarlo al nodo successivo. Se c'era un errore, il pacchetto veniva ritrasmesso immediatamente tra i due nodi.
    
- **Conseguenze (Lentezza):** Questo controllo continuo garantiva una consegna perfetta, ma rendeva la rete **molto lenta** e introduceva un alto ritardo (latenza), perché ogni nodo doveva fermare il pacchetto, verificarlo e inviare una conferma (ACK).
    
- **Struttura:** Definisce l'interfaccia tra il terminale dell'utente (**DTE** - Data Terminal Equipment) e l'apparato della rete dell'operatore telefonico (**DCE** - Data Circuit-terminating Equipment).
![[Pasted image 20260415163637.png]]

**In sintesi:** X.25 era una rete estremamente **robusta ma pesante**, progettata per far viaggiare i dati in modo sicuro su linee fisiche di pessima qualità. Con l'arrivo della fibra ottica (molto più affidabile), è stata sostituita da tecnologie più veloci come il [[Frame Relay]].