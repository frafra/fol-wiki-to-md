\_\_TOC\_\_

Introduzione
------------

Il plugin Flash è diventato essenziale per la corretta visualizzazione di molti siti web. Flash è una soluzione proprietaria, e benché ci siano molte alternative ad esso, come gnash, rimane il più utilizzato.

Installazione tramite Repository
--------------------------------

Una volta configurato il repository di Adobe si procede come segue:

`# dnf install flash-plugin`

Installazione alternativa tramite lpf
-------------------------------------

Il plugin Flash può essere installato anche tramite [lpf](https://github.com/leamas/lpf), che sta per *Local Package Factory*, disponibile nei repository [RPMFusion](RPMFusion "wikilink"). Questo programma, semplice e user-friendly per l'interfaccia grafica di cui è fornito, consente di creare un pacchetto aggiornato all'ultima versione disponibile del plugin flash.

Per installarlo da terminale è sufficiente eseguire:

`# dnf install lpf-flash-plugin`

Per iniziare la costruzione e la creazione del pacchetto flash si può lanciare il programma dal menù dell'utente, oppure da terminale con:

`$ lpf update flash-plugin`

L'esecuzione di lpf creerà un pacchetto rpm locale e provvederà alla sua installazione.

Verifica Flash Plugin
---------------------

Per verificare la presenza o meno del plugin Flash, basta digitare nella barra degli indirizzi del proprio browser:

[`about:plugins`](about:plugins)

Se presente, verrà visualizzata un riga contenente la dicitura *Shockwave Flash*.

<Categoria:Internet>
