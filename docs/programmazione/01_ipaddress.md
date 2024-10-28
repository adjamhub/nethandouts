# ipaddress

!!! warning "IPv4 vs IPv6"

    Il modulo `ipaddress` gestisce perfettamente sia l'indirizzamento **IPv4** che quello basato su **IPv6**. <br>
    Per semplicità, in questa trattazione ci concentreremo solo sull'indirizzamento IPv4.
    

Il modulo `ipaddress` è un modulo per la gestione e la manipolazione degli indirizzi IP (IPv4/IPv6). Per poter utilizzare il modulo è necessario istanziare un oggetto della classe, un indirizzo.

Questo può essere fatto per valore:

``` python
>>> # indirizzo inserito tramite notazione decimale puntata
>>> a = ipaddress.ip_address('192.0.2.1')
IPv4Address('192.0.2.1')

>>> # indirizzo inserito in forma numerica (int)
>>> b = ipaddress.ip_address(3221225985)
IPv4Address('192.0.2.1')
```

Come per gli indirizzi, è possibile definire una rete di indirizzi (tramite un network address):

``` python
>>> # definizione tramite notazione decimale puntata più network mask in notazione CIDR
>>> net1 = ipaddress.ip_network('192.0.2.0/24')
IPv4Network('192.0.2.0/24')
```

Se inserisci un ip che non è un network address, la funzione `ip_network` da giustamente errore. Però se sei somaro sui network address, ma ci capisci di Python, 
è possibile ottenere un indirizzo di rete a partire da qualunque indirizzo IP, tramite l'opzione `strict=False`:


``` python
>>> # se sbagli il network address, ip_network da errore
>>> net2 = ipaddress.ip_network('192.0.2.1/24')
ValueError: 192.0.2.1/24 has host bits set

>>> # se invece usi l'opzione strict=False, Python se la calcola da solo a partire da qualunque indirizzo IP
>>> net3 = ipaddress.ip_network('192.0.2.1/24', strict=False)
IPv4Network('192.0.2.0/24')
```

Come per gli indirizzi, è possibile utilizzare i numeri interi anche per la definizione delle reti:

``` python
>>> net4 = ipaddress.ip_network(3221225984)
IPv4Network('192.0.2.0/32')
```

Se vuoi indicare un IP indicando esplicitamente la maschera di sottorete, devi usare la notazione CIDR e la funzione `ip_interface`.
A partire da questa... puoi fare parecchie cosine con l'oggetto indirizzo:


``` python
>>> host1 = ipaddress.ip_interface('192.0.2.1/24')
IPv4Interface('192.0.2.1/24')
>>> net1 = host1.network
IPv4Network('192.0.2.0/24')
```

Anche con le reti, è possibile fare parecchie cose in maniera abbastanza semplice:

``` python
>>> net4 = ipaddress.ip_network('192.0.2.0/24')
>>> net4.num_addresses
256
>>> for x in net4.hosts():
        print(x)  
192.0.2.1
192.0.2.2
192.0.2.3
192.0.2.4
...
192.0.2.252
192.0.2.253
192.0.2.254
>>> mask = net4.netmask
IPv4Address('255.255.255.0')
```

Gli oggetti di tipo network possono essere trattate anche come liste:

``` python
>>> net4[1]
IPv4Address('192.0.2.1')

>>> net4[25]
IPv4Address('192.0.2.25')

>>> net4[-1]
IPv4Address('192.0.2.255')
```


<br>
<br>

