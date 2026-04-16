Il **Doppino Telefonico** (in inglese _Twisted Pair_) è il mezzo trasmissivo cablato più antico, economico e ancora oggi il più diffuso per collegare i computer all'interno di una rete locale (LAN) o per l'ultimo miglio della linea telefonica.

### **Da cosa è composto e perché è "intrecciato"**

Il doppino base è formato semplicemente da **due fili di rame** (spessi circa 1 millimetro), ciascuno ricoperto da una guaina di plastica isolante.

La caratteristica ingegneristica geniale è che questi due fili non corrono dritti e paralleli, ma sono **intrecciati** (attorcigliati) l'uno sull'altro a formare un'elica.

- **A cosa serve l'intreccio?** Quando la corrente elettrica viaggia in un filo, genera un campo elettromagnetico che "sporca" il filo vicino (questo disturbo reciproco si chiama **diafonia** o _crosstalk_). Inoltre, due fili paralleli si comportano come un'antenna, catturando i rumori elettrici dell'ambiente circostante. Intrecciando i fili, le onde elettromagnetiche *si irradiano in direzioni opposte a ogni giro*, **annullandosi a vicenda** e proteggendo il segnale.
    

### **I Limiti**

Nonostante sia pratico, il doppino ha i limiti fisici peggiori tra i mezzi guidati:

- **Forte Attenuazione:** Il segnale elettrico perde potenza molto velocemente mentre viaggia nel rame. Sulle lunghe distanze, è necessario installare dei "ripetitori" ogni pochi chilometri per amplificare il segnale, altrimenti si spegne.
	- è la **legge di joule:** più è lungo il cavo, più calore produce, quindi disperde energia e peggiora il segnale.
    
- **Banda limitata:** Ha una larghezza di banda molto inferiore rispetto al cavo coassiale o alla fibra ottica.
	- La **larghezza di banda** è funzione della sezione del conduttore e della lunghezza del cavo.
    

### **Varietà: La Schermatura (UTP vs STP)**

Per combattere le interferenze (ad esempio se il cavo deve passare vicino a grossi motori industriali o cavi della corrente), esistono diverse varianti di schermatura:

- **UTP (Unshielded Twisted Pair - Non schermato):** È il cavo LAN classico che usiamo in casa o in ufficio. Ha solo la guaina di plastica esterna. È economico, flessibile, ma più vulnerabile ai rumori esterni.
- **STP (Shielded Twisted Pair - Schermato):** Includono una schermatura metallica per ogni coppia di cavi. (ma nessuna schermatura esterna).
- **S/UTP:** è un cavo UTP ma con schermatura *esterna*.
- **S/STP:** ha sia schermatura interna (per ciascun cavo) che esterna.

![[Pasted image 20260416121007.png]]

### **Le Categorie (Cat 3, Cat 5, Cat 6...)**

I doppini UTP si dividono in categorie in base alle loro prestazioni.

(*TIA/EIA:* norma tecnica principale per il cablaggio strutturato in edifici commerciali.)
 In **TIA/EIA** e versioni successive si definisce una classificazione dei sistemi per cavi e connettori impiegati in un doppino.

Le categorie ufficialmente riconosciute sono: 
- **Cat. 3**
- **Cat. 5**
- **Cat. 6**