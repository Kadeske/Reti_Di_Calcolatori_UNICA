I servizi **orientati alla connessione**: sono quelli in cui **l’ordine dei dati** è garantito. Nel caso di sistemi simplex, in cui nel canale possono viaggiare più pacchetti alla volta esclusivamente in un senso, non si hanno interferenze perché **il canale è ad uso esclusivo**.

Deve avere un **instaurazione** cioè determinare chi è pronto a comunicare e si tira su il canale, un trasferimento dati e un rilascio (butto giù il canale da ambo i lati).

Nei servizi privi di connessione: non vi è un unico canale di comunicazione, ma una **magliatura**, questo permette il trasferimento di più informazioni contemporaneamente perché si sfrutta meglio la rete utilizzando i nodi liberi disponibili. Questo servizio però **non garantisce l’ordine d’arrivo dei pacchetti**, quindi il ricevente si dovrà occupare di riordinarli, inoltre vi è un ritardo generale perché deve attraversare un percorso più frastagliato. Si dice che è a fase unica perché **ogni singolo pacchetto deve possedere l’indirizzo d’arrivo** perché sennò si perdono in rete in quanto vi sono tanto percorsi.

![[Pasted image 20260415161412.png]]

