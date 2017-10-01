Per ampliare un filesystem che poggia su una struttura LVM si potrà svolgere tutto a caldo, senza dover forzatamente smontare i filesystem.

-   Per prima cosa controllare che il Volume Group a cui appartiene il Logical Volume da allargare, possieda lo spazio libero necessario per l'ampliamento. Lanciare un vgs e controllare che nella colonna "VFree", ci sia abbastanza spazio libero da sfruttare.

<!-- -->

    [root@pc ~]# vgs -a
      VG         #PV #LV #SN Attr   VSize VFree
      VolGroup00   2   3   0 wz--n- 9.84G 992.00M

-   Tramite il comando lvextend allargare il filesystem per la dimensione desiderata. E' possibile allargare il Logical Volume per tutta la dimensione libera del Volume Group (con -l +100%FREE), oppure di una dimensione specifica (con -L <dimensione>).

<!-- -->

    [root@pc ~]# lvs
      LV       VG         Attr   LSize   Origin Snap%  Move Log Copy%  Convert
      LogVol00 VolGroup00 -wi-ao   7.38G
      LogVol01 VolGroup00 -wi-ao 512.00M
      LogVol02 VolGroup00 -wi-ao   1.00G
    [root@vrhel5 ~]# lvextend -l +100%FREE /dev/VolGroup00/LogVol02
      Extending logical volume LogVol02 to 1.97 GB
      Logical volume LogVol02 successfully resized
    [root@vrhel5 ~]# lvs
      LV       VG         Attr   LSize   Origin Snap%  Move Log Copy%  Convert
      LogVol00 VolGroup00 -wi-ao   7.38G
      LogVol01 VolGroup00 -wi-ao 512.00M
      LogVol02 VolGroup00 -wi-ao   1.97G

-   Allargare la dimensione del filesystem, invocando il comando resize2fs sul filesystem da ampliare.

<!-- -->

    [root@pc ~]# df -h
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/VolGroup00-LogVol00 7.2G  1.6G  5.3G  23% /
    /dev/mapper/VolGroup00-LogVol02 1.0G   35M  970M   10% /prova
    /dev/hda1              99M   12M   82M  13% /boot
    tmpfs                 125M     0  125M   0% /dev/shm
    [root@pc ~]# resize2fs -p /dev/VolGroup00/LogVol02
    resize2fs 1.39 (29-May-2006)
    Filesystem at /dev/VolGroup00/LogVol02 is mounted on /prova; on-line resizing required
    Performing an on-line resize of /dev/VolGroup00/LogVol02 to 516096 (4k) blocks.
    The filesystem on /dev/VolGroup00/LogVol02 is now 516096 blocks long.
    [root@pc ~]# df -h
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/VolGroup00-LogVol00 7.2G  1.6G  5.3G  23% /
    /dev/mapper/VolGroup00-LogVol02 2.0G   35M  1.9G   2% /prova
    /dev/hda1              99M   12M   82M  13% /boot
    tmpfs                 125M     0  125M   0% /dev/shm

### NOTE IMPORTANTI

In alcuni casi dove si svolge un grow di un filesystem sotto stress (con un accesso in I/O molto alto durante l'attività), si potrebbe avere un blocco del sistema. Nello specifico il sistema dovrebbe non terminare le attività di resize, mantenendo il sistema in idle e un load average molto alto. Provando ad eseguire un kill del processo relativo al resize non cambierà nulla e si dovrà riavviare il sistema.

<Categoria:LVM>
