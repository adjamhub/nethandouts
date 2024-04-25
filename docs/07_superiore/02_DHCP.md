# Protocollo DHCP


DHCP (*Dynamic Host Configuration Protocol*) è un protocollo del livello superiore 
della suite di protocolli Internet, 
utilizzato per l’assegnazione automatica degli indirizzi IP che permette una 
configurazione dinamica di tutte le impostazioni di rete per le stazioni che lo utilizzano.

Il protocollo è basato sul paradigma client/server e utilizza il protocollo UDP 
del livello di trasporto con il server in ascolto sulla porta 67 e il client in
comunicazione sulla porta 68: se già conoscete il livello di trasporto, 
questi numeri di porta ci dicono che sia client che server DHCP devono 
essere eseguiti con privilegi amministrativi.


## Configurazione di rete: informazioni necessarie.

Dico una banalità: per connettersi ad una rete un dispositivo ha bisogno di 
un indirizzo IP! Vero! Necessario, ma non sufficiente!

Le informazioni necessarie ad un dispositivo che vuole connettersi alla rete sono le seguenti:

1. **Indirizzo IP**

    Questa informazione serve ad identificare un dispositivo all'interno di una rete. 
    Ogni dispositivo su una rete chiusa ha un indirizzo IP diverso. 
    Quindi, ad esempio, ogni dispositivo che si connette a internet ha un diverso indirizzo IP.

2. **Subnet Mask**

    Questo parametro serve per capire a quale “sotto-rete” appartiene un dispositivo. 
    Una sotto-rete è un gruppo locale di dispositivi collegati allo stesso router. 
    Affronteremo meglio questo concetto studiando il protocollo IP.

3. **Default Gateway**

    Questo parametro è quello che serve al dispositivo per connettersi a tutti i dispositivi che non appartengono alla sua sotto-rete. 
    Senza questa informazione è possibile solo una connessione locale fra i dispositivi della stessa sotto-rete.

4. **Elenco dei server DNS utilizzabili**

    Tipicamente vengono forniti gli indirizzi di 2 server DNS che verranno utilizzati in sequenza. 
    Senza questa informazione la rete funziona, ma i nomi di dominio non possono essere risolti, 
    rendendo la navigazione molto complicata (o per certi versi impossibile).


Ora... in quale modo un dispositivo può ottenere queste informazioni? Ci sono 2 modalità:

1. tramite una **configurazione statica**, con l’utente che inserisce manualmente queste informazioni nel sistema operativo.
2. Tramite una **configurazione dinamica**, con il sistema operativo configurato per ottenere le informazioni tramite DHCP




## Logica di funzionamento

Il client DHCP, solitamente appena il dispositivo viene acceso, fa una richiesta al server per ottenere un indirizzo IP e 
tutte le informazioni necessarie alla configurazione della rete.

Ma... il dispositivo non ha ancora un indirizzo IP, come fa a comunicare? E anche se lo avesse, 
come fa a sapere dove si trova il server DHCP a cui indirizzare la richiesta?

La risposta a tutte queste domande è una sola: il client DHCP utilizza per la comunicazione il **broadcast**, in particolare comunicando 
tramite l’indirizzo speciale `255.255.255.255`: **il broadcast della rete corrente!**.

Nel primo messaggio del client esso scrive una richiesta di questo tipo:


> Ci sarebbe un indirizzo IP per la scheda XX:XX:YY:YY:ZZ:ZZ ?


Il numero che esso indica si chiama indirizzo MAC ed è un identificatore univoco della scheda di rete: tutte le schede di rete prodotte 
in tutto il mondo in tutta la storia del pianeta Terra sono state identificate con un indirizzo MAC diverso. Ne parleremo studiando il livello di rete.

Tutti ricevono la richiesta del client che ha bisogno di informazioni (ovviamente! È stata inviata in broadcast...) 
ma solo il dispositivo con il server DHCP la prende in considerazione e produce una risposta di questo tipo:


> L’indirizzo IP per la scheda XX:XX:YY:YY:ZZ:ZZ è 10.11.12.13.
> Allegate le informazioni necessarie per la configurazione di rete.


La risposta del server deve essere rinviata ancora in broadcast, infatti il dispositivo destinatario non ha ancora un indirizzo: 
tutti riceveranno anche questo messaggio, ma l’unico autorizzato ad utilizzare quell’IP sarà quello con la scheda indicata.




## Server DHCP


Abbiamo capito in quale modo un client può richiedere ad un server DHCP un indirizzo IP e le informazioni per la configurazione della rete. 
Ma quanti IP ha da assegnare un server DHCP?

Ogni server DHCP viene configurato con un intervallo di indirizzi, definito ***scope***, che può utilizzare per le assegnazioni.

Chiaramente il server non può usufruire del suo stesso servizio e quindi la configurazione di rete di un dispositivo in cui si eseguirà un server DHCP deve essere statica.

Il server DHCP non regala gli IP ai client che li richiedono ma li fornisce in affitto (in **lease**) per un tempo di affitto prestabilito (**lease time**).

Al termine del lease, il client deve liberare l’IP che gli è stato affidato, ma ha ovviamente la possibilità di richiedere un nuovo lease al server.

Ogni volta che il server fornisce un lease ad un client esso si costruisce una tabella che contiene per ogni riga:

- l’indirizzo IP assegnato
- l’indirizzo MAC che ha fatto la richiesta
- la data e l’ora di scadenza del lease

In questo modo, oltre ad avere sempre il controllo sulla situazione delle prenotazioni degli indirizzi, ha anche la possibilità di riassegnare lo stesso IP dopo la scadenza del lease.

<br>
<br>

