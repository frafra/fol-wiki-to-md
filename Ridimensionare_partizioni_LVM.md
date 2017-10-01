\_\_TOC\_\_

Introduzione
------------

Per chi si dovesse trovare a ridimensionare delle partizioni LVM ( Logical Volume Manager) di Fedora è necessario un procedimento piuttosto atipico, rispetto al resize di normali partizioni, che prevede prima di tutto un ridimensionamento del filesystem custodito nell'LVM poi il resize del volume.

Solitamente chi installa Fedora 11 in automatico avrà le partizioni distribuite sullo spazio libero disponibile nell'hardisk secondo il seguente schema:

`partizione /boot (filesystem ext3)`
`partizione lvm ---> VolGroup00 (filesystem ext4 in default) -----> LogVol00 (/swap) + LogVol01 (/)`

Lo spazio libero iniziale è stato diviso in due partizioni: /boot NON LVM e la partizione LVM vera e propria.

Procedimento
------------

Si opera con LVM non montata quindi si è costretti ad accedere al disco rigido con una live version di fedora.
Controllare lo stato del disco:

`# fdisk -l`
`# blkid -L`
`/dev/sda1  ext3             /boot                     `
`/dev/mapper/VolGroup00-LogVol00 ( /dev/sda2)`
`/dev/mapper/VolGroup00-LogVol01  (swap)`

L'LVM può essere studiata graficamente dal tool adatto:

`# system-config-lvm`

Supponiamo che la partizione da ridimensionare occupi 485GB e che si chiami */dev/mapper/VolGroup00-LogVol00*; da terminale:

`# e2fsck -f /dev/mapper/VolGroup00-LogVol00`

Questo comando si occupa di controllare il volume indicato.

`# resize2fs -p /dev/mapper/VolGroup00-LogVol00 225G `

Con resize2fs si ridimensiona il filesystem fino alle dimensioni indicate (225GB). Questo comando funziona sia con ext2/ext3 sia con l'ext4 introdotto a partire da Fedora 11.

`# lvm lvreduce -L 250G /dev/mapper/VolGroup00-LogVol00  `

Con *lvreduce* si riduce la dimensione del volume logico indicato fino a 250GB.

`# resize2fs /dev/mapper/VolGroup00-LogVol00  `

Con questo comando si riespande il filesystem occupando il volume con le nuove dimensioni.

`# vgreduce --removemissing /dev/sda2`

Ultimo comando: rimuove il volume logico liberato con le operazioni precedenti, qualora facesse ancora parte del gruppo di volumi logici. */dev/sad2* è la partizione fisica che ospita il gruppo di volumi logici.

Sempre da terminale si può ora installare gparted:

`# yum -y install gparted`
`# gparted`

e formattare lo spazio libero in ntfs, fat32, ext4 o lasciarlo come libero.

Si ricorda che tutte le operazioni vanno necessariamente eseguite da sistema live, testato su LVM Fedora 10, ma dovrebbe andare bene anche per Fedora 11.

Riferimenti
-----------

-   Pagine man: lvm, resize2fs, e2fsck, lvreduce, vgreduce;
-   <http://tldp.org/HOWTO/LVM-HOWTO/>

<Categoria:Sistema>
