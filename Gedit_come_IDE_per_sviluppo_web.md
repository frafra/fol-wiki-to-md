\_\_TOC\_\_

Introduzione
------------

Gedit è l'editor di testo di default di Gnome e spesso viene declassato a un editor di testo qualsiasi. Gedit però, se viene configurato correttamente in base alle proprie esigenze, è molto più potente di quello che si pensa. Soprattutto per chi sviluppa pagine web, che perciò utilizza HTML/XHTML, CSS, Javascript, PHP, MySQL, Ruby, etc, Gedit può rappresentare una valida alternativa a molti altri blasonati editor di testo; rimane però un ottimo strumento anche per altri campi della programmazione oltre a quello web.
In questa guida si vuole fare un esempio di come è possibile personalizzare Gedit come IDE per lo sviluppo di pagine web.

Funzionalità
------------

Una delle caratteristiche più apprezzate di Gedit è la sua stabilità, cosa non da poco se parliamo di un lavoro così dispendioso in termini di tempo come la scrittura di codice. L'evidenziazione dei tag dei singoli linguaggi, l'indicazione delle righe e il margine destro completano un layout gradevole e utile per lo sviluppatore.
Altre funzionalità sono:

-   Evidenziazione delle coppie di parentesi;
-   Librerie Snippet;
-   Miglioramento di codice HTML e PHP;
-   Personalizzazione tramite tools esterni;
-   Finestra laterale con supporto FTP e SSH, nonchè supporto HTML, XHTML, CSS e PHP;
-   Facile gestione di colori con il color-picker.

In realtà ce ne sono molte altre ed elencarle tutte sarebbe impossibile, la lista completa dei cambiamenti si trova nella [pagina git](https://git.gnome.org/browse/gedit/tree/NEWS) del progetto.
Un esempio di come potrebbe presentarsi Gedit dopo alcune personalizzazioni è il seguente. <img src="Gedit.png" title="fig:Gedit potrebbe presentarsi anche così." alt="Gedit potrebbe presentarsi anche così." width="350" />

Preferenze
----------

<img src="gedit_vista.png" title="fig:Le preferenze di Gedit." alt="Le preferenze di Gedit." width="250" /> Per dare un po' di verve all'editor e renderlo più funzionale rispetto alle impostazioni di default, si può andare in **Modifica -&gt; Preferenze** e modificare le impostazioni.
Una buona impostazione potrebbe essere:

-   **Vista**
    -   Mostrare i numeri di riga
    -   Mostrare il margine destro alla colonna 80 (che è un valore di default ma va bene)
    -   Attivare a capo automatico
    -   Dividere le parole su due righe (togliere la spunta)
    -   Evidenziare la riga corrente
    -   Evidenziare le parentesi corrispondenti

<!-- -->

-   **Editor**
    -   Ampiezza tabulazione: 4 (ampiezza in caratteri vuoti dello spazio alla pressione del tasto *tab*)
    -   Inserire gli spazi invece delle tabulazioni
    -   Attivare rientro automatico
    -   Non salvare alcuna copia di backup

<!-- -->

-   **Caratteri**
    -   Monospace 10
    -   Schema colore a piacimento (Cobalt è quello della schermata sopra)

<!-- -->

-   **Plugin**: da qui si attivano o disattivano i plugin installati.

Plugins
-------

Quasi tutte le funzioni elencate all'inizio non sono disponibili nell'installazione standard di Gedit, ma si possono attivare facilmente con alcuni plugin, selezionabili e personalizzabili poi dal gestore interno di Gedit.
I seguenti plugin sono utili per la gran parte dell'utenza, ma all'occorrenza se ne possono trovare altri. I più utili si trovano sulla [pagina ufficiale dei plugins](http://live.gnome.org/Gedit/Plugins) del progetto. Tutti i seguenti plugin hanno solitamente più di una funzione, attivabile attraverso la gestione dei plugin che si trova nelle *Preferenze*, come descritto sopra.

### Gedit-plugins

La raccolta base di plugin che non deve mancare. Si installa digitando:

`# yum install gedit-plugins`

Comprende già una buona base degli strumenti utili, andare in *Modifica -&gt; Preferenze -&gt; Plugins* per attivare quelli necessari alle proprie esigenze.

### LaTeX plugin

Un altroplugin che non deve mancare se si lavora con LaTeX è il plugin per Gedit, con il quale è possibile anche esportare direttamente il pdf.

`# yum install gedit-latex`

### Evidenziazione dei tag

Essenziale per la scrittura di qualsiasi codice se non ci si vuole perdere dopo 5 righe.

`# yum install gtksourceview`

### Syntax Highlighting

L'evidenziazione dei tag ha dei colori standard, che si possono però personalizzare ulteriormente. Un pacchetto che da al codice PHP il colore caratteristico, è [questo](http://www.micahcarrick.com/files/gedit_php_highlight.xml). Si può applicare facilmente digitando:

`$ curl -O `[`http://www.micahcarrick.com/files/gedit_php_highlight.xml`](http://www.micahcarrick.com/files/gedit_php_highlight.xml)
`$ gconftool-2 --load=./gedit_php_highlight.xml /apps/gedit-2/preferences/syntax_highlighting/PHP`

### Autocompletamento

Plugin utile per non dover scrivere sempre tutta la parola o stringa, Gedit proporrà le parole digitate nel documento fino a quel momento.

`# yum install gtksourcecompletion`

### Lista Tag

La lista dei Tag appare nel pannello laterale e suggerisce, per ogni linguaggio inserito, i tag. Cliccando su uno di essi, questo viene inserito nel documento. Il pacchetto che viene suggerito contiene i tag di:

-   PHP
-   CSS
-   XHTML

Per utilizzarlo basta [scaricare il pacchetto](http://www.micahcarrick.com/files/gedit_webdev_tags-0.1.tar.gz), scompattarlo nella directory desiderata, e copiare le estensioni nella cartella nascosta taglist nella propria home.
Il tutto da terminale si può ridurre così:

`$ curl -O `[`http://www.micahcarrick.com/files/gedit_webdev_tags-0.1.tar.gz`](http://www.micahcarrick.com/files/gedit_webdev_tags-0.1.tar.gz)
`$ tar -xzf gedit_webdev_tags-0.1.tar.gz`
`$ mkdir -p ~/.local/share/gedit/plugins/taglist/`
`$ cp gedit_webdev_tags-0.1/*.tags ~/.local/share/gedit/plugins/taglist/`

### Tools esterni

Un'altra raccolta di tools utili sono i **Tools esterni**, che, una volta attivati dalle *Preferenze*, propongono molte altre funzioni utili, come il Php beautifier oppure la possibilità di rimuovere gli spazi a fine riga. Scaricare il [pacchetto dei tools esterni](http://www.micahcarrick.com/files/gedit_external_tools.tar.gz) e, dopo averlo scompattato, copiarlo nella directory locale dell'utente. Se non fosse presente la directory indicata, procedere prima con la creazione manuale della stessa.

`$ curl -O `[`http://www.micahcarrick.com/files/gedit_external_tools.tar.gz`](http://www.micahcarrick.com/files/gedit_external_tools.tar.gz)
`$ tar -xzf gedit_external_tools.tar.gz`
`$ mkdir -p ~/.gnome2/gedit/`
`$ cp gedit_external_tools/ ~/.gnome2/gedit/`

Ai tools esterni si accede tramite il menu *Strumenti -&gt; External tools*.

Riferimenti
-----------

-   [Home](http://projects.gnome.org/gedit/) del progetto Gedit;
-   [Blog di Micah Carrick](http://www.micahcarrick.com/gedit-html-editor.html), in particolare la sezione dedicata a Gedit;
-   [Gedit](http://it.wikipedia.org/wiki/Gedit) su Wikipedia.

[Categoria:Ambiente Desktop](Categoria:Ambiente_Desktop "wikilink") [Categoria:Programmazione e Sviluppo](Categoria:Programmazione_e_Sviluppo "wikilink")
