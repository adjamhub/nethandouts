# NAT


NAT (Network Address Translation), noto anche come ***Masquerading** è una tecnica di rete implementabile
nei router che consiste nel modificare gli indirizzi IP contenuti negli header dei pacchetti in transito su di essi.

Le due principali tipologie di NAT sono il **Source Nat (SNAT)** e il **Destination NAT (DNAT)**


## Source NAT

SNAT viene utilizzato da tutti quei client che si trovano all'interno di una rete privata e hanno bisogno di accedere ad un host pubblico,
cosa che non potrebbero fare con il loro IP privato.

Esso trasla l'indirizzo IP del mittente (privato) nell'indirizzo IP pubblico del router che opera l'SNAT. Può modificare con la porta sorgente
dell'header TCP/UDP.

Tipicamente questa tecnica permette a multipli host all'interno di una rete privata locale di accedere alla rete Internet.

Il router che fa SNAT lo esegue dopo che è stato deciso il routing.



## Destination NAT

DNAT viene utilizzato da tutti quei client che si trovano su Internet (hanno un IP pubblico) e hanno bisogno di accedere ad uno specifico host
privato, impossibile da raggiungere direttamente con un IP pubblico.

Esso trasla l'indirizzo IP del destinatario (pubblico) nell'indirizzo IP privato dell'host che detiene il servizio *masquerato* dall'IP pubblico.
Può modificare con la porta di destinazione dell'header TCP/UDP (**port forwarding**).

Tipicamente questa tecnica permette di ospitare servizi (ad esempio un sito web) all'interno di una rete privata, rendendoli accessibili dall'esterno.

Il router che fa DNAT lo esegue prima di decidere il routing.

<br>
<br>

