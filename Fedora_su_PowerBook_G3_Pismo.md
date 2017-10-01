INSTALLAZIONE GRAFICA
---------------------

E' possibile fare l'installazione grafica, anche se durante tutta la procedura lo schermo non si vede centrato.
A fine installazione basta lanciare **system-config-display** da una finestra di terminale e reimpostare lo schermo come "LCD Panel 1024x768" dall'elenco dei Generic LCD Display. Oppure dall'elenco di monitor Apple il modello "Apple PowerBook G3 Series (1999-2000)".
In realtà la seconda opzione l'ho provata, ma l'impostazione non viene mantenuta e la risoluzione dello schermo viene sempre impostata come troppo larga, ma non ho insistito con le prove perché con l'impostazione schermo generico tutto funziona bene.

TASTO DESTRO DEL TRACKPAD
-------------------------

Per il tasto destro del trackpad (che non c'è perché i computer Apple hanno mouse e trackpad monotasto) è possibile utilizzare il tasto command (mela) oppure F12 aggiungendo le seguenti righe al file **/etc/sysctl.conf**

`# Emulate the middle mouse button with F11 and the right with F12.`
`#dev/mac_hid/mouse_button_emulation = 1`
`#dev/mac_hid/mouse_button2_keycode = 87`
`#dev/mac_hid/mouse_button3_keycode = 88`
`dev/mac_hid/mouse_button3_keycode = 125`
`dev/mac_hid/mouse_button2_keycode = 126`
`dev/mac_hid/mouse_button_emulation = 1`

Inoltre per attivare o disattivare il tap sul trackpad modificare il file **/etc/sysconfig/trackpad** modificando la riga **TRACKPAD\_OPT=tap** in **TRACKPAD\_OPT=notap**

PERSONALIZZARE IL TRACKPAD
--------------------------

Ho trovato cercando su google alcune impostazioni che vanno aggiunte al file **/etc/X11/xorg.conf** che dovrebbero servire a personalizzare il comportamento del trackpad, non le ho provate, ma le riporto in caso possano servire, si riferivano a Fedora 5.
Purtroppo ho salvato solo il testo e non la fonte da cui provengono, me ne scuso con l'autore.

Sono necessari i driver synaptics, che possono essere installati col comando **yum install synaptics**

Inserire la seguente riga (quella in grassetto "InputDevice") nella sezione "ServerLayout" di /etc/X11/xorg.conf

`Section "ServerLayout"`
`…`
**`InputDevice` `"TouchPad"`**
`…`
`EndSection`

Poi aggiungere le righe seguenti di seguito nel file

`Section "InputDevice"`
`Identifier "TouchPad"`
`Driver "synaptics"`
`Option "SendCoreEvents" "true"`
`Option "Device" "/dev/input/mice"`
`Option "Protocol" "auto-dev"`
`Option "LeftEdge" "0"`
`Option "RightEdge" "850"`
`Option "TopEdge" "0"`
`Option "BottomEdge" "645"`
`Option "MinSpeed" "0.4"`
`Option "MaxSpeed" "1.5"`
`Option "AccelFactor" "0.05"`
`Option "FingerLow" "55"`
`Option "FingerHigh" "60"`
`Option "HorizScrollDelta" "0"`
`Option "VertScrollDelta" "30"`
`Option "UseShm" "true"`
`Option "SHMConfig" "on"`
`EndSection`

Riporto cosa dovrebbe succedere ma non ho provato il tutto:
Dovrebbe essere possibile scorrere le finestre usando la parte di destra del trackpad, simulare un tasto centrale facendo tap con due dita e il tasto destro facendo tap con tre dita.
I valori di MinSpeed, MaxSpeed e AccelFactor possono essere modificati per variare le velocità e l'accelerazione del puntatore.
Infine inserendo le seguenti righe dovrebbe essere possibile disabilitare il tap singolo e usare solo il tasto per farlo, e simulare il click destro facendo tap con due dita invece che tre.

`Option "TapButton2" "3"`
`Option "TapButton3" "2"`
`Option "MaxTapMove" "0"`

TASTIERA QZERTY
---------------

Per scegliere la tastiera **qzerty** invece che **qwerty** bisogna aggiungere l'applet "indicatore tastiera" sulla barra di gnome. Dall'indicatore tastiera poi è possibile sia scegliere il layout giusto (disposizioni--&gt; aggiungi--&gt; Italia--&gt; varianti: Macintosh), sia correggere un bug nel riconoscimento tastiera che inverte i tasti "@\#" con "&lt;&gt;" per fare questo bisogna scegliere il tab "opzioni di disposizione" e poi il gruppo "opzioni varie di compatibilità" e selezionare la voce "swap keycodes of two keys when Mac keyboards are misdetected by kernel"

Il **tasto Alt di destra** viene riconosciuto come se fosse il sinistro, per poterlo usare va premuto prima Fn (=Function) poi Alt destro e poi rilasciato Fn, continuando a tenere premuto Alt destro.
In questo modo il tasto Alt di destra può essere usato come selettore di terza posizione (il tasto AltGr delle tastiere PC) **ctrl+alt+F1** e **ctrl+alt+F7**.
Queste due combinazioni di tasti sono utili rispettivamente per passare in modalità testo e tornare in modalità grafica, per evitare che la pressione del tasto F1 venga interpretata come "diminuire la luminosità" bisogna prima premere ctrl+alt e poi contemporaneamente il tasto Fn e infine F1 o F7.

### Spiegazioni aggiuntive

Per aggiungere l'indicatore tastiera: click col tasto destro sulla barra di gnome e poi scegliere "aggiungi al pannello" e poi la voce "indicatore tastiera".
Infine cliccando col tasto destro su indicatore tastiera è possibile impostare le varie preferenze.

SCHEDA AUDIO
------------

Funziona e viene riconosciuta bene, ma per qualche motivo il driver poi non viene caricato in automatico.
Per fare il test dell'audio si può lanciare da una finestra di terminale il programma **system-config-soundcard**.
Per forzare il caricamento all'avvio aggiungere la seguente riga nel file **/etc/rc.d/rc.local**

`/sbin/modprobe snd-powermac`

ASCOLTARE MP3
-------------

E' possibile installare i vari codec dal repository livna tramite i pacchetti gstreamer-plugins\* e gstreamer-ffmpeg da liva si può installare anche il player audio/video VLC.
Livna fa conflitto in alcuni casi con freshrpms, quindi va tenuto disattivato e abilitato con yum solo per le installazioni necessarie.
Come lettore mutlimediale mi sembra molto buono Rhythmbox, che permette anche di leggere MP3 direttamente da un iPod (provato con iPod nano 2nd gen).

### Spiegazioni aggiuntive

yum è un comando che serve a installare e rimuovere software, va a cercare i pacchetti e le loro dipendenze su vari siti detti repository (=repo), per configurare il repo livna bisogna aggiungere il seguente file di testo nella cartella **/etc/yum.repos.d** il nome del file deve essere **livna.repo** e il contenuto il seguente:

`[livna]`
`name=Livna for Fedora Core $releasever - $basearch - Base`
`baseurl=`
`        `[[`http://rpm.livna.org/fedora/$releasever/$basearch/`](http://rpm.livna.org/fedora/$releasever/$basearch/)](http://rpm.livna.org/fedora/$releasever/$basearch/)
`        `[[`http://livna.cat.pdx.edu/fedora/$releasever/$basearch/`](http://livna.cat.pdx.edu/fedora/$releasever/$basearch/)](http://livna.cat.pdx.edu/fedora/$releasever/$basearch/)
`        `[[`http://wftp.tu-chemnitz.de/pub/linux/livna/fedora/$releasever/$basearch/`](http://wftp.tu-chemnitz.de/pub/linux/livna/fedora/$releasever/$basearch/)](http://wftp.tu-chemnitz.de/pub/linux/livna/fedora/$releasever/$basearch/)
`        `[[`http://ftp-stud.fht-esslingen.de/pub/Mirrors/rpm.livna.org/fedora/$releasever/$basearch/`](http://ftp-stud.fht-esslingen.de/pub/Mirrors/rpm.livna.org/fedora/$releasever/$basearch/)](http://ftp-stud.fht-esslingen.de/pub/Mirrors/rpm.livna.org/fedora/$releasever/$basearch/)
`        `[[`http://mirror.atrpms.net/livna/fedora/$releasever/$basearch/`](http://mirror.atrpms.net/livna/fedora/$releasever/$basearch/)](http://mirror.atrpms.net/livna/fedora/$releasever/$basearch/)
`        `[[`ftp://mirrors.tummy.com/pub/rpm.livna.org/fedora/$releasever/$basearch/`](ftp://mirrors.tummy.com/pub/rpm.livna.org/fedora/$releasever/$basearch/)](ftp://mirrors.tummy.com/pub/rpm.livna.org/fedora/$releasever/$basearch/)
`failovermethod=priority`
`#mirrorlist=`[`http://rpm.livna.org/mirrorlist-7`](http://rpm.livna.org/mirrorlist-7)
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-livna`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-livna)

La riga **enabled=0** significa che il repo non è abilitato, quindi non viene usato per cercare software se non richiesto al momento di lanciare il comando yum.
Quindi per installare vlc e i codec scrivere **yum --enablerepo=livna vlc gstreamer-plugins\* gstreamer-ffmpeg**

IBERNAZIONE E SOSPENSIONE
-------------------------

Funzionano, ma il modulo firewire non è compatibile con la ripresa dell'attività (credo sia una pecca di Fedora purtroppo, perchè con la distribuzione YellowDog funziona senza problemi), quindi bisogna disattivarlo prima di sospendere o ibernare.
Tramite il comando **/sbin/rmmod firewire\_ohci** si può rimuovere il modulo, e se serve il firewire ricaricarlo con **/sbin/modprobe firewire\_ohci**.
Sicuramente c'è un modo più elegante per far caricare il modulo in modo automatico all'inserimento di una periferica firewire, ma non ho cercato informazioni in proposito.

UPDATEDB
--------

In Fedora 8 per architettura powerpc il comando updatedb (utile per aggiornare il database di ricerca su cui si basa il comando locate) ha un bug per cui se lanciato semplicemente come updatedb esce con un errore:

`` updatedb: src/updatedb.c:730: scan_cwd: Asserzione `name_size > 1' fallita. ``
`Abortito`

Per evitare questo bisogna usare l'opzione **updatedb --prunepaths /sys** invece che semplicemente updatedb.

NOTE:
-----

Per apportare modifiche ai file di configurazione bisogna essere utente root (amministratore), i file di configurazione sono dei semplici file di testo, modificabili con programmi come **vi**, **nano** o **gedit**.
Per diventare root scrivere **su** in una finestra di terminale, dare invio e poi inserire la password di root.

<Categoria:Hardware>
