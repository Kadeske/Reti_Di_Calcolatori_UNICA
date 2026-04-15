Questo argomento spiega il viaggio "fisico" dei dati rispetto a quello "logico". La regola d'oro da ricordare è: **la comunicazione è concettualmente orizzontale** (es. il Livello 4 di un host parla con il Livello 4 dell'altro), **ma fisicamente è verticale** (i dati scendono i livelli da una parte, viaggiano sul cavo, e risalgono dall'altra).

![[Pasted image 20260415141221.png]]
## Ecco l'esempio passo per passo dell'invio di un Messaggio (M) tra l'Host 1 e l'Host 2:
### Fase 1: Discesa nell'Host 1 (Mittente)

L'obiettivo è codificare il messaggio in modo che l'operazione inversa sul destinatario sia automatica.

1. **Livello Applicativo (5):** Il processo crea il Messaggio originale (M).
    
2. **Incapsulamento (Livello 4):** Il messaggio scende. Il Livello 4 aggiunge in testa le sue informazioni di controllo, creando un **Header (H4)**. L'Header serve per far capire al Livello 4 del destinatario come gestire i dati.
    
3. **Suddivisione (Livello 3):** Spesso il messaggio incapsulato è troppo grande per la rete. Il Livello 3 **spezza il messaggio** in unità più piccole (es. M1 e M2) e appiccica a ognuna un proprio **Header (H3)**, fondamentale per far capire che sono pezzi della stessa comunicazione.
    
4. **Mezzo Fisico (Livello 1):** Scendendo ancora, tutto diventa bit (0 e 1) e viaggia sul Canale Fisico.
    

### Fase 2: Risalita nell'Host 2 (Destinatario)

All'arrivo, l'Host 2 esegue la decodifica inversa, togliendo le intestazioni una ad una ("decapsulamento").

1. **Riassemblaggio (Livello 3):** Lo strato 3 dell'Host 2 riceve i pezzi, legge gli **Header H3**, li scarta e li usa per ricomporre l'ordine corretto dei frammenti (M1 e M2).
    
2. **La Trasparenza:** I dati uniti vengono passati al Livello 4. Un concetto chiave è la _trasparenza_: il Livello 4 dell'Host 2 riceve il blocco intero e **non sa (e non gli interessa) che al livello inferiore il messaggio era stato spezzato**.
    
3. **Controllo Errori (Livello 4):** Lo strato 4 analizza l'**Header H4** per assicurarsi che non ci siano stati errori o incongruenze durante il viaggio. Se è tutto ok, rimuove l'Header H4.
    
4. **Consegna (Livello 5):** Il Messaggio originale (M), ormai pulito da ogni Header, arriva al livello superiore, dove l'applicazione lo visualizza all'utente finale.
    

**Cosa succede se c'è Internet di mezzo?**

Se gli host non sono connessi da un cavo diretto (come accade quasi sempre), in mezzo c'è una **Subnet** (sottorete) composta da **Router**. I pacchetti rimbalzano da un router all'altro (protocolli _router-router_). È importante ricordare che **i router non hanno tutti i livelli**: si fermano al Livello 3 (Rete). Leggono l'indirizzo, instradano il pacchetto e lo rimandano giù sul cavo. Solo quando il pacchetto arriva finalmente all'Host 2 potrà risalire fino ai livelli 4 e 5!