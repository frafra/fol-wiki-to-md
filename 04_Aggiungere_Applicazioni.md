Come usare Yum
--------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

Yum è un gestore di pacchetti molto potente. Yum risolverà al tuo posto le dipendenze e installerà facilmente le tue applicazioni. Yum anche, su tua richiesta, cercherà, rimuoverà, e farà l'elenco dei pacchetti.

`usage: yum [options] < update | install | info | remove | list |`
`clean | provides | search | check-update | groupinstall |`
`groupupdate | grouplist | groupinfo | groupremove |`
`makecache | localinstall | erase | upgrade | whatprovides |`
`localupdate | resolvedep | shell | deplist >`
`opzioni:`
`-h, --help            show this help message and exit`
`-t, --tolerant        be tolerant of errors`
`-C                    run entirely from cache, don't update cache`
`-c  [config file]     config file location`
`-R  [minutes]         maximum command wait time`
`-d  [debug level]     debugging output level`
`-e  [error level]     error output level`
`-y                    answer yes for all questions`
`--version             show Yum version and exit`
`--installroot=[path]  set install root`
`--enablerepo=[repo]   enable one or more repositories (wildcards allowed)`
`--disablerepo=[repo]  disable one or more repositories (wildcards allowed)`
`--exclude=[package]   exclude package(s) by name or glob`
`--obsoletes           enable obsoletes processing during updates`
`--noplugins           disable Yum plugins`

A prima vista questo può spaventare un po', ma in realtà è facile.

### Esempi

-   Cercare un'applicazione

Yum cercherà tra tutti i tuoi repos abilitati e ti dirà dove puoi trovare il pacchetto richiesto:

`yum search nome_applicazione `

-   Yum può elencare tutti i pacchetti disponibili presso i repos che tu hai abilitato e ti dice da dove puoi ottenere i pacchetti:

`yum list available `

-   Per trovare ulteriori informazioni su uno specifico pacchetto:

`yum info nome_applicazione `

-   Per installare applicazioni

L'installazione è veramente molto facile

`yum install nome_applicazione `

-   Rimuovere i pacchetti rpm

Yum può rimuovere un'applicazione e le dipendenze installate con l'applicazione in questione. Non rimuoverà le dipendenze se un'altra applicazione installata ne fa uso.

`yum remove nome_applicazione `

-   Aggiornamento del sistema

Yum può aggiornare il sistema per te senza ulteriori interventi da parte tua

`yum update `

-   Non sei sicuro se hai le updates?

`yum check-update `

-   Installazione locale

Hai scaricato un pacchetto rpm e non puoi installarlo con il comando rpm a causa delle dipendenze?

`yum localinstall /percorso/al/pacchetto/rpm `

Elenca i tuoi ultimi update con rpm
-----------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

`rpm -qa --last | tac`

Come installare un'interfaccia grafica (GUI) per yum
----------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install yumex

<li>
Applicazioni -&gt; Strumenti di Sistema -&gt; Yum Extender

</li>
</ol>
Network Manager per Gnome
-------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

Avvia il servizio

`chkconfig --level 345 NetworkManager on`
`chkconfig --level 345 NetworkManagerDispatcher on`
`service NetworkManager start`
`service NetworkManagerDispatcher start`

Digita le informazioni per il tuo sistema. [Qui](http://www.fedorajim.homelinux.com/samples/NetworkManagerConnected.png) trovi degli screenshot

Come installare un Menu Editor per GNOME
----------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install alacarte

<li>
Applicazioni -&gt; Accessori -&gt; Alacarte Menu Editor

</li>
</ol>
Come installare Clipboard Daemon per GNOME
------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  I primi 6 comandi vengono eseguiti da root, l'ultimo dall'utente (exit ti riporta al tuo ambiente di lavoro).

wget -c <http://easylinux.info/uploads/gnome-clipboard-daemon-1.0.bin.tar.bz2>

`tar jxvf gnome-clipboard-daemon-1.0.bin.tar.bz2 -C /usr/bin/`
`rm -f gnome-clipboard-daemon-1.0.bin.tar.bz2`
`chown root:root /usr/bin/gnome-clipboard-daemon`
`chmod 755 /usr/bin/gnome-clipboard-daemon`
`gnome-clipboard-daemon &`
`exit`
`export EDITOR=gedit && crontab -e`

<li>
Aggiungi la seguente linea alla fine del file

</li>
`@reboot gnome-clipboard-daemon`

<li>
Salva il file modificato

</li>
</ol>
Come installare J2SE Runtime Environment (JRE) con il Plug-in per Mozilla Firefox
---------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Scarica il file autoestraente per Linux (jre-1\_5\_0\_06-linux-i586.bin) da [qui](http://java.com/en/download/manual.jsp) e salvalo nella tua home.

mv jre-1\_5\_0\_06-linux-i586.bin /opt

`cd /opt`
`chmod +x jre-1_5_0_06-linux-i586.bin`
`./jre-1_5_0_06-linux-i586.bin`
`ln -s /opt/jre1.5.0_06/plugin/i386/ns7/libjavaplugin_oji.so `
`/usr/lib/mozilla/plugins/libjavaplugin_oji.so`

<li>
Il plugin Java è ora installato. Conferma con il comando seguente che il link simbolico sia di colore verde

</li>
`ls /usr/lib/mozilla/plugins`

<li>
Per avviare applicazioni java come limewire, continua cosi:

</li>
`gedit /etc/profile.d/java.sh`

<li>
Inserisci le seguenti righe nel nuovo file

</li>
`#!/bin/sh`
`JAVA_HOME=/usr/java/jre1.5.0_06`
`export JAVA_HOME`
`JAVA_BIN=$JAVA_HOME/bin`
`CLASSPATH=$CLASSPATH:$JAVA_HOME:$JAVA_HOME/lib`
`PATH=$JAVA_BIN:$PATH`
`export JAVA_BIN CLASSPATH PATH`

<li>
Salva il file che hai editato

</li>
`source /etc/profile.d/java.sh`
`/usr/sbin/alternatives --install /usr/bin/java java /opt/jre1.5.0_06/bin/java 2`
`/usr/sbin/alternatives --config java`

<li>
Vedrai la seguente schermata

</li>
`There are 2 programs which provide 'java'.`
`  Selection    Command`
`-----------------------------------------------`
`*+ 1           /usr/lib/jvm/jre-1.4.2-gcj/bin/java`
`   2           /opt/jre1.5.0_06/bin/java`
`Enter to keep the current selection[+], or type selection number:`

<li>
Digita 2

-   Testa la tua installazione di Java
    </li>

</ol>
Come installare il plug-in di Flash Player (Macromedia Flash) per Mozilla Firefox
---------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum --enablerepo=flash install flash-plugin

<li>
Riavvia Mozilla Firefox

</li>
</ol>
Come installare un lettore per file PDF (Adobe Reader)
------------------------------------------------------

Tu puoi già leggere i documenti in formato .pdf, ma se desideri farlo con Adobe Reader:

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

wget -c <http://ardownload.adobe.com/pub/adobe/reader/unix/7x/7.0.5/enu/AdobeReader_enu-7.0.5-1.i386.rpm>

`yum -y install compat-libstdc++-33`
`rpm -i AdobeReader_enu-7.0.5-1.i386.rpm`
`rm -f AdobeReader_enu-7.0.5-1.i386.rpm`

<li>
Applicazioni -&gt; Office -&gt; Adobe Reader

</li>
</ol>
Aggiungere Adobe Acrobat ai plugins di mozilla
----------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

Linkare Acrobat Reader nella directory dei plug-in di mozilla, ti permetterà di vedere i file pdf nel browser invece che con l'Acrobat Reader

`cd /usr/lib/mozilla/plugins`
`ln -s /usr/local/Adobe/Acrobat7.0/Browser/intellinux/nppdf.so`

Come installare un Download Manager (Downloader for X)
------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install d4x

<li>
Applicazioni -&gt; Internet -&gt; Downloader for X

</li>
</ol>
Come installare un Client FTP (gFTP)
------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install gftp

<li>
Applicazioni -&gt; Internet -&gt; gFTP

</li>
</ol>
Come installare una File share utility (DC++)
---------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

wget -c <http://easylinux.info/uploads/linuxdcpp.tar.gz>

`tar zxvf linuxdcpp.tar.gz -C /opt`
`rm -f linuxdcpp.tar.gz`
`gedit /usr/share/Applicazioni/dcpp.desktop`

<li>
Inserisci le seguenti righe nel nuovo file:

</li>
`[Desktop Entry]`
`Encoding=UTF-8`
`Name=DC++`
`Exec=/opt$ /opt/linuxdcpp/dcpp`
`Terminal=false`
`Type=Application`
`StartupNotify=true`
`Icon=eyes.png`
`Categories=Application;Network;`

<li>
Applicazioni -&gt; Internet -&gt; DC++

</li>
</ol>
Come installare un client P2P per BitTorrent (Azureus)
------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare J2SE Runtime Environment (JRE) con il Plug-in per Mozilla Firefox](#Come_installare_J2SE_Runtime_Environment_(JRE)_con_il_Plug-in_per_Mozilla_Firefox "wikilink")

wget -c <http://heanet.dl.sourceforge.net/sourceforge/azureus/Azureus_2.3.0.6_linux.tar.bz2>

`tar jxvf Azureus_2.3.0.6_linux.tar.bz2 -C /opt`
`gedit /usr/share/Applicazioni/azureus.desktop`

<li>
Aggiungi le seguenti righe nel nuovo file

</li>
`[Desktop Entry]`
`Name=Azureus`
`Comment=A Bittorrent client`
`Exec=/opt/azureus/azureus`
`Icon=/opt/azureus/Azureus.png`
`Terminal=false`
`Type=Application`
`Categories=Application;Network;`

<li>
Applicazioni -&gt; Internet -&gt; Azureus

</li>
</ol>
Come installare un Client P2P per eMule (aMule)
-----------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install amule

<li>
Applicazioni -&gt; Internet -&gt; aMule

</li>
</ol>
Come installare un Client P2P per Gnutella (LimeWire)
-----------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare J2SE Runtime Environment (JRE) con il Plug-in per Mozilla Firefox](#Come_installare_J2SE_Runtime_Environment_(JRE)_con_il_Plug-in_per_Mozilla_Firefox "wikilink")

wget -c <http://easylinux.info/uploads/LimeWireOther.zip>

`unzip -u LimeWireOther.zip -d /opt/`
`rm -f LimeWireOther.zip`
`gedit /usr/bin/runLime.sh`

<li>
Aggiungi le seguenti righe nel nuovo file

</li>
`cd /opt/LimeWire/`
`./runLime.sh`

<li>
Salva il file

</li>
`chmod +x /usr/bin/runLime.sh`
`gedit /usr/share/Applicazioni/LimeWire.desktop`

<li>
Aggiungi le seguenti righe nel nuovo file

</li>
`[Desktop Entry]`
`Name=LimeWire`
`Comment=LimeWire`
`Exec=runLime.sh`
`Icon=/opt/LimeWire/LimeWire.ico`
`Terminal=false`
`Type=Application`
`Categories=Application;Network;`

<li>
Salva il file

</li>
<li>
Applicazioni -&gt; Internet -&gt; LimeWire

</li>
</ol>
Come installare Messenger (Skype)
---------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

wget -c <http://download.skype.com/linux/skype_staticQT-1.2.0.18.tar.bz2>

`tar jxvf skype_staticQT-1.2.0.18.tar.bz2 -C /opt/`
`ln -s /opt/skype-1.2.0.18/skype /usr/bin/skype`
`cp /opt/skype-1.2.0.18/skype.desktop /usr/share/Applicazioni/skype.desktop`
`cp /opt/skype-1.2.0.18/icons/skype_32_32.png /usr/share/pixmaps/skype.png`
`rm -f skype_staticQT-1.2.0.18.tar.bz2`

<li>
Applicazioni -&gt; Internet -&gt; Skype

</li>
</ol>
Come installare Codecs per applicazioni multimediali
----------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

`yum -y install gstreamer-plugins*`
`yum -y install lame`
`yum -y install ffmpeg`
`yum -y install mjpegtools`
`yum --enablerepo=atrpms install w32codec`
`gst-register-0.8`

Come installare la possibilità di riprodurre a video i DVD
----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

`wget -c `[`http://download.videolan.org/pub/libdvdcss/1.2.9/rpm/libdvdcss2-1.2.9-1.i386.rpm`](http://download.videolan.org/pub/libdvdcss/1.2.9/rpm/libdvdcss2-1.2.9-1.i386.rpm)
`rpm -i libdvdcss2-1.2.9-1.i386.rpm`

Come installare un lettore di contenuti multimediali (MPlayer) con il relativo Plug-in per Mozilla Firefox
----------------------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare Codecs per applicazioni multimediali](#Come_installare_Codecs_per_applicazioni_multimediali "wikilink")
4.  Leggi [Come installare la possibilità di riprodurre a video i DVD](#Come_installare_la_possibilità_di_riprodurre_a_video_i_DVD "wikilink")

yum -y install mplayer-gui

`yum -y install mplayerplug-in`

<li>
Applicazioni -&gt; Audio e Video -&gt; MPlayer

</li>
<li>
Riavvia Mozilla Firefox

</li>
</ol>
Come installare un lettore di contenuti multimediali (VLC)
----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare Codecs per applicazioni multimediali](#Come_installare_Codecs_per_applicazioni_multimediali "wikilink")
4.  Leggi [Come installare la possibilità di riprodurre a video i DVD](#Come_installare_la_possibilità_di_riprodurre_a_video_i_DVD "wikilink")

yum -y install videolan-client

<li>
Applicazioni -&gt; Audio e Video -&gt; MPlayer

</li>
</ol>
Come installare un lettore di contenuti multimediali (XMMS)
-----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare Codecs per applicazioni multimediali](#Come_installare_Codecs_per_applicazioni_multimediali "wikilink")

yum -y install xmms

`yum -y install xmms-mp3`
`yum -y install xmms-skins`

<li>
Applicazioni -&gt; Audio e Video -&gt; XMMS

</li>
</ol>
Come installare un lettore di contenuti multimediali (amaroK)
-------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare Codecs per applicazioni multimediali](#Come_installare_Codecs_per_applicazioni_multimediali "wikilink")

yum -y install amarok

<li>
Applicazioni -&gt; Audio e Video -&gt; amarok

</li>
</ol>
Come installare un lettore di contenuti multimediali (RealPlayer 10)
--------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install compat-libstdc++-33

<li>
Scarica RealPlayer Gold da [qui](http://www.real.com/realcom/R?href=http%3A%2F%2Fforms.real.com%2Freal%2Fplayer%2Fdownload.html%3Ff%3Dunix%2FRealPlayer10GOLD.rpm%26product%3Dplayerplus%26system%3Dlinux&pageid=linuxPage&pageregion=advanced_install&src=linux&pcode=rn&opage=linux).

</li>
<li>
Installalo.
*Supponiamo che il file .rpm è stato scaricato sul tuo Desktop, perché Firefox lo fa per impostazione predefinita.*

</li>
`rpm -ivh Desktop/RealPlayer10GOLD.rpm`
`yum remove HelixPlayer`

<li>
Applicazioni -&gt; Audio e Video -&gt; RealPlayer 10

</li>
</ol>
Come installare un'applicazione per Streaming (streamtuner)
-----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

wget -c <ftp://ftp.freshrpms.net/pub/dag/dries/packages/streamtuner/fc4-i386/streamtuner-0.99.99-1.2.fc4.rf.i386.rpm>

`rpm -ivh streamtuner-0.99.99-1.2.fc4.rf.i386.rpm`
`rm -f streamtuner-0.99.99-1.2.fc4.rf.i386.rpm`

<li>
Applicazioni -&gt; Audio e Video -&gt; streamtuner

</li>
</ol>
Come installare ID3 Tag Editor (EasyTAG)
----------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum --enablerepo=freshrpms install easytag

<li>
Applicazioni -&gt; Audio e Video -&gt; EasyTAG

</li>
</ol>
Come installare un editor per file Video (Kino)
-----------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare Codecs per applicazioni multimediali](#Come_installare_Codecs_per_applicazioni_multimediali "wikilink")

yum -y install kino

<li>
Applicazioni -&gt; Audio e Video -&gt; Kino

</li>
</ol>
Come installare un editor per file Audio (Audacity)
---------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare Codecs per applicazioni multimediali](#Come_installare_Codecs_per_applicazioni_multimediali "wikilink")

yum -y install audacity

<li>
Applicazioni -&gt; Audio e Video -&gt; Audacity

</li>
</ol>
Come installare un ripper per DVD (dvd::rip)
--------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare Codecs per applicazioni multimediali](#Come_installare_Codecs_per_applicazioni_multimediali "wikilink")
4.  Leggi [Come installare la possibilità di riprodurre a video i DVD](#Come_installare_la_possibilità_di_riprodurre_a_video_i_DVD "wikilink")
5.  Leggi [Come installare un lettore di contenuti multimediali (MPlayer) con il relativo Plug-in per Mozilla Firefox](#Come_installare_un_lettore_di_contenuti_multimediali_(MPlayer)_con_il_relativo_Plug-in_per_Mozilla_Firefox "wikilink")
6.  Leggi [Come installare un compressore RAR (rar)](#Come_installare_un_compressore_RAR_(rar) "wikilink")

yum -y install perl-Video-DVDRip

`yum --enablerepo=freshrpms install vcdimager`
`yum -y install cdrdao`
`yum --enablerepo=freshrpms install subtitleripper`
`ln -fs /usr/bin/rar /usr/bin/rar-2.80`
`gedit /usr/share/Applicazioni/dvdrip.desktop`

<li>
Inserisci le seguenti linee nel nuovo file

</li>
`[Desktop Entry]`
`Name=dvd::rip `
`Comment=dvd::rip`
`Exec=dvdrip`
`Icon=/usr/share/perl5/Video/DVDRip/icon.xpm`
`Terminal=false`
`Type=Application`
`Categories=Application;AudioVideo;`

<li>
Salva il file modificato

</li>
<li>
Applicazioni -&gt; Audio e Video -&gt; dvd::rip

</li>
</ol>
Come installare un visualizzatore di Immagini (Gwenview)
--------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install gwenview

`yum -y install kipi-plugins`
`yum -y install ImageMagick`

<li>
Applicazioni -&gt; Grafica -&gt; Gwenview

</li>
</ol>
Come installare un client per la posta elettronica (Mozilla Thunderbird)
------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install thunderbird

<li>
Applicazioni -&gt; Internet -&gt; Thunderbird EMail

</li>
</ol>
Come installare un lettore di News (Pan)
----------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install pan

<li>
Applicazioni -&gt; Internet -&gt; Pan Lettore di News

</li>
</ol>
Come installare un lettore per RSS/RDF/Atom (RSSOwl)
----------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare J2SE Runtime Environment (JRE) con il Plug-in per Mozilla Firefox](#Come_installare_J2SE_Runtime_Environment_(JRE)_con_il_Plug-in_per_Mozilla_Firefox "wikilink")

wget -c <http://easylinux.info/uploads/rssowl_linux_1_1_3_bin.tar.gz>

`tar zxvf rssowl_linux_1_1_3_bin.tar.gz -C /opt/`
`chown -R root:root /opt/rssowl_linux_1_1_3_bin/`
`gedit /usr/bin/runRSSOwl.sh`

<li>
Inserisci le seguenti linee nel nuovo file

</li>
`export MOZILLA_FIVE_HOME=/usr/lib/mozilla-firefox`
`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${MOZILLA_FIVE_HOME}:${LD_LIBRARY_PATH}`
`cd /opt/rssowl_linux_1_1_3_bin/`
`./run.sh`

<li>
Salva il file modificato

</li>
`chmod +x /usr/bin/runRSSOwl.sh`
`gedit /usr/share/Applicazioni/RSSOwl.desktop`

<li>
Inserisci le seguenti linee nel nuovo file

</li>
`[Desktop Entry]`
`Name=RSSOwl`
`Comment=RSSOwl`
`Exec=runRSSOwl.sh`
`Icon=/opt/rssowl_linux_1_1_3_bin/rssowl.xpm`
`Terminal=false`
`Type=Application`
`Categories=Application;Network;`

<li>
Salva il file modificato

</li>
<li>
Applicazioni -&gt; Internet -&gt; RSSOwl

</li>
</ol>
Come installare un CHM viewer (GnoCHM)
--------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y --enablerepo=dries install gnochm

<li>
Applicazioni -&gt; Accessori -&gt; CHM Viewer

</li>
</ol>
Come installare un Web Authoring System (Nvu)
---------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install xorg-x11-deprecated-libs

`wget -c `[`http://www.nvu.com/download/linux/1.0/nvu-1.0-RedHat_and_Fedora/nvu-1.0-1.rhel4.fs.i386.rpm`](http://www.nvu.com/download/linux/1.0/nvu-1.0-RedHat_and_Fedora/nvu-1.0-1.rhel4.fs.i386.rpm)
`rpm -ivh nvu-1.0-1.rhel4.fs.i386.rpm`

<li>
Applicazioni -&gt; Programmazione -&gt; Nvu

</li>
</ol>
Come installare un Web Authoring System (bluefish)
--------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install bluefish

<li>
Applicazioni --&gt; Programmazione --&gt; Bluefish Editor

</li>
</ol>
Come installare un ambiente di sviluppo orientato al web per KDE (quanta plus)
------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install kdewebdev

<li>
Applicazioni -&gt; Programmazione -&gt; Quanta Plus

</li>
</ol>
Come installare un'applicazione per la contabilità personale (GnuCash)
----------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install gnucash

`rm -fr /usr/share/gnome/apps/Applicazioni/`
`gedit /usr/share/Applicazioni/GnuCash.desktop`

<li>
Inserisci le seguenti linee nel nuovo file

</li>
`[Desktop Entry]`
`Name=GnuCash`
`Comment=GnuCash Personal Finance`
`Exec=gnucash`
`Icon=/usr/share/pixmaps/gnucash/gnucash-icon.png`
`Terminal=false`
`Type=Application`
`Categories=Application;Office;`

<li>
Salva il file modificato

</li>
<li>
Applicazioni -&gt; Office -&gt; GnuCash

</li>
</ol>
Come installare un'applicazione per il Desktop Publishing (Scribus)
-------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install scribus

<li>
Applicazioni -&gt; Office -&gt; Scribus

</li>
</ol>
Come installare un'applicazione per masterizzare CD/DVD (GnomeBaker)
--------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install gnomebaker

<li>
Applicazioni -&gt; Audio e Video -&gt; GnomeBaker

</li>
</ol>
Come installare un'applicazione per masterizzare CD/DVD (k3b)
-------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install k3b

<li>
Applicazioni -&gt; Audio e Video -&gt; K3b

</li>
</ol>
Come installare un Editor di partizioni (GParted)
-------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install gparted

<li>
Applicazioni -&gt; Strumenti di Sistema -&gt; GParted

</li>
</ol>
Come installare un Firewall personale (Firestarter)
---------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install firestarter

<li>
Applicazioni -&gt; Strumenti di Sistema -&gt; Firestarter

</li>
</ol>
Come installare un analizzatore di traffico di rete (Ethereal)
--------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install ethereal ethereal-gnome

<li>
Applicazioni -&gt; Internet -&gt; Ethereal

</li>
</ol>
Come installare un compressore RAR (rar)
----------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum --enablerepo=freshrpms install rar unrar

<li>
Applicazioni -&gt; Accessori -&gt; Archive Manager

</li>
</ol>
Come installare dei Fonts aggiuntivi
------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install xfonts-arabic

`yum -y install xfonts-chinese`
`yum -y install xfonts-gujarati`
`yum -y install xfonts-hebrew`
`yum -y install xfonts-hindi`
`yum -y install xfonts-japanese`
`yum -y install xfonts-xorg-truetype`
`wget -c `[`http://easylinux.info/uploads/msttcorefonts-1.3-4.noarch.rpm`](http://easylinux.info/uploads/msttcorefonts-1.3-4.noarch.rpm)
`rpm -ivh msttcorefonts-1.3-4.noarch.rpm`
`/etc/init.d/xfs restart`

<li>
Leggi \#15.4 Come riavviare GNOME senza riavviare il computer

</li>
</ol>
Come installare delle Applets per il Desktop (gDesklets)
--------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install gdesklets

<li>
Applicazioni -&gt; Accessori -&gt; gDesklets

</li>
<li>
Per ulteriori informazioni vedi [questo](http://gdesklets.gnomedesktop.org/)

</li>
</ol>
Come installare un Compilatore
------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

`yum -y install gcc`
`yum -y install gcc-c++`

Come implementare un ambiente di sviluppo
-----------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Aggiungi i repo di sviluppo

gedit /etc/yum.repos.d/fedora-devel.repo

<li>
Aggiungi le seguenti linee al nuovo file

</li>
`[development]`
`name=Fedora Core $releasever - Development Tree`
`#baseurl=`[`http://download.fedora.redhat.com/pub/fedora/linux/core/development/$basearch/`](http://download.fedora.redhat.com/pub/fedora/linux/core/development/$basearch/)
`mirrorlist=`[`http://fedora.redhat.com/download/mirrors/fedora-core-rawhide`](http://fedora.redhat.com/download/mirrors/fedora-core-rawhide)
`enabled=1`
`gpgcheck=0`

<li>
Salva il file modificato

</li>
`yum groupinstall "Development Tools"`

</ol>
Come installare un'IDE, Integrated Development Environment (Anjuta)
-------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

rpm --import /usr/share/rhn/RPM-GPG-KEY

`yum -y install anjuta`

<li>
Applicazioni -&gt; Programmazione -&gt; Anjuta IDE

</li>
</ol>
Come installare un tool per la modellazione 3D (Blender 3d)
-----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install blender

<li>
Applicazioni -&gt; Grafica -&gt; Blender 3D modeller

</li>
</ol>
Come installare il gioco jFrozen-Bubble
---------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install frozen-bubble

<li>
Applicazioni -&gt; Giochi -&gt; Frozen-Bubble

</li>
<li>
Per altri giochi vedi [questo](http://games.linux.sk/) oppure [il sito di Tuxgames](http://www.tuxgames.com/)

</li>
</ol>
Come installare un planetario virtuale (Stellarium)
---------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install stellarium

<li>
Applicazioni -&gt; Grafica -&gt; Stellarium nightsky renderer

</li>
</ol>
Come installare le applicazioni KDE Edutainment
-----------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install kdeedu

<li>
Applicazioni -&gt; Edutainment -&gt; ...

</li>
</ol>
<Categoria:Fedoraserver>
