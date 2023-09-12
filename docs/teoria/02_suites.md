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

- `TCP/IP`; originariamente caratteristica dei sistemi UNIX

    - In grado di gestire il routing: adatta anche per reti geografiche.
    - Robusta (nei livelli inferiori) e flessibile (nei livelli superiori)

- `IPX/SPX`; tipica dei sistemi XEROX e Novell NetWare

    - Ottimizzata per reti locali/domestiche
    - Distingue a livello di rete client e server

- `NetBEUI`; tipica dei sistemi Microsoft (prima dell'adozione di TCP/IP con Win98SE)

    - Utilizza i nomi NETBIOS (molto limitati)
    - Non adatta al routing (inutilizzabile su reti geografiche)

- `AppleTalk`; tipica dei sistemi Apple (pre Mac OS X)

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


![Confronto fra OSI e TCP/IP](images/OSI_vs_TCPIP.png)

