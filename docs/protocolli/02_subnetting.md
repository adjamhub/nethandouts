# Subnetting

La tecnica di organizzazione degli indirizzi a classi è divenuta limitante nel momento in cui il numero
di indirizzi **assegnati** è iniziato velocemente a salire. Questo perché l'assegnazione per classi degli
indirizzi tende per costruzione a sprecarne una grande quantità: infatti vi ricordo che la caratteristica
principale di IPv4 è quella di aggregare fisicamente tutti i dispositivi che dal punto di vista logico sono
aggregati, ovvero che hanno la stessa parte di rete.

Gli indirizzi IP mondiali sono gestiti da un unico ente centrale: **ICANN (Internet Corporation for
Assigned Names and Numbers)**. Questi vengono distribuiti ai provider di servizi internet per reti,
cioè ogni provider può richiedere una rete di indirizzi IP, di cui rivendere gli indirizzi IP validi e poi,
una volta terminati, richiederne una nuova.

Ad esempio, il provider PUNTO.IT, che lavora in Italia e prevede di avere oltre 50mila clienti, ottiene
da ICANN la rete di classe B di indirizzo 150. 60. 0. 0 (max 65534 host). Se dopo alcuni anni, il
volume di affari di PUNTO.IT supera quota 65534, esso sarà costretto a richiedere ad ICANN una
nuova assegnazione.

Capita però che a volte gli affari non vadano bene... se PUNTO.IT arriva a non più di 30.000 clienti, si
ritrova in mano con oltre 35000 IP che non riesce a vendere nel mercato, né può prestare ad altri per le
proprie assegnazioni!

Tutti IP sprecati...

Il subnetting è una tecnica che si prefigge di mitigare il problema della frammentazione e del mancato
utilizzo degli indirizzi IP per costruzione di IPv4. Quello che è importante capire è che esso si
“incastra” perfettamente dentro IPv4, non negando la sua organizzazione per classi, ma cercando
localmente di addolcire l’asperità della frammentazione.

Ad esempio, se nel caso di PUNTO.IT, una “magia” permettesse di “spaccare” la rete 150. 60. 0. 0 in
due con 32000 host ciascuno (circa), il problema dello spreco di indirizzi IP sarebbe praticamente
risolto!

PUNTO.IT avrebbe gli IP a lui necessari (con 2000 host circa disponibili per “migliorare” il suo
mercato) e il secondo gruppo sarebbe riassegnabile ad un altro provider (ad esempio DOT.COM) per il


suo mercato.

Proviamo a riassumere il problema, evidenziandolo con un esempio, per meglio analizzare le possibili
soluzioni:

**_Esempio_**

_Alla società fittizia_ **_PuntoIt_** _, provider di servizi internet per l'italia, viene assegnata la rete di classe B
150. 60. 0. 0. Questo significa che PuntoIt ha a disposizione fino a 65.534 IP da rivendere prima di
poterne richiedere un'altra._

_Immaginiamo che PuntoIt non riesca a rivendere più di 30.000 connessioni internet, a causa della
concorrenza: più di 35 mila indirizzi sono “sprecati” in mano a essa senza possibilità per altri di
utilizzarli!_

_In questo caso, una tecnica di “suddivisione” delle classi di indirizzi sarebbe una manna dal cielo..._

Risulta ovvio che la tecnica proposta definisce una soluzione transitoria del problema, in attesa
dell’adozione della versione 6 del protocollo IP. Il concetto alla base del subnetting è l'abolizione della
suddivisione prestabilita in parte di rete e parte di host che avviene nelle 5 classi di indirizzi IPv4 A, B,
C, D, E.

Nel subnetting si elimina (localmente) il concetto di classe prestabilita di indirizzo IP specificando per
ogni indirizzo o blocco di indirizzi il numero di bit utilizzati per indicare la parte di rete e di
conseguenza quelli rimanenti per la parte di host.

Viene dunque identificata come **notazione CIDR** la seguente tecnica:

Nell'indirizzamento a classi eravamo soliti indicare un indirizzo di rete e la sua subnet mask, ad
esempio:

Indirizzo IP e relativa subnet mask

192.168.0.1 / 255.255.255.

La relativa notazione CIDR mantiene semplicemente l'informazione del **numero di bit riservati alla
parte di rete** , nell'esempio precedente:


Indirizzo IP con notazione CIDR

192.168.0.1 / 24

Ovviamente in questo caso lo spazio riservato alla parte di host si desume per differenza (32 – 24 = 8).

Cerchiamo di capire quello che si può fare aiutandoci con l’esempio relativo al Provider italiano
PuntoIt. Nell'esempio precedente, esso aveva assegnata la rete di classe B di indirizzo 150. 60. 0. 0
con un volume di affari di 30.000 connessioni vendute circa.

Nella sua suddivisione in parte di rete e parte di host ha 16 bit per la rete e i restanti 16 per la parte di
host. Ma, quanti bit di host gli servono realmente per gestire le 30.000 connessioni? Ragionando un po'
si capisce che gliene servono solo 15, infatti:

#### 215 – 2 = 32.

mentre ad esempio, usandone solo 14 avremmo avuto:

#### 214 – 2 = 16.

Può dunque risparmiare un bit della parte di host e usarlo per distinguere i due gruppi: il primo gruppo
di indirizzi sarà quello con questo bit uguale a ZERO, il secondo sarà quello con bit uguale a UNO.

Praticamente questo ultimo bit della parte di host viene utilizzato per distinguere i gruppi ovvero
diventa **_come un bit della parte di rete_**. Quindi si potrà considerare le due reti come:

- Quella che ha la parte di rete 150. 60 e il bit seguente ZERO
- Quella che ha la parte di rete 150. 60 e il bit seguente UNO

La parte di rete delle sottoreti che così si creano passa da 16 a 16 + 1 = 17 bit, mentre la parte di host
passa da 16 a 16 – 1 = 15 bit.

Il provider in questione che realizza il subnetting potrà dunque rivendere le classi in eccesso ad altri


provider. Il subnetting dovrà essere gestito da un dispositivo “di collegamento” (i pacchetti di tutti i
dispositivi che appartengono alla nuova suddivisione dovranno attraversarlo) con la rete internet.

Le 2 sottoreti così formate avranno i seguenti indirizzi:

### Prima sottorete : 150. 60. 00000000. 0 / 17

### Seconda sottorete: 150. 60. 10000000. 0 / 17

Da qui, applicando le solite regole (tutti i bit di host a ZERO per il network address, tutti a UNO per il
broadcast address...) si ottengono i seguenti IP

**Prima sottorete**

subnetwork address **150. 60. 0. 0 / 17**

primo indirizzo valido **150. 60. 0. 1 / 17**

...

ultimo indirizzo valido **150. 60. 127. 254 / 17**

Broadcast address **150. 60. 127. 255 / 17**

```
Seconda sottorete
```
```
subnetwork address 150. 60. 128. 0 / 17
```
```
primo indirizzo valido 150. 60. 128. 1 / 17
```
...

```
ultimo indirizzo valido 150. 60. 255. 254 / 17
```
```
Broadcast address 150. 60. 255. 255 / 17
```

## Esercizi sul subnetting

**Esercizio 101**

Eseguire il subnetting della rete con network address di classe B 150. 40. 0. 0, cercando di ottenere
almeno 6 sottoreti.

Elencare:

- il numero di bit da prestare alla parte di rete
- il numero di sottoreti create e il numero di host ottenuti per sottorete
- il network address, il primo indirizzo valido, l'ultimo indirizzo valido e il broadcast address
    della terza sottorete

**Esercizio 102**

Eseguire il subnetting della rete con network address di classe B 150. 40. 0. 0, facendo in modo che
in ogni sottorete ci siano almeno 1000 host.

Elencare:

- il numero di bit da prestare alla parte di rete
- il numero di sottoreti create e il numero di host ottenuti per sottorete
- il network address, il primo indirizzo valido, l'ultimo indirizzo valido e il broadcast address
    della seconda sottorete

**Esercizio 103**

Si prenda in considerazione una divisione di sottorete per una organizzazione dotata di una rete di
indirizzi di classe B (ad esempio, la classe 180. 40. 0. 0 / 16) che dovrà contenere almeno 76 sottoreti.
Quanti host potranno esserci su ciascuna sottorete?


**Esercizio 104**

Una organizzazione ha deciso di dividere il proprio network address di classe B, sfruttando il terzo
ottetto per le reti fisiche, ma si è accorta di non aver sufficiente spazio per ospitare 255 host in ogni
rete. Spiegare.

**Esercizio 105**

Ha senso creare una porzione di sottorete in un indirizzo di rete di classe C? Se sì, quante porzioni è
possibile creare? Con quanti host? Se no, spiegare le proprie motivazioni.

**Esercizio 106**

Consideriamo una rete con 25 dispositivi. Calcolare la maschera di sottorete che minimizzi lo spreco di
host per rete. Assegnare gli indirizzi ai dispositivi estraendo una opportuna sottorete dall'indirizzo di
rete di classe C 193. 212. 100. 0 / 24.

**Esercizio 107**

Considerare 2 sottoreti A e B con numero di host A + B = 18. Calcolare la maschera di sottorete che
minimizzi lo spreco di indirizzi IP e assegnare ai singoli dispositivi prendendo gli IP dall'indirizzo di
rete 193. 200. 10. 0 / 24 in modo che le due sottoreti siano contigue.

**Esercizio 108**

Considerare 2 sottoreti A e B connesse da un router R. Il numero di hosts per sottorete è rispettivamente
40 e 15. Si ha in gestione l'indirizzo di rete 193. 200. 10. 0 / 24. Assegnare indirizzi alle due sottoreti
in maniera contigua e in modo che abbiano lo stessa subnet mask.

**Esercizio 109**

L'indirizzo di rete di classe B 142. 8. 0. 0 è suddiviso in sottoreti dedicando 6 bit alla subnet e 10 bit
agli host. Si specifichi l'indirizzo del terzo host della seconda subnet e gli indirizzi minimo e massimo
degli host della quarta subnet. Infine verificare se l'indirizzo 142. 8. 252. 124 è un indirizzo corretto e


valido (cioè assegnabile ad un dispositivo).

**Esercizio 110**

Un piccolo numero di indirizzi IP consecutivi sono disponibili partendo da 192. 214. 11. 0.
Supponiamo che le organizzazioni A, B, C richiedano rispettivamente 100, 50, 40 indirizzi.

Per ognuno di questi specificare:

- il primo indirizzo IP assegnato
- l'ultimo indirizzo IP assegnato
- l'indirizzo di rete e di broadcast per ogni sottorete

**Esercizio 111**

Si determini il subnetting IP in cui si vogliono creare 62 sottoreti in classe B con indirizzo di partenza
128. 10. 0. 0

- determinare la subnet mask
- determinare il numero di host per sottorete
- determinare, in una delle sottoreti, indirizzo di rete, intervallo degli indirizzi di host e indirizzo
    di broadcast

**Esercizio 112**

Si determini il subnetting IP in cui si vogliono creare 10 sottoreti in classe C con indirizzo di partenza
193. 200. 10. 0 e calcolare:

- la subnet mask
- il numero di host per sottorete
- in una delle sottoreti, indirizzo di rete, intervallo degli indirizzi di host e indirizzo di broadcast



