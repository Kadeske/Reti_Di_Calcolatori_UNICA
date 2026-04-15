
È un protocollo che unisce l'infrastruttura fisica economica di un **Bus** (un singolo cavo condiviso) con l'ordine rigoroso di un **Anello logico**. È stato creato per ambienti industriali (es. catene di montaggio) dove le collisioni casuali dell'Ethernet (CSMA/CD) non erano accettabili.

Il suo funzionamento si basa su questi concetti chiave:

1. **Topologia Ibrida:** Fisicamente, tutti i nodi sono attaccati allo stesso cavo orizzontale. **Logicamente**, i nodi sono numerati e organizzati ad anello (es. il nodo 1 passa al 4, il 4 passa al 2, il 2 passa all'1).
    
2. **Il Token (Gettone):** È un piccolo frame di controllo speciale che circola continuamente nella rete seguendo rigorosamente l'ordine logico (non quello fisico).
    
3. **Diritto di Trasmissione:** Un nodo **può trasmettere dati SOLO se è in possesso del Token**.
    - Se ha il token e ha dati, li invia, poi passa il token al vicino logico.
    - Se ha il token ma non ha nulla da dire, lo passa immediatamente al vicino logico.
        
![[Pasted image 20260415134524.png]]

**Pro e Contro Principali:**

- **Vantaggio - Assenza di collisioni e Determinismo:** Dato che parla solo chi ha il gettone, nessuno si scontra. Soprattutto, c'è un tempo massimo di attesa garantito (si sa esattamente quanto tempo impiega il token a fare un giro completo).
    
- **Svantaggio - Gestione complessa:** Il protocollo è pesante. Se il token viene perso (es. interferenza) o se il nodo che possiede il token si guasta improvvisamente, la rete si blocca e servono procedure complesse per "eleggere" un nodo che generi un nuovo token.
    
