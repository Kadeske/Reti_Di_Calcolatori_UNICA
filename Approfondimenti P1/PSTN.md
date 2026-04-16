
### **1. La Natura del PSTN (Un progetto nato per la voce)**

Il PSTN non è nato per i computer, ma con un unico e semplice obiettivo: **trasmettere la voce umana**.

Poiché la voce non ha bisogno di grande precisione per essere "più o meno comprensibile", la rete fu costruita al risparmio. Questo spiega perché, quando abbiamo provato ad attaccarci i computer decenni dopo, abbiamo sbattuto contro due limiti fisici enormi:

- **Velocità limitatissima:** Il canale analogico base permetteva al massimo 56 Kbps.
    
- **Connessione non persistente:** La linea doveva essere "composta" ogni volta, non era sempre attiva (e mentre navigavi non potevi ricevere telefonate).
    

### **2. L'Evoluzione della Rete (Il problema dei troppi fili)**
![[Pasted image 20260416165257.png]]
Tre fasi storiche, corrispondenti alle tre immagini della Figura 2.20:

- **(Figura A) La Rete Completamente Interconnessa (Il Caos):**
    
    All'inizio, se compravi un telefono, dovevi tirare fisicamente un cavo da casa tua a casa del tuo amico. Se volevi chiamare 10 amici, dovevi stendere 10 cavi dal tuo salotto. In poco tempo le città divennero una giungla impraticabile di cavi sospesi. Era un modello che matematicamente non poteva funzionare su larga scala.
    
- **(Figura B) Il Commutatore Centralizzato (La Soluzione Bell):**
    
    La Bell Telephone Company ebbe l'intuizione geniale: stendere **un solo cavo** da ogni casa fino a un edificio centrale (l'ufficio di commutazione). Lì c'era un operatore umano. Tu giravi la manovella, l'operatore rispondeva e, usando un cavo a ponte, collegava fisicamente il tuo filo a quello dell'amico che volevi chiamare. Il numero di fili in città crollò drasticamente.
    
- **(Figura C) La Gerarchia (L'espansione globale):**
    
    Ben presto, la singola centrale non bastò più. Come unire la centrale di Roma con quella di Milano? Non si potevano collegare tutte le centrali locali tra loro (sarebbe tornato il caos della figura A). Fu inventata così la **centrale di commutazione di secondo livello** (una centrale che collega tra loro altre centrali). Questo sistema a matrioska crebbe fino a raggiungere una **gerarchia a 5 livelli**.
    

### **3. I Tre Pilastri del Sistema (1890)**

Grazie a questa evoluzione, già a fine '800 la struttura della rete era definita nelle sue tre parti fondamentali, che esistono ancora oggi:

1. **Gli uffici di commutazione:** I nodi centrali che instradano le chiamate.
    
2. **I cavi tra clienti e centrale:** Il famoso "doppino telefonico" di cui abbiamo parlato prima (il cosiddetto "ultimo miglio").
    
3. **Le connessioni a lunga distanza (Dorsali):** I cavi ad alta capacità che collegano tra loro gli uffici di commutazione di città o nazioni diverse.
