Introduzione
------------

A differenza di KDE che offre di per se molti widgets, su Gnome ci si avvale dei desklet, il più delle volte dei gdesklets. Ma ci sono anche altre possibilità, tra cui una è la famosa cairo-dock, una barra che assomiglia (poi dipende come la si configura) a quella MacOS e dalla quale è possibile gestire tutte le funzionalità (o quasi) dei pannelli di Gnome.

Installazione
-------------

Per installare Cairo-dock ci si avvale di Yum:

`# yum install cairo-dock cairo-dock-devel cairo-dock-plug-ins cairo-dock-core`

Configurazione
--------------

In *Applicazioni -&gt; Strumenti di Sistema* a questo punto saranno presenti due voci, una che richiama cairo-dock con e una senza l'uso di OpenGL. Selezionando quella con OpenGL si apre una barra in basso, che rimane completamente configurabile.
Alcune delle possibili configurazioni riguardano:

-   Lancia cairo-dock all'avvio di Fedora
-   Tema;
-   Icone da utilizzare;
-   Dimensione icone;
-   Visualizzazione barra.

Aggiunta di nuovi lanciatori
----------------------------

Per aggiungere dei lanciatori esiste una funzione molto semplice:

1.  Avviare l'applicazione che si vuole aggiungere;
2.  Si apre un'icona sulla barra delle applicazioni in uso;
3.  Click sull'icona con il tasto destro;
4.  Seleziona "aggiungi come lanciatore";
5.  Fatto.

Una volta configurato tutto si possono anche eliminare i pannelli di Gnome. Successivamente il desktop si presenta così: <img src="Cairo.jpg" title="fig:Alla fantasia non viene posto nessun limite. Questo è un esempio di come Cairo potrebbe apparire." alt="Alla fantasia non viene posto nessun limite. Questo è un esempio di come Cairo potrebbe apparire." width="500" />

Risoluzione Problemi
--------------------

Utilizzando DE come xfce o lxde può capitare che ci si ritrovi un bordo nero attorno a cairo dock, in quanto il [compositing window manager](http://it.wikipedia.org/wiki/Compositing_window_manager) non è attivo.
Una soluzione potrebbe essere quella di utilizzarne uno per fornire così l'accelerazione 2D necessaria, come può essere **xcompmgr**, semplice e leggero.
Per configurarlo si può seguire [questa](http://forum.fedoraonline.it/viewtopic.php?id=19395) discussione sul forum di fedoraonline.

[Categoria:Ambiente Desktop](Categoria:Ambiente_Desktop "wikilink")
