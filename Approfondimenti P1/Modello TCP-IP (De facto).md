Ecco la sintesi del modello **TCP/IP**, seguendo la struttura dei tuoi appunti e mantenendo lo stesso stile sintetico e preciso.

Il modello **TCP/IP** (conosciuto anche come modello _Internet_ o _DoD_) è il modello di riferimento **de facto** su cui si basa l'intera rete globale. A differenza dell'ISO-OSI, è nato da esigenze pratiche e si divide in **4 livelli** principali:

---

### 1. Livello Host-to-Network (o Livello Link)

È il livello più basso e corrisponde all'unione dei livelli Fisico e Data Link dell'ISO-OSI.

- **Compiti**: Gestisce l'interfaccia tra l'host e il mezzo trasmissivo. Si occupa di come i pacchetti devono essere inviati fisicamente sulla rete (es. via cavo Ethernet o Wi-Fi).
    
- **Protocolli tipici**: Ethernet, 802.11 (Wi-Fi), PPP.
    

### 2. Livello Internet

È il cuore del modello e corrisponde al livello di Rete dell'ISO-OSI.

- **Compiti**: Permette agli host di inviare pacchetti in qualsiasi rete e farli viaggiare indipendentemente verso la destinazione. Si occupa dell'**instradamento** (routing) e della gestione degli indirizzi logici. Non garantisce l'ordine di arrivo.
    
- **Protocollo principale**: **IP** (Internet Protocol).
    

### 3. Livello di Trasporto

Permette la comunicazione diretta tra le applicazioni degli host (comunicazione end-to-end).

- **Compiti**: Riceve i dati dal livello superiore e, se necessario, li spezza in segmenti. Offre due tipologie di servizio:
    
    - **TCP**: Orientato alla connessione, affidabile, garantisce l'ordine e il controllo di flusso.
        
    - **UDP**: Privo di connessione, non garantisce l'ordine, è veloce e senza fronzoli.
        
- **Protocolli principali**: **TCP** e **UDP**.
    

### 4. Livello Applicazione

Include tutti i protocolli di alto livello che le applicazioni usano per comunicare. Riassume i livelli Sessione, Presentazione e Applicazione dell'ISO-OSI.

- **Compiti**: Fornisce i servizi direttamente all'utente (es. trasferimento file, posta elettronica).
    
- **Protocolli tipici**: HTTP (Web), FTP (File), SMTP (Email), DNS (Nomi di dominio).
    

---

