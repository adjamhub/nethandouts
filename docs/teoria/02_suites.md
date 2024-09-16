# Implementazioni reali


Vedremo in questo capitolo le informazioni di base sulle implementazioni di reti aderenti al modello OSI e la (breve) storia che ha 
portato una a primeggiare sulle altre.


<!-- xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
## Suite e protocolli

Più che approfondire le specifiche del modello OSI sarà interessante andare a studiare quelle suite di
protocolli che rappresentano una sua implementazione reale. Ma prima di procedere, cerchiamo di
capire bene cosa si intende con queste nuove terminologie:

!!! note Protocollo di rete

    Un **_protocollo_** è un insieme di regole utilizzate per favorire la comunicazione tra due o più entità. 
    Ovviamente nel caso specifico di un **_protocollo di rete_**, queste regole andranno a definire le modalità di
    interazioni fra due o più dispositivi.

Uno **_stack (o una suite) di protocolli_** è un insieme di protocolli che collaborano fra loro per ottenere uno scopo comune.

Presentiamo qui le più famose suite di protocolli di rete che possono essere definite come
implementazioni pratiche del modello OSI.


## Suite di rete


- `NetBEUI`; tipica dei sistemi Microsoft (prima dell'adozione di TCP/IP con Win98SE)

    - Utilizza i nomi NETBIOS (molto limitati)
    - Non adatta al routing (inutilizzabile su reti geografiche)

- `AppleTalk`; tipica dei sistemi Apple (pre Mac OS X)

    - Progettata per reti locali e servizi specifici (trasferimento file, supporto multiclient avanzato)
    - Utilizza un servizio di naming basato su broadcast

- `IPX/SPX`; tipica dei sistemi XEROX e Novell NetWare

    - Ottimizzata per reti locali/domestiche
    - Distingue a livello di rete client e server

- `TCP/IP`; originariamente caratteristica dei sistemi UNIX

    - In grado di gestire il routing: adatta anche per reti geografiche.
    - Robusta (nei livelli inferiori) e flessibile (nei livelli superiori)


Ovviamente ogni produttore di software per OS spinse per l'adozione globale del suo stack e, finché la
disputa avvenne solo sulle reti locali, nessuno ebbe la meglio.

Quando si cominciò a sviluppare una rete estesa, apparve chiaro che l'unica suite avente tutte le carte in
regola per gestire tutto lo stack di rete era solo una: **TCP/IP**.


## Internet Protocol Suite (TCP/IP)

La `Internet Protocol Suite` è un insieme di protocolli di rete che implementa la pila di protocolli su cui funziona Internet. 

Se la cercate in rete o nella letteratura attuale, la troverete nominata in vari modi: ***Internet Protocol Suite***, o più semplicemente ***Suite Internet***, 
o addirittura con il nomignolo ***TCP/IP***, che deriva dalla grande importanza storica 
dei suoi due protocolli più rappresentativi: TCP e IP.

La necessità di implementare realmente i livelli descritti ha portato ad una semplificazione di alcune parti del modello OSI, come si desume dalla figura seguente:

![Confronto fra OSI e TCP/IP](images/OSI_vs_TCPIP.png)

Come vedremo, le implementazioni dei livelli superiori sono affidate al *software* (e quindi vanno insieme!). Livello di trasporto e di rete hanno i compiti più gravosi
e quindi rimangono da soli: i compiti del livello di trasporto sono affidati al *Sistema Operativo*, quelli del livello di rete al cosiddetto *firmware* (driver, router, etc),
infine quelli del livello inferiore all'*hardware*!!!

Semplice e schematico :smile:
