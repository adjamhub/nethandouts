# Implementazioni reali


blah blah


<!-- xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
## Suite e protocolli

Più che approfondire le specifiche del modello OSI sarà interessante andare a studiare quelle suite di
protocolli che rappresentano una sua implementazione reale. Ma prima di procedere, cerchiamo di
capire bene cosa si intende con queste nuove terminologie:

!!! note Protocollo di rete

    Un **_protocollo_** _è un insieme di regole utilizzate per favorire la comunicazione tra due o più entità. 
    Ovviamente nel caso specifico di un **_protocollo di rete_**, queste regole andranno a definire le modalità di
    interazioni fra due o più dispositivi.

Uno **_stack (o una suite) di protocolli_** è un insieme di protocolli che collaborano fra loro per ottenere uno scopo comune.

Presentiamo qui le più famose suite di protocolli di rete che possono essere definite come
implementazioni pratiche del modello OSI.


## blah blah

- TCP/IP Originariamente caratteristica dei sistemi UNIX

    - In grado di gestire il routing: adatta anche per reti geografiche.
    - Robusta (nei livelli inferiori) e flessibile (nei livelli superiori)

- IPX/SPX Tipica dei sistemi XEROX e Novell NetWare

    - Ottimizzata per reti locali/domestiche
    - Distingue a livello di rete client e server

- NetBEUI Tipica dei sistemi Microsoft (prima dell'adozione di TCP/IP con Win98SE)

    - Utilizza i nomi NETBIOS (molto limitati)
    - Non adatta al routing (inutilizzabile su reti geografiche)

- AppleTalk Tipica dei sistemi Apple (pre Mac OS X)

    - Progettata per reti locali e servizi specifici (trasferimento file, supporto multiclient avanzato)
    - Utilizza un servizio di naming basato su broadcast

Ovviamente ogni produttore di software per OS spinse per l'adozione globale del suo stack e, finché la
disputa avvenne solo sulle reti locali, nessuno ebbe la meglio.

Quando si cominciò a sviluppare una rete estesa, apparve chiaro che l'unica suite avente tutte le carte in
regola per gestire tutto lo stack di rete era solo una: **TCP/IP**.


## Internet Protocol Suite (TCP/IP)

La suite di protocolli TCP/IP è un insieme di protocolli di rete che implementa la pila di protocolli su
cui funziona Internet. Sebbene il suo nome più corretto sarebbe **_Internet Protocol Suite_** , il nome
TCP/IP ha preso ormai piede dovuto alla grande importanza dei suoi due protocolli più rappresentativi:
TCP e IP.

Storicamente la sua implementazione è venuta come risposta ad un problema pratico, in forte contrasto
con lo sviluppo teorico del modello OSI, ma questo non ha minato la possibilità di confrontarli come
facce opposte della stessa medaglia.


**(tabella) Confronto fra modello OSI e stack TCP/IP**

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

## Lo svilppo dei protocolli dello Stack TCP/IP

Se avete seguito bene la discussione sull’affermazione della Suite Internet sulle suite supportate
nientemeno che da tre delle aziende più importanti della storia dell’informatica (Microsoft, Apple,
Novell), ci sarà una questione che probabilmente non vi ha convinto del tutto: chi è che ha “pensato” i
protocolli della Suite Internet??? Ok... all’inizio abbiamo detto che è stato un lavoro a più mani
iniziato all’università di Berkeley, nel Sud della California... molti avranno sentito anche la storia della
rete ARPAnet, storicamente considerata l’antenata della rete Internet e sovvenzionata dall’esercito
degli Stati Uniti...

Ma adesso chi porta avanti lo sviluppo delle idee e dei protocolli? E chi gestisce tutto questo
ambaradan? Andiamo avanti ancora con le idee degli anni 70-80?? No...

La risposta a questa domanda sta in 3 associazioni diverse, con composizione e scopi diversi, ma con
acronimi simili, che quasi te le fa confondere: **IETF**, **IEEE**, **ICANN**.

> **IETF (Internet Engineering Task Force, <a href="https://www.ietf.org/" target="_blank">https://www.ietf.org/</a>** è un 
> organismo internazionale libero, composto da tecnici, specialisti e ricercatori appassionati allo sviluppo dei protocolli e
> delle tecnologie della rete Internet.
> 
> **E’ un organismo senza una sede fisica, se non il web (The Internet).**

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
IETF. Diamo un occhio al “famoso” [RFC 791](https://tools.ietf.org/html/rfc).

La seconda associazione che entra in gioco si chiama **IEEE** , una associazione americana senza scopo
di lucro che raduna scienziati professionisti riconosciuti a livello internazionale e che si prefigge
l’obiettivo di promuovere le nuove tecnologie.

> **IEEE (Institute of Electrical and Electronics Engineers, <a href="https://www.ieee.org/" target="_blank">https://www.ieee.org/</a>)** 
> è una associazione che raggruppa ingegneri e scienziati di tutte le più grandi aziende del mondo, che collaborano
> alla creazione di nuovi *standard* per l’elettronica, l’informatica, l’elettrotecnica e le
> telecomunicazioni.

Anche qui ci troviamo di fronte ad una associazione che promuove la creazione di “standard” per il settore.

Cerchiamo di farla semplice. IETF si occupa di formalizzare tutti i protocolli del livello superiore, di
trasporto e di rete. IEEE si occupa di tutte le specifiche (anche hardware) che afferiscono al livello
inferiore.

Storicamente questo finto dualismo si spiega col fatto che le implementazioni dei livelli “alti” hanno
sempre avuto bisogno delle migliori idee per svilupparsi al meglio e la struttura di IETF permette a
chiunque di contribuire ad una idea o di portare la propria; quando si parla del livello inferiore andiamo
a toccare la sfera di appartenenza dei produttori di hardware, che in IEEE spesso trovano il giusto
compromesso fra innovazione e collaborazione.

E la terza società? È quella che si occupa di gestire il tutto!

> **ICANN (Internet Corporation for Assigned Names and Numbers, <a href="https://www.icann.org/" target="_blank">https://www.icann.org/</a>)** 
> è un ente di gestione internazionale registrato presso il Dipartimento del commercio degli Stati Uniti. 

Fondata nel 1998, dal 2016 ha pieno controllo sui 3 compiti fondamentali di gestione della rete Internet:

1. la gestione e lo smistamento degli indirizzi IP

2. la gestione e l’organizzazione dei nomi di dominio

3. la gestione e il supporto dei protocolli della rete Internet

Qui potremo discutere giorni sulla frasetta “...presso il Dipartimento del commercio...”. Non
preoccupatevi. Sono anni che il mondo discute su questa cosa. E ancora non si è arrivati ad una
conclusione degna di questo nome. ICANN verrà fuori nei nostri discorsi quando parleremo dei
protocolli da lei direttamente gestiti.


