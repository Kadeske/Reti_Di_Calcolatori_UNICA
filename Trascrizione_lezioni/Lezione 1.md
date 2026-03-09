Differenza tra reti di calcolatori e sistemi distribuiti

Cosa intendiamo per calcolatori: un computer, mainframe, un qualcosa che possa processare I/O e con possibilmente una memoria

Obiettivo reti: condividere risorse ed avere alta affidabilità.

Alta affidabilità: es. dati persistenti, transazioni sicure per una banca.
Come posso sapere come è andata a finire una comunicazione?


### DIGITAL DIVIDE 
differenza tra soggetti utilizzatori e società utilizzatrici di strumenti di  Information e Communication Technologies e soggetti e società non in grado di impiegare o disporre di strumenti ICT.

**pacchetto**: sottoinsieme ordinato di dati con un intestazione o senza.
Il pacchetto a ciruito virtuale... 

3 tipi di reti: 
- broadcast: viene collegato a tutti i nodi
- multicast: individuano un sottoinsieme di nodi a cui collegarsi
- point-to-point: individuano un solo nodo a cui collegarsi

### Classificazione di reti 
- **LAN**  (Local)
- **MAN** (Metropolitan)
- **WAN** (Wide)
- Wirless network
- Home network
- Internetworks
![[Pasted image 20260309170134.png]]
Perche ordine di grandezza max 1km? boh non ha risposto, ha iniziato a fare esempi tipo "per collegare monserrato a qua non possiamo dire Local Area Net"


### Topologia trasmissiva 

La rete è divisa in **nodi di commutazione** e **linee di trasmissione/comunicazione**

![[Pasted image 20260309171258.png]]

Le linee sono in grado di far comunicare solo tra nodo e nodo? No, posso essere instradate informazione partite da un altro nodo precedente.
Per questo si dividono in  linee di trasmissione e linee di comunicazione.

![[Pasted image 20260309171632.png]]
Modello token ring: c'è un token che indica quando un nodo può comunicare (si rferisce a (b))
Mod token bus: uguale ma è un bus

### Wireless Networks 

Tipologie:
- System interconnection
- Wireless LANs
- Wireless WANs

### Inter network 
Due reti collegate da un **gateway**.

![[Pasted image 20260309171949.png]]

Il gateway è una macchina che interfaccia su 7 livelli (?)

Le due reti sono diverse, con protocolli, algoritmi, token, controlli, etc... diversi.
Spesso capita che una WAN sia divisa in due (o più) reti con protocolli differenti, che quindi necessitano di un gateway per comunicare.
L'operazione utilizzata dai gateway è il **Tunnelling**.

## PASSIAMO AL SOFTWARE DELLE RETI 

L'obiettivo è ridurre la complessità (e quindi i tempi).

"Come posso renderlo più semplice?" "Ridurre/dividere i problemi"
Ma cosa significa ridurre i problemi in una rete?
In una rete si dividono in layer, con ciascuno un compito diverso.

 Una macchina di livello n per comunicare con un altra di livello n deve utilizzare delle regole per il colloquio dette **protocolli**.
Protocolli: Regole per il colloquio di due macchine di livello n.

Se organizzo un file da inviare in 10 trame, e la trama 4 arriva errata, devo chiedere l'invio solo della trama 4. Questo è il compito dei protocolli. Risparmiano quindi dati.

Ho quindi diviso i compiti in livelli diversi. (già detto 10 minuti fà)

![[Pasted image 20260309172955.png]]

Il livello n-esimo di una macchina colloquia con il livello n-esimo di un altra macchina.

Quindi se le macchine sono diverse basta che abbiano gli stessi livelli e protocolli per poter comunicare.
Tutto però passa attraverso il mezzo fisico.

I dati non passano da livello a livello direttamente, ma gli attraversano tutti venendo incapsulati man mano che passano fino ad arrivare a quello più alto.




