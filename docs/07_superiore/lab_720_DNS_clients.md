# DNS Clients



!!! note "Argomenti teorici e requisiti tecnici"
    
    Prerequisti: **OS, terminale**
    
    Argomenti trattati: **DNS, URL, Indirizzamento IP**


La funzionalità di risoluzione DNS ai software che ne hanno bisogno
(praticamente tutti quelli che si connettono alla rete) viene solita
fornita dal Sistema Operativo tramite le API di sistema.

Se però si vogliono ottenere risoluzioni DNS da poter consultare e
studiare, è possibile utilizzare un client DNS testuale. Fra i pochi che
esistono la scelta ricade forzatamente su **nslookup** (name server
lookup) che ha il pregio di essere molto semplice (purtroppo a volte a
scapito della dovizia di particolari) e di essere disponibile su tutti i
sistemi operativi importanti.

Il client nslookup può essere eseguito in due modalità:

1. command line mode
2. interactive mode



## nslookup: command line mode

Questa modalità è la più semplice e scarna. Si digita **nslookup HOST**
e questi ritorna la risoluzione (i record A, AAAA e CNAME presenti)
dell'host fornito e termina

``` 
$ nslookup www.adjam.org
Server:         172.104.237.57
Address:        172.104.237.57#53

Non-authoritative answer:
Name:   www.adjam.org
Address: 217.64.195.209
Name:   www.adjam.org
Address: 2001:4b78:1001::5701
```

Come si vede, in *command line mode* nslookup restituisce una risposta
standard contentente il server che ha fatto la risoluzione (un server
non autorevole, come vediamo sotto) e le risoluzioni trovate,
evidentemente, in questo caso, un record A e un record AAAA.



## nslookup: interactive mode

Per entrare in *interactive mode* basta digitare **nslookup** senza
parametri od opzioni. In questo modo cambia il prompt (diventa un
maggiore, **>**) e lì si può richiedere la risoluzione di qualunque
host ci interessi. Quando abbiamo finito, possiamo uscire dalla modalità
interattiva digitando **exit**.

``` 
$ nslookup

> google.it
Server:         172.104.237.57
Address:        172.104.237.57#53

Non-authoritative answer:
Name:   google.it
Address: 172.217.17.67
Name:   google.it
Address: 2a00:1450:400e:805::2003

> libero.it
Server:         172.104.237.57
Address:        172.104.237.57#53

Non-authoritative answer:
Name:   libero.it
Address: 213.209.17.209

> exit

$
```

la modalità interattiva permette inoltre di fornire alcuni parametri ad
nskooup per modificare la risoluzione richiesta, specificandola meglio:

  comando           descrizione
  ----------------- ---------------------------------------------------------------------------------------------------------------------------------------
  host              l'host da risolvere.
  server ip         l'ip del server DNS da utilizzare nelle prossime risoluzioni interattive
  set type=record   serve per richiedere la risoluzione del tipo di record indicato. Valori possibili per *record* sono: A, AAAA, CNAME, MX, NS, PTR ...

Qua di seguito farò 2 esempi per vedere come si utilizzano le 2 opzioni
non testate: *server* e *set type*



### Esempio #1: cambiare server DNS

Voglio specificare ancora una volta che questa opzione è disponibile
solo in modalità interattiva e che il cambio di server DNS vale solo per
le risoluzioni DNS fatte con nslookup in **questa** modalità
interattiva! Il sistema non è minimamente interessato da questa modifica
e alla chiusura di nslookup neanche esso se ne ricorderà:

``` 
$ nslookup

(la prima risoluzione, fatta col server DNS di default)
> www.liceodavincijesi.edu.it
Server:         172.104.237.57
Address:        172.104.237.57#53

Non-authoritative answer:
Name:   www.liceodavincijesi.edu.it
Address: 89.46.109.18

(cambio di server DNS per la risoluzione)
> server 1.1.1.1
Default server: 1.1.1.1
Address: 1.1.1.1#53

(la prossima risoluzione viene fatta verso il server 1.1.1.1)
> gazzetta.it
Server:         1.1.1.1
Address:        1.1.1.1#53

Non-authoritative answer:
Name:   gazzetta.it
Address: 40.1
```



### Esempio #2: risolvere un record MX

Può essere utile e interessante risolvere un record MX tramite nslookup.
Per farlo dobbiamo impostare il tipo di record da risolvere con *set
type*. Ricordo però che il record MX ci dirà praticamente il record A
che individua il dispositivo che fornisce il servizio di posta, che
dovrà dunque poi essere risolto per ottenere l'indirizzo IP.

``` 
$ nslookup

(chiedo di risolvere record MX)
> set type=MX

(risolvo libero.it come MX. Il record MX punta il record con host indicato sotto)
> libero.it
Server:         172.104.237.57
Address:        172.104.237.57#53

Non-authoritative answer:
libero.it       mail exchanger = 10 smtp-in.libero.it.

(ritorno a risolvere record A, come di default)
> set type=A

(risolvo il record A abbinato al record MX)
> smtp-in.libero.it
Server:         172.104.237.57
Address:        172.104.237.57#53

Non-authoritative answer:
Name:   smtp-in.libero.it
Address: 213.209.1.129
```


## Web clients

Capita spesso di voler utilizzare il DNS non tanto per verificare il
funzionamento di un server, ma per verificare l'effettiva risolvibilità
di un sito web. In questo caso tornano utili alcuni client DNS
implementati direttamente come servizi WEB. Ne cito alcuni, ritrovati
rigorosamente nella prima pagina del mio motore di ricerca preferito
all'input *DNS web clients*:

-   <https://toolbox.googleapps.com/apps/dig/>

    Rappresenta la versione web del famoso client testuale *dig*,
    sviluppato al server *BIND*, il server web più famoso al mondo. Poco
    da dire e facile da usare. Molto completo nelle risposte (troppo per
    noi?), ma molto semplice da utilizzare nella sua interfaccia web.

-   <https://www.whatsmydns.net/>

    Esso è un sito che permette di specificare una stringa di ricerca,
    un tipo di record ed effettua la stessa ricerca su una serie di
    almeno 20 server DNS sparsi per il mondo. È un servizio molto comodo
    e interessante, nel caso si voglia studiare la propagazione di un
    certo nome di dominio.

    

<br>
<br>

