### Creazione stiped LV

Viene riportato il test di come costruire un LV in modalità striped, in modo che la scrittura/lettura venga spalmata su tutti i PV inseriti all'interno del VG, in modo da aumentare le performance di I/O nel caso si stiano utilizzando delle device con una buona capacità di scrittura sulle singole block device. Per prima cosa verificare che non ci siano già dei PV disponibili sul sistema, per creare il nostro VG.

    [root@localhost tmp]# pvs
      PV         VG         Fmt  Attr PSize PFree
      /dev/hda2  VolGroup00 lvm2 a-   7.88G    0 

Verificare la disponibilità di dischi senza alcun dato scritto, per poter creare le partizioni e poi inizializzare i PV da agganciare al VG.

    [root@localhost tmp]# fdisk -l

    Disk /dev/hda: 8589 MB, 8589934592 bytes
    255 heads, 63 sectors/track, 1044 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes

       Device Boot      Start         End      Blocks   Id  System
    /dev/hda1   *           1          13      104391   83  Linux
    /dev/hda2              14        1044     8281507+  8e  Linux LVM

    Disk /dev/sda: 1024 MB, 1024000000 bytes
    32 heads, 62 sectors/track, 1008 cylinders
    Units = cylinders of 1984 * 512 = 1015808 bytes

    Disk /dev/sda doesn't contain a valid partition table

    Disk /dev/sdb: 1024 MB, 1024000000 bytes
    32 heads, 62 sectors/track, 1008 cylinders
    Units = cylinders of 1984 * 512 = 1015808 bytes

    Disk /dev/sdb doesn't contain a valid partition table

    Disk /dev/sdc: 1024 MB, 1024000000 bytes
    32 heads, 62 sectors/track, 1008 cylinders
    Units = cylinders of 1984 * 512 = 1015808 bytes

    Disk /dev/sdc doesn't contain a valid partition table

    Disk /dev/sdd: 1024 MB, 1024000000 bytes
    32 heads, 62 sectors/track, 1008 cylinders
    Units = cylinders of 1984 * 512 = 1015808 bytes

    Disk /dev/sdd doesn't contain a valid partition table

    [root@localhost tmp]# fdisk /dev/sda
    [root@localhost tmp]# fdisk /dev/sdb
    [root@localhost tmp]# fdisk /dev/sdc
    [root@localhost tmp]# fdisk -l

    Disk /dev/hda: 8589 MB, 8589934592 bytes
    255 heads, 63 sectors/track, 1044 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes

       Device Boot      Start         End      Blocks   Id  System
    /dev/hda1   *           1          13      104391   83  Linux
    /dev/hda2              14        1044     8281507+  8e  Linux LVM

    Disk /dev/sda: 1024 MB, 1024000000 bytes
    32 heads, 62 sectors/track, 1008 cylinders
    Units = cylinders of 1984 * 512 = 1015808 bytes

       Device Boot      Start         End      Blocks   Id  System
    /dev/sda1               1        1008      999905   83  Linux

    Disk /dev/sdb: 1024 MB, 1024000000 bytes
    32 heads, 62 sectors/track, 1008 cylinders
    Units = cylinders of 1984 * 512 = 1015808 bytes

       Device Boot      Start         End      Blocks   Id  System
    /dev/sdb1               1        1008      999905   83  Linux

    Disk /dev/sdc: 1024 MB, 1024000000 bytes
    32 heads, 62 sectors/track, 1008 cylinders
    Units = cylinders of 1984 * 512 = 1015808 bytes

       Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1               1        1008      999905   83  Linux

Inizializzare un PV per ogni disco appena partizionato sul sistema.

    [root@localhost tmp]# pvcreate /dev/sda1
      Physical volume "/dev/sda1" successfully created
    [root@localhost tmp]# pvcreate /dev/sdb1
      Physical volume "/dev/sdb1" successfully created
    [root@localhost tmp]# pvcreate /dev/sdc1
      Physical volume "/dev/sdc1" successfully created
    [root@localhost tmp]# pvs
      PV         VG         Fmt  Attr PSize   PFree  
      /dev/hda2  VolGroup00 lvm2 a-     7.88G      0 
      /dev/sda1             lvm2 --   976.47M 976.47M
      /dev/sdb1             lvm2 --   976.47M 976.47M
      /dev/sdc1             lvm2 --   976.47M 976.47M

Creare il VG con tutti i PV appena inizializzati con un nome desiderato. Nel nostro esempio il VG si chiamerà vg\_test che avrà una dimensione totale pari alla somma di tutti i PV aggiunti durante la creazione di quest'ultimo.

    [root@localhost tmp]# vgcreate vg_test /dev/sda1 /dev/sdb1 /dev/sdc1
      Volume group "vg_test" successfully created
    [root@localhost tmp]# vgs
      VG         #PV #LV #SN Attr   VSize VFree
      VolGroup00   1   2   0 wz--n- 7.88G    0 
      vg_test      3   0   0 wz--n- 2.86G 2.86G
    [root@localhost tmp]# pvs
      PV         VG         Fmt  Attr PSize   PFree  
      /dev/hda2  VolGroup00 lvm2 a-     7.88G      0 
      /dev/sda1  vg_test    lvm2 a-   976.00M 976.00M
      /dev/sdb1  vg_test    lvm2 a-   976.00M 976.00M
      /dev/sdc1  vg_test    lvm2 a-   976.00M 976.00M

Ora bisognerà creare un LV in modalità striped utilizzando le opzioni "-i" e "-I" del comando lvcreate. L'opzione "-i" specifica il numero di stripe che comporranno il LV, e solitamente è uguale al numero di PV presenti nel VG dove viene inizializzato il LV (nel nostro caso quindi 3). L'opzione "-I" specifica la dimensione in KB della granularità dello stripe, e questa dimensione dovrà essere una potenza di 2 (nel nostro caso sarà 4 KB).

    [root@localhost tmp]# lvcreate -i3 -I4 -l +100%FREE vg_test -n lv_test
      Logical volume "lv_test" created
    [root@localhost tmp]# lvs
      LV       VG         Attr   LSize   Origin Snap%  Move Log Copy%  Convert
      LogVol00 VolGroup00 -wi-ao   7.38G                                      
      LogVol01 VolGroup00 -wi-ao 512.00M                                      
      lv_test  vg_test    -wi-a-   2.86G     

Creare un filesystem sul nuovo LV se necessario. Dopo aver creato il filesystem utilizzare il comando tune2fs per eseguire il tuning del fs e, nello specifico, azzerare i valori che comportano un fsck forzato schedulato.

    [root@localhost tmp]# mkfs.ext3 /dev/vg_test/lv_test 
    mke2fs 1.39 (29-May-2006)
    Filesystem label=
    OS type: Linux
    Block size=4096 (log=2)
    Fragment size=4096 (log=2)
    375360 inodes, 749568 blocks
    37478 blocks (5.00%) reserved for the super user
    First data block=0
    Maximum filesystem blocks=767557632
    23 block groups
    32768 blocks per group, 32768 fragments per group
    16320 inodes per group
    Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912

    Writing inode tables: done                            
    Creating journal (16384 blocks): done
    Writing superblocks and filesystem accounting information: done

    This filesystem will be automatically checked every 38 mounts or
    180 days, whichever comes first.  Use tune2fs -c or -i to override.
    [root@localhost tmp]# tune2fs -c0 -i0 /dev/vg_test/lv_test
    tune2fs 1.39 (29-May-2006)
    Setting maximal mount count to -1
    Setting interval between checks to 0 seconds

Creare il mount point ed eseguire il mount manualmente. Se necessario fissare la modifica nel file /etc/fstab.

    [root@localhost tmp]# mkdir -p /mnt/test
    [root@localhost tmp]# mount /dev/vg_test/lv_test /mnt/test/
    [root@localhost tmp]# df -h
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/VolGroup00-LogVol00
                          7.2G  2.1G  4.7G  31% /
    /dev/hda1              99M   12M   82M  13% /boot
    tmpfs                 125M     0  125M   0% /dev/shm
    /dev/mapper/vg_test-lv_test
                          2.9G   69M  2.7G   3% /mnt/test

Per verificare le funzionalità della scrittura in parallelo su tutti i PV si potrà utilizzare il pacchetto sysstat, per campionare i dettagli di utilizzo delle device. Nello specifico sarà possibile eseguire un controllo tramite il comando iostat, per i KB in lettura/scrittura su ogni singola device. Nel nostro caso è stata eseguita la creazione di un file da 1 GB sul filesystem e tramite il comando iostat invocato su tutti i PV del VG, si nota che la scrittura viene eseguita in parallelo con valori di scrittura molto simili tra loro nello stesso campionamento (colonna "kB\_wrtn/s").

    [root@localhost ~]# iostat -kd sda1 sdb1 sdc1 1
    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1              0.00         0.00         0.00          0          0
    sdb1              0.00         0.00         0.00          0          0
    sdc1              0.00         0.00         0.00          0          0

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             40.62         8.33      4495.83          8       4316
    sdb1             20.83         4.17      3345.83          4       3212
    sdc1             19.79         4.17      3145.83          4       3020

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             35.87         0.00      4278.26          0       3936
    sdb1             53.26         0.00      5491.30          0       5052
    sdc1             53.26         0.00      5686.96          0       5232

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             42.86         0.00      4975.82          0       4528
    sdb1             42.86         0.00      5116.48          0       4656
    sdc1             43.96         0.00      5076.92          0       4620

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             51.61         0.00      6236.56          0       5800
    sdb1             50.54         0.00      6034.41          0       5612
    sdc1             46.24         0.00      6004.30          0       5584

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             42.39         0.00      5843.48          0       5376
    sdb1             43.48         0.00      5882.61          0       5412
    sdc1             41.30         0.00      5839.13          0       5372

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             35.56         0.00      4697.78          0       4228
    sdb1             36.67         0.00      4697.78          0       4228
    sdc1             40.00         0.00      4840.00          0       4356

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             30.77         8.79      2751.65          8       2504
    sdb1             31.87         4.40      2747.25          4       2500
    sdc1             32.97         8.79      2747.25          8       2500

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             33.71         0.00      3280.90          0       2920
    sdb1             47.19         0.00      4566.29          0       4064
    sdc1             41.57         0.00      3649.44          0       3248

    Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
    sda1             43.33         0.00      4737.78          0       4264
    sdb1             27.78         0.00      3466.67          0       3120
    sdc1             25.56         0.00      4368.89          0       3932

### Sostituzione PV appartenente allo striped LV

Può capitare che in alcuni casi si debba rimuovere un PV appartenente allo striped LV per guasti hardware o di altra natura. Questa parte della procedura indica come spostare i dati da un PV ad uno nuovo e rimuovere quello guasto. Per prima cosa creare una partizione ed inizializzare un PV sul disco presentato al sistema.

    [root@localhost tmp]# fdisk /dev/sdd
    [root@localhost tmp]# pvcreate /dev/sdd1
    Physical volume "/dev/sdd1" successfully created

Aggiungere il nuovo PV al VG che ospita lo stiped LV da sistemare.

    [root@localhost tmp]# vgextend vg_test /dev/sdd1
      Volume group "vg_test" successfully extended
    [root@localhost tmp]# vgs
      VG         #PV #LV #SN Attr   VSize VFree  
      VolGroup00   1   2   0 wz--n- 7.88G      0 
      vg_test      4   1   0 wz--n- 3.81G 976.00M
    [root@localhost tmp]# pvs
      PV         VG         Fmt  Attr PSize   PFree  
      /dev/hda2  VolGroup00 lvm2 a-     7.88G      0 
      /dev/sda1  vg_test    lvm2 a-   976.00M      0 
      /dev/sdb1  vg_test    lvm2 a-   976.00M      0 
      /dev/sdc1  vg_test    lvm2 a-   976.00M      0 
      /dev/sdd1  vg_test    lvm2 a-   976.00M 976.00M

Ora tramite il comando pvmove si potrà spostare il contenuto del vecchio PV verso quello nuovo senza perdere alcun dato. Lo spostamento sarà possibile farlo senza dover smontare il fs.

    [root@localhost tmp]# pvmove /dev/sda1 /dev/sdd1
      /dev/sda1: Moved: 10.2%
      /dev/sda1: Moved: 18.9%
      /dev/sda1: Moved: 27.0%
      /dev/sda1: Moved: 35.7%
      /dev/sda1: Moved: 43.9%
      /dev/sda1: Moved: 51.6%
      /dev/sda1: Moved: 59.4%
      /dev/sda1: Moved: 67.6%
      /dev/sda1: Moved: 75.8%
      /dev/sda1: Moved: 82.8%
      /dev/sda1: Moved: 92.6%
      /dev/sda1: Moved: 100.0%
    [root@localhost tmp]# pvs
      PV         VG         Fmt  Attr PSize   PFree  
      /dev/hda2  VolGroup00 lvm2 a-     7.88G      0 
      /dev/sda1  vg_test    lvm2 a-   976.00M 976.00M
      /dev/sdb1  vg_test    lvm2 a-   976.00M      0 
      /dev/sdc1  vg_test    lvm2 a-   976.00M      0 
      /dev/sdd1  vg_test    lvm2 a-   976.00M      0 
    [root@localhost tmp]# lvs
      LV       VG         Attr   LSize   Origin Snap%  Move Log Copy%  Convert
      LogVol00 VolGroup00 -wi-ao   7.38G                                      
      LogVol01 VolGroup00 -wi-ao 512.00M                                      
      lv_test  vg_test    -wi-ao   2.86G

Verificando sul vecchio PV lo spazio occupato sarà pari allo 0%

                       
    [root@localhost tmp]# pvs -o+pv_used
      PV         VG         Fmt  Attr PSize   PFree   Used   
      /dev/hda2  VolGroup00 lvm2 a-     7.88G      0    7.88G
      /dev/sda1  vg_test    lvm2 a-   976.00M 976.00M      0 
      /dev/sdb1  vg_test    lvm2 a-   976.00M      0  976.00M
      /dev/sdc1  vg_test    lvm2 a-   976.00M      0  976.00M
      /dev/sdd1  vg_test    lvm2 a-   976.00M      0  976.00M

Ora tramite il comando vgreduce sarà possibile rimuovere il vecchio PV da quelli utilizzati dal VG.

    [root@localhost test]# vgreduce vg_test /dev/sda1
      Removed "/dev/sda1" from volume group "vg_test"
    [root@localhost test]# vgs
      VG         #PV #LV #SN Attr   VSize VFree
      VolGroup00   1   2   0 wz--n- 7.88G    0 
      vg_test      3   1   0 wz--n- 2.86G    0 
    [root@localhost test]# pvs
      PV         VG         Fmt  Attr PSize   PFree  
      /dev/hda2  VolGroup00 lvm2 a-     7.88G      0 
      /dev/sda1             lvm2 --   976.47M 976.47M
      /dev/sdb1  vg_test    lvm2 a-   976.00M      0 
      /dev/sdc1  vg_test    lvm2 a-   976.00M      0 
      /dev/sdd1  vg_test    lvm2 a-   976.00M      0 

<Categoria:LVM>
