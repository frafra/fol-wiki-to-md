Introduzione
------------

Lo scopo di questa guida è l'installazione di un semplice centralino telefonico PBX composto da 1 server Asterisk, 2 client SIP, 1 client IAX2 e una rete telefonica ISDN TelecomItalia.
Questa guida è stata scritta da Nico Timeo, sistemista presso la Società [Techpoint](http://www.techpoint.catania.it/) di Catania. Vedetela come "un'esperienza condivisa". Ovviamente, si può partire da questa configurazione base, testata e funzionante, per implementare una centrale telefonica più complessa e con funzionalità estese. Non è una guida che spiega cos'è Asterisk e come è strutturato: per questo ci sono altre risorse (v. più avanti).

Hardware e software utilizzato
------------------------------

Ecco il sistema che costituisce il nostro server, che funzionerà come un vero e proprio "centralino" PBX (un altro modo per interfacciarsi al nostro PBX virtuale potrebbe essere un PC che soddisfi i requisiti minimi per Fedora):

`SERVER:`
`Motherboard:    Asus P4PE-X`
`Processore:    Pentium 4, 2.60 MHz`
`RAM:        512 MB`
`Video:        ATI Radeon 7000/VE`
`Audio:        Intel 82801 AC97 `
`LAN:        Broadcom BCM4401 100Base-T`
`ISDN:        Eicon Diva Server V-4BRI`

ovviamente munito di tastiera, mouse, lettore CD/DVD, e di tutti gli altri accessori utili ad un normale pc. Le postazioni Client (SIP), invece, saranno dei normali telefoni Sirio della Telecom Italia collegati tramite il connettore RJ11 ad un adapter Grandstream HandyTone-286.
Il software che utilizzeremo per il VoIP è il client IAX2 idefisk, liberamente scaricabile (per Linux, Windows e Mac OSX) dal sito di [Asteriskguru](http://www.asteriskguru.org/idefisk/free/)

Predisposizione
---------------

Il primo passo è ovviamente l'installazione del sistema operativo sul server. Scelgo la distro Fedora Core 4 (la 5 mi ha dato qualche problema...): l'installazione avviene da DVD con configurazione tipica per "Server". Aggiungo solo X Window e Gnome per l'interfaccia grafica.
Al termine dell'installazione provvedo ad effettuare tutti gli aggiornamenti ufficiali rilasciati finora con (N.B.: *Tutti i comandi che lancerò da questo momento vengono effettuati da root!*):

`# dnf update dnf`

e poi

`# dnf update`
`# reboot`

Dopo il riavvio mi ritrovo con il kernel 2.6.15-1.1831\_FC4 (il più recente, al momento in cui scrivo). Verifico che tra i servizi configurati all'avvio ci sia il minimo indispensabile per ciò che devo fare:

`acpid`
`apmd`
`auditd`
`autofs`
`cpuspeed`
`crond`
`haldaemon`
`iptables`
`messagebus`
`netfs`
`network`
`nifd`
`portmap`
`rpcgssd`
`rpcidmapd`
`sendmail`
`syslog`

Installazione driver scheda ISDN
--------------------------------

Sul sito ufficiale della [*Eicon*](http://www.eicon.com/) ci sono le versioni rpm dei driver già pacchettizzati per Fedora, ma solo per la Core 1 con un determinato kernel, quindi, dopo aver riempito \[<http://www.eicon.com/worldwide/products/MediaGateways/DivaServerforLinux.htm?dl=1&en_prod>=&regID=6261 un apposito modulo\], scarico gli rpm a livello di sorgente versione 7.7 per la mia scheda da [questo link](http://downloads.eicon.com/download/p/linux/source/105-23/download.htm). Stando alle informazioni che leggo, riportate anche sul sito [Voip-info](http://www.voip-info.org/), la scheda è supportata da Asterisk... bene! E visto che ci sono, scarico anche la *Quick Installation Guide*, la *Reference Guide* e le *Source Package installation notes*... mi saranno utili per l'installazione.
Per la corretta installazione dei driver è necessario scaricare il pacchetto kernel-devel:

`# dnf install kernel-devel`
`=============================================================================`
` Package                 Arch       Version          Repository        Size`
`=============================================================================`
`Installing:`
` kernel-devel            i686       2.6.15-1.1831_FC4  updates-released  4.3 M`
`Installing for dependencies:`
` hardlink                i386       1:1.0-1.13       base              8.7 k`

che installa i sorgenti del kernel nella directory */usr/src/kernels/2.6.15-1.1831\_FC4-i686/*. Seguendo le istruzioni presenti nel file *readme* creo un link a questa directory con il nome */usr/src/linux* con il comando:

`# ln -s /usr/src/kernels/2.6.15-1.1831_FC4-i686/ /usr/src/linux`

Per completare installo anche i pacchetti ncurses-devel, gcc e gcc-c++:

`=============================================================================`
` Package                 Arch       Version          Repository        Size`
`=============================================================================`
`Installing:`
` gcc                     i386       4.0.2-8.fc4      updates-released  2.8 M`
` gcc-c++                 i386       4.0.2-8.fc4      updates-released  2.8 M`
` ncurses-devel           i386       5.4-17           base              1.6 M`
`Installing for dependencies:`
` glibc-devel             i386       2.3.5-10.3       updates-released  1.9 M`
` glibc-headers           i386       2.3.5-10.3       updates-released  596 k`
` glibc-kernheaders       i386       2.4-9.1.94       base              706 k`
` libstdc++-devel         i386       4.0.2-8.fc4      updates-released  9.0 M`

A questo punto tutto è pronto per installare i sorgenti dei driver. Mi posiziono nella cartella dove ho scaricato il file e lancio il comando:

`# rpm -ivh divas4linux_EICON-105.541-1.i386.rpm`

che installa i sorgenti nella cartella */usr/lib/eicon/divas/src*, dalla quale invoco:

`# ./Build`

Questo è l'output... pare sia andato tutto bene!

`PROCESSING: Please press CTRL-C to abort (waiting 15 sec) ... OK`
`PROCESSING: Cleanup ... OK`
`PROCESSING: Check system environment ... OK`
`PROCESSING: Read kernel version ... OK`
`PROCESSING: Update kernel source tree ... OK`
`PROCESSING: Update kernel configuration ... OK`
`PROCESSING: Call 'make menuconfig'`
` ...   HOSTCC  scripts/kconfig/conf.o`
`  HOSTCC  scripts/kconfig/kxgettext.o`
`  HOSTCC  scripts/kconfig/mconf.o`
`  HOSTCC  scripts/kconfig/zconf.tab.o`
`  HOSTLD  scripts/kconfig/mconf`
`  HOSTCC  scripts/lxdialog/checklist.o`
`  HOSTCC  scripts/lxdialog/inputbox.o`
`  HOSTCC  scripts/lxdialog/lxdialog.o`
`  HOSTCC  scripts/lxdialog/menubox.o`
`  HOSTCC  scripts/lxdialog/msgbox.o`
`  HOSTCC  scripts/lxdialog/textbox.o`
`  HOSTCC  scripts/lxdialog/util.o`
`  HOSTCC  scripts/lxdialog/yesno.o`
`  HOSTLD  scripts/lxdialog/lxdialog`
`scripts/kconfig/mconf arch/i386/Kconfig`
`#`
`# using defaults found in .config`
`#`
`*** End of Linux kernel configuration.`
`*** Execute 'make' to build the kernel or try 'make help'.`
`OK`
`PROCESSING: Call 'make dep', please be patient ... OK`
`PROCESSING: Call 'make modules', please be patient ... OK`
`PROCESSING: Build MTPX adapter driver ... OK`
`PROCESSING: Install Diva modules ... divadidd.ko, divas.ko, diva_mnt.ko,`
`diva_idi.ko, divacapi.ko, kernelcapi.ko, capi.ko diva_mtpx.ko OK`
`PROCESSING: Cleanup ... OK`
`PROCESSING: Build Divatty ...  OK`
`PROCESSING: Cleanup ... OK`
`SUCCESS. You can configure and start your Diva adapter now.`

Ora vado a configurare i parametri della scheda:

`# cd /usr/lib/eicon/divas`

e poi

`# ./Config`

Imposto i parametri mantenendo i valori di default (che ci stanno bene) e proseguo fino alla fine. Terminata la configurazione avvio i driver con il comando:

`# ./Start`

Anche qui sembra andare tutto bene!

`Update CFGLib information ... succeeded`
`Start adapter Nr:1 - 'Diva Server V-4BRI-8', SN: 16737 ... OK`
`Save Diva Server V-4BRI-8 SN:16737 - PORT 1 initial XLOG to /var/log/diva1.log ... OK`
`Save Diva Server V-4BRI-8 SN:16737 - PORT 2 initial XLOG to /var/log/diva2.log ... OK`
`Save Diva Server V-4BRI-8 SN:16737 - PORT 3 initial XLOG to /var/log/diva3.log ... OK`
`Save Diva Server V-4BRI-8 SN:16737 - PORT 4 initial XLOG to /var/log/diva4.log ... OK`
`Load Diva IDI  driver ... OK`
`Load Diva MTPX driver ... OK`
`Load optimized Diva CAPI driver ... not available`
`Load KERNELCAPI driver ... OK`
`Load Diva CAPI driver ... OK`
`Load CAPI driver ... OK`
`  Successfully updated configuration of Diva Server V-4BRI-8 PORT: 1 SN:16737`
`  Successfully updated configuration of Diva Server V-4BRI-8 PORT: 2 SN:16737`
`  Successfully updated configuration of Diva Server V-4BRI-8 PORT: 3 SN:16737`
`  Successfully updated configuration of Diva Server V-4BRI-8 PORT: 4 SN:16737`
`  Successfully updated configuration of Diva TTY driver`
`  Successfully updated configuration of Diva MTPX driver`
`  Successfully updated configuration of Diva CAPI driver`

Installiamo Asterisk
--------------------

Per rispondere ai requisiti di compilazione installo *openssl-devel* e *cvs*:

`=============================================================================`
` Package                 Arch       Version          Repository        Size`
`=============================================================================`
`Installing:`
` cvs                     i386       1.11.19-9        updates-released  1.2 M`
` openssl-devel           i386       0.9.7f-7.10      updates-released  1.7 M`
`Installing for dependencies:`
` e2fsprogs-devel         i386       1.38-0.FC4.1     updates-released  512 k`
` krb5-devel              i386       1.4.1-5          updates-released  923 k`
` zlib-devel              i386       1.2.2.2-5.fc4    updates-released   98 k`

Ora, sempre da root:

`# cd /usr/local/src`
`# mkdir asterisk`
`# export CVSROOT=:pserver:anoncvs@cvs.digium.com:/usr/cvsroot`
`# cvs login`
`(la password è anoncvs)`
`# cvs checkout asterisk`
`# cd asterisk`
`# make`
`# make install`
`# make samples`

Per utilizzare la mia scheda *Eicon Diva Server V-4Bri* devo installare anche il driver *chan\_capi (Asterisk/OpenPBX ISDN CAPI chan driver)* scaricabile da [Sourceforge](http://sourceforge.net/projects/chan-capi/). Il file che prelevo è *chan\_capi-cm-0.6.4.tar.gz*, e lo copio in */usr/src/*:
Per risolvere le dipendenze installo anche *isdn4k-utils-devel*:

`# dnf install isdn4k-utils-devel`

Per installare chan\_capi:

`# cd /usr/src`
`# tar -xzf chan_capi-cm-0.6.4.tar.gz`
`# rm chan_capi-cm-0.6.4.tar.gz`
`# cd chan_capi-cm-0.6.4/`
`# make`
`# make install`

Per fare in modo che Asterisk venga avviato automaticamente al boot del server:

`# cd /usr/local/src/asterisk/contrib/init.d/`
`# cp rc.redhat.asterisk /etc/rc.d/init.d/asterisk`
`# chkconfig --add asterisk`

Per far funzionare *musiconhold* è necessario scaricare *mpg123* sempre da [Sourceforge](http://sourceforge.net/projects/mpg123). Per installarlo, basta copiare il file scaricato nella directory */usr/src* e poi:

`# cd /usr/src/`
`# tar -zxvf mpg123-0.59r.tar.gz`
`# rm mpg123-0.59r.tar.gz`
`# cd mpg123-0.59r/`
`# make linux`
`# make install`

Ora possiamo editare i parametri dei più importanti file di configurazione (presenti nella directory */etc/asterisk/*).

Configuriamo Asterisk
---------------------

1.  **capi.conf**

Questo file configura i parametri della scheda ISDN. Sono da notare il contesto nel quale confluiranno le chiamate in arrivo (*capi-in*) e il parametro *echocancel=yes*, che serve ad eliminare l'eco per le schede Eicon Diva Server.

`[general]`
`nationalprefix=0`
`internationalprefix=00`
`rxgain=0.8`
`txgain=0.8`
`language=it`
`[DIVA]`
`isdnmode=msn`
`incomingmsn=**il mio numero telefonico, senza lo 0 del prefisso**`
`defaultcid=**il mio numero telefonico, senza lo 0 del prefisso**`
`controller=1`
`group=1`
`softdtmf=on`
`relaxdtmf=on`
`accountcode=`
`context=capi-in`
`echocancel=yes`
`devices=2`

<li>
**modules.conf**

</li>
Questo file configura l'avvio o meno di alcuni moduli. E' da notare: l'avvio di *chan\_capi.so*, fondamentale per il funzionamento della scheda ISDN.

`[modules]`
`autoload=yes`
`noload => pbx_gtkconsole.so`
`noload => pbx_kdeconsole.so`
`noload => app_intercom.so`
`noload => chan_modem.so`
`noload => chan_modem_aopen.so`
`noload => chan_modem_bestdata.so`
`noload => chan_modem_i4l.so`
`load => res_musiconhold.so`
`noload => chan_alsa.so`
`load => res_features.so`
`load => chan_capi.so`
`[global]`
`chan_capi.so=yes`

<li>
**sip.conf**

</li>
Questo file configura i client che utilizzano il protocollo SIP. In questo esempio ne ho 2, l'interno 101 e l'interno 201. Sono i telefoni Sirio collegati all'ATA GrandStream. Da notare: la scelta dei codec influisce sulla qualità della conversazione, ma a codec migliore corrisponde un maggiore consumo di banda.

`[general]`
`allowguest=no`
`bindport=5060`
`bindaddr=**indirizzo ip del server**`
`nat=route`
`disallow=all`
`allow=G723.1`
`allow=ulaw`
`allow=alaw`
`allow=gsm`
`context=stuffcalls`
`language=it`
`[101]`
`type=friend`
`username=101`
`secret=**password scelta**`
`host=dynamic`
`context=test`
`mailbox=101`
`[201]`
`type=friend`
`username=201`
`secret=**password scelta**`
`host=dynamic`
`context=test`
`mailbox=201`

<li>
**iax.conf**

</li>
Questo file configura i client che utilizzano il protocollo IAX2, tipico di Asterisk. Molto simile al file sip.conf precedente, cambia solo il protocollo usato. In questo esempio ho un solo interno, il 102.

`[general]`
`bindport=4569`
`bindaddr=0.0.0.0`
`language=it`
`bandwidth=medium`
`disallow=all`
`allow=G723.1`
`allow=ulaw`
`allow=alaw`
`allow=gsm`
`jitterbuffer=no`
`forcejitterbuffer=no`
`tos=lowdelay`
`autokill=yes`
`[102]`
`type=friend`
`username=102`
`secret=**password scelta**`
`host=dynamic`
`context=test`
`mailbox=102`

<li>
**extensions.conf**

</li>
Questo è il file più complesso, gestisce il flusso delle chiamate.
Nell'esempio abbiamo tre contesti: capi-in per le chiamate in arrivo dalla rete telefonica esterna; test per le chiamate tra gli interni; stuffcalls per le chiamate non gestite. Da notare: alle chiamate provenienti dall'esterno viene applicato un filtro. Le chiamate ricevute dal lunedì al venerdì, dalle 9 alle 13 e dalle 15 alle 18 vengono accolte da una voce guida (il file instradamento) che invita a premere il tasto 1, 2 o 3 a seconda dell'interno con cui si vuole comunicare. La pressione dei suddetti tasti corrisponde agli interni 101, 201 e 102 definiti in precedenza.
Se la chiamata esterna viene ricevuta in un orario diverso, si verrà accolti da una voce che invita a richiamare durante gli orari di apertura dell'ufficio.
Le chiamate al numero 9888 interpellano la segreteria telefonica (voicemail).

`[general]`
`static=yes`
`writeprotect=yes`
`autofallthrough=yes`
`language=it`
`[stuffcalls]`
`exten => _.,1,Congestion`
`[test]`
`exten => 101,1,Dial(SIP/101,30)`
`exten => 101,2,Voicemail(u101)`
`exten => 101,3,Wait(2)`
`exten => 101,4,Hangup()`
`exten => 101,102,Voicemail(b101)`
`exten => 101,103,Wait(2)`
`exten => 101,104,Hangup()`
`exten => 102,1,Dial(IAX2/102,30)`
`exten => 201,1,Dial(SIP/201,30)`
`exten => 201,2,Voicemail(u201)`
`exten => 201,3,Wait(2)`
`exten => 201,4.Hangup()`
`exten => 201,102,Voicemail(b201)`
`exten => 201,103,Wait(2)`
`exten => 201,104,Hangup()`
`exten => _XXXXXXXXXX,1,Answer()`
`exten => _XXXXXXXXXX,2,Playtones(ring)`
`exten => _XXXXXXXXXX,3,Set(CALLERID(number)=**il mio numero di telefono**)`
`exten => _XXXXXXXXXX,4,Dial(CAPI/DIVA/${EXTEN})`
`exten => _XXXXXXXXXX,5,Hangup()`
`exten => 9888,1,VoicemailMain(${CALLERIDNUM})`
`exten => 9888,2,Hangup()`
`[capi-in]`
`exten => _XXXXXXXXX,1,Ringing()`
`exten => _XXXXXXXXX,2,Wait(2)`
`exten => _XXXXXXXXX,3,GoToIfTime(09:00-13:00|mon-fri|*|*?lavoro,1)`
`exten => _XXXXXXXXX,4,GoToIfTime(15:00-18:00|mon-fri|*|*?lavoro,1)`
`exten => _XXXXXXXXX,5,Playback(FuoriOrario)`
`exten => _XXXXXXXXX,6,Playback(FuoriOrario)`
`exten => _XXXXXXXXX,7,Hangup()`
`exten => lavoro,1,Background(instradamento)`
`exten => lavoro,2,Background(instradamento)`
`exten => lavoro,3,Background(instradamento)`
`exten => lavoro,4,Hangup()`
`exten => 1,1,Dial(SIP/101,30)`
`exten => 1,2,Voicemail(u101)`
`exten => 1,3,Wait(2)`
`exten => 1,4,Hangup()`
`exten => 1,102,Voicemail(b101)`
`exten => 1,103,Wait(2)`
`exten => 1,104,Hangup()`
`exten => 2,1,Dial(SIP/201,30)`
`exten => 2,2,Voicemail(u201)`
`exten => 2,3,Wait(2)`
`exten => 2,4,Hangup()`
`exten => 2,102,Voicemail(b201)`
`exten => 2,103,Wait(2)`
`exten => 2,104,Hangup()`
`exten => 3,1,Dial(SIP/102,30)`
`exten => 3,2,Voicemail(u102)`
`exten => 3,3,Wait(2)`
`exten => 3,4,Hangup()`
`exten => 3,102,Voicemail(b102)`
`exten => 3,103,Wait(2)`
`exten => 3,104,Hangup()`

</ol>
Avviamo Asterisk
----------------

Il primo avvio di Asterisk:

`$ asterisk -vvvgc`

Avviene correttamente! Ora possono iniziare le danze...

Asterisk ed i Firewall
----------------------

Noto che i tentativi di registrazione dei client SIP avvengono correttamente, ma per autenticarsi occorre che sul firewall del server sia aperta in uscita e in ricezione la porta 5060, e solo in uscita la porta 5004. Sui client invece occorre aprire solo in uscita le porte 5060 e 5004.
Una volta configurato il firewall correttamente i client si registrano e comunicano tra loro senza problemi! Eureka!

Risorse
-------

1.  Il sito ufficiale di [Asterisk](http://www.asterisk.org/);
2.  [L'User's Group Italia](http://www.asteriskpbx.it/) di Asterisk;
3.  Il [wiki](http://www.voip-info.org/wiki_Asterisk);
4.  Il sito di [Asteriskguru](http://www.asteriskguru.org/);

Copyright
---------

Questo articolo viene rilasciato sotto [Licenza Creative Commons](http://creativecommons.org/licenses/by-nc-sa/2.0/it/).

<Categoria:Fedoraserver>
