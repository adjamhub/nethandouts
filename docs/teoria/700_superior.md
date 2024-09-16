# Suite Internet: Livello Superiore

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
identificatori ben definiti: gli URL (vai a guardare sui supplementi!!!).


<br>
<br>

