
La **Quality of Service (QoS)** definisce l'insieme di parametri che descrivono le prestazioni, le garanzie e l'affidabilità che un livello della rete offre al livello superiore per una specifica comunicazione.



**Il Compromesso (Trade-off) della QoS:**

Ottenere una QoS altissima e garantita al 100% (nessun errore, ordine di arrivo perfetto) è **molto costoso in termini di tempo e risorse** (richiede continue conferme ACK, algoritmi di riordino e ritrasmissioni). Pertanto, la rete cerca di fornire a ogni applicazione solo il tipo di QoS di cui ha strettamente bisogno.

**Esempi pratici di esigenze diverse:**

1. **Trasferimento Dati (es. Email o Download File):** Richiede **affidabilità totale** (se manca un pacchetto, il file è inutilizzabile), ma _tollera bene i ritardi e il jitter_ (non è un dramma se un'email arriva due secondi dopo).
    
2. **Streaming Audio/Video in tempo reale (es. Telefonata VoIP o Skype):** Richiede _basso ritardo e pochissimo jitter_ (altrimenti la voce arriva a scatti e in ritardo), ma **tollera bene una bassa affidabilità** (se si perde un pacchetto audio, si sentirà solo un microscopico disturbo per una frazione di secondo, ma la conversazione può continuare).