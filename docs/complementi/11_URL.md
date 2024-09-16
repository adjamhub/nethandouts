# URL: Uniform Resource Locator

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

