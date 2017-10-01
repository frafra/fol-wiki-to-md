-   Per prima cosa smontare il filesystem che dovrà essere ridotto nella sua dimensione. Ricordarsi che il filesystem di root non può essere smontato a caldo.

<!-- -->

    [root@pc ~]# df -h   
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/VolGroup00-LogVol00  7.2G  1.6G  5.3G  23% /         
    /dev/hda1              99M   12M   82M  13% /boot     
    tmpfs                 125M     0  125M   0% /dev/shm  
    /dev/mapper/VolGroup00-LogVol02   2.0G   35M  1.9G   2% /prova 
    [root@pc ~]# umount /prova

-   Ora bisognerà ridurre la dimensione del filesystem con il comando resize2fs. Ricordarsi di ridurre il filesystem in modo corretto, non restringere un filesystem in una dimensione più piccola dello spazio già occupato, altrimenti si compromette il filesystem con relativa perdita di dati. Passare quindi la dimensione del nuovo filesystem al comando resize2fs.

<!-- -->

    [root@pc ~]# resize2fs -f /dev/VolGroup00/LogVol02 1G
    resize2fs 1.39 (29-May-2006)
    Resizing the filesystem on /dev/VolGroup00/LogVol02 to 262144 (4k) blocks.
    The filesystem on /dev/VolGroup00/LogVol02 is now 262144 blocks long.

-   Ridurre la dimensione del Logical Volume associato al fileystem della stessa dimensione impostata in precedenza nel resize2fs. Confermare l'operazione se si sono seguiti i passi corretti.

<!-- -->

    [root@pc ~]# lvreduce -L 1G /dev/VolGroup00/LogVol02
      WARNING: Reducing active logical volume to 1.00 GB
      THIS MAY DESTROY YOUR DATA (filesystem etc.)
    Do you really want to reduce LogVol02? [y/n]: y
      Reducing logical volume LogVol02 to 1.00 GB
      Logical volume LogVol02 successfully resized

-   Rimontare nuovamente il filesystem e verificare che la dimensione sia stata corretta come desiderato.

<!-- -->

    [root@pc ~]# mount /dev/VolGroup00/LogVol02
    [root@pc ~]# df -h
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/VolGroup00-LogVol0 7.2G  1.6G  5.3G  23% /
    /dev/hda1              99M   12M   82M  13% /boot
    tmpfs                 125M     0  125M   0% /dev/shm
    /dev/mapper/VolGroup00-LogVol021009M   35M  933M   4% /prova

<Categoria:LVM>
