Avviare linux in meno di 20 secondi usando *initng*.
Questo progetto è molto interessante e sembra verrà integrato nella prossima versione di Fedora, Fedora Core 5.

<http://initng.thinktux.net/index.php/Main_Page>

Per installare INITNG scaricare il pacchetto da qua:

<http://initng.thinktux.net/download/v0.5/initng-0.5.0.tar.gz>

Poi procedere scompattandolo e installandolo digitando:

`# tar -xvf initng-0.5.0.tar.gz`
`# cd initng-0.5.0`
`# ./configure`
`# make`

Ora si può installare dando o *make install* oppure creando un rpm usando [checkinstall](http://asic-linux.com.mx/~izto/checkinstall/).
Una volta installato il pacchetto andare nella cartella /etc/initng:

`cd /etc/initng`
`# more default.runlevel`
`system`
`daemon/sshd`
`daemon/acpid`
`daemon/dbus`
`net/AliceADSL`
`daemon/syslogd`
`system/alsasound`
`system/usb`
`daemon/syslogd`
`daemon/xfs`
`daemon/hald`
`daemon/gdm`

La voce daemon/syslogd è sbagliata, nel file originale c'è daemon/syslog, mentre su fedora si chiama daemon/syslogd con la d finale!
net/AliceADSL è il nome della interfaccia per l'ADSL, va sotituita con quella in uso!

`# more system.runlevel`
`system/initial`
`system/mountroot`
`system/mountfs`
`system/bootmisc`
`system/clock`
`system/hostname`
`system/modules`
`system/static-modules`
`system/hdparm`
`system/keymaps`
`system/urandom`
`system/consolefont`
`system/swap`
`system/iptables`
`system/firestarter`
`net/lo`
`daemon/agetty`

In questo file è stato aggiunto solo iptables e firestarter!

Ora per modificare il boot loader per Grub, si consiglia di aggiungere un altro title Fedora Core (2.6.14.....) INITNG ecc. copiando il proprio kernel di default e aggiungendo i comandi necessari per poter far partire il proprio Kernel originale in caso di problemi.
Il title aggiunto dovrebbe avere un aspetto molto simile a questo (in questo caso si ha un VolGroup):

`title Fedora Core (2.6.14-1.1653_FC4) INITNG`
`        root (hd0,0)`
`        kernel /vmlinuz-2.6.14-1.1653_FC4 ro root=/dev/VolGroup00/LogVol00 init=/sbin/initng vga=791 rhgb quiet`
`        initrd /initrd-2.6.14-1.1653_FC4.img`

L'installazione è andata a buon fine, funziona tutto egregiamente, inoltre il sistema si avvia in meno di 20 secondi a confronto dei 120 ed oltre di prima....si fermava per quasi un minuto solo per avviare l'ADSL, ora va liscio e veloce !!!!

Riferimenti
-----------

[<http://www.lucaporcu.com/modules/news/article.php?storyid=61>](http://www.lucaporcu.com/modules/news/article.php?storyid=61)

<Categoria:Sistema> [Categoria:Fedora Legacy](Categoria:Fedora_Legacy "wikilink")
