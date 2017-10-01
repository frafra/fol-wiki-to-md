Volevo segnalare questo utilissimo plasmoid per chi come me utilizza KDE 4.

Maggiori informazioni su questo plasmoid si trovano qui:
[<http://www.kde-look.org/content/show.php/Daisy?content=102077>](http://www.kde-look.org/content/show.php/Daisy?content=102077)

Prima di installarla su Fedora bisogna preparare il sistema e praticamente occorre installare quanto segue:
Con i privilegi di root:

`# yum install kdebase-workspace-python-applet`
`# yum install kdebase-devel`
`# yum install kdebase-workspace-devel`

quindi procere con il download dell'ultima versione che è compatibile anche con KDE 4.3, l'ultima attualmente valida e': [<http://daisyplasma.freehostia.com/dow>](http://daisyplasma.freehostia.com/dow) ... let-daisy-0.0.4.19.tar.gz

Decomprimere il file appena scaricato spostarsi all'interno della directory, con quanto segue:

`$ mkdir build`
`$ cd build`
`` $ cmake ../ -DCMAKE_INSTALL_PREFIX=`kde4-config --prefix` ``
`$ make`
`$ su`
`password`
`# make install`
`# kbuildsycoca4`

Quindi si può tranquillamente aggiungerlo come un normale plasmoid: tasto destro sul desktop e scegliere "aggiungi oggetto". Nella finestra di ricerca rapida scrivere "daisy" e quindi selezioniarla.

**Edit by Staff di FOL:**
Qualche nota a margine:

1.  Il link per il tar.gz segnalato dall'autore ci riporta alla home freehostia, vogliate procedere al download selezionando il suddetto tar.gz da [questa pagina.](http://daisyplasma.freehostia.com/pages/download.php)
2.  E' necessario avere installato gli strumenti di sviluppo:
        # yum groupinstall 'Strumenti di sviluppo'

3.  In alternativa al comando
        # kbuildsycoca4

    è possibile terminare la sessione e riautenticarsi.

[Categoria:Ambiente Desktop](Categoria:Ambiente_Desktop "wikilink")
