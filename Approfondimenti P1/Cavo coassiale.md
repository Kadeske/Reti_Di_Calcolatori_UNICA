Il **cavo coassiale** (spesso chiamato semplicemente _coax_) è stato progettato per risolvere i due più grandi difetti del doppino telefonico: la scarsa larghezza di banda e la vulnerabilità alle interferenze. 
Infatti è più isolato del doppino e raggiunge distanze più lunghe.

Esistono 2 tipi di cavo coassiale:
- 50 $\ohm$: su distanze da 1km arriva a **2Gbps** utilizzato per le trasmissioni **digitali** fin dall'inizio.
- 75 $\ohm$: non ha differenze dal 50 $\ohm$, è solamente arrivato dopo ed è stato assegnato a scopi differenti: trasmissioni **analogiche** (come le TV via cavo)


**Composizione e Schermatura**

A differenza dei due fili affiancati del doppino, il cavo coassiale ha una struttura cilindrica e concentrica, composta da quattro strati:

1. **Anima centrale:** Un filo di rame rigido che trasporta fisicamente il segnale elettrico.
    
2. **Isolante:** Uno spesso strato di materiale plastico che avvolge l'anima.
    
3. **Maglia metallica (Schermatura):** Una fitta rete di rame intrecciato (o un foglio di alluminio) che avvolge l'isolante. Finge da "gabbia di Faraday".
    
4. **Guaina esterna:** Il rivestimento in plastica nera o bianca che protegge il cavo dalle intemperie.

![[Pasted image 20260416122121.png]]
    
Questa struttura garantisce una **schermatura quasi perfetta**. La maglia metallica esterna blocca totalmente i rumori elettromagnetici dell'ambiente (impedendo che entrino) e al contempo evita che l'energia del segnale interno si disperda verso l'esterno.

**Vantaggi e Differenze rispetto al doppino**

- **Banda molto più ampia:** Grazie alla schermatura eccellente, il cavo coassiale offre una larghezza di banda analogica enormemente superiore rispetto al doppino.
    
- **Distanza e Velocità:** Può trasportare i dati a velocità più elevate e su distanze molto più lunghe prima di aver bisogno di un ripetitore per rinvigorire il segnale.
    

**Utilizzi**

- **In passato:** Era il re indiscusso delle reti informatiche. Le prime reti LAN (Ethernet) erano tutte cablate con grossi e rigidi cavi coassiali.
    
- **Oggi:** Nelle reti LAN è stato sostituito dal doppino (Cat 5/6) perché più economico e flessibile. Tuttavia, il coassiale è ancora lo standard assoluto per la **TV via cavo** e le antenne televisive, oltre a essere usato in alcune reti Internet metropolitane miste (Fibra fino al quartiere, Coassiale fino a casa).
    

**Modalità Trasmissive: Come sfruttare tutta questa banda?**

Avendo un "tubo" così capiente, gli ingegneri hanno sviluppato due modi per far viaggiare i dati al suo interno:

1. **Trasmissione in Banda Base (Baseband):** Tutta la capacità del cavo viene usata per trasmettere un **singolo segnale digitale**. È un po' come avere un'autostrada a 10 corsie, ma usarla per far passare un solo TIR gigante alla volta. Era il metodo usato nelle vecchie reti LAN dei computer.
    
2. **Trasmissione in Banda Larga (Broadband):** Sfrutta la tecnica del multiplexing **FDM** (Frequency Division Multiplexing). L'enorme larghezza di banda del cavo viene "affettata" in tanti **canali separati**, ognuno funzionante su una frequenza diversa.
    
    - _L'esempio perfetto è la TV:_ sullo stesso cavo fisico viaggiano contemporaneamente centinaia di canali televisivi diversi, senza che si disturbino a vicenda.
        
    - _Nelle reti dati:_ Questo metodo permette di **suddividere la banda in due canali direzionali**: un gruppo di frequenze viene riservato al traffico in discesa verso l'utente (Download) e un altro gruppo al traffico in salita verso la rete (Upload), permettendo a Internet e TV di convivere sullo stesso filo.