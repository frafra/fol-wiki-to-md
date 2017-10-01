Una piccola guida base per cominciare con Wine, un non emulatore che permette di installare ed eseguire programmi Win su Fedora.

Molti utenti che si affacciano a Linux provenendo dal mondo Winzoz e sentono la necessità di portarsi dietro molti programmi Windows senza magari osservare che Linux stesso offre tantissimi applicativi analoghi a quelli Windows ma FREE.
Come fare per far girare applicazioni Windows sotto Linux? Esistono vari sistemi; Wine è un sistema che permette di fare questo mettendo un buon compromesso tra facilità d'uso e economicità monetaria (è gratuito).

E' possibile reperire il pacchetto RPM per FC3 direttamente dal sito [www.winehq.com](http://www.winehq.com) oppure tramite Yum.

Wine non è un banale emulatore software, esso è composto da due grossi blocchi: una serie di DLL "riscritte" per Linux che compongono alcune parti del Core di Windows e da un programma che permette il loro interfacciamento sul sistema Linux.

Installazione
-------------

L'installazione è semplice e si effettua come Root. Dopodiché si può utilizzarlo (anzi è caldamente consigliato) come utente.
Wine creerà una cartella nascosta nella propria home chiamata .Wine al suo interno si troveranno due cartelle fondamentali:

dosdevice e fake\_windows

La prima contiene dei link logici ai dispositivi di massa (hdb, floppy, etc) e alla posizione /home/user/.wine/fake\_windows. Questi link logici portano il nome dei classici drive di Windows (a:, c:, d: etc).
Dentro Fake\_windows si troveranno la struttura di base delle cartelle di un sistema operativo Windows (Program files, Windows, Windows/System32 etcc).

Uso
---

Con .wine si può a questo punto installare i programmi Windows come se si usasse Windows stesso ovvero da shell basta digitare

`wine setup.exe `

per lanciare ad esempio il setup di una propria applicazione Windows.
Tale applicazione verrà eseguita in un ambiente virtuale ed installata nelle cartelle del proprio Fake\_windows.

In linea teorica è possibile installare ed eseguire tutto; in quanto molti programmi richiedono di configurare l'ambiente Wine in modo particolare.

Senza addentrarsi in particolari un po' complicati, si può utilizzare un tool molto potente che aiuta a *sistemare* Wine per poter far girare la maggior parte degli applicativi.
Questo programma si chiama Wine-tools e si può scaricare dalla sezione download di [www.winehq.com](http://www.winehq.com)

Questo script permette di impostare correttamente un ambiente Wine installando i componenti di base di Windows che sono necessari dalla maggior parte delle applicazioni Windows.
Questi componenti (DCOM98, IE, WindowMediaPlayer, Jet4.0, MFC library, etc..) sono componenti che non sono forniti di default insieme a Wine e necessitano di essere installati separatamente. Wine-tools effettua queste operazioni.
Una volta installato Wine-tools (lanciando il programma insall.sh) è possibile lanciarlo col comando da shell

`wine-tools`

Si aprirà una finestra a menu molto chiara che permetterà di installare i componenti suddetti. I componenti fondamentali da installare sono i seguenti:

`Windows Installer service`
`DCOM98`
`MFC Library`
`VB6 Runtime`
`IE 6 / Outlook Express`
`Windows Media Player`

Una volta installati questi componenti il proprio sistema Windows virtuale sarà compatibile con il 60-70% delle applicazioni Windows in circolazione e per installarle basta come detto prima lanciare il setup.exe dell'applicazione stessa.
Wine-tools permette anche già di installare diversi applicativi configurando just-in time il sistema Wine per quell'applicazione.

Per poter installare Wine-tools è necessario avere sul proprio sistema il pacchetto qtdialog (reperibile comunque dal repository o da [www.rpmfind.net](http://www.rpmfind.net)).

Wine è un mondo vasto e occorrerebbe stilare guide specifiche per ogni singolo aspetto ma si spera che questa guida sia utile per chi si avvicina per la prima volta a questo programma.
Wine possiede tante potenzialità che magari verranno sviscerate in altre guide più specifiche che verranno create in futuro(ad esempio si scoprirà anche che Wine può "allacciarsi" direttamente ad un sistema Windows vero installato in una partizione - purché sia FAT - e utilizzare direttamente tutti i programmi e i componenti installati sulla vera macchina Windows).

<Categoria:Virtualizzazione>
