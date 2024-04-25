# Protocolli del livello superiore

Come abbiamo già visto, i primi livelli del modello OSI e le loro
rispettive implementazioni nelle varie suite di protocolli per la rete,
definiscono le procedure e le modalità per effettuare il trasferimento
dei pacchetti di dati lungo un canale fisico o virtuale privo di errori.
I tre livelli successivi completano il modello OSI permettendogli di
offrire una interfaccia standard alle applicazioni, in modo che possano
utilizzare la rete secondo le proprie necessità.

Se questo però, e possibile in teoria tramite una stratificazione delle
operazioni nei tre livelli Sessione, Presentazione, Applicazione
sistemati uno sopra l'altro, ciò risulta più difficile nella pratica,
dove c'è stato uno sviluppo "orizzontale" dei vari protocolli di rete.
In pratica, mentre il livello OSI definisce operazioni di rete generiche
per tutte le applicazioni, la cui implementazione viene suddivisa fra i
vari livelli alti, la suite TCP/IP definisce un insieme di protocolli,
ognuno per affrontare (quasi) tutti gli aspetti di una determinata
tipologia di operazione.

Vedremo dunque in questo capitolo quali sono le operazioni che
determinano l'interfaccia offerta alle applicazioni queste operazioni
vengono in realtà eseguite tramite gli opportuni protocolli attivi nella
suite TCP/IP.


## I livelli superiori nella suite TCP/IP

I livelli superiori del modello OSI vengono implementati come un unico
livello onnicomprensivo nella suite TCP/IP. Questo perché i protocolli
di livello superiore, nel caso pratico si sono sviluppati come risposta
alle necessità di un determinato servizio di essere emesso e più che
concentrarsi sui compiti della trasmissione "pura" dei dati, sono
partiti dall'interazione con l'applicazione che necessita un servizio di
rete e con l'elaborazione dei dati da trasportare fino al momento in cui
questo trasporto doveva avere inizio (cioè ovviamente al livello di
trasporto). Abbiamo quindi non protocolli che si occupano
specificatamente di una delle attività descritte nei livelli OSI
superiori, ma protocolli che si occupano di un'attività tipica delle
applicazioni sovrastanti che li utilizzano: l'invio di file, di pagine
web, la risoluzione di indirizzi web in indirizzi di rete, etc.

La tabella e l'immagine seguente rappresentano e descrivono i protocolli
superiori più comuni.


| Protocollo                                    | Descrizione                           |
|-----------------------------------------------|---------------------------------------|
| HTTP<br>(Hyper Textual Transfer Protocol)     | Trasferimento degli ipertesti         |
| SMTP<br>(Simple Mail Transfer Protocol)       | Trasferimento della posta elettronica |
| FTP<br>(File Transfer Protocol)               | Trasferimento file                    |
| DHCP<br>(Dynamic Host Configuration Protocol) | Configurazione dinamica degli host    |
| DNS<br>(Domain Name Service)                  | Risoluzione dei nomi di host in indirizzi IP |
| IRC<br>(Internet Relay Chat)                  | Comunicazione istantanea diretta (chat)      |


Nelle sezioni successive andremo a presentare il funzionamento di alcuni
dei protocolli qui sopra descritti, cercando di metterne in evidenza
tanto i principi di funzionamento quanto l'utilizzo che comunemente se
ne fa.

In tutti i casi comunque, il livello superiore si occupa di rendere
disponibile una risorsa, sia essa un file (FTP), una pagina web (HTTP),
una mail (SMTP), eccetera...

Per identificare nella rete le risorse si utilizzano degli
identificatori ben definiti: gli URL.


## URL: Uniform Resource Locator

Un URL è una sequenza di caratteri compresi nel codice ASCII che
identifica univocamente l'indirizzo di una risorsa in una rete. L'idea
di base dell'invenzione degli URL è quella di identificare ogni risorsa
con un identificativo facile da ricordare (es: google.it, facebook.com)
invece di avere informazioni dettagliate sull'indirizzo IP, il socket e
il percorso relativo della risorsa.

La struttura completa di ogni URL, definita nel [***RFC 3986***](https://tools.ietf.org/html/rfc3986), è la seguente:

>
> scheme : // ( user ( : pass ) @ ) host ( :port ) ( /path ) ( ? query ) ( # fragment )
>

Nello schema sopraelencato le parentesi tonde indicano una informazione
opzionale che, se presente, utilizza il separatore indicato. Ad esempio,
se la query è presente nell'URL è sempre preceduta dal simbolo "?".
L'host è sempre presente. Pass e port, che sono entrambe precedute dal
simbolo ":" si distinguono perché una sta prima del simbolo "@" (e
dell'host) e una dopo.

Ognuna delle parti citate ha un significato identificativo per un
concetto derivato dalla struttura dei protocolli che un URL può
identificare:

***SCHEME*** (o PROTOCOL)<br>
Descrive il protocollo da utilizzare per
l'accesso ai server. Quando questa informazione
è assente, l'URL si dice ***relativo*** e sta al
software che lo utilizza scegliere (con un po'di fortuna) il protocollo da utilizzare.

***USERINFO*** (= USER : PASS) <br>
Specificano l'autenticazione per l'accesso alla risorsa. 
Nel protocollo HTTP, questa modalità di  autenticazione è ritenuta rischiosa per motivi di sicurezza e di *phishing*, mentre ad esempio, 
gli account di posta sono scritti tipicamente come <USER@HOST>.

***HOST*** <br>
rappresenta l'informazione che sarà passata al server DNS per l'identificazione dell'indirizzo 
IP del dispositivo in cui risiede la risorsa. É l'informazione più importante contenuta nell'URL.

**PORT** <br>
è un numero compreso fra 1 e 65535 che serve per distinguere le connessioni dal punto di vista logico. 
Molti protocolli utilizzano una porta fissa per identificare il server, in modo tale che questo numero venga spesso sottinteso.

**PATH** <br>
percorso ***relativo*** nel file system del server per raggiungere la risorsa.

**QUERY** <br>
Informazioni opzionali che devono essere elaborate dalla risorsa.

**FRAGMENT** <br>
identifica una parte specifica della risorsa.

<br>
<br>

Vediamo insieme qualche esempio di URL per cercare di capire meglio!

1) `http://www.liceodavincijesi.edu.it/area-studenti/`

Qui troviamo lo scheme (`http`) seguito dall'host (`liceodavincijesi.edu.it`) e dal path (`area-studenti`). 
Non sono presenti altre componenti.


2) `http://www.google.it/search?q=ciao`

Qui troviamo scheme (`http`), host (`www.google.it`), path (`search`) e query (`q=ciao`)


3) `mailto:andrea@liceodavincijesi.edu.it`

Qui troviamo scheme (`mailto`), user (`andrea`) e host (`liceodavincijesi.edu.it`). 
Lo schema mailto presenta una piccola eccezione alla regola in quanto non è seguito dal doppio slash (//).

4) `http://www.facebook.com@www.cicciobello.com/tihofregato/`

Se non hai cercato su internet il significato del termine phishing, in
questo esempio trovi uno dei più vecchi trucchi di mascheramento
dell'identità: qual è l'host qui? Su quale sito sei?

<br>
<br>

