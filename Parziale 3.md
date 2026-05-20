
# Livello di rete 

Di cosa si fa carico 

Compiti principali

In base a cosa si realizza il livello di rete (principi/decisioni)

Servizi con e senza connessione

## Principi di commutazione 

Definizione commutazione 

Scelta della tecnica in base a: ...

### Commutazione di circuito

img con spiegazione : 
da spiegare meglio

- router instradatori
- ritardo di instaurazione


## Commutazione di messaggio 

- Store and forward 

img da spiegare 

Non c'è una connessione.

Altra img da spiegare 

- Ritardo di trasferimento 

Il servizio di trasferimento non può consentire una comunicazione interattiva.

Non va bene per grandi file, quindi si divide in pacchetti.

## Commutazione di pacchetto 

Informazione divisa in unità di lunghezza massima predefinita: pacchetti.

Modalità: datagramma; circuito virtuale

### Spiegazione datagramma con immagine

Conto proprio, intestazione con dati aggiuntivi

ordine sparso, persi, duplicati.
Molte cose insieme ma si possono perdere

### Spiegazione circuito virtuale con immagine 

Problema del continuo utilizzo di un percorso

#### Algoritmi di routing
Cosa fanno 
Statici e dinamici (o adattivi) -> in base a cosa differiscono tra loro

Algoritmo in base al tipo di sottorete 
- sessione di routing 

Cosa ci si aspetta da un algoritmo di routing  (6 punti)

- metrica -> cosa è, cosa utilizza.
	- metrica inferiore

- Principio di ottimalità (CON IMG e spiegazione)

- bilanciamento del carico
	- modalità di load balancing (equal-cost e unequal-cost)

- termine **convergenza**
	- tempo di consistenza (ha senso solo per alg. dinamici)


### Principali Algoritmi di Routing Statici
sono 3

#### Shortest Path Routing 

Con immagine da commentare (migliora di molto il commento, è troppo specifico all'esempio e mancano dei dettagli generali)

- interdistanze 

#### Flooding

cosa fe 
perche non conviene con molti pacchetti 

Tecniche per migliorarne il traffico generato 
(contatore di hop, scarta alla seconda vista, selective flooding)

#### Flow based routing

calcolo in anticipo

Informazioni necessarie per applicarlo

Assunzioni (2)

$$\text{ritardo singola linea}=\frac{\text{traffico sulla linea}}{\text{traffico totale della rete}}$$
Come calcolare il ritardo medio dell'intera rete: somma pesata dei ritardi delle linee  
Su cosa si basa questo metodo (flow based routing) considerata una topologia nota(6 punti)

### Principali algoritmi di routing dinamici 
sono 2 

#### Distance Vector

Ho un vettore di ritardi per ciascun nodo che ho a disposizione.
Quindi ciascun nodo avrà un vettore.
(controlla poi, può confondere)

Router stima i vicini con **pacchetti ECHO**, contando quanto ci mettono a tornare indietro. (viene fatto più volte come test)

Ad ogni intervallo i router condividono le loro tabelle con i vicini. Ogni router ricalcola la propria in base alle nuove informazioni 

Immagini con spiegazione (sono 3 tabelle, 2 simili tra loro)

- Paradosso dello scambio all'infinito
#### Link State Routing

Ogni tot i router testano i loro vicini e condividono le info con gli altri.
Ogni router ricostruisce localmente la topologia completa della rete.

E' suddiviso in 5 passaggi: 
Chi c'è vicino -> pacchetti HELLO
Quanto sono lenti i vicini -> pacchetti ECHO (Costruisce la **Neighbour Table**)
Viene costruito un pacchetto LSP (Link State Packet) che contiene ...
Invio dell'LSP con flooding.
Calcolo del cammino minimo tra tutti i router avendo ricevuto gli LSP.


### Routing Gerarchico 

Per sottoreti molto grandi.

La rete viene divisa in regioni.

I router all'interno della stessa regione si conoscono.
Per comunicare con uno all'esterno, un router interno da da **router di confine**
Quindi si possono considerare due livelli di routing (interno e di confine/esterno)

### Broadcast Routing
