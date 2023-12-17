# Il Livello di Trasporto

Il livello di trasporto gestisce la conversazione tra mittente e
destinatario, nascondendo tutti i dettagli relativi al trasporto delle
informazioni lungo la rete.

I compiti del livello si possono inizialmente riassumere come nel
disegno sottostante: prende i dati dal livello applicazione, li divide
in pacchetti, vi aggiunge un'intestazione e li passa al sottostante
livello di rete.


<img style="width: 100%" alt="Segmentazione" src="../images/segmentation.png">


La Suite Internet offre a livello di trasporto due protocolli:

- **TCP** (Transmission Control Protocol) connesso e affidabile
- **UDP** (User Datagram Protocol) non connesso e non affidabile

<br>

A livello di trasporto, i termini connessione e affidabilità significano:

1.  ***connessione:***

    Un servizio si dice connesso (a livello di trasporto) quando si preoccupa di stabilire una comunicazione 
    con il destinatario preventiva all'invio reale dei dati.

2.  ***Affidabilità:***

    Un servizio si dice affidabile (a livello di trasporto) quando si preoccupa di rinviare al destinatario 
    ogni pacchetto che non gli è arrivato (o che gli è arrivato corrotto).


Un servizio di trasporto connesso e affidabile si preoccupa di stabilire una comunicazione preventiva con il destinatario.
Se questi è disponibile, invia i pacchetti numerandoli alla partenza e riordinandoli all'arrivo; in caso di pacchetti
corrotti o mancanti si preoccupa di richiedere al mittente un nuovo invio di dati, assicurando un arrivo completo degli stessi,
oppure una dichiarata impossibilità a ricevere i dati.

Un servizio di trasporto non connesso e non affidabile inizia subito l'invio dei pacchetti nell'ordine in cui essi sono arrivati dal livello precedente.
All'arrivo scarta semplicemente i pacchetti corrotti, senza richiedere alcun reinvio, toglie l'intestazione del livello di trasporto 
e passa il dato al livello superiore.


!!! note "Perché due protocolli?"

    **TCP è connesso e affidabile.**

    Alcune applicazioni, come ad esempio quelle per inviare mail o files,
    hanno bisogno di essere sicure che i loro dati arrivino tutti a
    destinazione e possono accettare piccoli rallentamenti nel trasporto.

    Queste applicazioni scelgono TCP.

    <br>
    
    **UDP è non connesso e non affidabile.**

    Alcune applicazioni, ad esempio quelle di video e audio streaming,
    gestiscono i dati in maniera che anche con piccoli "buchi" o "errori"
    essi siano fruibili; preferiscono "scartare" alcune parti del dato pur
    di proseguire nella trasmissione e non necessitano di un riordinamento.

    Queste applicazioni scelgono UDP.


