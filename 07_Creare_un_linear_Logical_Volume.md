Per creare una nuova struttura LVM bisognerà seguire alcuni passi specifici:

-   Mostrare le block device necessarie al sistema operativo.
-   Inizializzare le partizioni necessarie
-   Invocare la creazione dei PV sulle partizioni
-   Creare il VG agganciando i PV creati
-   Creare i LV in base alle esigenze del lavoro
-   Creare i filesystem ove necessario sui LV
-   Creare i mount point e montare i nuovi filesystem.

Di seguito vengono spiegati alcuni passi su come creare una semplice struttura LVM su un disco interno di un sistema Fedora.

-   Verificare che il disco venga riconosciuto dal sistema non appena connesso.

<!-- -->

    [root@localhost ~]# dmesg  | grep hdb
        ide0: BM-DMA at 0xd000-0xd007, BIOS settings: hda:DMA, hdb:DMA
    hdb: VBOX HARDDISK, ATA DISK drive
    hdb: max request size: 128KiB
    hdb: 4194304 sectors (2147 MB) w/256KiB Cache, CHS=4161/16/63, UDMA(33)
    hdb: cache flushes supported
     hdb: unknown partition table

-   Verificare che non ci siano partizioni attive sulla block device aggiunta e nel caso eliminarle. È possibile anche creare delle partizioni all'interno del disco. Infatti è possibile inizializzare un Physical Volume su una block device raw, ma anche su una partizione di una block device.

<!-- -->

    [root@localhost ~]# fdisk -l /dev/hdb

    Disk /dev/hdb: 2147 MB, 2147483648 bytes
    16 heads, 63 sectors/track, 4161 cylinders
    Units = cylinders of 1008 * 512 = 516096 bytes

    Disk /dev/hdb doesn't contain a valid partition table

-   Tramite il comando pvcreate si inizializza un PV su una block device o su una partizione.

<!-- -->

    [root@localhost ~]# pvcreate /dev/hdb
      Physical volume "/dev/hdb" successfully created

-   Lanciando il comando "pvs" si potrà verificare la lista dei PV presenti sul sistema. Il nostro nuovo PV sarà presente, ma non sarà ancora associato a nessun Volume Group (infatti la colonna VG è vuota).

<!-- -->

    [root@localhost ~]# pvs
      /dev/hdc: open failed: No medium found
      PV         VG         Fmt  Attr PSize PFree
      /dev/hda2  VolGroup00 lvm2 a-   7.88G    0
      /dev/hdb              lvm2 --   2.00G 2.00G

-   Tramite il comando vg\_create si potrà inizializzare un nuovo VG con il nome desiderato, aggiungendo poi la lista dei PV che comporranno il nostro VG che sarà composto da un solo PV. Ora dal comando pvs si noterà che il PV è associato al nostro nuovo VG, e tramite il vgs si noterà che il nuovo VG avrà la dimensione libera grande come il PV aggiunto.

<!-- -->

    [root@localhost ~]# vgcreate vg_test /dev/hdb
      Volume group "vg_test" successfully created
    [root@localhost ~]# vgs
      VG         #PV #LV #SN Attr   VSize VFree
      VolGroup00   1   2   0 wz--n- 7.88G    0
      vg_test      1   0   0 wz--n- 2.00G 2.00G
    [root@localhost ~]# pvs
      PV         VG         Fmt  Attr PSize PFree
      /dev/hda2  VolGroup00 lvm2 a-   7.88G    0
      /dev/hdb   vg_test    lvm2 a-   2.00G 2.00G

-   Ora si potrà suddividere il nostro VG in parti con i Logical Volume. Tramite il comando lvcreate sarà possibile partizionare lo spazio del disco in LV. Nel primo esempio verrà creato un LV nominato lv\_test1 con dimensione di 1 GB. Viene specificate l'opzione -L, che permettere di specificare la dimensione in Kb, Mb, Gb, Tb e Pe.

<!-- -->

    [root@localhost ~]# lvcreate -L 1024M vg_test -n lv_test1
      Logical volume "lv_test1" created
    [root@localhost ~]# lvs
      LV       VG         Attr   LSize   Origin Snap%  Move Log Copy%  Convert
      LogVol00 VolGroup00 -wi-ao   7.38G                                     
      LogVol01 VolGroup00 -wi-ao 512.00M                                     
      lv_test1 vg_test    -wi-a-   1.00G                                     
    [root@localhost ~]# vgs
      VG         #PV #LV #SN Attr   VSize VFree  
      VolGroup00   1   2   0 wz--n- 7.88G       0
      vg_test      1   1   0 wz--n- 2.00G 1020.00M
    [root@localhost ~]# pvs
      PV         VG         Fmt  Attr PSize PFree  
      /dev/hda2  VolGroup00 lvm2 a-   7.88G       0
      /dev/hdb   vg_test    lvm2 a-   2.00G 1020.00M

-   Nel secondo esempio verrà creato un LV nominato lv\_test2 con dimensione pari a tutto lo spazio disponibile sul VG. Viene specificata l'opzione -l, che permette di indicare la dimensione in extend o percentuale. Come si noterà dall'output dei comandi pvs e vgs, lo spazio disponibile sarà pari a 0.

<!-- -->

    [root@localhost ~]# lvcreate -l +100%FREE vg_test -n lv_test2
      Logical volume "lv_test2" created
    [root@localhost ~]# lvs
      LV       VG         Attr   LSize    Origin Snap%  Move Log Copy%  Convert
      LogVol00 VolGroup00 -wi-ao    7.38G                                     
      LogVol01 VolGroup00 -wi-ao  512.00M                                     
      lv_test1 vg_test    -wi-a-    1.00G                                     
      lv_test2 vg_test    -wi-a- 1020.00M                                     
    [root@localhost ~]# vgs
      VG         #PV #LV #SN Attr   VSize VFree
      VolGroup00   1   2   0 wz--n- 7.88G    0
      vg_test      1   2   0 wz--n- 2.00G    0
    [root@localhost ~]# pvs
      PV         VG         Fmt  Attr PSize PFree
      /dev/hda2  VolGroup00 lvm2 a-   7.88G    0
      /dev/hdb   vg_test    lvm2 a-   2.00G    0

-   Ora verrà creato un filesystem di tipo ext3 su ogni LV creato in precedenza.

<!-- -->

    [root@localhost ~]# mkfs.ext3 /dev/vg_test/lv_test1
    mke2fs 1.39 (29-May-2006)
    Filesystem label=
    OS type: Linux
    Block size=4096 (log=2)
    Fragment size=4096 (log=2)
    131072 inodes, 262144 blocks
    13107 blocks (5.00%) reserved for the super user
    First data block=0
    Maximum filesystem blocks=268435456
    8 block groups
    32768 blocks per group, 32768 fragments per group
    16384 inodes per group
    Superblock backups stored on blocks:
        32768, 98304, 163840, 229376

    Writing inode tables: done                           
    Creating journal (8192 blocks): done
    Writing superblocks and filesystem accounting information: done

    This filesystem will be automatically checked every 38 mounts or
    180 days, whichever comes first.  Use tune2fs -c or -i to override.
    [root@localhost ~]# mkfs.ext3 /dev/vg_test/lv_test2
    mke2fs 1.39 (29-May-2006)
    Filesystem label=
    OS type: Linux
    Block size=4096 (log=2)
    Fragment size=4096 (log=2)
    130560 inodes, 261120 blocks
    13056 blocks (5.00%) reserved for the super user
    First data block=0
    Maximum filesystem blocks=268435456
    8 block groups
    32768 blocks per group, 32768 fragments per group
    16320 inodes per group
    Superblock backups stored on blocks:
        32768, 98304, 163840, 229376

    Writing inode tables: done                           
    Creating journal (4096 blocks): done
    Writing superblocks and filesystem accounting information: done

    This filesystem will be automatically checked every 30 mounts or
    180 days, whichever comes first.  Use tune2fs -c or -i to override.

-   Con il comando tune2fs è possibile modificare alcuni parametri del filesystem. Nel nostro esempio viene ridotto a 0 il conteggio dei mount (-c0) e l'intervallo di giorni massimo (-i0) , che fa scattare di default un fsck forzato sul filesystem. La nota viene specificata inoltre nell'output del comando mkfs.ext\*. Inoltre con l'opzione -o vengono passate alcune opzioni di mount del filesystem.

<!-- -->

    [root@localhost ~]# tune2fs -c0 -i0 -o acl,user_xattr /dev/vg_test/lv_test1
    tune2fs 1.39 (29-May-2006)
    Setting maximal mount count to -1
    Setting interval between checks to 0 seconds
    [root@localhost ~]# tune2fs -c0 -i0 -o acl,user_xattr /dev/vg_test/lv_test2
    tune2fs 1.39 (29-May-2006)
    Setting maximal mount count to -1
    Setting interval between checks to 0 seconds

-   Creare i mount point per i nuovi filesystem creati.

<!-- -->

    [root@localhost ~]# mkdir -p /mnt/test1
    [root@localhost ~]# mkdir -p /mnt/test2

-   Eseguire il mount manuale dei due filesystem.

<!-- -->

    [root@localhost ~]# mount /dev/vg_test/lv_test1 /mnt/test1
    [root@localhost ~]# mount /dev/vg_test/lv_test2 /mnt/test2
    [root@localhost ~]# blkid | grep test
    /dev/vg_test/lv_test1: UUID="29fb0d26-f9b6-44d8-8465-a5181836699b" TYPE="ext3"
    /dev/vg_test/lv_test2: UUID="62c10bcc-c356-4738-9489-457dc9fbb243" TYPE="ext3"

-   Verificare dal df che i due nuovi filesystem siano montati correttamente sul sistema.

<!-- -->

    [root@localhost ~]# df -k /mnt/test*
    Filesystem           1K-blocks      Used Available Use% Mounted on
    /dev/mapper/vg_test-lv_test1
                           1032088     34092    945568   4% /mnt/test1
    /dev/mapper/vg_test-lv_test2
                           1028056     17692    958140   2% /mnt/test2

-   Nel caso fissare i mount all'interno del /etc/fstab.

<Categoria:LVM>
