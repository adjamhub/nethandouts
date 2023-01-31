# Reti

## Il Modello OSI

_Copyright © 2006-2020 by Andrea Diamantini <adjam@protonmail.com>_

_Rilasciata sotto la licenza_ **_Creative Commons Attribuzione - Non commerciale - Condividi allo stesso modo 3.0 Italia_**_.
Per leggere una copia della licenza, visita il sito web [http://creativecommons.org/licenses/by-nc-sa/3.0/it/](http://creativecommons.org/licenses/by-nc-sa/3.0/it/)_


## Il modello OSI

Il **modello OSI** , acronimo di **Open Systems Interconnection** , è un modello per le architetture di rete,
organizzato in 7 livelli e stabilito nel 1978 dalla **ISO** , organizzazione internazionale per gli standard.

**ISO è la più importante organizzazione mondiale per definizione di norme tecniche.**

**Svolge funzioni consultive per l’ONU e l’UNESCO; i suoi membri sono gli organismi nazionali di
standardizzazione di 164 paesi nel mondo.**

**Sito Ufficiale (** https://www.iso.org/ **), Link Wikipedia (** https://it.wikipedia.org/wiki/ISO **)**

Viste le molteplici implementazioni differenti esistenti all'epoca, la comunità scientifica sentì la
necessità di organizzare un “ **_modello standard di riferimento per l'interconnessione di sistemi aperti_** ”
e avviò il progetto OSI ( **O** pen **S** ystems **I** nterconnection, ISO 7498).

Il modello ISO/OSI è costituito da uno sequenza di 7 livelli attraverso i quali viene ridotta la
complessità implementativa di un sistema di comunicazione per il networking, muovendosi dal livello
fisico, che rappresenta il mezzo fisico di propagazione dell'informazione al livello applicazione, che
rappresenta l'interfaccia del modello verso le applicazioni che lo utilizzano.

E' importante notare che il modello OSI è un modello! Cioè è un impianto assolutamente teorico. Le
operazioni descritte non avvengono nella realtà, ma sono da considerare piuttosto uno schema, un
suggerimento di come si potrebbe fare per implementare una connessione.

Come vedremo successivamente, le implementazioni reali del modello OSI differiscono anche
sensibilmente dalla teoria, ma l'importanza del modello rimane come standard da cui partire per
l'implementazione e come linea guida per le interconnessioni.


### I livelli del modello OSI

Il modello OSI è strutturato in sette livelli, ciascuno dei quali implementa uno specifico compito del
modello, identificato tramite uno specifico protocollo di comunicazione.

Dati due nodi A e B, sui quali immagineremo esserci due software pronti a comunicare tra loro, il
modello OSI stabilisce una procedura di elaborazione dei dati in transito fra i due nodi.

Ogni livello rielabora i dati secondo la sua necessità, scambiando eventualmente informazioni con il
corrispondente livello paritario nell’altro nodo, ma non con gli altri: ciò conferisce modularità al
sistema e semplicità di implementazione e re-implementazione.

Elaborati i dati, essi vengono dunque passati
al livello successivo, che li tratterà a sua volta,
aggiungendovi eventualmente opportune
informazioni relative al compito del livello in
questione e “colloquiando” con il livello
corrispondente.

Questa tecnica di gestione dei dati viene
definita **_incapsulamento_** ed è una
caratteristica alla base della formulazione del
modello OSI stesso.

Vediamo una descrizione puntuale dei livelli del modello OSI. La descrizione parte dal numero 7
poiché si immagina una comunicazione che parte da una applicazione attiva nell’host A che ha volontà
di comunicare con un’altra nell’host B.


###### Livello 7: Applicazione

Il livello di applicazione é il livello più alto del modello OSI. Nella teoria del modello dunque, è quello
progettato per fornire un **_insieme di interfacce comuni alle applicazioni_** , che permetta alle stesse di
comprendere come utilizzare i servizi della rete quali ad esempio il collegamento, il trasferimento file,
la gestione dello scambio di messaggi, l’elaborazione delle richieste.

###### Livello 6: Presentazione

Il livello di presentazione si occupa del **_formato dei dati_** per la comunicazione lungo la rete. In
particolare si occupa di uniformare le trasmissioni, codificando i dati da inviare in codice ASCII. Il
livello di presentazione, oltre a fornire un sistema di codifica unico (condiviso) per tutte le trasmissioni,
effettua, se possibile, anche una **compressione** per ridurre il volume dei dati da trasmettere.

###### Livello 5: Sessione

Il livello di sessione permette che due parti gestiscano una **_conversazione_** in corso, che viene appunto
definita **_sessione_**. Il corretto funzionamento di questo livello implica che le parti possano scambiarsi
dati fra di loro per tutta la durata della sessione.

###### Livello 4: Trasporto

L’obiettivo è quello di permettere un trasferimento di dati trasparente e, se necessario, affidabile
(implementando anche un controllo degli errori e delle perdite) tra due nodi.

Esso si occupa di identificare univocamente il punto di partenza e il punto di arrivo di una
comunicazione, definita **_connessione_**.

Si occupa inoltre di effettuare la frammentazione dei dati provenienti dal livello superiore in pacchetti,
detti **_segmenti_** e trasmetterli in modo efficiente usando il livello rete ed isolando da questo i livelli
superiori.

###### Livello 3: Rete

Questo livello è uno dei più importanti nella comunicazione poiché si occupa di stabilire il percorso per
andare dal mittente al destinatario: questo processo viene definito **_routing_**.


Per rendere possibile il routing, il livello di rete si occupa dell’ **_indirizzamento_** , ovvero della possibilità
di distinguere i dispositivi fra loro e di raggrupparli opportunamente.

Durante il calcolo del routing infine, il livello di rete gestisce anche il problema delle congestioni e cioè
cerca di calcolare i percorsi adatti in modo da evitare che troppi pacchetti arrivino allo stesso router
contemporaneamente.

La sua unità dati fondamentale è il **_pacchetto_**.

###### Livello 2: Data Link

Questo livello si occupa di **trasformare i dati da inviare** da informazioni digitali a segnali adatti al
livello fisico presente (cavo, wifi, etc.). Tipicamente questi pacchetti vengono definiti **_frame_** , provvisti
di header (intestazione) e tail (coda), usati anche per sequenze di controllo.

Questo livello si occupa anche di **controllare il flusso di dati** : se il mittente è più veloce del
destinatario, regola la frequenza di invio dei pacchetti per permettere al destinatario di non
sovraccaricarsi di dati e perdere parte del carico.

###### Livello 1: fisico

Il livello fisico si occupa di controllare l’hardware, i cablaggi e tutte le strutture materiali che
implementano la rete e i dispositivi che permettono la connessione.

In questo livello si decidono, tra le altre cose:

- Le tensioni scelte per rappresentare i valori logici
- La durata in microsecondi del segnale elettrico che identifica un bit
- L'eventuale trasmissione simultanea in due direzioni
- La forma e la meccanica dei connettori usati per collegare l'hardware al mezzo trasmissivo


### Implementazioni reali del Modello OSI

Più che approfondire le specifiche del modello OSI sarà interessante andare a studiare quelle suite di
protocolli che rappresentano una sua implementazione reale. Ma prima di procedere, cerchiamo di
capire bene cosa si intende con queste nuove terminologie:

_Un_ **_protocollo_** _è un insieme di regole utilizzate per favorire la
comunicazione tra due o più entità. Ovviamente nel caso specifico di un
protocollo di rete, queste regole andranno a definire le modalità di
interazioni fra due o più dispositivi._

_Uno_ **_stack (o una suite) di protocolli_** _è un insieme di protocolli che
collaborano fra loro per ottenere uno scopo comune._

Presentiamo qui le più famose suite di protocolli di rete che possono essere definite come
implementazioni pratiche del modello OSI.


##### TCP/IP Originariamente caratteristica dei sistemi UNIX

###### In grado di gestire il routing: adatta anche per reti geografiche.

###### Robusta (nei livelli inferiori) e flessibile (nei livelli superiori)

##### IPX/SPX Tipica dei sistemi XEROX e Novell NetWare

###### Ottimizzata per reti locali/domestiche

###### Distingue a livello di rete client e server

##### NetBEUI Tipica dei sistemi Microsoft (prima dell'adozione di TCP/IP con

###### Win98SE)

###### Utilizza i nomi NETBIOS (molto limitati)

###### Non adatta al routing (inutilizzabile su reti geografiche)

##### AppleTalk Tipica dei sistemi Apple (pre Mac OS X)

###### Progettata per reti locali e servizi specifici (trasferimento file,

###### supporto multiclient avanzato)

###### Utilizza un servizio di naming basato su broadcast

Ovviamente ogni produttore di software per OS spinse per l'adozione globale del suo stack e, finché la
disputa avvenne solo sulle reti locali, nessuno ebbe la meglio.

Quando si cominciò a sviluppare una rete estesa, apparve chiaro che l'unica suite avente tutte le carte in
regola per gestire tutto lo stack di rete era solo una: **TCP/IP**.


### Lo Stack Internet TCP/IP

La suite di protocolli TCP/IP è un insieme di protocolli di rete che implementa la pila di protocolli su
cui funziona Internet. Sebbene il suo nome più corretto sarebbe **_Internet Protocol Suite_** , il nome
TCP/IP ha preso ormai piede dovuto alla grande importanza dei suoi due protocolli più rappresentativi:
TCP e IP.

Storicamente la sua implementazione è venuta come risposta ad un problema pratico, in forte contrasto
con lo sviluppo teorico del modello OSI, ma questo non ha minato la possibilità di confrontarli come
facce opposte della stessa medaglia.

#### Confronto fra modello OSI e stack TCP/IP

```
Livello OSI Livello TCP/IP Protocolli TCP/IP
```
```
Applicazione
```
```
Presentazione Superiore HTTP, SMTP, DHCP, DNS, etc...
```
```
Sessione
```
```
Trasporto Trasporto TCP, UDP
```
```
Rete Rete
```
```
IP
ICMP, ARP
RIP, OSPF
BGP
Data Link
Inferiore Ethernet, PPP, ...
Fisico
```

#### Il problema dei protocolli dello Stack TCP/IP

Se avete seguito bene la discussione sull’affermazione della Suite Internet sulle suite supportate
nientemeno che da tre delle aziende più importanti della storia dell’informatica (Microsoft, Apple,
Novell), ci sarà una questione che probabilmente non vi ha convinto del tutto: chi è che ha “pensato” i
protocolli della Suite Internet??? Ok... all’inizio abbiamo detto che è stato un lavoro a più mani
iniziato all’università di Berkeley, nel Sud della California... molti avranno sentito anche la storia della
rete ARPAnet, storicamente considerata l’antenata della rete Internet e sovvenzionata dall’esercito
degli Stati Uniti...

Ma adesso chi porta avanti lo sviluppo delle idee e dei protocolli? E chi gestisce tutto questo
ambaradan?Andiamo avanti ancora con le idee degli anni 70-80?? No...

La risposta a questa domanda sta in 3 associazioni diverse, con composizione e scopi diversi, ma con
acronimi simili, che quasi te le fa confondere: IETF, IEEE, ICANN.

**IETF (Internet Engineering Task Force, https://www.ietf.org/) è un organismo internazionale
libero, composto da tecnici, specialisti e ricercatori appassionati allo sviluppo dei protocolli e
delle tecnologie della rete Internet.**

**E’ un organismo senza una sede fisica, se non il web (The Internet).**

La missione di IETF è quella di promuovere lo sviluppo aperto dei nuovi protocolli della Suite Internet,
tramite la stesura di documenti aperti alla discussione da parte di chiunque, denominati RFC (Request
For Comments).

Finita la discussione e approvato il documento da tutta l’associazione, l’RFC diventa immutabile e
diviene come se fosse una “ **legge di Internet** ”. Non è possibile “eliminare” un RFC approvato, ma è
possibile “superarlo” con un RFC successivo.

Ad esempio la prima versione del protocollo IP risale all’RFC numero 760, che poi è stato reso
obsoleto dai successivi 777, 791 ( **IPv4** ), aggiornato da 792, 1349, 2474 e nuovamente reso obsoleto da
2460 ( **IPv6** ) e così via... Non pensavate a tanto fermento dietro ad un solo protocollo eh?

Tutti gli RFC sono pubblicati in ASCII (No Word, No Pdf, No immagini, solo testo semplice!!!) sul sito
IETF. Diamo un occhio al “famoso” RFC 791: https://tools.ietf.org/html/rfc

La seconda associazione che entra in gioco si chiama **IEEE** , una associazione americana senza scopo


di lucro che raduna scienziati professionisti riconosciuti a livello internazionale e che si prefigge
l’obiettivo di promuovere le nuove tecnologie.

**IEEE (Institute of Electrical and Electronics Engineers, https://www.ieee.org/) è una associazione
che raggruppa ingegneri e scienziati di tutte le più grandi aziende del mondo, che “collaborano”
alla creazione di nuovi “standard” per l’elettronica, l’informatica, l’elettrotecnica e le
telecomunicazioni.**

Anche qui ci troviamo di fronte ad una associazione che promuove la creazione di “standard” per il
settore.

Cerchiamo di farla semplice. IETF si occupa di formalizzare tutti i protocolli del livello superiore, di
trasporto e di rete. IEEE si occupa di tutte le specifiche (anche hardware) che afferiscono al livello
inferiore.

Storicamente questo finto dualismo si spiega col fatto che le implementazioni dei livelli “alti” hanno
sempre avuto bisogno delle migliori idee per svilupparsi al meglio e la struttura di IETF permette a
chiunque di contribuire ad una idea o di portare la propria; quando si parla del livello inferiore andiamo
a toccare la sfera di appartenenza dei produttori di hardware, che in IEEE spesso trovano il giusto
compromesso fra innovazione e collaborazione.

E la terza società? La terza società, ICANN è quella che attualmente gestisce il grosso delle cose che si
possono gestire nella rete Internet.

**ICANN (Internet Corporation for Assigned Names and Numbers) è un ente di gestione
internazionale registrato presso il Dipartimento del commercio degli Stati Uniti. Fondata nel
1998, dal 2016 ha pieno controllo sui 3 compiti fondamentali di gestione della rete Internet:**

**1) la gestione e lo smistamento degli indirizzi IP**

**2) la gestione e l’organizzazione dei nomi di dominio**

**3) la gestione e il supporto dei protocolli della rete Internet**

Qui potremo discutere giorni sulla frasetta “...presso il Dipartimento del commercio...”. Non
preoccupatevi. Sono anni che il mondo discute su questa cosa. E ancora non si è arrivati ad una
conclusione degna di questo nome. ICANN verrà fuori nei nostri discorsi quando parleremo dei
protocolli da lei direttamente gestiti.




