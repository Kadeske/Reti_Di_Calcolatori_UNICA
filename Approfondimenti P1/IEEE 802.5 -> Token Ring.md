**Token Ring (Standard IEEE 802.5)**

Sviluppato originariamente da IBM, è un protocollo in cui sia la topologia fisica che quella logica sono ad **Anello**. I dati viaggiano in una sola direzione, passando di nodo in nodo.

Il funzionamento si basa su regole di "educazione" molto rigide:

1. **Il Token Libero:** Un piccolo frame di controllo (il gettone) circola continuamente e velocemente lungo l'anello chiuso.
    
2. **Cattura e Trasmissione:** Un nodo può trasmettere **SOLO** se cattura un token libero. Quando lo fa, cambia un bit nel token per segnalare che è "occupato", vi appiccica i suoi dati e lo invia al nodo successivo.
    
3. **Lettura:** Il pacchetto viaggia nell'anello. Tutti i nodi lo passano al vicino. Quando arriva al destinatario corretto, quest'ultimo lo legge, lo copia e accende un "bit di conferma" (ACK) nel pacchetto per dire "l'ho ricevuto e letto".
    
4. **Rimozione e Rilascio (Cruciale!):** Il pacchetto continua il suo giro finché non **torna al mittente originale**. Il mittente controlla la conferma, **rimuove il suo pacchetto** dalla rete e **rimette in circolo un nuovo token libero**.

![[Pasted image 20260415134721.png]]

**Pro e Contro Principali:**

- **Vantaggi - Niente collisioni e priorità:** Come nel Token Bus, il traffico è ordinato al 100%. In più, il Token Ring permette di assegnare "priorità" (un server può avere più diritto di parlare rispetto a un pc normale).
    
- **Svantaggi - Estrema fragilità:** Se il cavo si spezza in un punto o una scheda di rete si guasta, l'anello si interrompe e **l'intera rete cade** (problema storicamente mitigato usando dei concentratori centrali chiamati MAU). Inoltre, serve sempre un "Nodo Monitor" attivo per controllare che il token non vada perso o non giri all'infinito un pacchetto orfano.
