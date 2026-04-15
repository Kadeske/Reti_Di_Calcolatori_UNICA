
È lo standard per le reti locali senza fili. Al posto dei cavi, utilizza le **onde radio** (tipicamente nelle frequenze di 2.4 GHz e 5 GHz). Il mezzo trasmissivo è l'etere, che è condiviso e molto più soggetto a disturbi rispetto a un cavo di rame.

I concetti chiave da memorizzare sono:

1. **Due Modalità di Architettura:**
    
    - **Infrastruttura:** La rete ruota attorno a un **Access Point (AP)** (il router Wi-Fi di casa). L'AP coordina il traffico e fa da ponte verso la rete cablata esterna (Internet).
        
    - **Ad-Hoc:** I dispositivi (nodi) comunicano **direttamente tra loro** in modalità peer-to-peer, senza un punto di accesso centrale.
        
2. **CSMA/CA (Collision Avoidance):**
    
    A differenza del CSMA/CD cablato, via radio è quasi impossibile "ascoltare" una collisione mentre si trasmette (il proprio segnale coprirebbe gli altri). Quindi le collisioni non si rilevano, **si evitano (Avoidance)**. Prima di trasmettere, il nodo aspetta che il canale sia libero, poi attende un tempo casuale aggiuntivo per ridurre le probabilità di scontro.
    
3. **Il Problema del Nodo Nascosto (Hidden Node):**
    
    È il problema classico del Wi-Fi. Esempio: Il nodo A e il nodo C vogliono parlare con l'AP centrale B. B è abbastanza vicino da sentire entrambi, ma **A e C sono troppo lontani tra loro per sentirsi**. A e C potrebbero credere che il canale sia libero e trasmettere contemporaneamente, scontrandosi su B senza accorgersene.
    
4. **La Soluzione: Protocollo RTS/CTS:**
    
    Per evitare il nodo nascosto, il CSMA/CA usa un meccanismo di "prenotazione" del canale:
    
    - **RTS (Request To Send):** Prima di inviare i dati veri, il nodo A manda un piccolo messaggio all'AP chiedendo "Posso trasmettere?".
        
    - **CTS (Clear To Send):** L'AP risponde "Sì, via libera". Questo segnale CTS viene inviato in broadcast e **raggiunge anche il nodo nascosto C**.
        
    - **Risultato:** Ora C sa che A sta per parlare e se ne sta in silenzio, anche se non sente fisicamente il nodo A. A trasmette, e alla fine l'AP invia un **ACK (Acknowledge)** per confermare il successo.
        

