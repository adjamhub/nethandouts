# Dispositivi di rete

I dispositivi di rete rappresentano tutti quei nodi in una rete che
hanno semplicemente il compito di far funzionare le comunicazioni, senza
realmente "partecipare" al dialogo.

Questi dispositivi vengono tipicamente classificati in base al livello
di rete in cui tipicamente lavorano:

---

**Livello Fisico**

-   ***HUB***: è il dispositivo di rete più semplice, tipicamente il
    centro di un collegamento a stella. La sua funzione è semplicemente
    quella di smistare il segnale in arrivo da un cavo in tutte le altre
    porte con una tecnica diffusiva. Per questa ragione viene
    tipicamente definito un "ripetitore multiporta".
    
-   **REPEATER**: nel campo delle telecomunicazioni un ripetitore può
    essere indistintamente un dispositivo analogico in grado di
    amplificare in uscita un segnale d'ingresso o un dispositivo
    digitale in grado di rigenerare un segnale per la trasmissione.

---

**Livello Data-Link**

-   **SWITCH**: lo switch (o "commutatore") è il dispositivo di rete che
    si occupa dell'instradamento a livello di rete locale, controllando
    gli indirizzi MAC inseriti nei vari frame e dirigendoli ognuno verso
    la NIC proprietaria dello stesso. Per questo motivo viene
    solitamente definito un "hub intelligente". Più formalmente, si dice
    che uno switch è in grado di minimizzare il **dominio di
    collisione** (l'insieme dei dispositivi che risentono di una
    collisione) senza modificare quello di broadcast (l'insieme dei
    dispositivi che ricevono i pacchetti di broadcast).
    
-   **BRIDGE**: questo dispositivo di rete serve a collegare tra loro
    due segmenti diversi dal punto di vista fisico, ma che rappresentano
    lo stesso segmento dal punto di vista logico. La sua caratteristica
    principale consiste nel separare in un diverso dominio di collisione
    i segmenti fisici ad esso collegati.


---

**Livello di Rete**

-   **ROUTER**: Il router è senza dubbio il più complesso ed
    interessante dispositivo di rete ed è quello che si occupa
    dell'instradamento dei pacchetti su reti diverse,
    dell'aggiornamento e della manutenzione della tabella di routing,
    del controllo delle liste di accessi (ACL) basate su IP e delle
    cosiddette LAN Virtuali (VLAN).

<br>
<br>

