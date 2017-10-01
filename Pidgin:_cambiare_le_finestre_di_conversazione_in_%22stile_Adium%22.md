Introduzione
------------

Non so voi, ma per quanto apprezzi tantissimo la potenza e versatilità di Pidgin, lo stile grafico ultra-minimalista non mi è mai piaciuto un granchè. Non sarebbe meglio invece avere almeno nelle finestre di conversazione uno stile simile a quello di Adium (il software IM installato su tutti i Mac)?
Condivido qui quel poco che ho trovato, con il mio personale adattamento per i sistemi Fedora.

Installazione
-------------

Per poter usufruire dei temi di Adium, è necessaria la compilazione di un plugin chiamato *Pidgin-webkit*, ma è più semplice di quanto si immagini.
Prima di tutto bisogna installare i pacchetti necessari per compilare il tutto, da root digitare:

`# yum -y install wget bzr webkitgtk webkitgtk-devel pidgin-devel`

Fatto questo, uscire dall'utente root e clonare il codice da compilare digitando questo comando:

`$ bzr branch lp:pidgin-webkit`

e selezionare la cartella con i sorgenti:

`$ cd pidgin-webkit`

Per il corretto funzionamento del plugin si avrà bisogno di una patch, che si scarica con il comando:

`$ wget `[`http://launchpadlibrarian.net/23856598/pidgin-webkit-tempfile-2.patch`](http://launchpadlibrarian.net/23856598/pidgin-webkit-tempfile-2.patch)

e si applica con:

`$ patch -i pidgin-webkit-tempfile-2.patch`

Dopodichè, gli ultima passi da compiere sono la compilazione:

`$ make`

...e l'installazione:

`$ make install`

Ora si può trovare il plugin nell'elenco apposito di pidgin, non si dovrà fare altro che abilitarlo e provare la moltitudine di temi che si possono trovare [qui](http://www.adiumxtras.com/index.php?a=search&cat_id=5). Alcuni temi bloccano pidgin, ma quelli "classici" (come Renkoo) funzionano alla perfezione.

<Categoria:Internet>
