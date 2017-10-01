Introduzione
------------

All'avvio dei PC viene eseguita una serie di step per arrivare al caricamento del sistema operativo (Linux o Windows) ed in questa pagina verranno descritti a grandi linee tutti i passaggi svolti nella boot sequence di un sistema Linux.

Bios e Post
-----------

Il BIOS è il primo stadio del processo di avvio che viene avviato dall'accensione. Il BIOS, che risiede nella ROM è eseguito da un particolare indirizzo di memoria al quale è inizializzato, dall'accensione, il contatore di programma della CPU. In questa fase viene effettuata l'inizializzazione base dell'hardware POST (power on self test) che passa il controllo del sistema allo stadio successivo fornito dall'utente. Tipicamente vengono caricati in memoria i primi settori del primo dispositivo selezionato trovato (disco fisso, dischetto floppy, CD-ROM, ...) e viene eseguito questo codice iniziale che può essere una qualsiasi tra le cose seguenti.

-   Il codice del bootloader
-   Il codice del kernel del sistema operativo finale, se può essere contenuto in questo piccolo spazio.

Tipicamente il sistema viene avviato dalla partizione specificata del disco fisso primario. I primi 2 settori del disco fisso nei PC più datati contengono il master boot record (MBR). Le informazioni sulle partizioni del disco, inclusa la selezione per l'avvio sono memorizzate alla fine di questo MBR. Il primo codice boot loader eseguito dal BIOS occupa la parte restante di questo MBR.

Bootloader (Lilo/Grub)
----------------------

Il bootloader ha il compito di caricare il kernel (cuore del sistema operativo) e quest'ultimo invece caricherà il restante software necessario.
In Linux in precedenza veniva utilizzato Lilo (Linux Loader), che aveva alcune limitazioni nel suo utilizzo tra le quali:

-   permette di caricare fino a 16 selezioni differenti;
-   non può eseguire il boot tramite rete;
-   non ha un'interfaccia interattiva con cui interagire;
-   deve essere reinstallato da capo, ogni volta che viene modificato il file di configurazione.

Negli anni successivi il Grub di Linux, è diventato il bootloader più usato grazie alla sua portabilità verso altri sistemi, e Lilo è stato deprecato.
Grub permette di avere diverse caratteristiche tra cui:

-   permette di caricare infinite selezioni differenti;
-   ha un'interfaccia interattiva funzionale con cui interagire;
-   permette il boot da rete, ma anche da altri device come cd-rom, device USB, LVM o ISCSI;
-   permette di caricare più sistemi operativi differenti.

La sua funzionalità più utile è quella di poter caricare non solo sistemi operativi liberi, ma anche sistemi proprietari come Windows. Le device viste da Grub non vengono nominate come in Linux, con la nomenclatura "sd..." ma utilizzano una particolare nomenclatura che può cambiare da sistema a sistema, infatti i nomi vengono associati in base alle informazioni passate dal bios. Non è detto quindi che una device denominata "sda" dal sistema operativo, sia la prima unità che Grub nomina come "hd0". Ogni disco viene nominato "hd..", e il numero parte da zero, mentre il secondo valore passato indica la partizione scritta sul disco.
E' possibile passare anche una partizione estesa del disco stesso. Per esempio, la prima partizione di un disco è (hd0,0) mentre la prima partizione estesa sarà (hd0,4). Grub non fa distinzione tra device IDE o SCSI ed utilizza delle nomenclature anche per floppy (con la sigla "fd") e per cdrom (con la sigla "cd").

Stage 1
-------

Grub ha diversi stage di caricamento che permettono l'avvio del sistema non appena il server viene avviato. Quando il BIOS viene eseguito va a leggere sul disco fisso il primo settore chiamato MBR (Master Boot Record), che contiene la tabella delle partizioni nei primi 63 byte, mentre i successivi 446 bytes vengono usati per caricare il primo stage di Grub. In questo stage sono contenute le primi frazioni di codice da eseguire per il caricamento del kernel, ma non avendo lo spazio per contenere tutte le informazioni, viene richiamatao lo stage 1.5

`[root@cellopc-mini grub]# file stage1`
`stage1: x86 boot sector; GRand Unified Bootloader, stage1 version 0x3, GRUB version 0.94, code offset 0x48`

Stage 1.5
---------

Dato che la dimensione del MBR non è abbastanza grande per contenere il codice completo di Grub, viene riservato lo spazio addiacente al MBR stesso (solitamente fino al primo cilindro) per caricare lo stage 1.5.
Questo stage è una fase intermedia per inizializzare il caricamento effettivo del kernel e permette di montare determinate tipologie di filesystem. Nel filesystem che verrà montato saranno contenute le immagini del kernel ed initrd per eseguire il boot del sistema.

`[root@cellopc-mini grub]# ls -l *stage1_5`
`-rw-r--r--. 1 root root 13056 Nov 19 09:38 e2fs_stage1_5`
`-rw-r--r--. 1 root root 12416 Nov 19 09:38 fat_stage1_5`
`-rw-r--r--. 1 root root 11648 Nov 19 09:38 ffs_stage1_5`
`-rw-r--r--. 1 root root 11672 Nov 19 09:38 iso9660_stage1_5`
`-rw-r--r--. 1 root root 13104 Nov 19 09:38 jfs_stage1_5`
`-rw-r--r--. 1 root root 11824 Nov 19 09:38 minix_stage1_5`
`-rw-r--r--. 1 root root 14072 Nov 19 09:38 reiserfs_stage1_5`
`-rw-r--r--. 1 root root 11924 Nov 19 09:38 ufs2_stage1_5`
`-rw-r--r--. 1 root root 11280 Nov 19 09:38 vstafs_stage1_5`
`-rw-r--r--. 1 root root 13576 Nov 19 09:38 xfs_stage1_5`
`[root@cellopc-mini grub]# file e2fs_stage1_5`
`e2fs_stage1_5: GRand Unified Bootloader stage1_5 version 3.2, identifier 0x2, GRUB version 0.97,`
`                                                           configuration file /boot/grub/stage2`

Stage 2
-------

Lo stage 2 risiede in una qualsiasi parte del disco, solitamente nella partizione /boot, grande 500 MB. In questa partizione sono contenute tutte le informazioni, i kernel usati e soprattutto la lista dei kernel da utilizzare (file /boot/grub/menu.lst).

`[root@cellopc-mini grub]# file stage2 `
` `
`stage2: GRand Unified Bootloader stage2 version 3.2, installed partition 65535,identifier 0x0,GRUB version 0.97,`
`                                                                      configuration file (hd0,0)/grub/grub.conf`

Il file menu.lst
----------------

Il file menu.lst contiene diverse informazioni principali per il caricamento dei kernel.

`[cello@cellopc grub]$ cat /boot/grub/menu.lst`
`# grub.conf generated by anaconda`
`#`
`# Note that you do not have to rerun grub after making changes to this file`
`# NOTICE:  You have a /boot partition.  This means that`
`#          all kernel and initrd paths are relative to /boot/, eg.`
`#          root (hd0,0)`
`#          kernel /vmlinuz-version ro root=/dev/VolGroup00/LogVol00`
`#          initrd /initrd-version.img`
`#boot=/dev/sda`
`default=0`
`timeout=0`
`splashimage=(hd0,0)/grub/splash.xpm.gz`
`hiddenmenu`
`title Fedora (2.6.27.9-159.fc10.i686)`
`       root (hd0,0)`
`       kernel /vmlinuz-2.6.27.9-159.fc10.i686 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`       initrd /initrd-2.6.27.9-159.fc10.i686.img`
`title Fedora (2.6.27.7-134.fc10.i686)`
`       root (hd0,0)`
`       kernel /vmlinuz-2.6.27.7-134.fc10.i686 ro root=/dev/VolGroup00/LogVol00 rhgb quiet`
`       initrd /initrd-2.6.27.7-134.fc10.i686.img`
`title Fedora 10(2.6.27.5-117.fc10.i686)`
`       root (hd0,0)`
`       kernel /vmlinuz-2.6.27.5-117.fc10.i686 ro root=UUID=f06adec0-e94a-4904-8f56-53168e6c8ecf rhgb quiet`
`       initrd /initrd-2.6.27.5-117.fc10.i686.img[/code]`

-   splashimage (hdn,m)/grub/Name.xpm.gz è il file immagine di splash;
-   default *n* è la voce di boot predefinita, scelta al termine del tempo per la selezione da parte dell'utente;
-   timeout *m* tempo *m* in secondi per effettuare una selezione, prima che sia lanciata la predefinita;
-   password -md5 str password cifrata di boot 'str';
-   title str stringa di titolo 'str' per una voce di boot;
-   root (hdn,m) partizione basilare, dove è alloggiato il kernel;
-   kernel /path ro root=/dev/device specifica l'immagine del kernel che verrà caricata in memoria;
-   initrd /initrd.img contiene l'initial ram disk da utilizzare.

Vmlinuz
-------

Dopo che viene eseguita la scelta dello specifico kernel da caricare verrà letto per prima cosa il path del file vmlinuz associato alla voce "kernel" nel file /boot/grub/menu.lst. Questo file è una semplice immagine del kernel che viene copiata in memoria per poter caricare tutti i moduli e componenti del filesystem di root temporaneo fornito da initrd o initramfs.
Oltre a questa immagine del kernel caricata in memoria, tra i parametri viene specificato anche quale sarà la root device che dovrà essere caricata per lanciare la fase di init.

Initrd e Initramfs
------------------

Oltre all'immagine del kernel viene caricata in memoria anche un'immagine del filesystem di root temporanea, che servirà al caricamento del vero filesystem di root. Questo piccolo filesystem temporaneo permette di eseguire le primissime operazioni di boot senza dover accedere al vero filesystem di root, che verrà caricato in una fase successiva.
Nella prime versioni del kernel 2.6 veniva utilizzato initrd (initial ram disk), una semplice immagine di un filesystem ext2/ext3 che viene caricato nella ramdisk, per poi essere considerata come una vera e propria block device.
Per esigenze di sviluppo è stato creato initramfs (inital ram filesystem) cioè un *archivio cpio* compresso che viene caricato in tmpfs. La prima differenza tra initrd e initramfs è che la dimensione del secondo è molto minore del primo e quindi viene caricato prima durante la fase di boot. Inoltre initramfs viene caricato in tmpfs, motivo per cui la dimensione può essere modificata dinamicamente mentre per quanto riguarda il caricamento di initrd nella ramdisk, risulta molto più difficile da modificare.
Sempre per quanto riguarda initrd si dovrà avere un modulo per caricare il filesystem nella ramdisk. Inoltre, dato che initrd è un filesystem scompattato nella ramdisk si è legati al vero filesystem di root che viene specificato nel parametro "root=", mentre con initramfs non esiste alcun dispositivo legato all'immagine decompressa nella tmpfs, quindi si può montare il filesystem di root vero e proprio via rete o tramite altri metodi (iscsi, SAN,...). La struttura di initrd è la seguente:

`[root@cw-spmi-mgm01 test]# file initrd-2.6.18-92.el5.img`
`initrd-2.6.18-92.el5.img: gzip compressed data, from Unix, last modified: Sat Feb  6 10:24:19 2010, max compression`
`[root@cw-spmi-mgm01 test]# gunzip -c /boot/initrd-2.6.18-92.el5.img | cpio -ivmdq`
`[root@cw-spmi-mgm01 test]# tree`
`.`
`|-- bin`
`|   |-- dmraid`
`|   |-- insmod`
`|   |-- kpartx`
`|   |-- lvm`
`|   |-- modprobe -> /sbin/nash`
`` |   `-- nash ``
`|-- dev`
`|   |-- console`
`|   |-- mapper`
`|   |-- null`
`|   |-- ptmx`
`|   |-- ram -> ram1`
`|   |-- ram0`
`|   |-- ram1`
`|   |-- rtc`
`|   |-- systty`
`|   |-- tty`
`|   |-- tty0`
`|   |-- tty1`
`|   |-- tty10`
`|   |-- tty11`
`|   |-- tty12`
`|   |-- tty2`
`|   |-- tty3`
`|   |-- tty4`
`|   |-- tty5`
`|   |-- tty6`
`|   |-- tty7`
`|   |-- tty8`
`|   |-- tty9`
`|   |-- ttyS0`
`|   |-- ttyS1`
`|   |-- ttyS2`
`|   |-- ttyS3`
`` |   `-- zero ``
`|-- etc`
`` |   `-- lvm ``
`` |       `-- lvm.conf ``
`|-- init`
`|-- lib`
`|   |-- cciss.ko`
`|   |-- dm-mirror.ko`
`|   |-- dm-mod.ko`
`|   |-- dm-snapshot.ko`
`|   |-- dm-zero.ko`
`|   |-- ehci-hcd.ko`
`|   |-- ext3.ko`
`|   |-- firmware`
`|   |-- jbd.ko`
`|   |-- lpfc.ko`
`|   |-- ohci-hcd.ko`
`|   |-- scsi_mod.ko`
`|   |-- scsi_transport_fc.ko`
`|   |-- sd_mod.ko`
`` |   `-- uhci-hcd.ko ``
`|-- proc`
`|-- sbin -> bin`
`|-- sys`
`|-- sysroot`

La struttura di initramfs è la seguente:

`[root@cellopc-mini boot]# file initramfs-2.6.35.6-48.fc14.i686.img`
`initramfs-2.6.35.6-48.fc14.i686.img: gzip compressed data, from Unix, last modified: Mon Nov 22 18:45:23 2010, `
`                                                                                               max compression`

Il *tree* lo si potrà verificare direttamente sul proprio PC, qui sarebbe troppo esteso da pubblicare.
Dopo il caricamento del kernel e dell'initrd/initramfs in memoria verrà lanciato lo script "init" che eseguirà il mount di sysfs, tmpfs, proc e devpts con il caricamento di alcuni moduli per l'attivazione del kernel e quando avrà montato la root verrà eseguito uno switch tra le due root directory, passando il controllo di tutto al processo /sbin/init (che avrà pid 1).

Init scripts
------------

Il processo "/sbin/init" ha pid pari ad 1 ed è da considerarsi il padre di tutti i processi che vengono lanciati dal sistema.

`[code][root@cellopc-mini kernel]# ps -ef | grep /sbin/init`
`root         1     0  0 09:11 ?        00:00:01 /sbin/init`

Il processo init non fa altro che leggere nel file /etc/inittab il runlevel contenuto nella riga "initdefault" e da qui eseguirà lo start di tutti i processi marcati con S\*, che sono contenuti nella directory "/etc/rc<N>.d" in ordine alfabetico.

`[code][root@cellopc-mini rc3.d]# cat /etc/inittab `
`id:5:initdefault: `
`[root@cellopc-mini rc3.d]# ls -l /etc/rc5.d/S*`
`lrwxrwxrwx. 1 root root 17 Oct 22 20:24 /etc/rc5.d/S00livesys -> ../init.d/livesys`
`lrwxrwxrwx  1 root root 17 Nov 19 13:36 /etc/rc5.d/S01sysstat -> ../init.d/sysstat`
`lrwxrwxrwx. 1 root root 22 Oct 22 20:18 /etc/rc5.d/S02lvm2-monitor -> ../init.d/lvm2-monitor`
`lrwxrwxrwx  1 root root 28 Nov 20 11:55 /etc/rc5.d/S04dkms_autoinstaller -> ../init.d/dkms_autoinstaller`
`lrwxrwxrwx  1 root root 16 Nov 22 12:49 /etc/rc5.d/S11auditd -> ../init.d/auditd`
`lrwxrwxrwx. 1 root root 21 Oct 22 20:17 /etc/rc5.d/S11portreserve -> ../init.d/portreserve`
`lrwxrwxrwx  1 root root 17 Nov 19 12:16 /etc/rc5.d/S12rsyslog -> ../init.d/rsyslog`
`lrwxrwxrwx. 1 root root 18 Oct 22 20:20 /etc/rc5.d/S13cpuspeed -> ../init.d/cpuspeed`
`lrwxrwxrwx. 1 root root 20 Oct 22 20:18 /etc/rc5.d/S13irqbalance -> ../init.d/irqbalance`
`lrwxrwxrwx. 1 root root 20 Oct 22 20:17 /etc/rc5.d/S22messagebus -> ../init.d/messagebus`
`lrwxrwxrwx. 1 root root 24 Oct 22 20:24 /etc/rc5.d/S23NetworkManager -> ../init.d/NetworkManager`
`lrwxrwxrwx. 1 root root 22 Oct 22 20:18 /etc/rc5.d/S24avahi-daemon -> ../init.d/avahi-daemon`
`lrwxrwxrwx  1 root root 14 Nov 19 12:13 /etc/rc5.d/S25cups -> ../init.d/cups`
`lrwxrwxrwx. 1 root root 15 Oct 22 20:18 /etc/rc5.d/S25netfs -> ../init.d/netfs`
`lrwxrwxrwx. 1 root root 19 Oct 22 20:19 /etc/rc5.d/S26haldaemon -> ../init.d/haldaemon`
`lrwxrwxrwx  1 root root 19 Nov 19 12:12 /etc/rc5.d/S26udev-post -> ../init.d/udev-post`
`lrwxrwxrwx  1 root root 17 Nov 20 12:32 /etc/rc5.d/S30vboxdrv -> ../init.d/vboxdrv`
`lrwxrwxrwx  1 root root 25 Nov 20 12:24 /etc/rc5.d/S35vboxweb-service -> ../init.d/vboxweb-service`
`lrwxrwxrwx  1 root root 14 Nov 19 12:15 /etc/rc5.d/S55sshd -> ../init.d/sshd`
`lrwxrwxrwx  1 root root 16 Nov 19 13:35 /etc/rc5.d/S64mysqld -> ../init.d/mysqld`
`lrwxrwxrwx. 1 root root 15 Oct 22 20:19 /etc/rc5.d/S90crond -> ../init.d/crond`
`lrwxrwxrwx. 1 root root 13 Oct 22 20:18 /etc/rc5.d/S95atd -> ../init.d/atd`
`lrwxrwxrwx. 1 root root 22 Oct 22 20:24 /etc/rc5.d/S99livesys-late -> ../init.d/livesys-late`
`lrwxrwxrwx. 1 root root 11 Oct 22 20:18 /etc/rc5.d/S99rc-local -> ../rc.local`

Al termine del lancio di tutti gli script il sistema sarà up e running.

<Categoria:Grub>
