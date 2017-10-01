Introduzione
------------

Chromium è un browser open source multipiattaforma mantenuto dal team di sviluppo [The Chromium Project](https://www.chromium.org/).
Dal codice sorgente di Chromium viene sviluppato "[Google Chrome](https://www.google.it/intl/it/chrome/browser/desktop/)", che aggiunge porzioni di software non libero quali Flash Player, video H.264 e audio ACC - MP3. Chromium supporta invece nativamente i codec Vorbis, Theora and WebM per audio e video in HTML5, tuttavia Flash Player può essere installato in Chromium in un secondo momento.
Dal mese di agosto 2016 Chromium è incluso nei repository Fedora e, per chi non lo avesse ancora fatto, è possibile installare Chromium tramite dnf. Per coloro che invece lo hanno installato in precedenza dal repo COPR è consigliato disinstallare Chromium, togliere il repo COPR (ormai vetusto) dal proprio sistema e reinstallare Chromium seguendo le indicazioni di questa guida.

Installazione
-------------

L'installazione in Fedora 24 e 25 è molto semplice:

`# dnf install chromium`

Configurazione plugin
---------------------

Per utilizzare il plugin *Adobe Flash Player* su Chromium è possibile seguire questa procedura:

-   Aprire la pagina di download [Adobe Flash Player](https://get.adobe.com/flashplayer/otherversions/)
    -   Selezionare il tipo di Sistema operativo installato: **Linux (64 bit)** oppure **Linux (32-bit)**
    -   Selezionare e scaricare la versione plugin FP 25.0 (o successive) for Linux xx-bit (tar.gz) **PPAPI**

<!-- -->

-   Scompattare il file flash\_player\_ppapi\_linux.xx\_xx.tar.gz nella cartella /usr/lib64/chromium-browser/PepperFlash/
-   Riavviare Chromium e verificare l'installazione dalla barra degli indirizzi digitando: <chrome://plugins>

Riferimenti
-----------

-   Homepage del progetto [Chromium](https://www.chromium.org/)
-   Pagina wiki del Fedora Project [Chromium](https://fedoraproject.org/wiki/Chromium)

<Categoria:Internet>
