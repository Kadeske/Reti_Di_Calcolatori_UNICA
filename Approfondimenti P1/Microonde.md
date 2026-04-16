
Salendo di frequenza (**sopra i 100 MHz**), le onde smettono di espandersi in tutte le direzioni e *iniziano a comportarsi quasi come un raggio di luce*.

**1. Direzionalità e Allineamento (Line-of-Sight)**

- Le microonde viaggiano quasi in **linea retta**.
    
- Si usano **antenne paraboliche** per "mettere a fuoco" l'onda e concentrare tutta l'energia in un raggio strettissimo. Questo permette di avere un **rapporto segnale/rumore molto alto** (segnale potentissimo e pulito).
    
- _Il vincolo:_ Le antenne trasmittenti e riceventi devono essere **accuratamente allineate** a vista. Se non si "guardano" perfettamente, la comunicazione non avviene.
    
- _Il vantaggio:_ Grazie a questa estrema direzionalità, puoi mettere più antenne vicine sullo stesso tetto che comunicano con destinazioni diverse senza che si disturbino tra loro.
    

**2. L'Ostacolo Principale: La Curvatura Terrestre**

Dato che viaggiano dritte come un raggio laser, le microonde non possono seguire la curva del pianeta. Se due città sono troppo lontane, la "pancia" della Terra si metterà fisicamente in mezzo bloccando il segnale.

- Per risolvere il problema, si è costretti ad **aumentare l'altezza delle antenne** (più l'antenna è alta, più riesce a "guardare oltre" l'orizzonte) oppure a installare una catena di **ripetitori** intermedi.
    
- L'immagine nei tuoi appunti riporta proprio la formula geometrica (e il relativo disegno) che lega la distanza raggiungibile all'altezza dell'antenna: $d = \sqrt{h \cdot 10^4 \cdot a}$ (dove $a$ è un fattore di correzione atmosferica).
    

**3. I Punti Deboli (Edifici, Multipath e Pioggia)**

- **Ostacoli solidi:** A differenza delle onde radio a bassa frequenza, le microonde **non attraversano molto bene gli edifici**.
    
- **Multipath Fading:** Anche le microonde rimbalzano, sdoppiandosi e creando interferenze distruttive al ricevitore. Se succede, il sistema è costretto a riallocare la trasmissione su un'altra banda di frequenza.
    
- **Il Meteo:** Hanno una **forte dipendenza dalle condizioni climatiche**. Le molecole d'acqua presenti nella pioggia o nella nebbia assorbono fisicamente l'energia delle microonde, abbattendo drasticamente il segnale.
    

**4. Utilizzi e Vantaggi Economici**

- **Impieghi comuni:** Telefonia cellulare, televisione, e comunicazioni telefoniche su lunga distanza (le dorsali che collegano le città).
    
- **Perché si usano?** Il vantaggio principale è puramente **economico e logistico**. Se devi collegare due città separate da una montagna, una valle o un'area urbana super-congestionata, installare due semplici tralicci (pali controventati) con delle parabole in cima costa infinitamente meno rispetto a scavare trincee per 50 Km per posare un cavo in fibra ottica.
    

---

Per aiutarti a visualizzare il problema del punto 2 (che di solito all'esame viene chiesto chiedendo di commentare proprio quel disegno delle due antenne), ho generato un piccolo simulatore della curvatura terrestre.

Prova ad abbassare l'antenna e guarda come il pianeta blocca letteralmente il raggio a microonde!

Mostrami la visualizzazione

Vuoi passare ora a come questo concetto viene portato nello spazio con i **Satelliti**?