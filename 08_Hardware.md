Come fare funzionare il chip wireless Intel IPW2200 b,g
-------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink") Scarica [il firmware](http://ipw2200.sourceforge.net/firmware.php?fid=6), accetta la licenza d'uso e salva il file sul tuo desktop; quindi apri un terminale e digita quanto segue:

mkdir tmp

`mv ~/Desktop/*-2.4.tgz ~/tmp `
`cd tmp`
`tar -zxvf ipw2200-fw-2.4.tgz`
`cp * /lib/firmware`
`rmmod ipw2200`
`modprobe ipw2200`
`iwconfig`

dovresti vedere un access point. Puoi utilizzare Network Manager per controllare la tua attività wireless

<li>
Leggi [Network manager per Gnome](04_Aggiungere_Applicazioni#Network_manager_per_Gnome "wikilink")

</li>
</ol>
Come installare i driver della scheda grafica (NVIDIA)
------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install nvidia-glx kernel-module-nvidia-$(uname -r)

<li>
Leggi [Come riavviare GNOME senza riavviare il computer](15_Trucchi_vari#Come_riavviare_GNOME_senza_riavviare_il_computer "wikilink")

</li>
<li>
In caso di problemi leggi nV News sul forum \[<http://www.nvnews.net/vbulletin/forumdisplay.php?s>=&forumid=14 "Linux and nVidia Graphics"\]

</li>
</ol>
Come installare i driver della scheda grafica (ATI)
---------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install ati-fglrx kernel-module-fglrx-$(uname -r)

<li>
Se possiedi una motherboard Intel, dovrai modificare il tuo xorg.conf dopo avere installato i drivers:

</li>
`gedit /etc/X11/xorg.conf`

<li>
Trova la seguente riga

</li>
`Driver "fglrx"`

<li>
Aggiungi la riga seguente

</li>
`Option "UseInternalAGPGART" "no"`

</ol>
Come identificare il chipset del tuo modem
------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare un Compilatore](04_Aggiungere_Applicazioni#Come_installare_un_Compilatore "wikilink")

wget -c <http://easylinux.info/uploads/scanModem.gz>

`gunzip -c scanModem.gz > scanModem`
`chmod +x scanModem`
`cp scanModem /usr/bin/`

<li>
Per identificare il chipset del modem

</li>
`scanModem`
`gedit Modem/ModemData.txt`

</ol>
Come vedere il contenuto della tabella delle partizioni
-------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

fdisk -l

</ol>
Come vedere lo spazio usato su disco dal filesystem
---------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

df -T -h

</ol>
Come vedere quali dispositivi sono montati
------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

mount

</ol>
Come elencare i dispositivi PCI
-------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

lspci

</ol>
Come elencare i dispositivi USB
-------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

lsusb

</ol>
Come incrementare la velocità del CD/DVD-ROM
--------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

'' Assumiamo che /dev/cdrom sia il CD/DVD-ROM ''

`/sbin/hdparm -d1 /dev/cdrom`
`gedit /etc/hdparm.conf`

<li>
Inserisci le seguenti linee nel nuovo file

</li>
`/dev/cdrom {`
`    dma = on`
`}`

<li>
Salva il file modificato

</li>
</ol>
Come montare/smontare manualmente il CD/DVD-ROM, e come mostrare tutti i file/directory nascoste ed associate
-------------------------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che /dev/cdrom0 sia il CD/DVD-ROM*

<li>
Per montare il CD/DVD-ROM

</li>
`mount /media/cdrom0/ -o unhide`

<li>
Per smontare il CD/DVD-ROM

</li>
`umount /media/cdrom0/`

</ol>
Come forzare manualmente il montaggio/smontaggio del CD/DVD-ROM
---------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che /dev/cdrom0 sia il CD/DVD-ROM*

`umount /media/cdrom0/ -l`

</ol>
Come rimontare /etc/fstab senza effettuare il reboot della macchina
-------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

mount -a

</ol>
<Categoria:Fedoraserver>
