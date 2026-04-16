La fibra ottica è un mezzo trasmissivo che non trasporta energia elettrica, ma **luce**. È il mezzo di punta per le comunicazioni a *grandissima distanza* e ad *altissima velocità*.
Per sua natura **subisce meno le interferenze degli agenti atmosferici**.

**1. Materiali e Vantaggi**

- **Materiali:** È realizzata in purissimo **vetro (silice)** o, per utilizzi a cortissimo raggio e a basso costo, in materiali plastici.
    
- **Vantaggi principali:** Larghezza di banda teoricamente infinita, bassissima attenuazione (il segnale viaggia per decine di km senza bisogno di ripetitori) e totale **immunità alle interferenze elettromagnetiche** (essendo vetro, non fa da antenna e non soffre di diafonia). Inoltre è sottile e leggera.
    

**2. Come funziona e Convenzione dei Bit**

Il principio di comunicazione è il più semplice possibile: si accende e si spegne una luce.

- **Convenzione:** Un impulso di luce = **bit 1**. Assenza di luce = **bit 0**.
    

**3.  Come funziona fisicamente (Il Fenomeno della Riflessione Totale Interna)**

Come fa la luce a curvare e seguire il cavo senza uscire fuori? Sfrutta la fisica dell'ottica.

La fibra è composta da un cilindro interno (**Core** o nucleo) avvolto da un cilindro esterno (**Cladding** o mantello). Entrambi sono di vetro, ma hanno densità diverse (indici di rifrazione differenti).
![[Pasted image 20260416124221.png]]

- Se un raggio di luce colpisce il confine tra core e cladding con un angolo molto piatto (superiore all'angolo critico), **rimbalza completamente all'interno come se fosse uno specchio**, senza disperdersi. Questo fenomeno si chiama _riflessione totale interna_.
    
- **Da cosa dipende?** Dipende dalla differenza esatta tra l'indice di rifrazione del core e quello del cladding (il core deve essere otticamente più "denso") e dall'angolo con cui entra la luce.
    

**4. Fibre Monomodali e Multimodali**

- **Fibra Monomodale (Single-mode):** Ha un core sottilissimo (circa 8-10 micron), grande quanto la lunghezza d'onda della luce stessa. La luce non può rimbalzare a zig-zag, ma è **costretta a viaggiare in un'unica linea retta** (un solo "modo"). Non c'è dispersione, rendendola perfetta per le grandissime distanze (dorsali oceaniche).
	- La **velocità** teorica massima è di **100.000 Gbps**(100 Tbps), quella reale è di *10 Gbps*, che è il limite di conversione dei segnali elettrici in segnali luminosi (ottici).
	![[Pasted image 20260416124356.png]]


- **Fibra Multimodale:** Ha un core abbastanza largo (es. 50 o 62.5 micron). La luce entra formando **vari raggi che rimbalzano sulle pareti con angolazioni diverse**. Questi diversi percorsi sono chiamati "modi". Poiché i raggi fanno percorsi diversi, alcuni arrivano prima e altri dopo, "spalmando" il segnale nel tempo. È usata per distanze medie (es. all'interno di un campus).
	- multimodale **Step index**: l'indice di rifrazione cambia repentinamente.
	- multimodale **gradex index**: l'indice di rifrazione cambia gradualmente (*riduce la dispersione modale*)
![[Pasted image 20260416124440.png]]
    
|**Tipo Fibra**|**Diametro Core [μm]**|**Diametro Cladding [μm]**|
|---|---|---|
|Fibra Monomodale|8,0 - 12,0|125,0|
|Fibra Multimodale|50,0 - 62,5|125,0|



**5. Generazione e Ricezione del segnale**

- **Come si genera (Sorgente):** Si usano due tecnologie. I **LED** (economici, luce più diffusa, usati per le fibre multimodali) oppure i diodi **Laser** (costosi, fascio precisissimo e potente, usati per le fibre monomodali).
    
- **Come si riceve:** All'altro capo del cavo c'è un **Fotodiodo**. È un sensore che rileva gli impulsi luminosi in arrivo e li ritraduce istantaneamente in impulsi elettrici comprensibili per il computer.
	- ha tempi di trasformazione di 

Quindi la sorgente dati **invia una segnale elettrico**, che viene convertito dal *modulatore TX ottico* che converte il segnale elettrico in luminoso. Il segnale transita sul canale ottico (fibra ottica). Infine il segnale luminoso arriva al *demodulatore RX ottico* che trasforma la luce in segnale elettrico per il destinatario.
![[Pasted image 20260416123846.png]]

Differenza tra LED e Laser per la generazione della luce:

|**Elemento**|**LED**|**Laser a Semiconduttore**|
|---|---|---|
|_Tasso di trasmissione dati_|Bassa|Alta|
|_Tipo di fibra_|Multimodale|Multimodale e monomodale|
|_Distanza_|Breve|Lunga|
|_Durata_|Lunga|Breve|
|_Sensibilità alla temperatura_|Scarsa|Elevata|
|_Costo_|Basso|Alto|


**6. Come si possono collegare le fibre (3 modi)**

Se devi unire due cavi rotti o prolungarne uno, hai tre strade, con costi e precisioni differenti:

1. **Connettori ottici:** Simili alle prese a muro. Si attaccano e staccano facilmente, ma perdono circa il 10-20% della luce al passaggio.
    
2. **Splicing (Giunzione) meccanico:** Le due estremità vengono tagliate di netto, allineate in un tubetto e incollate con un gel speciale. Discreta precisione.
    
3. **Fusione ottica:** È il metodo migliore. Un macchinario speciale fonde letteralmente a caldo il vetro delle due estremità, unendole a livello molecolare. La perdita di luce è quasi zero.
    

**7. Utilizzi pratici vs Cavi in Rame**

- **Utilizzi:** Dorsali transoceaniche (che collegano i continenti sott'acqua), reti metropolitane, connessioni FTTH (la fibra che arriva fin dentro i nostri modem di casa).
    
- **Differenza dal rame (Pro e Contro):** La fibra stravince per velocità e distanza. Tuttavia, le terminazioni e i macchinari per la fibra costano molto di più rispetto alle porte Ethernet. Inoltre, la fibra non può trasportare corrente per alimentare dispositivi (come fa il rame con il PoE) e, se piegata troppo bruscamente, il vetro interno si spezza irreparabilmente, mentre il rame si piega senza problemi.
    

