
### **La Natura del PSTN (Un progetto nato per la voce)**

Il PSTN non è nato per i computer, ma con un unico e semplice obiettivo: **trasmettere la voce umana**.

Poiché la voce non ha bisogno di grande precisione per essere "più o meno comprensibile", la rete fu costruita al risparmio. Questo spiega perché, quando abbiamo provato ad attaccarci i computer decenni dopo, abbiamo sbattuto contro due limiti fisici enormi:

- **Velocità limitatissima:** Il canale analogico base permetteva al massimo 56 Kbps.
    
- **Connessione non persistente:** La linea doveva essere "composta" ogni volta, non era sempre attiva (e mentre navigavi non potevi ricevere telefonate).
    

### **L'Evoluzione della Rete (Il problema dei troppi fili)**
![[Pasted image 20260416165257.png]]
Tre fasi storiche, corrispondenti alle tre immagini della Figura 2.20:

- **(Figura A) La Rete Completamente Interconnessa (Il Caos):**
    
    All'inizio, se compravi un telefono, dovevi tirare fisicamente un cavo da casa tua a casa del tuo amico. Se volevi chiamare 10 amici, dovevi stendere 10 cavi dal tuo salotto. In poco tempo le città divennero una giungla impraticabile di cavi sospesi. Era un modello che matematicamente non poteva funzionare su larga scala.
    
- **(Figura B) Il Commutatore Centralizzato (La Soluzione Bell):**
    
    La Bell Telephone Company ebbe l'intuizione geniale: stendere **un solo cavo** da ogni casa fino a un edificio centrale (l'ufficio di commutazione). Lì c'era un operatore umano. Tu giravi la manovella, l'operatore rispondeva e, usando un cavo a ponte, collegava fisicamente il tuo filo a quello dell'amico che volevi chiamare. Il numero di fili in città crollò drasticamente.
    
- **(Figura C) La Gerarchia (L'espansione globale):**
    
    Ben presto, la singola centrale non bastò più. Come unire la centrale di Roma con quella di Milano? Non si potevano collegare tutte le centrali locali tra loro (sarebbe tornato il caos della figura A). Fu inventata così la **centrale di commutazione di secondo livello** (una centrale che collega tra loro altre centrali). Questo sistema a matrioska crebbe fino a raggiungere una **gerarchia a 5 livelli**.
    

### **I Tre Pilastri del Sistema (1890)**

Grazie a questa evoluzione, già a fine '800 la struttura della rete era definita nelle sue tre parti fondamentali, che esistono ancora oggi:

1. **Gli uffici di commutazione:** I nodi centrali che instradano le chiamate.
    
2. **I cavi tra clienti e centrale:** Il famoso "doppino telefonico" di cui abbiamo parlato prima (il cosiddetto "ultimo miglio").
    
3. **Le connessioni a lunga distanza (Dorsali):** I cavi ad alta capacità che collegano tra loro gli uffici di commutazione di città o nazioni diverse.

### **L'Ultimo Miglio e la Connessione Locale**

- **Il Doppino:** Da ogni telefono di casa partono due cavi di rame (il famoso doppino) che arrivano dritti alla centrale locale più vicina dell'azienda telefonica (distanza tra 1 e 10 km).
    
- **UCR (Unità di Concentrazione Remota):** Nelle piccole località o zone isolate, al posto di una vera centrale c'è un "concentratore" (un armadio in strada). Raccoglie i doppini degli utenti e li spedisce tramite fibra ottica (a 2 o 8 Mb/s) alla vera centrale urbana più vicina.
    

### **La Gerarchia (Dal Comune alla Nazione)**

Dal basso verso l'alto, ecco i nodi che compongono l'albero della rete PSTN:

1. **CU / CRU (Centrale Urbana / Centrale di Rete Urbana):** È il livello base di commutazione per un Comune o quartiere. Gestisce i collegamenti diretti tra i telefoni di quell'area.
    
2. **SGU (Stadio di Gruppo Urbano):** È un livello superiore che serve un'area molto più vasta (60-80 mila numeri). A un SGU sono collegate decine di CU e CRU sottostanti.
    
3. **SGT (Stadio di Gruppo di Transito):** È il livello regionale/provinciale. Raccoglie tutto il traffico degli SGU di una regione.
    
4. **CN (Centrale Nazionale):** Il vertice della piramide. Gestisce il traffico tra regioni diverse (collegando gli SGT tra loro).
    

### **Come viaggia una chiamata (La regola della scalata)**

Il percorso della chiamata dipende da dove si trova il destinatario. La rete cerca di risolvere la connessione al livello "più basso" possibile:

- **Chiamata allo stesso quartiere:** Se chiami il tuo vicino di casa, i vostri due doppini arrivano alla _stessa centrale locale_. Il commutatore vi collega elettricamente subito lì. Fine.
    
- **Chiamata nello stesso comune/città:** Se chiamante e chiamato sono su centrali locali diverse, ma condividono la stessa centrale interurbana (CU), il percorso sale di un gradino, si collega alla CU e scende al chiamato.
    
- **Chiamata Lunga Distanza:** Se non c'è una CU in comune (es. chiami da Milano a Palermo), il percorso deve "scalare la gerarchia" fino a trovare un nodo in comune (probabilmente passerà dalla Centrale Nazionale).
    

### **Il dettaglio fondamentale per gli ISP (Internet Service Provider)**

Gli appunti fanno un'osservazione importantissima per l'esame riguardo allo **SGU (Stadio di Gruppo Urbano)**.

- È esattamente in questo snodo (lo SGU) che i vari provider di Internet (come Vodafone, Fastweb, Wind) "attaccano" i loro macchinari alla rete nazionale di Telecom/TIM.
    
- **Cosa succede quando cambi operatore a casa?** Nessun tecnico viene a scavar ti il giardino per posare un nuovo cavo. Molto semplicemente, allo SGU di competenza, un tecnico stacca il tuo cavo dal macchinario del vecchio provider e lo attacca a quello del nuovo provider. Il provider si preoccupa e paga solo per gestire i collegamenti da quello SGU in poi.
    
