Introduzione
------------

I driver per le schede video ati NON funzionano per schede del tipo *9250* e precedenti. Si consiglia, se non si ha assoluta necessità, di non installarli, perchè trattasi sempre di software non GPL.

Installazione
-------------

L'installazione viene seguita tramite Yum:

`# yum install akmod-fglrx xorg-x11-drv-fglrx xorg-x11-drv-fglrx-libs.i386`

Ora bisogna lanciare system-config-display:

`# system config-display`

Premere semplicemente *ok* per creare ***xorg.conf***. Se *system-config-display* non è presente nel sistema, bisognerà prima installarlo:

`# yum install system-config-display`

Configurazione
--------------

`# aticonfig --initial -f`
`# gedit /etc/X11/xorg.conf`

Aggiungere alla sezione *Device*:

    Option "OpenGLOverlay" "off"
    Option "VideoOverlay" "on"

    aggiungere in coda

    Section "Extensions"
    Option "Composite" "Enable"
    EndSection


    Section "ServerFlags"
    Option "AIGLX" "on"
    EndSection

    Section "DRI"
    Mode 0666
    EndSection

In alcuni casi è necessario aggiungere alla sezione *Screen* la risoluzione da adottare: ***'Modes "1280x1024" "1024x768"*** oppure quella supportata dal vostro monitor.

Modifica del boot
-----------------

Spostare il ramdisk, mantenendone una copia di sicurezza, con i seguenti comandi:

`` # mv /boot/initrd-`uname -r`.img /boot/initrd-`uname -r`.img.backup ``

Dopodiché si ricostruisce il Ramdisk:

`` # mkinitrd -v /boot/initrd-`uname -r`.img  `uname -r` ``

Poi:

`# gedit /boot/grub/grub.conf`

Aggiungere alla linea del kernel l'opzione: ***nopat***.
Se ci sono errori al boot riguardanti le librerie *libdrm* aggiungere anche : ***nomodeset***.

Ora si può dare un restart del sistema e godersi la scheda Ati.

[Categoria:Schede grafiche](Categoria:Schede_grafiche "wikilink")
