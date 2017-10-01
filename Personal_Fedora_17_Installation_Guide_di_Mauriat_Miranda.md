Questa è una guida <i>personale</i> alla configurazione di Fedora 17.
Questa pagina fornisce delle informazioni che qualcuno potrebbe trovare utili. Ricorda che quanto segue ha funzionato per <i>me</i>, e assicurati di avere effettuato copie di backup dei tuoi file critici nel caso in cui tu dovessi provare ad eseguire quanto qui riportato. Questa guida è stata testata dall'autore utilizzando entrambe le versioni a 32bit e a 64bit. I sistemi descritti si avviano correttamente anche in dual-boot con Windows 7. (*al 6 giugno il test su 32bit è solo parziale*)

Supporti di installazione
-------------------------

Fedora 17 viene distribuita in singoli CD-ROM o DVD-ROM per l'installazione. Il disco DVD-ROM è il metodo di installazione utilizzato in questa guida. Facendo il boot dal DVD si farà partire l'installer, il quale farà si che Fedora venga installata o che venga fatto l'upgrade di una versione precedente sulla propria macchina.

Esistono anche dei "LiveCD" che possono avviare il sistema ed eseguire una installazione di base di Fedora 17 nella memoria RAM, fornendo inoltre un metodo più semplice di installazione (non completo come quello del DVD o dei multi-CD ). Il LiveCD predefinito rende disponibile Gnome (es: Fedora-17-x86\_64-Live-Desktop.iso). Esiste uno specifico LiveCD che rende disponibile KDE. Entrambi forniscono un programma di installazione, ma entrambi rendono disponibile molto meno software che un DVD. Inoltre richiedono più memoria per essere usati. Il LiveCD può essere utile per dimostrazioni.

Installazione
-------------

E' **fortemente raccomandata** la lettura delle [Note di Rilascio di Fedora](http://docs.fedoraproject.org/release-notes/f17/it-IT/html/) e della [Guida ufficiale all'Installazione](http://docs.fedoraproject.org/install-guide/f17/en-US/html/) prima di installare Fedora.
Un'ulteriore raccomandazione è quella di leggere i [Problemi comuni](https://fedoraproject.org/wiki/Common_F17_bugs) prima di installare.
Scaricare il file immagine del DVD di Fedora 17 da un [mirror](http://mirrors.fedoraproject.org/publiclist/Fedora/17/) di Fedora (o usare [torrent](http://torrent.fedoraproject.org)) e masterizzarlo (per ulteriori informazioni su come scaricare i CD o il DVD di [Fedora](http://www.mjmwired.net/resources/mjm-download-fedora.html), oltre a [come masterizzare le immagini ISO](http://docs.fedoraproject.org/en-US/Fedora/17/html/Burning_ISO_images_to_disc/index.html).

Avviare il sistema dal DVD. Se si sceglie di usare il [LiveCD](http://www.mjmwired.net/resources/mjm-fedora-f17.html#installmedia) per favore si tenga presente che i passi successivi potrebbero essere differenti. Se si vuole fare la **Configurazione della rete** durante l'installazione, assicurarsi di selezionare *Configura Rete* quando si è al prompt per il proprio hostname. Per le impostazioni delle **connessioni di rete** selezionare *modifica* per impostare la propria rete di default e assicurarsi di selezionare di connettersi automaticamente. Modificare anche le altre impostazioni se necessario. Per [ulteriori informazioni](http://docs.fedoraproject.org/en-US/Fedora/17/html/Installation_Guide/sn-Netconfig-x86.html#sn-Netconfig-x86-edit).

### Partizionare

-   Se si ha un disco fisso vuoto o si desidera cancellare l'intero contenuto del disco fisso, si può lasciare che l'installer *usi l'intero spazio disponibile*;
-   Se si desidera avviare in dual-boot o salvare dei dati contenuti nel disco fisso, bisogna selezionare o *diminuire il sistema corrente* oppure *Usa lo spazio libero*;
-   Per i miei sistemi seleziono: Crea un layout personalizzato.

In questo caso raccomando almeno 3 partizioni: una partizione primaria / di root di 8-12GB, una partizione /home di 10GB+ e una partizione swap di 2GB. La partizione principale è quella dove saranno installate le applicazioni. La partizione /home conterrà tutti i dati personali (meglio se la si può definire di grandi dimensioni). La partizione di swap dovrebbe essere almeno pari alla dimensione della memoria fisica del proprio sistema (1GB, 2GB, 4GB), sistemi con grandi dimensioni di memoria comunque non hanno bisogno di grandi spazi per lo swap. ([Per sapere di più](http://docs.fedoraproject.org/en-US/Fedora/17/html/Installation_Guide/s2-diskpartrecommend-x86.html)).

### Boot Loader

-   Se si possiede un disco fisso vuoto o si desidera che Fedora sia il proprio *Sistema Operativo Principale*, si possono lasciare le opzioni predefinite. Questo funziona anche per sistemi in dual boot con altri sistemi operativi (p.e. Windows).
-   Se si desidera mantenere Windows come sistema operativo principale, bisogna installare Grub sulla partizione /, **NON nell'MBR**. Per fare questo, selezionare Configure Advanced Boot Loader Options per poi installare Grub nel *First sector of boot partition*. Gli utenti **Windows 7** (o **Vista**) possono usare [EasyBCD](http://neosmart.net/dl.php?id=1) (freeware download per Windows). Se si sta ancora utilizzando Windows XP (o 2000) si può utilizzare [Bootpart](http://www.winimage.com/bootpart.htm) per avviare Linux. Un´alternativa a Bootpart è descritta nel \[<http://www.tldp.org/HOWTO/Linux+NT-Loader.html>" NT OS Loader + Linux mini-HOWTO\] o nel [Grub Win2K Howto](http://www.geocities.com/epark/linux/grub-w2k-HOWTO.html). Io raccomando di fare come me, così non si correrà il rischio di danneggiare la propria installazione di Windows in un ambiente Dual-Boot. **Questa opzione richiede del lavoro in più. Si tenga presente che anche l'opzione predefinita di installazione sull'MBR funziona.**

### Selezione dei pacchetti'''

Se si possiede una connessione veloce ad Internet, non è necessario installare nulla in fase di installazione. Fedora può facilmente aggiungere altro software in un secondo momento. La selezione di default dei pacchetti da installare è in genere accettabile. La maggior parte degli utenti dovrebbe installare Fedora con l'opzione Desktop Grafico. I seguenti DE sono installabili attraverso l'opzione "personalizza ora":

-   Sotto la voce *Ambienti Desktop* selezionare almeno uno tra:
    -   KDE Software Compilation
    -   LXDE
    -   Xfce

Possono essere installati anche successivamente se si desidera. Per ulteriori informazioni leggere [Desktop alternativi](http://www.mjmwired.net/resources/mjm-fedora-f17.html#desktops).

Installare i pacchetti selezionati e riavviare.

Per coloro che hanno optato per installare grub sul primo settore della partizione / invece che nell'MBR, è necessario seguire una delle guide sopra citate per avviare Fedora e configurando Windows//Vista o XP/2000.

Dopo il **primo avvio**: Dopo il primo avvio di Fedora seguire le istruzioni sullo schermo.

Nel menu **Crea utente** assicurarsi di creare un utente. Se questo utente dovrà essere anche *ammnistratore*, selezionare *aggiungi al gruppo degli amministratori*.

Configurare sudo
----------------

Fedora, come tutte le altre distribuzioni Linux, ha un utente root ed ha anche utenti individuali. L'utente root è il "superutente", al pari di "Amministratore" in Windows.

Occorre usare il proprio account personale per gli usi quotidiani. Per l'account che amministra il sistema invece si dovrebbe selezionare *Aggiungi al gruppo amministratori*. Questo permette di utilizzare l'utente normale come 'root', utilizzando il comando *sudo*.

Se si è configurato sudo al primo boot, è in ordine così. Altrimenti si può configurare *sudo* manualmente, digitando come root:

`echo 'loginname ALL=(ALL) ALL' >> /etc/sudoers`
`Dove 'loginname' è il proprio account per un utente individuale.`
`Va usato 'ALL=(ALL) NOPASSWD:ALL' se non si vuole richiesta una password.`
` Se viene richiesta una password durante l'uso di 'sudo', si dovrà fornire la password dell'utente, non quella di root.`

Esempio:

`[`**`mirandam`**`@charon ~]$ su`
`Password:   <--Inserire root password`
`[root@charon mirandam]# echo `**`'mirandam`**` ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers`
`[root@charon mirandam]# exit`

Il seguente è un esempio di come sudo lascia eseguire i comandi di root:

`[mirandam@charon ~]$ du -sh /root`
`` du: `/root':  ``**`Permission` `denied`**`      <-- Senza sudo!!!`
`[mirandam@charon ~]$ sudo du -sh /root`
`163M    /root                       <-- Con sudo!!!`

Configurare yum
---------------

Fedora usa *yum* per installare ed aggiornare il proprio software. Quando è connesso ad internet, yum determina automaticamente le dipendenze delle applicazioni.

### Repository di Fedora

Fedora ha due repository abilitati come impostazione predefinita: *fedora* (gli stessi pacchetti che vengono forniti con i CD o con il DVD), ed *updates* (pacchetti di aggiornamento, più recenti di fedora).

### YUM Plugins

Yum ha disponibile molti plugins. Molti utenti trovano utile *fastestmirror*, il plugin che accelera il download cercando collegamenti più veloci.
Per installarlo:

`[mirandam@charon ~]$ sudo yum install yum-plugin-fastestmirror`

### Repository di Terze Parti

Per le applicazioni che non sono allineate con la politica di Fedora (MP3, DVD, MPEG, Driver binari, etc), deve essere usato un repository di "parte terza". Il repository consigliato per Fedora è: [RPMFusion](http://rpmfusion.org/). Per lo scopo di questa guida tutte le installazioni possono essere fatte con questo repository, altrimenti verrà indicato espressamente. Per installare RPM-Fusion digitate:

`[mirandam@charon ~]$ sudo rpm -ivh `[`http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm`](http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm)
`[mirandam@charon ~]$ sudo rpm -ivh `[`http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm`](http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm)

Ambienti Desktop alternativi
----------------------------

Molti utenti trovano Gnome 3 difficile da usare e dovrebbero provare delle alternative. I seguenti ambienti Desktop sono supportati da Fedora. Da notare che sono tutti opzionali. Utilizzate yum se volete installarli:

[KDE](http://www.mjmwired.net/resources/mjm-fedora-f16.html#kde) è un desktop completo alla pari di Gnome. Comunque va utilizzato in modo diverso rispetto a Gnome. E' l'ambiente Desktop più vicino a Gnome ([ulteriori informazioni](http://kde.org/)).
Per installarlo:

`[mirandam@charon ~]$ sudo yum groupinstall "KDE Software Compilation"`

[LXDE](http://www.mjmwired.net/resources/mjm-fedora-f16.html#lxde) è un ambiente molto leggero. E' utile per PC datati e utilizza molto meno spazio rispetto a Gnome e KDE. E' paragonabile a versioni più vecchie di Windows ([ulteriori informazioni](http://lxde.org/)).
Per installarlo:

`[mirandam@charon ~]$ sudo yum groupinstall LXDE`

[Xfce](http://www.mjmwired.net/resources/mjm-fedora-f16.html#xfce) è un ambiente leggero simile a LXDE. Consuma molto meno risorse rispetto a Gnome e molti utenti lo paragonano alle prime versioni di Gnome ([ulteriori informazioni](http://www.xfce.org/)).
Per installarlo:

`[mirandam@charon ~]$ sudo yum groupinstall XFCE`

*Note: Xfce è la mia scelta personale/raccomandata.*

Installare lettori MP3
----------------------

Fedora viene distribuita senza alcuna forma di supporto ai file di tipo MP3. Per aggiungere il supporto all'esecuzione di MP3 si **deve installare da "terze parti"**. Quanto segue richiede l'uso del repository di [RPMFusion](RPMFusion "wikilink").

### XMMS

Semplice, vecchia GUI, opzioni minimalistiche (ma molto popolari).
Installazione, con yum:

`[mirandam@charon ~]$ sudo yum install xmms xmms-mp3 xmms-faad2 xmms-flac xmms-pulse xmms-skins`

### Audacious

Un player in versione base, ma un po' meglio di XMMS.
Installazione, con yum:

`[mirandam@charon ~]$ sudo yum install audacious `**`audacious-plugins-freeworld*`**
`N.B.: C'è un '*' alla fine del comando.`

### Rythmbox/Gstreamer

Una semplice applicazione audio simile al layout di iTunes.
Gran parte dei componenti di Rythmbox e di Gstreamer dovrebbero essere già installati durante l'installazione di Gnome (sopra citata). I componenti che non vengono installati sono quelli relativi all'MP3 (e ad altri formati).
Installazione, con yum:

`[mirandam@charon ~]$ sudo yum install rhythmbox gstreamer-plugins-ugly gstreamer-plugins-bad gstreamer-ffmpeg gstreamer-plugins-bad-nonfree`

### Amarok

Una moderna applicazione ricca di opzioni aggiuntive.
E' di aiuto avere già KDE installato (come prima citato).
Installazione, yum:

`[mirandam@charon ~]$ sudo yum install amarok xine-lib-extras-freeworld`

### Comando combinato

Per chi volesse **TUTTO**, seguire questo comando:

`[mirandam@charon ~]$ sudo yum install xmms xmms-mp3 xmms-faad2 xmms-flac xmms-pulse \`
`xmms-skins audacious audacious-plugins-freeworld* rhythmbox \`
`gstreamer-plugins-ugly gstreamer-plugins-bad gstreamer-ffmpeg \`
`gstreamer-plugins-bad-nonfree amarok xine-lib-extras-freeworld`

Installare i Media Players
--------------------------

Fedora ha un numero limitato di lettori sia Audio che Video. Per il video e il multimedia (DVD, etc.) faremo anche qui uso di repository di terze parti: [RPMFusion](RPMFusion "wikilink"). Accertati di avere configurato il repository RPMFusion prima di procedere. Nota che le molte dipendenze in librerie, plugins e codecs sono condivisi tra queste applicazioni oltre che con i lettori MP3.
I media player più famosi sono i seguenti. Ognuno di questi ha i propri punti di forza. Installa quello che preferisci, sebbene almeno *MPlayer* e *VLC* sono raccomandati.

### Mplayer

Mplayer è disponibile sia in una versione a riga di comando (mplayer) sia in una versione GUI, anch'essa con il potente tool di encoding Mencoder (molto valido per il ripping o la compressione audio/video). In aggiunta esiste un plugin per il web, molto funzionale, che permette la riproduzione di molti formati popolari in Firefox/Mozilla (WMV, QuickTime, etc).
Installazione con yum, con [RPMFusion](RPMFusion "wikilink") abilitato:

`[mirandam@charon ~]$ sudo yum install mplayer mplayer-gui gecko-mediaplayer mencoder`

-   Da notare che mencoder è opzionale ma fornisce molte opzioni di decodifica.
-   **Binary Codecs:** Per favore installa i [Binary Codecs](http://www.mjmwired.net/resources/mjm-fedora-f17.html#binarycodecs) per un maggiore supporto di formati che MPlayer non supporta nativamente.
-   MPlayer dovrebbe funzionare con le impostazioni di default di Pulse Audio.

### Xine

Xine è simile, per molti aspetti, ad MPlayer, ma manca delle applicazioni a riga di comando e dell'encoder. Comunque ha un pieno supporto del DVD playback e una buona usabilità.
Installazione con yum, con [RPMFusion](RPMFusion "wikilink") abilitato:

`[mirandam@charon ~]$ sudo yum install xine xine-lib-extras xine-lib-extras-freeworld`

**Binary Codecs:** Per favore installa i [Binary Codecs](http://www.mjmwired.net/resources/mjm-fedora-f17.html#binarycodecs) per un maggiore supporto di formati che Xine non supporta in maniera nativa. **DVD Playback:** Per riprodurre correttamente i DVD leggi DVD Playback poche righe più giù.

### Banshee

Banshee è un player simile a iTunes che supporta la sincronizzazione con molti altri dispositivi.
Installazione con yum, con [RPMFusion](RPMFusion "wikilink") abilitato:

`[mirandam@charon ~]$ sudo yum install banshee gstreamer-plugins-ugly gstreamer-plugins-bad gstreamer-ffmpeg`

### Binary Codecs

MPlayer projects mantiene un package completo di codecs binary, per i quali non esiste una diretta opzione open source, alcuni di questi file includono Window's DLL. Questi sono condivisi sia da Xine che da Mplayer.

-   Andare su : [<http://www.mplayerhq.hu/MPlayer/releases/codecs>](http://www.mplayerhq.hu/MPlayer/releases/codecs/)
-   Selezionare il package (.tar.bz2) che corrisponde alla tua versione di Fedora. Molti utenti 32-bit useranno: [all-20110131.tar.bz2](http://www.mplayerhq.hu/MPlayer/releases/codecs/all-20110131.tar.bz2)
-   Installare i codecs:

`[mirandam@charon Download]$ sudo mkdir -p /usr/lib/codecs`
`[mirandam@charon Download]$ sudo tar -jxvf all-20071007.tar.bz2 --strip-components 1 -C /usr/lib/codecs/`

### VLC

VLC è un semplice media player con una interfaccia molto semplice da usare. Supporta anche il DVD playback. Benchè molte esigenze sarebbero accontentate con Xine e Mplayer, alcuni preferiscono VLC.
Installazione con yum, con [RPMFusion](RPMFusion "wikilink") abilitato:

`[mirandam@charon ~]$ sudo yum install vlc`

### DVD Playback

Per ragioni non-tecniche il pacchetto *libdvdcss* esiste solo sul repository di ATrpms.

-   Configurare il repo di ATrpms:

`[mirandam@charon Download]$ wget `[`http://www.mjmwired.net/resources/files/atrpms.repo`](http://www.mjmwired.net/resources/files/atrpms.repo)
`[mirandam@charon Download]$ sudo cp ./atrpms.repo /etc/yum.repos.d/atrpms.repo`
`[mirandam@charon Download]$ sudo rpm --import `[`http://packages.atrpms.net/RPM-GPG-KEY.atrpms`](http://packages.atrpms.net/RPM-GPG-KEY.atrpms)

-   Installare il pacchetto:

\[mirandam@charon ~\]$ sudo yum --enablerepo=atrpms install libdvdcss

Installare i font TrueType di Microsoft
---------------------------------------

Il sito ufficiale per questo pacchetto è [<http://corefonts.sourceforge.net>](http://corefonts.sourceforge.net/), ma comunque sto utilizzando questo [SPEC file](http://www.mjmwired.net/resources/files/msttcore-fonts-2.0-3.spec).
Per mia comodità ho creato il pacchetto RPM msttcorefonts-2.0-3.noarch.rpm (*non linkare direttamente a questo link*):

[msttcore-fonts-2.0-3.noarch.rpm](http://www.mjmwired.net/resources/files/msttcore-fonts-2.0-3.noarch.rpm)

`[mirandam@charon Download]$ sudo rpm -ivh msttcore-fonts-2.0-3.noarch.rpm`

Fedora incoraggia l'uso dei [Liberation Fonts](https://www.redhat.com/promo/fonts/). Tali font dovrebbero essere già installati come impostazione predefinita (e inclusi nel DVD).

Installare Google Chrome
------------------------

Google Chrome è un browser ben mantenuto e aggiornato. Lo consiglio fortemente. Uno dei vantaggi di Chrome è che non è strettamente integrato a una versione specifica di Fedora (come per esempio lo è Firefox).

1.  Installare il repository di Google Chrome

\[mirandam@charon Download\]$ wget <http://www.mjmwired.net/resources/files/google-chrome.repo>

`[mirandam@charon Download]$ sudo cp ./google-chrome.repo /etc/yum.repos.d/google-chrome.repo`
`[mirandam@charon Download]$ sudo rpm --import `[`https://dl-ssl.google.com/linux/linux_signing_key.pub`](https://dl-ssl.google.com/linux/linux_signing_key.pub)

<li>
Installare Google Chrome

</li>
`[mirandam@charon Download]$ sudo yum install google-chrome-stable`

</ol>
Per utenti che necessitano di una versione più nuova, instabile o beta, il comando precedente può essere modificato con *beta* o *unstable*. **Questo NON è raccomandato**.

**ALTERNATIVA: Open Source Google Chrome: Chromium**

Alcuni utenti probabilmente preferiscono una versione completamente open source di Chrome: Chromium. Chromium è prodotto specificatamente per Fedora, per cui sarà più veloce, utilizzerà più componenti condivisi del sistema e potrà essere ottimizzato con impostazioni migliori. *Questa versione, comunque, non sempre è l'ultima. Potrebbe non essere raccomandata per tutti gli utenti*.

Sia Chrome che Chromium possono coesistere sullo stesso sistema senza andare in conflitto.

1.  Installare il repository Chromium di "Spot"

\[mirandam@charon Download\]$ wget <http://repos.fedorapeople.org/repos/spot/chromium-stable/fedora-chromium-stable.repo>

`[mirandam@charon Download]$ sudo cp ./fedora-chromium-stable.repo /etc/yum.repos.d/fedora-chromium-stable.repo`

<li>
Installare Chromium

</li>
`[mirandam@charon Download]$ sudo yum install chromium`

</ol>
Ulteriori informazioni su Chromium sono disponibili sul [Fedora Wiki](http://fedoraproject.org/wiki/Chromium). Chromium può coesistere con Google Chrome.

Adobe Flash Plugin
------------------

Il plugin per Adobe Flash può essere installato dal sito web di Adobe. Gli utenti dovrebbero utilizzare il repository YUM di Adobe. (raccomandato)

1.  **Installare il repository di Adobe**

**32-bit**

`[mirandam@charon Download]$ sudo rpm -ivh `[`http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm`](http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm)
`[mirandam@charon Download]$ sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux`

**64-bit**

`[mirandam@charon Download]$ sudo rpm -ivh `[`http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm`](http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm)
`[mirandam@charon Download]$ sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux`

<li>
**Installare il Flash Plugin**

</li>
`[mirandam@charon Download]$ sudo yum install flash-plugin`

Riavviare Firefox o altri browser Mozilla.

</ol>
Ulteriori informazioni sono disponibili sul [Fedora Wiki](https://fedoraproject.org/wiki/Flash).

Java Runtime Environment
------------------------

Fedora dovrebbe supportare Java con *OpenJDK* (basato su Sun Java) e il web plugin Icedtea. In caso contrario può essere installato con yum:

`[mirandam@charon ~]$ sudo yum install java-1.7.0-openjdk icedtea-web`

Con OpenJDK installato, le applicazioni e le applet Java dovrebbero funzionare automaticamente. Potrebbe essere che alcuni applet non funzionano correttamente, proprio perchè OpenJDK ha ancora qualche limite.*Gran parte degli utenti dovrebbero apprezzare OpenJDK nell'uso quotidiano*.

### Usare invece Sun Java

Se preferisci il *Sun Java* o se OpenJDK non funziona correttamente, puoi scaricare Sun Java ed usarlo con Fedora.
Download del pacchetto Java da: [<http://www.oracle.com/technetwork/java/javase/downloads/index.html>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
Sotto *Java Platform, Standard Edition* seleziona: **Download JRE** (JDK è per sviluppatori)
Alla pagina successiva accetta l'accordo di Licenza:

Per utenti 32-bit: seleziona "Linux **x86**"
jre-7u5-linux-i586.**rpm**

Per utenti 64-bit: seleziona "Linux **x64**"
jre-7u5-linux-x64.**rpm**

Installazione:

`[mirandam@charon Download]$ sudo rpm -ivh jre-7u5-linux-i586.rpm`
`-O-`
`[mirandam@charon Download]$ sudo rpm -ivh jre-7u5-linux-x64.rpm`

Quando si esegue un comando *java*, Fedora preferisce usare OpenJDK, per usare il Sun Java si usi il comando *alternatives*:

`[mirandam@charon Download]$ sudo /usr/sbin/alternatives --install /usr/bin/java java /usr/java/default/bin/java 20000`

Lo stesso è da applicare al Mozilla/Firefox Plugin:

Per **sistemi a 32 bit**

`[mirandam@charon Download]$ sudo /usr/sbin/alternatives --install /usr/lib/mozilla/plugins/libjavaplugin.so \`
`libjavaplugin.so /usr/java/default/lib/i386/libnpjp2.so 20000`

Per **sistemi a 64 bit**

`[mirandam@charon Download]$ sudo /usr/sbin/alternatives --install /usr/lib64/mozilla/plugins/libjavaplugin.so \`
`libjavaplugin.so.x86_64 /usr/java/default/lib/amd64/libnpjp2.so 20000`

Potrebbe essere necessario riavviare Firefox.
**Nota**: Se desideri ritornare ad *OpenJDK* puoi eseguire i seguenti comandi per passare da Sun a OpenJDK.

`[mirandam@charon ~]$ sudo /usr/sbin/alternatives --config java`
`[mirandam@charon ~]$ sudo /usr/sbin/alternatives --config libjavaplugin.so`
`(o per 64-bit)`
`[mirandam@charon ~]$ sudo /usr/sbin/alternatives --config libjavaplugin.so.x86_64`

*Per fare l'update:* se fai l'update del pacchetto JRE, scarica semplicemente il pacchetto RPM e installalo. Non serve utilizzare il comando *alternatives* in quanto le impostazioni rimangono intatte. Il comando seguente contiene tutto quello che servirà:

`[mirandam@charon Download]$ sudo rpm -ivh jre-7u6-linux-x64.rpm`

Ulteriori informazioni: [Install Documentation for Linux](http://www.oracle.com/technetwork/java/javase/manual-plugin-install-linux-136395.html)

Installare Adobe Acrobat
------------------------

Per visualizzare i file PDF, Fedora raccomanda l'utilizzo di *evince* o *okular*. Il seguente è indirizzato a utenti che necessitano di Adobe Acrobat Reader.
Per utenti Yum:
Installare il repository di Adobe e poi il Reader:

`[mirandam@charon Download]$ sudo rpm -ivh `[`http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm`](http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm)
`[mirandam@charon Download]$ sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux`
`[mirandam@charon Download]$ sudo yum install AdobeReader_enu`

Per altre lingue l'installazione è simile: AdobeReader\_fra Se non sei sicuro del nome esatto cercalo con:
*yum info AdobeReader\_fra*
Altrimenti installalo manualmente. (**NOTA**: utenti 64 bit dovrebbero sempre usare yum per risolvere tutte le dipendenze necessarie 32 bit).
La versione corrente di Adobe Acrobat è la 9.x e il file da scaricare varia in funzione della lingua. Non tutte le lingue sono supportate nella versione per Linux.

Configurare Samba - Condividere file con Windows
------------------------------------------------

Se si possiedono computer con Windows installato o una Lan e si vuole condividere file tra macchine Windows e Linux, bisogna configurare Samba. Per configurare samba occorre: (1) installare Samba, (2) aggiungere le 'shares' (risorse condivise), (3) aggiungere gli utenti, (4) avviare il servizio Samba e (5) impostare le opzioni di sicurezza (Firewall e SELinux).

### Installare Samba

`[mirandam@charon ~]$ sudo yum install samba samba-client cifs-utils`

### Aggiungere 'Shares'

Bisogna editare **/etc/samba/smb.conf** come root: (usando *nano* al posto di *gedit* se non si utilizza una GUI)

`[mirandam@charon ~]$ sudo gedit /etc/samba/smb.conf`

Definire il nome del Windows Workgroup nella sezione \[global\].
Aggiungere le shares alla fine del file. Ad esempio:

    [c_drive]
       path = /media/c_drive
       public = yes
       writable = no
    [netshare]
       path = /data/
       public = yes
       writable = yes

Se si definisce come 'writable' (scrivibile), la risorsa **deve essere** scrivibile prima su Linux. I permessi addizionali devono corrispondere (esempio: *drwxrw-rw*).
Se i dati della directory home (tutti i file personali sotto */home/nomeutente*) devono essere accessibili, bisogna indicare 'browseable = yes' sotto \[homes\] (~riga 279).
Il file di configurazione è *molto descrittivo*, occorre leggerlo da cima a fondo per avere maggiori idee o informazioni.

### Aggiungere gli utenti

Per avere accesso alle shares, bisogna essere degli utenti definiti. Aggiungere *utenti e password* valide usando il comando *smbpasswd*.
Tali parametri SARANNO il nome utente e la password da usare per il login **da Windows** per accedere al computer Linux. La password **NON deve necessariamente coincidere** con la password Linux.

`[mirandam@charon ~]$ sudo smbpasswd -a username`
`New SMB password:`
`Retype new SMB password:`
`Added user username.`

### Avviare il servizio Samba

`[mirandam@charon ~]$ sudo systemctl start smb.service nmb.service`

Rendere effettivo l'avvio di Samba ad ogni avvio di Fedora.

`[mirandam@charon ~]$ sudo systemctl enable smb.service nmb.service`

Riavviare Samba per ogni cambiamento a utenti/password od a *smb.conf*:

`[mirandam@charon ~]$ sudo systemctl restart smb.service`

### Gestione sicurezza per Samba

**Firewall**

Il Firewall di default bloccherà Samba, per permettergli l'accesso digita:

`[mirandam@charon ~]$ system-config-firewall`

Per abilitare Samba a lavorare attraverso il proprio firewall, bisogna configurare 'Samba' come un 'Servizio fidato' e confermarlo con 'Applica'. In alternativa, e se non si ha accesso a un server grafico bisogna digitare nel terminale:

`[mirandam@charon ~]$ sudo system-config-firewall-tui`

Per abilitare Samba a lavorare attraverso il proprio firewall, utilizza il tasto <TAB> per scendere fino alla voce *personalizza*. Nei 'servizi fidati' seleziona 'Samba' e premi il tasto <TAB> fino a poter dare *OK*.

**SELinux**

SELinux ha un *controllo significativo* su Samba e ne limita differenti parti. Si avvii *system-config-selinux*. Per favore si leggano le righe \#20 - \#59 in */etc/samba/smb.conf* per una migliore spiegazione. In alternativa si può digitare:

`[mirandam@charon ~]$ system-config-selinux`

Selezionare *Boolean* e digitare *Samba* nel filtro.
Se si ottiene il seguente errore:

`bash: system-config-selinux: command not found...`

prima bisogna eseguire:

`$ sudo yum install policycoreutils-gui`

Per attivare ogni cambiamento apportato alla configurazione di SELinux o di smb.conf, è raccomandato riavviare Samba.

Ulteriori informazioni
----------------------

------------------------------------------------------------------------

Commenti, suggerimenti, domande o qualunque altro contributo a questa o a una qualunque delle [altre mie pagine](http://www.mjmwired.net/resources.php) sono ben accetti. Per favore usate il seguente [link](http://www.mjmwired.net/contact.php) per contattarmi.
Aiutatemi: se avete trovato questa guida o ogni altra risorsa collegata utile, per favore considerate di aiutare il mio sito raccomandando questa pagina ad altri o linkandola. Io apprezzo tutto il supporto che posso ricevere. Grazie in anticipo.
Potete anche scegliere di donare qualcosa con [Amazon.com wishlist](http://www.amazon.com/gp/registry/registry.html/ref=wlem-si-ht_gotowl/103-7306043-1450224?id=2EPXY2P66KUM1)

**Disclaimer:** The author makes no claim to the accuracy of the information provided. This information is provided in the hope that it will be useful, but WITHOUT ANY WARRANTY. There is no implied support from referencing this guide. Any help that is provided is at will. Use this information at your own risk. Always make proper backups and use caution when modifying critical system files.
**PER FAVORE NON** fate copie in mirror, traducete o copiate questa pagina *senza* contattarmi. Io ho speso diverse ore di lavoro personalmente per ricercare e verificare quanto è qui riportato.

[**Copyright © 2003-2011**](http://www.mjmwired.net/about.php#copyright) **by Mauriat Miranda** (mjmwired.net).

<Categoria:Traduzioni>
