\_\_TOC\_\_

Introduzione
------------

LibreOffice, dalla release di Fedora 15, è incluso nei [repository](:Categoria:Repository "wikilink"), come specificato nella [documentazione](http://fedoraproject.org/wiki/Features/LibreOffice/it) del fedoraproject.
Questa guida prevede l'installazione da sorgenti su rilasci di fedora precedenti alla 15 o in caso di particolari bisogni.

Recupero dei pacchetti necessari
--------------------------------

Si possono scaricare i pacchetti dal [sito ufficiale](http://it.libreoffice.org/download/) anche con il proprio browser.
Per effettuare un download avendo la certezza di scaricare un file non corrotto utilizzare il download via torrent.

-   archivio del programma, che avrà un nome simile a questo **LibreOffice\_VERSIONE\_Linux\_ARCHITETTURA\_rpm.tar.gz**;
-   language pack italiano, con un nome simile a questo **LibreOffice\_VERSIONE\_Linux\_ARCHITETTURA\_rpm\_langpack\_it.tar.gz**.

Per versioni precedenti la 4.0.0 i pacchetti hanno invece questa sintassi: *LibO\_VERSIONE\_Linux\_ARCHITETTURA\_install-rpm\_en-US.tar.gz* e *LibO\_VERSIONE\_Linux\_ARCHITETTURA\_langpack-rpm\_it.tar.gz*.
Per scaricare i vari pacchetti si crea una directory di comodo nella quale salvare i file:

`$ mkdir ~/Libreoffice`

si entra nella directory appena creata:

`$ cd ~/Libreoffice`

ora si passa a scaricare i file necessari; i comandi utilizzabili sono wget o, in mancanza, curl, così:

`$ wget http://download.documentfoundation.org/libreoffice/stable/VERSIONE/rpm/ARCHITETTURA/LibreOffice_VERSIONE_Linux_ARCHITETTURA_rpm.tar.gz http://download.documentfoundation.org/libreoffice/stable/VERSIONE/rpm/ARCHITETTURA/LibreOffice_VERSIONE_Linux_ARCHITETTURA_rpm_langpack_it.tar.gz`

Installazione di LibreOffice
----------------------------

Una volta scaricati i pacchetti si estraggono i file con il seguente comando (utilizzare il tasto tab per il completamento automatico):

`$ tar -xzvf LibreOffice_VERSIONE_Linux_ARCHITETTURA_rpm.tar.gz`

Per l'installazione vera e propria degli rpm bisogna acquisire i diritti di root:

`$ su`

quindi inserire la password di root del sistema; ora tramite yum si procede all'installazione di tutti gli rpm:

`# yum install --nogpgcheck LibreOffice_VERSIONE_Linux_ARCHITETTURA_rpm/RPMS/*.rpm`

A conclusione dell'operazione si avrà LibreOffice installato su Fedora; per avviare le singole suite, basterà lanciare da terminale da utente:

`$ /opt/libreoffice4.0/program/swriter`
`$ /opt/libreoffice4.0/program/sdraw`
`$ /opt/libreoffice4.0/program/sbase`
`$ /opt/libreoffice4.0/program/simpress`
`$ /opt/libreoffice4.0/program/scalc`
`$ /opt/libreoffice4.0/program/smath`

Integrazione con il menù di sistema
-----------------------------------

Libreoffice si può integrare nel menù di sistema, ossia avere la possibilità di poterlo lanciare graficamente dai menù dei vari DE. Se si sono seguite le istruzioni precedenti riguardo all'installazione degli eseguibili veri e propri, da terminale dare:

`$ cd ~/Libreoffice`
`$ su`
`# yum install --nogpgcheck LibreOffice_VERSIONE_Linux_ARCHITETTURA_rpm/RPMS/desktop-integration/libreoffice4.0-freedesktop-menus-_VERSIONE_.noarch.rpm`

Installazione lingua italiana
-----------------------------

Per installare la lingua italiana estrarre dall'archivio scaricato all'inizio il Language Pack. Posizionarsi nella cartella RPMS e ridare lo stesso comando di prima.
Seguire queste istruzioni:

`$ wget http://download.documentfoundation.org/libreoffice/stable/VERSIONE/rpm/ARCHITETTURA/LibreOffice_VERSIONE_Linux_ARCHITETTURA_rpm_langpack_it.tar.gz`
`$ tar -xzvf LibreOffice_VERSIONE_Linux_ARCHITETTURA_rpm_langpack_it.tar.gz`
`$ cd LibreOffice_VERSIONE_Linux_ARCHITETTURA_rpm_langpack_it/RPMS/`
`$ su`
`# yum install --nogpgcheck *.rpm`

Fatto questo sarà attiva anche la lingua italiana nei vari programmi.

Risoluzione di problemi vari
----------------------------

-   In caso il bordo delle finestre abbia un gusto "retrò" da Windows95, come riportato da qualche utente sul [forum del fedoraproject.org](http://forums.fedoraforum.org/showpost.php?p=1634609&postcount=5) può essere necessario installare:

`# yum install pangox-compat`

-   Come detto dalla documentazione stessa di LibreOffice, può essere necessario installare java per far funzionare alcuni componenti:

*Per alcune caratteristiche del software - ma non tutte - è richiesto Java. Java è necessario per Base.*

Riferimenti
-----------

-   [Home della Document Foundation](http://www.documentfoundation.org/), di cui LibreOffice fa parte.
-   [Pagina di download di LibreOffice.](http://it.libreoffice.org/download/)
-   [Documentazione ufficiale.](http://www.libreoffice.org/get-help/installation/linux/)

<Categoria:Ufficio>
