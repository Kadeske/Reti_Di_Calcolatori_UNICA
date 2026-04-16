### **1. Il Problema della Corrente Continua e la Modulazione**

Abbiamo visto che il doppino in rame è pessimo per trasmettere segnali digitali puri (corrente continua o DC) su lunghe distanze.

Per aggirare il problema, il modem genera un "suono" continuo (chiamato **portante d'onda sinusoidale**, di solito tra 1000 e 2000 Hz). Per trasmettere i bit (0 e 1), il modem altera leggermente questo suono continuo. Le tre tecniche base sono:

- **Modulazione d'ampiezza (AM):** Utilizza due diverse ampiezze per rappresentare 0 e 1.
    
- **Modulazione di frequenza (FSK):** Utilizza due o più toni.
    
- **Modulazione di fase:** L'onda portante viene spostata di 0 o 180 gradi ad intervalli uniformi.



### **2. La Regola d'Oro: Baud vs. Bit per secondo (bps)**

Il teorema di Nyquist afferma che anche con una linea a 3.000 Hz perfetta  non c’è alcun modo di ottenere un campionamento più veloce di 6.000 Hz.

Questa è la classica domanda a trabocchetto dell'esame. Baud rate e Bit rate **non sono la stessa cosa**!

- **Baud rate:** È il numero di "campioni" (o simboli) trasmessi in un secondo. Indica quante volte al secondo il segnale cambia stato. A causa del _Teorema di Nyquist_, su una linea telefonica analogica il limite massimo fisico è di circa **2.400 Baud**.
    
- **Bit rate (bps):** È la quantità effettiva di dati (0 e 1) trasmessi in un secondo.
    

**Il trucco ingegneristico:** Se il cavo ci limita a soli 2.400 "cambiamenti" al secondo (baud), come facciamo ad andare più veloci?

Semplice: facciamo in modo che ogni singolo cambiamento (simbolo) **trasporti più di un bit alla volta**. Se uso 4 livelli di tensione diversi invece di 2, con un solo simbolo trasmetto 2 bit (00, 01, 10, 11). A 2.400 baud avrò quindi una velocità di 4.800 bps!

### **3. QAM e i Diagrammi a Costellazione**

Per infilare ancora più bit dentro un singolo simbolo, gli ingegneri hanno combinato la modulazione di Ampiezza con quella di Fase, creando lo schema **QAM** (_Quadrature Amplitude Modulation_).

I grafici coi puntini nei tuoi appunti (le figure _b_ e _c_) sono i **diagrammi a costellazione**. Ogni puntino nero rappresenta una specifica combinazione di ampiezza e fase dell'onda.

- **QAM-16:** Ha 16 puntini. Visto che $2^4 = 16$, ogni puntino (simbolo) trasporta esattamente **4 bit**.
    
- **QAM-64:** Ha 64 puntini. Ogni puntino trasporta **6 bit**.
    
![[Pasted image 20260416170600.png]]

**Il problema del Rumore e la correzione TCM:**

Più puntini metti nel grafico, più questi sono vicini tra loro. Se la linea è rumorosa, il segnale arriva "sporco" e il modem ricevente potrebbe confondere un puntino con quello vicino, leggendo i bit sbagliati! Per risolvere questo problema, i modem moderni (dallo standard V.32 in poi) aggiungono dei bit extra di controllo (_bit di parità_) per correggere gli errori al volo (tecnica **TCM**).

### **4. Il Limite Fisico (Perché ci siamo fermati a 56 kbps?)**

I tuoi appunti si chiudono spiegando il tetto massimo invalicabile dei vecchi modem.

Con i vari standard (V.32, V.34, ecc.), stringendo sempre di più i puntini della costellazione, si era arrivati a un limite fisico di **33.600 bps**. Oltre questa soglia, il rumore del cavo analogico locale rendeva i puntini troppo vicini per essere distinti.

![[Pasted image 20260416170632.png]]

**Come si è arrivati al famoso standard V.90 a 56 kbps?**

Sfruttando un calcolo matematico sul Teorema di Nyquist: il canale telefonico ha un'ampiezza di 4.000 Hz. Nyquist dice che il campionamento massimo è il doppio (8.000 campioni/sec). Se usiamo 8 bit per campione (7 di dati e 1 di controllo, come negli USA), otteniamo $8.000 \times 7 = \mathbf{56.000\ bps}$. Questo era il limite matematico assoluto per una telefonata analogica!
