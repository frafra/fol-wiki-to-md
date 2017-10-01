LVMDUMP
-------

Il comando lvmdump permette di collezionare dati utili su LVM in caso di problemi.
Verranno raccolte tutte le informazioni e salvate in un file .tgz creato nella cartella da dove si invoca il comando.
È possibile specificare l'opzione "-a" per aumentare la verbosità e il numero di file collezionati. Questa opzione è utile in caso di freeze (stallo) di LVM, per approfondire il debug di problemi.

    [root@cellopc ~]# lvmdump -a
    Creating dump directory: /root/lvmdump-cellopc-20100316150828
     
    Gathering LVM volume info...
      vgscan...
      pvscan...
      lvs...
      pvs...
      vgs...
    Gathering LVM & device-mapper version info...
    Gathering dmsetup info...
    Gathering process info...
    Gathering console messages...
    Gathering /etc/lvm info...
    Gathering /dev listing...
    Gathering /sys/block listing...
    Creating report tarball in /root/lvmdump-cellopc-20100316150828.tgz...

Il file conterrà questo tipo di files:

    [root@cellopc ~]# tar tvfz /root/lvmdump-cellopc-20100316150828.tgz
    drwxr-xr-x root/root         0 2010-03-16 16:08 lvmdump-cellopc-20100316150828/
    -rw-r--r-- root/root       464 2010-03-16 16:08 lvmdump-cellopc-20100316150828/dmsetup_info
    -rw-r--r-- root/root     52095 2010-03-16 16:08 lvmdump-cellopc-20100316150828/vgscan
    -rw-r--r-- root/root    177772 2010-03-16 16:08 lvmdump-cellopc-20100316150828/dev_listing
    -rw-r--r-- root/root       261 2010-03-16 16:08 lvmdump-cellopc-20100316150828/vgs
    -rw-r--r-- root/root      2093 2010-03-16 16:08 lvmdump-cellopc-20100316150828/pvs
    -rw-r--r-- root/root      6700 2010-03-16 16:08 lvmdump-cellopc-20100316150828/messages
    -rw-r--r-- root/root     18276 2010-03-16 16:08 lvmdump-cellopc-20100316150828/ps_info
    -rw-r--r-- root/root       348 2010-03-16 16:08 lvmdump-cellopc-20100316150828/lvs
    -rw-r--r-- root/root       135 2010-03-16 16:08 lvmdump-cellopc-20100316150828/dmsetup_table
    -rw-r--r-- root/root     88641 2010-03-16 16:08 lvmdump-cellopc-20100316150828/sysblock_listing
    -rw-r--r-- root/root       184 2010-03-16 16:08 lvmdump-cellopc-20100316150828/pvscan
    -rw-r--r-- root/root       109 2010-03-16 16:08 lvmdump-cellopc-20100316150828/dmsetup_status
    drwxr-xr-x root/root         0 2010-03-04 09:14 lvmdump-cellopc-20100316150828/lvm/
    drwx------ root/root         0 2010-03-03 23:29 lvmdump-cellopc-20100316150828/lvm/archive/
    -rw------- root/root      1149 2010-03-03 22:37 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00006.vg
    -rw------- root/root      1159 2010-03-03 23:27 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00008.vg
    -rw------- root/root      1160 2010-03-03 23:01 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_new_00000.vg
    -rw------- root/root      1151 2010-03-03 22:33 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00004.vg
    -rw------- root/root      1131 2010-03-03 21:47 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00003.vg
    -rw------- root/root      1131 2010-03-03 21:47 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00002.vg
    -rw------- root/root      1145 2009-12-04 09:20 lvmdump-cellopc-20100316150828/lvm/archive/lv_data_00001.vg
    -rw------- root/root      1177 2010-03-03 23:29 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00009.vg
    -rw------- root/root      1452 2009-12-04 09:17 lvmdump-cellopc-20100316150828/lvm/archive/vg_root_00000.vg
    -rw------- root/root      1138 2010-03-03 22:33 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00005.vg
    -rw------- root/root       830 2009-12-04 09:21 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00001.vg
    -rw------- root/root      1132 2009-12-04 09:17 lvmdump-cellopc-20100316150828/lvm/archive/lv_data_00000.vg
    -rw------- root/root       806 2009-12-04 09:20 lvmdump-cellopc-20100316150828/lvm/archive/lv_data_00002.vg
    -rw------- root/root      1178 2010-03-03 23:29 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00010.vg
    -rw------- root/root      1156 2010-03-03 23:01 lvmdump-cellopc-20100316150828/lvm/archive/vg_data_00007.vg
    drwx------ root/root         0 2010-03-03 23:29 lvmdump-cellopc-20100316150828/lvm/backup/
    -rw------- root/root      1159 2010-03-03 23:29 lvmdump-cellopc-20100316150828/lvm/backup/vg_data
    -rw------- root/root      1458 2010-03-03 22:00 lvmdump-cellopc-20100316150828/lvm/backup/vg_root
    -rw-r--r-- root/root     18793 2010-03-04 09:14 lvmdump-cellopc-20100316150828/lvm/lvm.conf
    drwx------ root/root         0 2010-03-16 16:08 lvmdump-cellopc-20100316150828/lvm/cache/
    -rw------- root/root      1859 2010-03-16 16:08 lvmdump-cellopc-20100316150828/lvm/cache/.cache
    -rw-r--r-- root/root      2366 2010-03-16 16:08 lvmdump-cellopc-20100316150828/lvmdump.log
    -rw-r--r-- root/root       538 2010-03-16 16:08 lvmdump-cellopc-20100316150828/versions

Aggiungendo l'opzione "-m" verranno collezionati anche i metadata di tutti i PV (Volumi Fisici) in uso:

    [root@cellopc ~]# lvmdump -am
    Creating dump directory: /root/lvmdump-cellopc-20100316151008
     
    Gathering LVM volume info...
      vgscan...
      pvscan...
      lvs...
      pvs...
      vgs...
    Gathering LVM & device-mapper version info...
    Gathering dmsetup info...
    Gathering process info...
    Gathering console messages...
    Gathering /etc/lvm info...
    Gathering /dev listing...
    Gathering /sys/block listing...
    Gathering LVM metadata from Physical Volumes...
      /dev/sda2
      /dev/sda3
    Creating report tarball in /root/lvmdump-cellopc-20100316151008.tgz...

LVMDISKSCAN
-----------

Questo comando permette di avere una lista di tutti i volumi gestiti da LVM sulla macchina:

    [root@node02 rules.d]# lvmdiskscan -l
      WARNING: only considering LVM devices
      /dev/vda2              [       7.51 GiB] LVM physical volume
      /dev/mapper/lunsvn01p1 [     972.65 MiB] LVM physical volume
      0 LVM physical volume whole disks
      2 LVM physical volumes

LVMSAR
------

Non ancora implementato in LVM2.

LVMSADC
-------

Non ancora implementato in LVM2.

LVMCHANGE
---------

Non ancora implementato in LVM2.

<Categoria:LVM>
