\_\_TOC\_\_

Introduzione
------------

Spesso capita a molti principianti nel momdo del pinguino che restano legati a vecchie distribuzioni, perchè sono soddisfatti del lavoro svolto e non vogliono rovinarlo. Per paura che il nuovo prodotto non dia le stesse soddisazioni restano congelati.
Questo articolo vuole incoraggiare i nuovi utenti ad andare avanti senza rovinare il sistema funzionante.

Procedura di installazione
--------------------------

Come descritto nel titolo, tre sistemi operativi sullo stesso HD: una installazione di Windows XP e due distribuzioni di fedora.
Come procedere per avere i tre sistemi utilizzabili senza problemi:

1.  Installare Windows XP (deve necessariamente essere il primo ad essere installato): ovviamente se si ha voglia di metterci anche Fedora non bisogna far occupare tutto l'HD. Qui si può leggere come partizionare senza riempire l'HD:
    <http://www.megalab.it/articoli.php?id=220&pagina=2>
    Se Windows occupa già tutto l'HD, utilizzando gparted, si ha la possibilità di restringerlo a proprio piacimento lasciando spazio non allocato per installare fedora. Qui il manuale *gparted*: <http://www.nerio.it/linux/aulataliercio/distro/fedoracore6/>
2.  Ora è installato il primo sistema, e si ha spazio non allocato sul disco fisso. Per non riempire tutto lo spazio non allocato con Fedora si utilizza sempre *gparted*. Con gparted si crea una nuova partizione nello spazio non allocato, e definendola in fat32 ,così da ottenere al centro delle due partizioni esistenti, lo spazio non allocato per il II sistema da installare (esempio fc7).
3.  Ora è installato fc7 in dualboot con Windows.

Si può avviare Fedora e con l'aiuto del nostro terminale da root digitare:

`# gedit /boot/grub/grub.conf`

Si aprirà il grub.conf generato da anaconda.

`# grub.conf generated by anaconda`
`#`
`# Note that you do not have to rerun grub after making changes to this file`
`# NOTICE:  You have a /boot partition.  This means that`
`#          all kernel and initrd paths are relative to /boot/, eg.`
`#          root (hd0,1)`
`#          kernel /vmlinuz-version ro root=/dev/VolGroup00/LogVol00`
`#          initrd /initrd-version.img`
`#boot=/dev/sda`
`default=0`
`timeout=5`
`splashimage=(hd0,1)/grub/splash.xpm.gz`
`hiddenmenu`
`title Fedora (2.6.22.1-41.fc7)`
`    root (hd0,1)`
`    kernel /vmlinuz-2.6.22.1-41.fc7 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`    initrd /initrd-2.6.22.1-41.fc7.img`
`title Fedora (2.6.21-1.3194.fc7)`
`    root (hd0,1)`
`    kernel /vmlinuz-2.6.21-1.3194.fc7 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`    initrd /initrd-2.6.21-1.3194.fc7.img`
`title Other`
`    rootnoverify (hd0,0)`
`    chainloader +1`

<li>
Ora prima di lanciare fc8 come III sistema con gparted si dovrà eliminare la partizione in fat32 e rendere lo spazio non allocato, così con l'aiuto di anaconda si installerà anche fc8.

</li>
Il nuovo grub generato da anaconda ha sovrascritto il vecchio di fc7, ma la copia dell'altro grub.conf è sulla penna USB! Bene:stessa procedura da root:

`# gedit /boot/grub/grub.conf`

Nel grub.conf dovranno essere aggiunte le seguenti righe prelevate dal grub.conf di fc7 salvato sulla pen drive. Le righe da copiare sono le seguenti:

`title Fedora (2.6.22.1-41.fc7)`
`    root (hd0,1)`
`    kernel /vmlinuz-2.6.22.1-41.fc7 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`    initrd /initrd-2.6.22.1-41.fc7.img`
`title Fedora (2.6.21-1.3194.fc7)`
`    root (hd0,1)`
`    kernel /vmlinuz-2.6.21-1.3194.fc7 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`    initrd /initrd-2.6.21-1.3194.fc7.img`

Il grub.conf che si otterrà è il seguente:

`# grub.conf generated by anaconda`
`#`
`# Note that you do not have to rerun grub after making changes to this file`
`# NOTICE:  You have a /boot partition.  This means that`
`#          all kernel and initrd paths are relative to /boot/, eg.`
`#          root (hd0,1)`
`#          kernel /vmlinuz-version ro root=/dev/VolGroup00/LogVol00`
`#          initrd /initrd-version.img`
`#boot=/dev/sda`
`default=0`
`timeout=5`
`splashimage=(hd0,1)/grub/splash.xpm.gz`
`hiddenmenu`
`title Fedora (2.6.23.9-85.fc8)`
`    root (hd0,1)`
`    kernel /vmlinuz-2.6.23.9-85.fc8 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`    initrd /initrd-2.6.23.9-85.fc8.img`
`title Fedora (2.6.23.1-42.fc8)`
`    root (hd0,1)`
`    kernel /vmlinuz-2.6.23.1-42.fc8 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`    initrd /initrd-2.6.23.1-42.fc8.img`
`title Fedora (2.6.22.1-41.fc7)`
`    root (hd0,1)`
`    kernel /vmlinuz-2.6.22.1-41.fc7 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`    initrd /initrd-2.6.22.1-41.fc7.img`
`title Fedora (2.6.21-1.3194.fc7)`
`    root (hd0,1)`
`    kernel /vmlinuz-2.6.21-1.3194.fc7 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`    initrd /initrd-2.6.21-1.3194.fc7.img`
`title Other`
`    rootnoverify (hd0,0)`
`    chainloader +1 `

Ovviamente prima di chiudere il grub.conf è necessario salvare le modifiche. Al prossimo reboot del sistema sul vostro splash screen di fedora 8 potete fare il boot di fc7.

</ol>
<Categoria:Installazione> [Categoria:Fedora Legacy](Categoria:Fedora_Legacy "wikilink")
