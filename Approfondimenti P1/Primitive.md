Le **primitive** sono operazioni (routine di servizio) che un'entità di livello $n$ utilizza per accedere ai servizi offerti dal livello sottostante $n-1$. La tipologia di primitive dipende dalla classe di servizio offerta.

### Primitive Principali (Esempio Base)

|**Primitiva**|**Significato**|**Descrizione Operativa**|
|---|---|---|
|**LISTEN**|Attesa bloccante|Il server si mette in attesa di una connessione in arrivo.|
|**CONNECT**|Stabilisce connessione|Il client (o un pari) stabilisce una connessione con un'entità in attesa.|
|**RECEIVE**|Attesa messaggio|Entità (client o server) in attesa bloccante di un messaggio in arrivo.|
|**SEND**|Invia messaggio|Permette l'invio di dati al peer in entrambe le direzioni.|
|**DISCONNECT**|Termina connessione|Avvia la fase di rilascio e chiusura della sessione.|

---

## Tipologie di Metodi (Interazione tra Livelli)

Ogni primitiva può implementare dei **metodi** specifici per gestire il flusso tra i livelli $n$ (superiore) e $n-1$ (inferiore):

- **`request()`**: Un'entità richiede che il servizio svolga un'azione (Da $n$ a $n-1$).
    
- **`indication()`**: L'entità deve essere informata dal servizio su un evento (Da $n-1$ a $n$).
    
- **`response()`**: L'entità vuole rispondere a un evento (Da $n$ a $n-1$).
    
- **`confirm()`**: L'entità viene informata sull'esito della sua richiesta iniziale (Da $n-1$ a $n$).
    

---

## Modelli di Comportamento: Affidabile vs Non Affidabile

La combinazione di questi metodi determina la qualità del servizio e l'affidabilità della comunicazione.

### 1. Servizio NON Affidabile (Senza conferma)

Si basa solo sulle prime due fasi:

1. **A** invia una `<primitiva>.request()` (Livello $n \to n-1$).
    
2. **B** riceve una `<primitiva>.indication()` (Livello $n-1 \to n$).
    
    _In questo caso, il mittente non sa se l'azione è andata a buon fine._
    

### 2. Servizio Affidabile (Con conferma)

Per garantire l'affidabilità, si completano tutte e 4 le fasi:

1. **A** invia una `<primitiva>.request()`.
    
2. **B** riceve una `<primitiva>.indication()`.
    
3. **B** risponde con una `<primitiva>.response()`.
    
4. **A** riceve una `<primitiva>.confirm()`.
    

**Esempio Pratico: Connessione (CONNECTION)**

Se l'entità **A** vuole instaurare una connessione con **B**:

- **A** invia una `CONNECT.request`.
    
- **B** riceve la `CONNECT.indication` e accetta con una `CONNECT.response`.
    
- **A** riceve la `CONNECT.confirm` che chiude il cerchio: ora la connessione è stabilita e confermata.