# Protocollo ARP


ARP (Address Resolution Protocol) è un protocollo "storico" delle reti,
implementato nel 1982 tramite l'[**RFC 826**](https://tools.ietf.org/html/rfc826), rappresenta uno strumento
indispensabile del protocollo di rete e grazie anche al suo opposto RARP
(Reverse ARP) si pone come strumento di collegamento fra il livello di
rete e quello inferiore.

Per essere spedito infatti, un pacchetto IP deve essere passato al
livello inferiore che avrà il compito di individuare fisicamente il
dispositivo del destinatario e di trasformare in segnali fisici i dati
logici contenuti nei pacchetti IP. La procedura di individuazione fisica
del destinatario si risolve tramite il protocollo ARP, che è in grado di
abbinare ad ogni indirizzo logico (un indirizzo IP) un indirizzo fisico
(un **indirizzo MAC**) che identifica univocamente un dispositivo.

L'indirizzo MAC, o indirizzo fisico, è un identificatore univoco per
una NIC (Network Interface Card, una scheda di rete). Questo significa
che ogni scheda di rete prodotta sulla Terra possiede un indirizzo MAC
diverso e che questo permette di tracciare il costruttore, il pezzo
prodotto e in molti casi persino l'acquirente (da parte della ditta
produttrice).

L'indirizzo MAC é formato da 6 coppie di cifre esadecimali, indicate di
solito con due punti che li separano, ad esempio: 00:C0:9F:3C:C0:20

Delle 6 coppie le prime 3 (in questo caso 00:C0:9F) identificano la
ditta produttrice, mentre le 3 rimanenti identificano il "pezzo" nel
lotto di produzione.

Questa identificazione così vincolante (conoscere l'indirizzo MAC di un
dispositivo... è tanta roba!) può avvenire solo in una rete locale,
infatti ARP manda in broadcast una richiesta del tipo:

```
Who has 192.168.0.13? Tell 192.168.0.10
```

Tutti i dispositivi della rete locale riceverano la richiesta ma solo
uno avrà quell'indirizzo IP e risponderà (in unicast, all'indirizzo
indicato) con il suo indirizzo MAC

```
192.168.0.13 is at 01:02:03:04:05:06
```

A questo punto, colui che ha fatto la richiesta (il dispositivo con
indirizzo 192.168.0.10 nel nostro esempio) inserirà nella sua cache ARP
la coppia indirizzo IP / indirizzo MAC. In questo modo non avrà bisogno
di richiedere ogni volta l'intervento del protocollo ARP per risolvere
un indirizzo.

Allo stesso modo però, per permettere cambiamenti nella configurazione
della rete, ad ogni voce nella cache viene assegnata un `TTL (Time To Live)`, 
un tempo oltre il quale la voce viene cancellata.

Il TTL di default dura 2 minuti. Ogni volta che avviene traffico fra le
due stazioni il TTL si resetta a 2 minuti. Oltre 10 minuti la voce in
cache viene comunque eliminata.


