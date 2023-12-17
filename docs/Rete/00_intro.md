# Il livello di rete

Il livello di rete della suite Internet è probabilmente quello che di più aderisce negli scopi e nelle funzioni alla strutturazione teorica
stabilita nel modello OSI, che riconduce i compiti principali di questo livello ai seguenti compiti:

- l'**indirizzamento**, ovvero la possibilità di distinguere i dispositivi tra loro e di raggrupparli opportunamente.

- L'**impacchettamento**, ovvero la preparazione dei pacchetti adatti ad essere trasferiti nella rete Internet 
  per andare dal mittente al destinatario (adesso che con l'indirizzamento può distinguerli).

- L'**instradamento**, ovvero la scelta del percorso che un generico pacchetto dati deve compiere per andare dal mittente al destinatario.

- La **gestione delle congestioni**, che durante l'instradamento possono verificarsi se troppi pacchetti sono indirizzati verso un
  unico percorso di rete, eventualmente troppo trafficato.


Andando avanti nella trattazione cercheremo di capire chi si occupa di quale compito e possibilmente perché il livello di rete 
è organizzato in questo modo! 
Prima però... vediamo un po' di terminologia, indispensabile per capire i concetti a cui faremo riferimento.


## Terminologia


**host**<br>
Qualunque dispositivo che accede alla rete tramite un indirizzo IP, grazie al quale può essere identificato univocamente.

**routing (instradamento)**<br>
Scelta del percorso che un pacchetto IP deve compiere.

**router**<br>
Software che determina il routing. Poiché tipicamente queste operazioni vengono svolte su dispositivi dedicati,
il termine indica spesso anche l'apposito dispositivo di rete, in cui è stato installato il software per la selezione del percorso
dei pacchetti che transitano su di esso.

**tabella di routing**<br>
Set di informazioni che permettono al router di stabilire il percorso per ogni pacchetto in transito.



## Caratteristiche

A livello di rete distinguiamo 2 caratteristiche che ci permettono di
classificare i servizi offerti. Le caratteristiche sono:

1.  ***Connessione:*** Un servizio si dice connesso (a livello di rete) quando si preoccupa di stabilire un percorso con il
    destinatario preventivo all'invio reale dei dati. Prima si stabilisce un percorso dal mittente al destinatario, 
    poi si inviano tutti i pacchetti sempre in quella direzione.

    Viceversa, un servizio non connesso a livello di rete deve calcolare il tragitto per ogni pacchetto inviato.

2.  ***Affidabilità***: Un servizio si dice affidabile (a livello di rete) quando ogni nodo del percorso si preoccupa 
    di avvisare il nodo precedente se un pacchetto gli è arrivato da esso.

    Viceversa un servizio non affidabile a livello di rete non avvisa nessuna per ogni pacchetto ricevuto o no 
    in attraversamento sui nodi.


**Tutti i protocolli di rete della Suite Internet non sono né connessi, né affidabili**.  Per ogni pacchetto viene calcolato un percorso (potenzionalmente diverso)
e tutti i controlli di affidabilità vengono lasciati (eventualmente) al livello di trasporto.


!!! tip "Protocolli connessi e affidabili a livello di rete"

    Se volete un esempio di protocollo di rete connesso dovete pensare a
    quello della *vecchia telefonia mobile*. Grande qualità per un certo tipo
    di dati (le telefonate da telefono fisso nel 1920 funzionavano meglio
    delle telefonate con *WhatsApp* nel 2020) ma poca flessibilità per il
    grande numero di dati presenti in una rete come la rete Internet. Oltre
    alla naturale gestione dei problemi insita in una struttura non connessa
    (ogni volta si ricalcola la strada, se una non c'è più se ne sceglie
    un'altra. Nei protocolli connessi finché va tutto bene ok, ma se va
    male...).

    Se volete un esempio di protocollo di rete affidabile... confesso. Non
    lo so. Mi sembra veramente un livello di controllo assurdo per comunicazioni "veloci".


**Il primo protocollo di rete che si incontra è sempre il protocollo IP**!! Esso è responsabile dell'impacchettamento e dell'indirizzamento.

Avere questi compiti e questa posizione lo rende l'unico protocollo della Suite Internet ad essere eseguito sempre e comunque! Tutti gli 
altri protocolli di rete utilizzano i pacchetti IP, che vengono definiti **datagrammi** e presentano la caratteristica di essere **instradabili**,
ovvero di essere adatti alle operazioni di routing.

Per la precisione, il protocollo IP si occupa perfino dell'instradamento del primo salto del pacchetto, ovvero dell'uscita dal dispositivo del mittente,
tramite la sua **logica di base del protocollo IP.**

Esso confronta l'indirizzo IP del mittente del pacchetto con quello del destinatario e si comporta secondo le seguenti regole:

-   Se l'indirizzo IP del mittente è uguale all'IP del destinatario,
    oppure uno degli indirizzi è della classe 127, il pacchetto viene
    passato al livello superiore (tecnica del **loopback**).
-   Se il destinatario si trova sullo stesso segmento di rete del
    mittente, il pacchetto viene inviato in maniera diretta,
    individuando il destinatario tramite ARP (un altro protocollo di
    rete, che vedremo fra breve).
-   Se il destinatario NON si trova nella stessa rete del mittente, si
    invia il pacchetto al **default gateway**.


Impacchettato correttamente, inserito in un indirizzamento organizzato e finalmente fuori dal disposirivo mittente, il prossimo compito del livello
di rete viene affidato ai protocolli di routing.


