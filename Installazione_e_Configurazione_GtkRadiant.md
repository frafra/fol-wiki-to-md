Introduzione
------------

Per chi ancora non lo conoscesse, **GtkRadiant 1.6** (conosciuto anche come ZeroRadiant) è un applicativo utile per coloro che desiderano creare una propria mappa all'interno di un gioco **FirstPersonShooter** (traducibile in italiano con "Sparatutto"). In particolare, nel corso di questa guida, imposteremo l'applicazione per creare mappe su UrbanTerror, ma è realizzato per funzionare anche con Wolfenstein Enemy Territory, Tremulous, UFO:Alien Invasion, Doom3, Warsow, ovviamente tutta la serie Quake, compreso Quake III Arena e qualche altra dozzina di videogiochi; per una lista completa dei programmi supportati controllate nel link a Wikipedia in fondo alla pagina.
Dopo questa introduzione passiamo alla fase pratica.

Installazione Dipendenze
------------------------

Installiamo le dipendenze per la nostra Fedora:

`# yum install libxml2-devel glib-devel zip libjpeg-devel gtk+-devel gtk2-devel gtkglext-devel scons subversion git libjpeg-turbo-devel`

Installazione GtkRadiant
------------------------

Posizioniamoci nella directory home del vostro utente:

`$ cd`

### Scarichiamo i Sorgenti

Per scaricare i sorgenti useremo un utile strumento chiamato git, installato precedentemente. Quindi scarichiamo gli ultimi pacchetti disponibili dal server di sviluppo di GtkRadiant:

`$ git clone `[`https://github.com/TTimo/GtkRadiant`](https://github.com/TTimo/GtkRadiant)` ./GtkRadiant-src`

### Download Mappe Base e Compilazione dei Sorgenti

Spostiamoci nella directory creata:

`$ cd ~/GtkRadiant-src`

Ora scaricheremo dei dati extra per la creazione di mappe per vari videogame (tra cui il nostro UrbanTerror):

`$ scons target=setup`

Ed ora possiamo procedere alla compilazione vera e propria:

`$ scons target=radiant,q3map2 config=release`

Dopo che avrà macinato un bel po' la compilazione sarà finita, qualora aveste problemi controllate attentamente di aver seguito i punti superiori.

### Pulizia dei Pacchetti inutili

Spostiamo la cartella **install**, che è l'unica parte che ci interesserà d'ora in avanti, nella home e la rinominiamo:

`$ mv ~/GtkRadiant-src/install/ ~/GtkRadiant`

Eliminiamo quindi i dati ormai inutili:

`$ cd && rm -rf GtkRadiant-src/`

Configurazione UrbanTerror
--------------------------

Qualora voleste provare le mappe direttamente sul vostro pc è consigliato non usare la directory di installazione normale ma crearvi una directory urbanterror solo per il map editor, al fine di evitare spiacevoli problemi come il non poter più giocare perché avete "mischiato" mappe vostre, eccetera...
Scaricate quindi il file **.zip** dalla pagina di download [qui](http://www.urbanterror.info/downloads/) (consiglio personalmente di scaricare dal server ftp con un gestore di download al fine di incrementare la velocità).
Scaricato il pacchetto nella vostra Home (in questa parte di guida ipotizziamo che il pacchetto si chiami UrbanTerror411.zip, se così non fosse rinominatelo con il nome corretto), date il seguente comando:

`$ unzip UrbanTerror411.zip`

Rendiamo eseguibili i pacchetti necessari:

`$ cd ~/UrbanTerror/`
`$ chmod +x ioUrbanTerror.* ioUrTded.*`

Configurazione GtkRadiant ottimizzata per UrbanTerror
-----------------------------------------------------

A questo punto finalmente lanciamo e configuriamo GtkRadiant:

`$ ~/GtkRadiant/radiant.bin`

<img src="GtkRadiant1.png" title="Prima schermata GtkRadiant" alt="Prima schermata GtkRadiant" width="150" />

Ci comparirà una finestra come questa a destra.
Nella casella *Game to configure* scegliamo **UrbanTerror (standalone)**, nella casella *Name* lasciamo anche lì **UrbanTerror (standalone)** e nella casella *Engine directory* inserite le coordinate della cartella UrbanTerror precedentemente creata, quindi **/home/*NOME\_UTENTE*/UrbanTerror** (inserendo il nome del vostro utente), infine premiamo su Ok.
![Seconda schermata GtkRadiant](GtkRadiant2.png "fig:Seconda schermata GtkRadiant")

Fatto anche questo ci comparirà una seconda finestra come questa.
Lasciate anche qui come è già impostato **UrbanTerror (standalone)** e scegliete poi a piacere vostro se volete che all'avvio del programma parta in automatico con il gioco impostato (primo box) e se volete che salvi la console in un file radiant.log (secondo box); fatte le vostre scelte premete ok.
A questo punto potete crearvi, a vostra discrezione, un collegamento al desktop del file radiant.bin per una maggiore usabilità.

Creazione Mappe
---------------

La creazione delle mappe esula dallo scopo di questa guida. Se vorrete creare mappe visitate il seguente [link](http://daffy.nerius.com/radiant/#first-map), fonte base per questa guida, [qui](http://radiant.robotrenegade.com/manual/) il manuale ufficiale di GtkRadiant e [qui](http://www.urbanterror.info/support/tutorials/leveldesign/) la sezione del manuale di UrbanTerror per la creazione di mappe.
Create le vostre mappe posizionatele dentro la Home nella cartella *UrbanTerror/q3ut4/*

Perché separare le Mappe dal Gioco
----------------------------------

Abbiamo scaricato e configurato UrbanTerror in un'altra directory per mantenere separato il gioco su server pubblici da quello per creare le mappe. Per provare la vostra mappa in formato pk3 inseritela nella vostra home nella cartella UrbanTerror/q3ut4/ e date questi comandi da terminale:

`$ ~/UrbanTerror/ioUrbanTerror.i386 +set sv_pure 0 +set g_gametype X +devmap NOME_VOSTRA_MAPPA`

Questa operazione lancerà UrbanTerror (se avete Fedora a 64bit sostituite **i386** con **x86\_64**), selezionate la modalità di gioco che volete guardando l'elenco sotto, e vi lancerà automaticamente la mappa che avete scelto.
Potete crearvi dei piccoli script con un qualunque editor di testi vogliate da inserire nella cartella UrbanTerror per testare le vostre mappe in diverse modalità di gioco. Un esempio può essere questo:

`#! /bin/bash`
`` ARC1=`uname -p` ``
`if [ $ARC1 = 'i686' ]; then`
`   ARC2=i386`
`else`
`   ARC2=$ARC1`
`fi`
`./ioUrbanTerror.$ARC2 +set sv_pure 0 +set g_gametype X +devmap $*`

Bisogna fare attenzione ad il tipo di gioco da inserire al posto della X, seguendo questo elenco:

-   Free For All (FFA) &gt; 0
-   Team DeatMatch (TDM) &gt; 3
-   Team Survivor (TS) &gt; 4
-   Follow the Leader &gt; 5
-   Capture and Hold &gt; 6
-   Capture The Flag (CTF) &gt; 7
-   Bombmode &gt; 8

Salvate gli script con un nome a vostra scelta, chiudete e da terminale posizionatevi nella cartella UrbanTerror e dategli i permessi di esecuzione:

`$ chmod +x NOME_SCRIPT`

Ora eseguitelo

`$ ./NOME_SCRIPT NOME_MAPPA`

Ad esempio:

`$ ./Urt_FFA ut4_algiers`

In questo modo darete avvio alla mappa **ut4\_algiers** in modalità FFA.

That's that, enjoy it! :D

Riferimenti
-----------

-   [HOME](http://icculus.org/gtkradiant/) del progetto;
-   [Guida](http://daffy.nerius.com/radiant/) di ispirazione per questo "port" su fedora;
-   [Pagina su Wikipedia](http://en.wikipedia.org/wiki/GtkRadiant#Supported_games) riguardo Gtkradiant, in particolare la lista dei giochi supportati.

<Categoria:Giochi> <Categoria:Sistema>
