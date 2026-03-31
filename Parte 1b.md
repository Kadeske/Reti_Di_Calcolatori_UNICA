### 1. I Concetti di Base della Standardizzazione

Per far sì che dispositivi e sistemi sviluppati da aziende diverse in tutto il mondo possano comunicare tra loro, è fondamentale stabilire delle regole comuni. Nel mondo delle telecomunicazioni e dell'informatica, gli standard si dividono in due macro-categorie:

- **Standard _de facto_**: Sono standard "di fatto" o di mercato; si tratta di tecnologie e protocolli che si sono imposti nell'uso comune grazie al loro successo commerciale, pur senza un'investitura iniziale da parte di un ente normativo.
    
- **Standard _de jure_**: Sono gli standard formali e legali, approvati e definiti "per legge" da organizzazioni ufficiali preposte alla normazione.
    

---

### 2. L'ITU (International Telecommunication Union)

L'ITU è un'organizzazione con radici storiche molto profonde, nata molto prima dell'avvento dei computer moderni, dimostrando come la necessità di standardizzare le comunicazioni sia un problema antico.

- L'ITU è stata fondata nel 1865 dai rappresentanti dei Governi Europei, con l'obiettivo originario di standardizzare l'uso del telegrafo.
    
- A testimonianza della sua importanza globale, nel 1947 l'ITU è diventata ufficialmente un'agenzia dell'ONU.
    
- A livello organizzativo, l'ITU è divisa in tre settori specializzati:
    
    - **ITU-R**: È il settore Radiocomunicazioni, che si occupa della gestione e dell'assegnazione delle frequenze.
        
    - **ITU-T**: È il settore dedicato alla standardizzazione delle telecomunicazioni e, nello specifico, della trasmissione dati.
        
    - **ITU-D**: È il settore Sviluppo, che ha l'obiettivo di promuovere lo sviluppo tecnologico.
        

**Approfondimento sull'ITU-T**

- L'ITU-T, che fino al 1 marzo 1993 era conosciuto con l'acronimo C.C.I.T.T. (Comitè Consultatif International Telegraphique Telephonique), ha il compito di suggerire degli standard che possono poi essere adottati dalle varie nazioni o aziende.
    
- Questo organo è composto da una pluralità di attori: le Amministrazioni (come le PTT nazionali o il Dipartimento di Stato USA), operatori privati riconosciuti (es. AT&T, Vodafone), organizzazioni regionali di telecomunicazioni (come l'europea ETSI), industrie del settore, enti scientifici e altre organizzazioni come ISO, banche o compagnie aeree.
    
- Strutturalmente, l'ITU-T è organizzato in modo fortemente gerarchico: è composto da 10 Gruppi di Studio (Study Groups), che si suddividono a loro volta in Gruppi di Lavoro (Working Parties), i quali sono formati infine da Gruppi di Esperti (Expert Teams).
    

---

### 3. L'ISO (International Standard Organization)

Mentre l'ITU è storicamente legata alle telecomunicazioni pure, l'ISO si occupa di normazione in ambiti molto più vasti, tra cui ovviamente l'informatica.

- L'ISO è stata fondata nel 1946 e comprende ben 157 stati con le loro rispettive organizzazioni di standardizzazione nazionali.
    
- Tra i membri nazionali che compongono l'ISO troviamo enti molto noti, come l'ANSI (Stati Uniti), il BSI (Regno Unito), l'ANFOR (Francia), il DIN (Germania) e l'UNI per l'Italia.
    
- La struttura dell'ISO prevede la creazione di Comitati Tecnici (Technical Committee), come ad esempio il "TC97" dedicato a "Computer e elab. informazioni", che a loro volta si diramano in Sotto-Comitati (Sub Committee) e poi in Gruppi di Lavoro (Working Group).
    

**Il processo di creazione di uno standard ISO**

La definizione di un nuovo standard segue un iter rigoroso, descritto nel documento come una "Macchina a stati finiti":

- **CD (Committee Draft)**: È la fase iniziale, in cui una bozza viene proposta da un Working Group (WG).
    
- **DIS (Draft Int Standard)**: Successivamente, se la bozza passa, diventa un documento approvato a maggioranza.
    
- **IS (International Standard)**: Rappresenta lo stadio finale e la pubblicazione ufficiale dello standard.
    

---

### 4. L'IEEE (Institute of Electrical and Electronics Engineers)

L'IEEE è un'altra istituzione fondamentale, particolarmente focalizzata sull'ingegneria elettrica, elettronica e sui protocolli di rete locale (LAN).

- L'IEEE è l'ente che gestisce la vasta e celebre famiglia di standard di rete identificata dai gruppi di lavoro "802.x".
    
- All'interno di questa famiglia rientrano standard di uso quotidiano, come le Wireless LAN (comunemente note come WiFi), le Personal area network (come lo standard Zigbee), e le reti wireless a banda larga (come il WiMAX).

![[Pasted image 20260331150627.png]]
La freccia in giù indica che è meno utilizzato.


I gruppi di lavoro possono essere:
- Required
- Recommended
- Experimental
- Obsolete

---

### 5. Standardizzazione di Internet (La gestione degli RFC)

Internet ha un ecosistema di normazione separato e peculiare, nato in un ambiente accademico e di ricerca, e basato sulla pubblicazione aperta di documenti tecnici.

- L'organo direttivo principale è l'**IAB** (Internet Architecture Board), attivo dal 1983, che ha il compito di definire gli **RFC** (Request For Comments), ovvero i documenti ufficiali che descrivono i protocolli di Internet.
    
- L'IAB coordina due entità operative: l'**IRTF** (Internet Research Task Force) che si occupa della ricerca a lungo termine, e l'**IETF** (Internet Engineering Task Force) focalizzata sull'ingegneria e sulla tecnologia attuale.
    
- Ai processi di studio e discussione partecipa anche la **ISOC** (Internet Society), chiunque ci si può associare ed è presente in ogni nazione. "Raggruppa i lavoratori da tutto il mondo".

![[Pasted image 20260331150835.png]]

**Il processo di standardizzazione di un RFC**

Come per l'ISO, anche la trasformazione di un RFC in standard ufficiale segue una precisa "Macchina a stati finiti":

- **PS (Proposed Standard)**: È il primo passo in cui lo standard viene formalmente proposto.
    
- **DS (Draft Standard)**: Dopo un periodo di 4 mesi, il documento passa allo stato di bozza avanzata.
    
- **IS (Internet Standard)**: Dopo ulteriori 4 mesi di test e validazioni, il protocollo diventa uno standard ufficiale di Internet.
    
![[Pasted image 20260331151002.png]]

(Ci sono molti )

---

### 6. Unità di Riferimento

Per comprendere le prestazioni delle reti (es. velocità di trasmissione o dimensioni dei pacchetti) è necessario utilizzare correttamente i prefissi del Sistema Internazionale.

- **Multipli (Prefissi accrescitivi)**: Partono dal Kilo (1.000, 10^3) per salire a Mega (1.000.000, annotato nel documento con un probabile refuso tipografico come 10^8 al posto del corretto 10^6), Giga (10^9), Tera (10^12), Peta (10^15), Exa (10^18), Zetta (10^21) e Yotta (10^24).
    
- **Sottomultipli (Prefissi diminutivi)**: Partono da milli (0,001, 10^-3) per scendere a micro, nano (10^-9), pico (10^-12), femto (10^-15), atto (10^-18), zepto (10^-21) e yocto (10^-24).