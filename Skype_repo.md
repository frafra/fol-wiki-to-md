\_\_TOC\_\_

Introduzione
------------

[Skype](http://www.skype.com/intl/it) è un software proprietario di messaggistica istantanea e VoIP. Una soluzione alternativa a skype può essere, ad esempio, l'applicazione non proprietaria ed open-source [Ekiga](Ekiga "wikilink").

Risoluzione dipendenze
----------------------

Skype, essendo, come già detto, software proprietario, mette a disposizione un RPM già compilato per Fedora, ma questo pacchetto necessita di librerie a 32bit per funzionare; gli utenti che usano versioni di fedora con architetture differenti sono costretti ad installare tutte le dipendenze a 32bit. Per installare le dipendenze:

`# yum install libXScrnSaver.i?86 libX11.i?86 libXv.i?86 libv4l.i?86 alsa-plugins-pulseaudio.i?86 qt-x11.i?86`

Installazione tramite pacchetto RPM
-----------------------------------

Innanzitutto bisogna provvedere a scaricare l'ultima versione di skype disponibile per fedora. È sufficiente andare sul sito ufficiale sotto la voce [download](http://www.skype.com/it/download-skype/skype-for-computer/) o più semplicemente reperirlo direttamente da [qui](http://www.skype.com/go/getskype-linux-beta-fc10).

Da terminale raggiungere la cartella dove è stato scaricato il pacchetto (probabilmente `$HOME/Scaricati`) e installarlo:

`$ cd /percorso/fino/a/skype`
`$ su`
`# yum install ./skype-*`

Installazione alternativa tramite lpf
-------------------------------------

Skype può essere installato anche tramite [lpf](https://github.com/leamas/lpf), che sta per *Local Package Factory*, disponibile nei repository [RPMFusion](RPMFusion "wikilink"). Questo programma, semplice e user-friendly per l'interfaccia grafica di cui è fornito, consente di creare un pacchetto aggiornato all'ultima versione disponibile di skype.

Per installarlo da terminale è sufficiente eseguire:

`# yum install lpf-skype`

Per iniziare la costruzione e la creazione del pacchetto skype si può lanciare il programma dal menù dell'utente, oppure da terminale con:

`# lpf update skype`

L'esecuzione di lpf creerà un pacchetto rpm locale e provvederà alla sua installazione.

<Categoria:Repository> <Categoria:Yum>
