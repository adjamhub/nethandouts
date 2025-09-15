# La Suite Internet


La `Internet Protocol Suite` è un insieme di protocolli di rete che implementa la pila di protocolli su cui funziona Internet. 

Se la cercate in rete o nella letteratura attuale, la troverete nominata in vari modi: ***Internet Protocol Suite***, o più semplicemente ***Suite Internet***, 
o addirittura con il nomignolo ***TCP/IP***, che deriva dalla grande importanza storica 
dei suoi due protocolli più rappresentativi: TCP e IP.

!!! note "Protocolli (di rete) e suite(s)"

    Un **_protocollo_** è un insieme di regole utilizzate per favorire la comunicazione tra due o più entità. 
    Ovviamente nel caso specifico di un **_protocollo di rete_**, queste regole andranno a definire le modalità di
    interazioni fra due o più dispositivi.
    <br><br>
    Uno **_stack (o una suite) di protocolli_** è un insieme di protocolli che collaborano fra loro per ottenere uno scopo comune.

La necessità di implementare realmente i livelli descritti ha portato ad una semplificazione di alcune parti del modello OSI, come si desume dalla figura seguente:

![Confronto fra OSI e TCP/IP](images/OSI_vs_TCPIP.png)

Come vedremo, le implementazioni dei livelli superiori sono affidate al *software* (e quindi vanno insieme!). Livello di trasporto e di rete hanno i compiti più gravosi
e quindi rimangono da soli: i compiti del livello di trasporto sono affidati al *Sistema Operativo*, quelli del livello di rete al cosiddetto *firmware* (driver, router, etc),
infine quelli del livello inferiore all'*hardware*!!!

NOTA: qui ci va un disegnino sul funzionamento della suite: la storia di un pacchetto!!!

Semplice e schematico :smile:
