# Subnetting

La tecnica di organizzazione degli indirizzi in classi è divenuta limitante nel momento in cui il numero
di indirizzi **assegnati** è iniziato velocemente a salire. Questo perché l'assegnazione per classi degli
indirizzi tende per costruzione a sprecarne una grande quantità: infatti vi ricordo che la caratteristica
principale di IPv4 è quella di aggregare fisicamente tutti i dispositivi che dal punto di vista logico sono
aggregati, ovvero che hanno la stessa parte di rete.

Proviamo a spiegare la questione.

Gli indirizzi IP mondiali sono gestiti da un unico ente centrale: **ICANN (Internet Corporation for Assigned Names and Numbers)**. 
Questi vengono distribuiti ai **provider di servizi internet** per reti, cioè ogni provider può richiedere una rete di indirizzi IP, 
di cui rivendere gli indirizzi IP validi e poi, una volta terminati, richiederne una nuova.


!!! tip "Internet Service Providers"
    
    Gli **ISP**, acronimo per *Internet Service Providers*, ovvero *provider di servizi internet* sono quelle
    società che forniscono connettività ai privati.
    
    In Italia le più famose sono TIM, Vodafone, Fastweb, Iliad, etc...
    
Ogni provider ovviamente gestisce la sua propria rete fisica e quindi necessita di un indirizzamento separato dagli altri.

Capito a grandi linee il funzionamento dell'indirizzamento su Internet, proviamo con un esempio a spiegare come IPv4 sia, per sua stessa natura,
una fonte di spreco per l'utilizzo degli indirizzi IP.

Ad esempio, al provider (di fantasia) *PUNTO.IT*, che lavora in Italia, viene assegnata da ICANN la rete di classe B di indirizzo `150.60.0.0` (max 65534 host). 
Se il volume di affari di PUNTO.IT si attesta (ad esempio) in 30 mila utenti, esso starà sprecando più di 34 mila indirizzi che non possono essere assegnati a 
nessun altro!!!

> Il **subnetting** è una tecnica che si prefigge di mitigare il problema dello spreco di indirizzi IPv4, quando il problema è
> casuato dalla natura stessa di IPv4 (problema della frammentazione delle reti).
>
> Il subnetting è una tecnica **migliorativa** per IPv4 (una vera genialata, secondo me). 
> Si incastra perfettamente nella sua organizzazione per classi senza stravolgere la logica di base di IPv4.


**La tecnica del subnetting divide una rete in N sottoreti (dove N è una potenza di 2).**

Ad esempio, nel caso di PUNTO.IT precedentemente illustrato, dividendo la rete in 2 parti (da 32 mila indirizzi ciascuna), il problema dello spreco di indirizzi
sarebbe praticamente annullato: PUNTO.IT avrebbe gli IP a lui necessari (con 2000 host circa disponibili per “migliorare” il suo
mercato) e il secondo gruppo sarebbe riassegnabile ad un altro provider (ad esempio DOT.COM) per il suo mercato.

Proviamo a scrivere i dati del problema per rendere evidente la tecnica:


Rete iniziale affidata alla società "PuntoIt": `150.60.0.0 / 16`

Se come abbiamo detto, vogliamo dividere la rete in due sottoreti, dovremo *rubare* alcuni bit dalla parte di host e *spostarli* nella parte
di rete, ad indicare la *parte di sottorete*. 

Ma quanti bit? 

Questo dipende chiaramente da quante sottoreti vogliamo fare. Per fare due sottoreti prendere un bit: la prima sottorete avrà il bit di sottorete a 0, 
la seconda il bit di sottorete a 1.

Dove lo prendiamo questo bit?

L'ho già detto... dalla parte di host!

Sì... ma quale prendiamo??

Questa è la domanda più intelligente finora... i bit da prendere sono quelli più a sinistra, in modo da ottenere una suddivisione comunque compatta fra parte di
rete e parte di host. Quindi:


- la prima sottorete avrà parte di rete `150. 60` e il bit seguente **ZERO**.
- la seconda sottorete avrà parte di rete `150. 60` e il bit seguente **UNO**.

A questo punto i bit di rete diventano `16 + 1 = 17` !!!

```
Prima sottorete :   150. 60. 00000000. 0 / 17

Seconda sottorete:  150. 60. 10000000. 0 / 17
```

Da qui, applicando le solite regole (tutti i bit di host a ZERO per il network address, tutti a UNO per il
broadcast address...) si ottengono i seguenti IP:

**Prima sottorete**

subnetwork address:      **150. 60. 0. 0 / 17** <br>
primo indirizzo valido:  **150. 60. 0. 1 / 17** <br>
...<br>
ultimo indirizzo valido: **150. 60. 127. 254 / 17**<br>
Broadcast address:       **150. 60. 127. 255 / 17**<br>

<br>

**Seconda sottorete**

subnetwork address:      **150. 60. 128. 0 / 17**<br>
primo indirizzo valido:  **150. 60. 128. 1 / 17**<br>
...<br>
ultimo indirizzo valido: **150. 60. 255. 254 / 17**<br>
Broadcast address:       **150. 60. 255. 255 / 17**<br>


!!! tip "Suggerimento"
    
    Quando facciamo un subnetting ricordiamoci di indicare **sempre** la subnet mask di riferimento!
    
    La notazione CIDR è stata inventata appositamente per il subnetting... usiamo sempre quella!
    
    



## Esercizi sul subnetting

**Esercizio 101**

Eseguire il subnetting della rete con network address di classe B 150. 40. 0. 0, cercando di ottenere
almeno 6 sottoreti.

Elencare:

- il numero di bit da prestare alla parte di rete
- il numero di sottoreti create e il numero di host ottenuti per sottorete
- il network address, il primo indirizzo valido, l'ultimo indirizzo valido e il broadcast address
    della terza sottorete

---

**Esercizio 102**

Eseguire il subnetting della rete con network address di classe B 150. 40. 0. 0, facendo in modo che
in ogni sottorete ci siano almeno 1000 host.

Elencare:

- il numero di bit da prestare alla parte di rete
- il numero di sottoreti create e il numero di host ottenuti per sottorete
- il network address, il primo indirizzo valido, l'ultimo indirizzo valido e il broadcast address
    della seconda sottorete

---

**Esercizio 103**

Si prenda in considerazione una divisione di sottorete per una organizzazione dotata di una rete di
indirizzi di classe B (ad esempio, la classe 180. 40. 0. 0 / 16) che dovrà contenere almeno 76 sottoreti.
Quanti host potranno esserci su ciascuna sottorete?

---

**Esercizio 104**

Una organizzazione ha deciso di dividere il proprio network address di classe B, sfruttando il terzo
ottetto per le reti fisiche, ma si è accorta di non aver sufficiente spazio per ospitare 255 host in ogni
rete. Spiegare.

---

**Esercizio 105**

Ha senso creare una porzione di sottorete in un indirizzo di rete di classe C? Se sì, quante porzioni è
possibile creare? Con quanti host? Se no, spiegare le proprie motivazioni.

---

**Esercizio 106**

Consideriamo una rete con 25 dispositivi. Calcolare la maschera di sottorete che minimizzi lo spreco di
host per rete. Assegnare gli indirizzi ai dispositivi estraendo una opportuna sottorete dall'indirizzo di
rete di classe C 193. 212. 100. 0 / 24.

---

**Esercizio 107**

Considerare 2 sottoreti A e B con numero di host A + B = 18. Calcolare la maschera di sottorete che
minimizzi lo spreco di indirizzi IP e assegnare ai singoli dispositivi prendendo gli IP dall'indirizzo di
rete 193. 200. 10. 0 / 24 in modo che le due sottoreti siano contigue.

---

**Esercizio 108**

Considerare 2 sottoreti A e B connesse da un router R. Il numero di hosts per sottorete è rispettivamente
40 e 15. Si ha in gestione l'indirizzo di rete 193. 200. 10. 0 / 24. Assegnare indirizzi alle due sottoreti
in maniera contigua e in modo che abbiano lo stessa subnet mask.

---

**Esercizio 109**

L'indirizzo di rete di classe B 142. 8. 0. 0 è suddiviso in sottoreti dedicando 6 bit alla subnet e 10 bit
agli host. Si specifichi l'indirizzo del terzo host della seconda subnet e gli indirizzi minimo e massimo
degli host della quarta subnet. Infine verificare se l'indirizzo 142. 8. 252. 124 è un indirizzo corretto e
valido (cioè assegnabile ad un dispositivo).

---

**Esercizio 110**

Un piccolo numero di indirizzi IP consecutivi sono disponibili partendo da 192. 214. 11. 0.
Supponiamo che le organizzazioni A, B, C richiedano rispettivamente 100, 50, 40 indirizzi.

Per ognuno di questi specificare:

- il primo indirizzo IP assegnato
- l'ultimo indirizzo IP assegnato
- l'indirizzo di rete e di broadcast per ogni sottorete

---

**Esercizio 111**

Si determini il subnetting IP in cui si vogliono creare 62 sottoreti in classe B con indirizzo di partenza
128. 10. 0. 0

- determinare la subnet mask
- determinare il numero di host per sottorete
- determinare, in una delle sottoreti, indirizzo di rete, intervallo degli indirizzi di host e indirizzo
    di broadcast

---

**Esercizio 112**

Si determini il subnetting IP in cui si vogliono creare 10 sottoreti in classe C con indirizzo di partenza
193. 200. 10. 0 e calcolare:

- la subnet mask
- il numero di host per sottorete
- in una delle sottoreti, indirizzo di rete, intervallo degli indirizzi di host e indirizzo di broadcast


