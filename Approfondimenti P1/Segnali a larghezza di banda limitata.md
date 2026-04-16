### **Il concetto base: Il mezzo fisico come "Filtro"**

In un mondo ideale, un cavo (o l'aria per le onde radio) trasporterebbe i nostri bit sotto forma di un'onda quadra perfetta, con spigoli netti, all'infinito.

Nel *mondo reale*, però, *la materia di cui è fatto il cavo (il rame o il vetro) offre una certa "resistenza" fisica* ai cambiamenti troppo rapidi di energia. Di conseguenza, il mezzo trasmissivo si comporta come un imbuto, o meglio, come un **filtro**: fa passare bene le frequenze più basse, ma smorza, indebolisce e infine "taglia" le frequenze più alte.

Un segnale che viaggia in queste condizioni è detto, appunto, **a larghezza di banda limitata**.

### **Cos'è la Banda (I due significati che non devi confondere)**

All'esame, i professori amano chiedere la differenza tra i due modi in cui usiamo la parola "banda". È fondamentale distinguerli:

1. **Banda (o Larghezza di banda) Analogica:** È una **proprietà fisica** del cavo. Si misura in **Hertz (Hz)**. Rappresenta l'intervallo di frequenze (dalla più bassa alla più alta) che il cavo riesce a trasportare dalla sorgente alla destinazione senza che perdano troppa potenza. _Più il cavo è costruito bene, più questo intervallo è grande._
    
2. **Banda (o Larghezza di banda) Digitale (o Logica):** È la **velocità** del nostro trasferimento dati. Si misura in **bit al secondo (bps)**. Rappresenta la quantità massima di informazione (0 e 1) che riusciamo a far passare in quel cavo in un secondo.
    

### **Cosa comporta una banda (analogica) più ampia?**

Ripensiamo a Fourier: i bordi netti e veloci della nostra onda quadra sono formati dalle frequenze più alte (le ultime armoniche).

- Se abbiamo un cavo scadente con una **banda analogica stretta** (es. il vecchio doppino telefonico), taglierà via molte frequenze alte. L'onda arriverà molto arrotondata. Se proviamo a inviare i bit troppo velocemente, le onde arrotondate si "spalmeranno" l'una sull'altra, e il ricevitore leggerà solo una linea piatta e indistinta (i dati si corrompono).
    
- Se investiamo in un mezzo con una **banda analogica molto più ampia** (es. il cavo coassiale o la fibra ottica), il cavo lascerà passare molte più frequenze alte. L'onda arriverà a destinazione conservando i suoi spigoli netti.
    

**La conclusione logica:** Avere un'onda ben squadrata significa poter "stringere" i bit, inviandoli l'uno vicinissimo all'altro senza che si confondano. Quindi, **una banda analogica più ampia comporta direttamente la possibilità di avere una banda digitale (velocità di trasmissione) più alta.**

---

Per visualizzare esattamente cosa succede quando cerchiamo di spingere troppi dati in un "tubo" troppo stretto (fenomeno chiamato _Interferenza Intersimbolica_), ho creato questo simulatore.

Prova a impostare una velocità altissima e una banda strettissima: vedrai i bit fondersi tra loro!

Mostrami la visualizzazione