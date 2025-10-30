# Suite Internet: Livello di rete


Il livello di rete della suite Internet si occupa delle seguenti procedure:


- l'**indirizzamento**, ovvero la possibilità di distinguere i dispositivi tra loro e di raggrupparli opportunamente.

- L'**impacchettamento**, ovvero la preparazione dei pacchetti adatti ad essere trasferiti nella rete Internet 
  per andare dal mittente al destinatario (adesso che con l'indirizzamento può distinguerli).

- L'**instradamento**, ovvero la scelta del percorso che un generico pacchetto dati deve compiere per andare dal mittente al destinatario.

- La **gestione delle congestioni**, che durante l'instradamento possono verificarsi se troppi pacchetti sono indirizzati verso un
  unico percorso di rete, eventualmente troppo trafficato.


Prima di andare avanti, impariamo un minimo di terminologia, che ci tornerà utile per comprendere appieno i concetti a cui faremo riferimento.


## Terminologia


**host**<br>
Qualunque dispositivo che accede alla rete tramite un indirizzo IP, grazie al quale può essere identificato univocamente.

**routing (instradamento)**<br>
Scelta del percorso che un pacchetto IP deve compiere.

**router**<br>
Software che determina il routing. Poiché tipicamente queste operazioni vengono svolte su dispositivi dedicati,
il termine indica spesso anche l'apposito dispositivo di rete, in cui è stato installato il software per la selezione del percorso
dei pacchetti che transitano su di esso.

**tabella di routing**<br>
Set di informazioni che permettono al router di stabilire il percorso per ogni pacchetto in transito.


Ok, adesso siamo pronti!!!


## Protocollo IP


Quando si descrive il livello di rete non si può fare a meno di parlare del protocollo IP! Questo protocollo infatti,
interviene in tutte le connessioni (unico protocollo della suite sempre utilizzato) e si occupa di gran parte del lavoro!
Più precisamente si occupa dell'indirizzamento, dell'impacchettamento e della prima fase dell'instradamento!

---

**Indirizzamento**

Dovremmo aver già studiato l'indirizzamento IP! Quella struttura permette di distinguere tutti i dispositivi che appartengono alla rete Internet!!!

---

**Impacchettamento**

IP è l'unico protocollo di rete che fa pacchetti. Questi presentano la caratteristica di essere **instradabili**, ovvero di essere adatti alle operazioni di routing.
Tutti gli altri protocolli di rete intervengono **eventualmente** dopo IP, utilizzando direttamente i pacchetti IP per le loro operazioni, eventualmente modificando l'intestazione del pacchetto.

---

**Routing (primo step)**

Il protocollo IP si occupa perfino del primo instradamento, ovvero dell'uscita dal dispositivo del mittente tramite la sua **logica di base del protocollo IP.**

Esso confronta l'indirizzo IP del mittente del pacchetto con quello del destinatario e si comporta secondo le seguenti regole:

-   Se l'indirizzo IP del mittente è uguale all'IP del destinatario,
    oppure uno degli indirizzi è della classe 127, il pacchetto viene
    *rimbalzato* al livello di trasporto (tecnica del **loopback**).
-   Se il destinatario si trova sullo stesso segmento di rete del
    mittente, il pacchetto viene inviato in maniera diretta,
    individuando il destinatario tramite ARP (un altro protocollo di
    rete, che vedremo fra breve).
-   Se il destinatario NON si trova nella stessa rete del mittente, si
    invia il pacchetto al **default gateway**.


Impacchettato correttamente, inserito in un indirizzamento organizzato e finalmente fuori dal disposirivo mittente, il prossimo compito del livello
di rete viene affidato ai protocolli di routing.


<br>
<br>

