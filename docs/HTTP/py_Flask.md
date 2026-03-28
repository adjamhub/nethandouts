# Python: Flask Web Framework

Uno Web Framework rappresenta una collezione di librerie e moduli che permette ad uno web developer 
di scrivere applicazioni web senza occuparsi dei dettagli di basso livello.

> **Flask** è uno **Web Framework** scritto in Python,<br> 
> basato sul toolkit **WSGI Werkzeug** e sul template engine **Jinja2**.

**WSGI (Web Server Gateway Interface)** è una specifica che definisce una interfaccia universale 
di comunicazione fra un server web e una applicazione web: Werkzeug è semplicemente una implementazione 
WSGI utilizzata da Flask.

**Jinja2** è un template engine molto popolare per il linguaggio Python. Un sistema di web template combina 
un template (uno schema, uno scheletro) con delle sorgenti dati per creare una pagina web dinamica.

Flask è disponibile in pochi istanti tramite pip:

``` bash
$ pip install Flask
```

Oppure dall'interfaccia di Thonny per la gestione dei pacchetti (sottinteso: cerca Flask... Installa... Attendi... Boom!)


<!-- ################################################################################# -->
## Primi esempi con Flask

La più semplice applicazione sviluppabile con la libreria Flask è
strutturata in questo modo:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello, World!"
```

Se la eseguite con Thonny essa creera un avviso tipo questo:


    # Running the app with options chosen by Thonny. See Help for details.
    * Serving Flask app 'HelloWorld' (lazy loading)
    * Environment: development
    * Debug mode: off
    * Running on **http://127.0.0.1:5000/** (Press CTRL+C to quit)


Cliccando sul link [http://127.0.0.1:5000/](http://127.0.0.1:5000/)
o aprendolo direttamente nel browser vedremo una pagina semplice
semplice con scritto "Hello, World!".

A vederlo così non sembra difficile, ma ci sono alcune cosine che
risultano un po' strane a prima vista, provo a commentare tutto questo
primo codice e a spiegare la logica con cui si sviluppa utilizzando
Flask.

Importiamo l'oggetto Flask dal modulo flask

``` python
from flask import Flask
```

Questa operazione è l'operazione di base per lavorare con il modulo
Flask: non c'è molto altro da commentare se non che siamo già pratici di
questa modalità e che arriveranno man mano altri oggetti dal modulo
flask, secondo necessità.

Creiamo l'oggetto Flask che gestisce la nostra applicazione

``` python
app = Flask(__name__)
```

Tecnicamente questo oggetto rappresenta il server web... ovvero il
software che fornisce le pagine web agli utenti (che le richiedono
tramite i browser).

Per funzionare ha bisogno di un nome (si possono eseguire più oggetti
contemporaneamente, ma devono avere nome diverso).

Definiamo la funzione da eseguire.

```python
def index():
    return "Hello, World!"
```

Lo so, ho saltato la riga "complicata". Ma siccome ho bisogno di più
spazio per spiegarla... faccio prima questa che è facile.

La funzione in oggetto si chiama come vi pare e restituisce una stringa:
quella stringa sarà il contenuto della pagina web che vedremo sul
browser.

Impostiamo il decoratore della nostra applicazione

``` python
@app.route("/")
```

Un `decoratore` è una struttura Python relativamente complessa che si abbina ad una funzione 
(quella che indicate sotto alla riga con la @) e che ne modifica il comportamento (la ***decora***).

Il decoratore `route`, definito nella classe Flask di cui app è un oggetto si comporta in questo modo: 
quando il PATH dell'URL richiesto corrisponde al suo parametro esegue la funzione abbinata e restituisce
come contenuto della pagina WEB ciò che la funzione ritorna.

Il decoratore del nostro esempio viene scatenato perché il link in questione è [http://127.0.0.1:5000/](http://127.0.0.1:5000/): 
il PATH di questo URL è effettivamente la stringa "/".

Se volessimo "aggiungere una pagina" al nostro sito, raggiungibile all'URL [http://127.0.0.1:5000/nuovapagina](http://127.0.0.1:5000/nuovapagina/)
allora dovremmo aggiungere al nostro codice un nuovo decoratore abbinato ad una nuova funzione: una cosa del tipo

```python
@app.route("/nuovapagina/")
def nuovapagina():
    s = "<h1>Ciao</h1>
    s += "Sei sull'altra pagina..."
    return s
```

Spero sia tutto chiaro fin qui!

Avrete notato che Thonny esegue la app di Flask nell'indirizzo locale `127.0.0.1`, 
che non è raggiungibile dall'esterno. Per cambiare questo comportamento, eseguite in maniera esplicita la
funzione `run()` terminando il codice con una cosa tipo:

```python
if __name__ == "__main__":
    app.run(host = "0.0.0.0", port = 5000, debug = False)
```


<!-- ################################################################################# -->
## render_template

Finora le nostre funzioni restituivano semplici stringhe di testo. 
In una vera applicazione web vogliamo restituire pagine HTML complete. 
Potremmo costruire l'HTML direttamente in Python:

```python
@app.route('/')
def home():
    return '<html><body><h1>Ciao!</h1></body></html>'
```

Funziona, ma diventa presto ingestibile. I **template** risolvono questo problema: sono file HTML separati, con la possibilità di inserire dati dinamici al loro interno.

Flask usa il motore di template **Jinja2**, che è già incluso nell'installazione di Flask.

---

### Struttura delle cartelle

Flask si aspetta che i template siano nella cartella `templates`, nella stessa directory di `app.py`:

```
progettoFlask/
├── app.py
└── templates/
    └── index.html
```

Crea la cartella `templates` e al suo interno il file `index.html`:

```html
<!DOCTYPE html>
<html lang="it">
<head>
    <title>La mia prima pagina</title>
</head>
<body>
    <h1>Ciao, Flask!</h1>
</body>
</html>
```

Per restituire questo template da Flask si usa la funzione `render_template`:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')
```

Flask troverà automaticamente il file nella cartella `templates`.

---

### Passare dati al template

Il vantaggio dei template è che possiamo passare dati da Python all'HTML. Si usa il secondo argomento di `render_template`:

```python
@app.route('/')
def home():
    return render_template('index.html', nome='Marco', eta=17)
```

Modifica il body del file HTML in questo modo: le variabili si usano con la sintassi `{{ variabile }}`:

```html
<body>
    <h1>Ciao, {{ nome }}!</h1>
    <p>Hai {{ eta }} anni.</p>
</body>
```

Possiamo passare anche strutture dati più complesse, come liste e dizionari:

```python
@app.route('/')
def home():
    studenti = ['Alice', 'Bruno', 'Carla']
    return render_template('index.html', studenti=studenti)
```

### Cicli nei template

Per scorrere una lista si usa `for`:

```html
<p>
{% for studente in studenti %}
    {{ studente }}<br>
{% endfor %}
</p>
```

### Iterare su dizionari

Possiamo passare anche dizionari e iterare sulle loro chiavi e valori:

```python
@app.route('/prodotto')
def prodotto():
    info = {
        'nome': 'Zaino',
        'prezzo': 29.90,
        'disponibile': True
    }
    return render_template('prodotto.html', info=info)
```

```html
<dl>
{% for chiave, valore in info.items() %}
    <dt>{{ chiave }}</dt>
    <dd>{{ valore }}</dd>
{% endfor %}
</dl>
```

Oppure accedendo direttamente ai campi:

```html
<h2>{{ info.nome }}</h2>
<p>Prezzo: {{ info.prezzo }} €</p>
{% if info.disponibile %}
    <p>Disponibile</p>
{% else %}
    <p>Non disponibile</p>
{% endif %}
```


<!-- ################################################################################# -->
## Variabili dinamiche

Nel parametro del decoratore è possibile inserire delle variabili dinamiche marcando 
alcune parole con le parentesi angolari: `<variable>`.

Questo è uno di quegli innumerevoli casi in cui un esempio vale più di mille parole...

```python
from flask import Flask

app = Flask(__name__)

@app.route("/post/<id>")
def showPost(id):
    # do something...
    return "the post you're searching for has id " + id

@app.route("/<name>")
def test(name):
    return "Hello " + name

@app.route("/<val1>/<val2>")
def dai(val1, val2):
    return "val 1 = " + val1 + ", val 2 = " + val2
```

Come vedete, è possibile generare una pagina specifica a seconda
dell'URL utilizzato e avendo magari un "template" di riferimento per
la stessa...

In effetti è proprio così: guardate che roba.

Create una pagina web chiamata welcome.html in cui digitate il seguente
codice HTML

```html
<h1>Ciao!</h1>

So che ti chiami {{ nome_utente }}
```

Come vedete questa sintassi *non è esattamente HTML*... questo è ***Jinja2***, quel web template 
che dicevamo permette di creare pagine dinamiche... ricordate?

Salvata la pagina nella cartella dei templates, il codice che la fa
funzionare è semplicemente questo:

```python
from flask import Flask,render_template

app = Flask(__name__)

@app.route("/user/<name>")
def index(name):
    return render_template("pagina.html", nome_utente=name)
```

Adesso vi basta eseguire questo script e visitare il link <http://127.0.0.1:5000/user/unnomequalsiasi> ...


<!-- ################################################################################# -->
### Redirection Behaviour

Le due seguenti route sono diverse per la presenza o meno dello slash finale:

```python
@app.route("/home/")
def home():
    return "the home page"

@app.route("/about")
def about():
    return "the about page"
```

Nel primo caso (con lo slash alla fine) Flask immagina di riferirsi ad una cartella (da cui pescare il file index.html): se l'utente digita
l'URL `http://host:port/home` (senza slash) Flask automaticamente lo aggiunge per riferirsi (correttamente) alla cartella home.

Nel secondo caso (senza lo slash finale) Flask immagina che la pagina about sia solo una pagina: se l'utente digita l'URL
`http://host:port/about` (senza slash) tutto funziona normalmente, ma se l'utente aggiunge lo slash finale (digitando http://host:port/about/)
Flask ritorna un errore 404 di pagina non trovata.



<!-- ################################################################################# -->
## Gestione form

Un'altra cosa molto interessante che è possibile fare con il modulo
Flask è la gestione dei dati scambiati fra client e server, tipicamente
inviati con metodo POST (a volte anche con una semplice GET), quando ad
esempio si compila un form di iscrizione, si risponde ad un sondaggio
sul web o si mettono le proprie credenziali per accedere ad un servizio.

Per spiegare nella maniera più semplice possibile questa funzionalità ho
realizzato un esempio molto semplice in cui l'utente si trova davanti
due caselle di testo per inserire nome utente e password e Flask
raccoglie i dati e li rivisualizza come dimostrazione di averli letti.

Entrambe le pagine saranno servite dalla nostra applicazione Flask.

La pagina con il form HTML

```html title="form html, metodo POST"
<form action="/data" method="POST">

USER: <input name="username"><br>
PASS: <input name="password" type="password"><br>

<input type="submit" value="INVIA">
</form>
```

Ovviamente l'esempio è molto scarno, ma già sufficiente per la
comprensione. Il metodo di invio è `POST`, i dati da inviare sono 2,
identificati dai nomi `username` e `password`. La pagina a cui
questi dati saranno inviati si trova all'URL relativo `/data`.


!!! tip "Suggerimento"

    Se possibile, quando si usa Flask (e Python in genere), evitate di utilizzare il nome **pass**, che corrisponde ad una precisa istruzione Python... 
    meglio evitare confusione!!!

La pagina si chiamerà "login.html" e sarà ovviamente collocata nella
cartella "templates" della nostra app.

La pagina per visualizzare i dati:

```html title="dati.html"
USER: {{ username }} <br>
PASS: {{ password }} <br>
```

Ovviamente non ha molto senso visualizzare l'username e la password. Noi
qui lo facciamo solo per dimostrare che la lettura è andata a buon fine.

La pagina si chiamerà "dati.html" e (anche questa) sarà collocata nella cartella "templates".

Il codice Python Flask

```python
from flask import Flask,render_template,request

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("login.html")

@app.route("/data", methods=["POST"])
def login():
    if request.method == 'POST':
        u = request.form.get("username")
        p = request.form.get("password")
    return render_template("dati.html",username = u,password = p)
```

Come vedete il codice introduce un nuovo oggetto: `request`.

Questo oggetto serve per la gestione delle richieste, dei dati che esse
veicolano e così via.

Ancora una volta si utilizza il web template Jinja2 per la compilazione
dei dati... mi sembra davvero molto comodo, invece che fare congiunzioni
e magie con le stringhe.

Il metodo di invio (POST, nel nostro caso) va indicato nel decoratore.

Fatto!

Detto tutto questo... basta provare!


### Recupero dati inviati con GET

Oltre ai parametri dinamici nel path, puoi leggere i **dati contenuti nella query** dell'URL della richiesta:

```
http://127.0.0.1:5000/cerca?q=flask
```

```python
@app.route('/cerca')
def cerca():
    termine = request.args.get('q', '')
    return f'Stai cercando: {termine}'
```

`request.args.get('q', '')` legge il parametro `q` dall'URL. Il secondo argomento (`''`) è il valore di default se il parametro non è presente.


<br>
<br>
<br>

## Esercizi Finali


**Esercizio 1: Watchlist film**

Gestisci una lista personale di film.

Ogni film ha:

- `titolo` (stringa, obbligatorio)
- `regista` (stringa, obbligatorio)
- `anno` (intero, obbligatorio)
- `visto` (booleano, default `false`)

Pagina iniziale con i link alle seguenti pagine:

- Pagina che permette di aggiungere un film.
- Pagina che permette una ricerca (per titolo o per regista, con i radiobutton per scegliere)
- Pagina per vedere i film visti
- Pagina per vedere i film ancora 'da vedere'

Funzionalità aggiuntiva: nella pagina dei film da vedere accanto ad ogni film abbiamo un link (o un pulsante, o... quello che volete) per modificare il dato,
facendo diventare il film da 'da vedere' a 'visto' (campo 'visto' da `False` a `True`)

--

**Esercizio 2: Bacheca annunci**

Pubblica e gestisci annunci.

Ogni annuncio ha:

- `titolo` (stringa, obbligatorio)
- `testo` (stringa, obbligatorio)
- `autore` (stringa, obbligatorio)
- `data` (stringa ISO, generata automaticamente con `datetime.date.today().isoformat()`)

Pagina iniziale con i link alle seguenti pagine:

- Pagina che permette di aggiungere un annuncio
- Pagina che permette una ricerca per titolo o per autore
- Pagina che permette di vedere tutti gli annunci presenti in bacheca
- Pagina che permette di selezionare ed eliminare un annuncio
 

--

**Esercizio 3: Classifica torneo**

Gestisci la classifica di un torneo.

Ogni squadra ha:

- `nome` (stringa, obbligatorio)
- `punteggio` (intero, default `0`)
- `partite` (intero, default `0`)

All'inizio sono presenti le seguenti squadre: polli, aquile, somari, cavallette. All'inizio punteggio e partite sono tutte 0.

La pagina iniziale visualizza la classifica aggiornata e presenta i seguenti link:

- Aggiungi partita: due tendine per selezionare le squadre e due caselle di testo per il punteggio della partita. Alla fine, 2 punti alla squadra vincente, 0 a quella che perde. 1 ad entrambe per il pareggio.


Funzionalità aggiuntive suggerite:

- La classifica è sempre mostrata ordinata per punteggio decrescente

--

**Esercizio 4: Registro recensioni**

Tieni traccia di locali visitati.

Ogni recensione ha:

- `nome` (stringa, obbligatorio)
- `tipo` (stringa tra`"ristorante"`, `"bar"`, `"pizzeria"`)
- `voto` (intero da 1 a 10, obbligatorio)
- `commento` (stringa, opzionale)

Pagina iniziale che elenca tutti i risultati inseriti, con i link alle seguenti pagine:

- Pagina che permette di filtrare per tipo (URL /tipo/<tipo>)
- Pagina che permette di aggiungere una recensione.
- Pagina che permette di visualizzare solo la recensione con il voto più alto
- Pagina che permette di visualizzare solo la recensione con il voto più basso

Funzionalità aggiuntive suggerite:

- Mostra la media dei voti in cima alla pagina

<br>
<br>
<br>
