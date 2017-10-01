-   Dopo aver creato un device multipath creare un PV sulla partizione creata sul disco.

<!-- -->

    [root@cw-spmi-mgm02 mpath]# pvcreate /dev/mpath/HSV210_07p1 
      Physical volume "/dev/mpath/HSV210_07p1" successfully created
      Total: 5 [637.81 GB] / in use: 4 [617.82 GB] / in no VG: 1 [19.99 GB] 

-   Verificare che il PV sia stato creato correttamente, e che non sia legato a nessun VG.

<!-- -->

    [root@cw-spmi-mgm02 mpath]# pvs                                           
      PV                     VG         Fmt  Attr PSize   PFree               
      /dev/cciss/c0d0p2      VolGroup00 lvm2 a-    68.22G     0               
      /dev/mpath/HSV210_01p1 vg_export  lvm2 a-   499.99G     0               
      /dev/mpath/HSV210_02p1 vg_postfix lvm2 a-     1.91G     0               
      /dev/mpath/HSV210_02p2 vg_hyperic lvm2 a-    47.69G     0               
      /dev/mpath/HSV210_07p1            lvm2 --    19.99G 19.99G         

-   Associare il PV ad un nuovo VG o aggiungerlo ad un VG già esistente. Nell'esempio verrà creato un nuovo VG.

<!-- -->

    [root@cw-spmi-mgm02 mpath]# vgcreate vg_activemq /dev/mpath/HSV210_07p1 
      Volume group "vg_activemq" successfully created         

-   Non si potrà creare alcun logical volume sul nuovo VG perchè sono state apportate delle modifiche alla configurazione di LVM.
    È stato configurato LVM per non abilitare i logical volume che non siano dischi interni o che contengano il tag associato dal cluster. Infatto il cluster quando abilita dei VG associa un tag "@..." con il nome del nodo preso dal file di configurazione del cluster stesso.

<!-- -->

-   Per controllare eventuali etichette associate ai VG si dovrà utilizzare il comando vgs con l'opzione **-o+tags**.

<!-- -->

    [root@cw-spmi-mgm02 mpath]# vgs -a -o+tags
      VG          #PV #LV #SN Attr   VSize   VFree  VG Tags  
      VolGroup00    1   2   0 wz--n-  68.22G     0           
      vg_activemq   1   0   0 wz--n-  19.99G 19.99G          
      vg_export     1   1   0 wz--n- 499.99G     0           
      vg_hyperic    1   1   0 wz--n-  47.69G     0  mgmnode02
      vg_postfix    1   1   0 wz--n-   1.91G     0  mgmnode02

-   Se il VG non è attivo su qualche altro nodo e non ha nessuno tag associato allora si potrà attivarlo, forzando il tag manualmente e poi abilitandolo.
    Per prima cosa tramite il comando vgchange con l'opzione **--addtag** passare il tag (senza @) da associare al VG, e quindi il nome del VG.

Dopo aver fatto ciò abilitare il VG con il comando **vgchange** e l'opzione **-ay**.

    [root@cw-spmi-mgm02 mpath]# vgchange --addtag mgmnode02 vg_activemq
      Volume group "vg_activemq" successfully changed                  
    [root@cw-spmi-mgm02 mpath]# vgs -a -o+tags
      VG          #PV #LV #SN Attr   VSize   VFree  VG Tags  
      VolGroup00    1   2   0 wz--n-  68.22G     0           
      vg_activemq   1   0   0 wz--n-  19.99G 19.99G mgmnode02
      vg_export     1   1   0 wz--n- 499.99G     0           
      vg_hyperic    1   1   0 wz--n-  47.69G     0  mgmnode02
      vg_postfix    1   1   0 wz--n-   1.91G     0  mgmnode02
    [root@cw-spmi-mgm02 mpath]# vgchange -ay vg_activemq
      0 logical volume(s) in volume group "vg_activemq" now active

-   Ora è possibile creare il LV associandolo al VG appena attivato.

<!-- -->

    [root@cw-spmi-mgm02 mpath]# lvcreate -l +100%FREE vg_activemq -n lv_activemq
      Logical volume "lv_activemq" created                                      
    [root@cw-spmi-mgm02 mpath]# lvs                                             
      LV          VG          Attr   LSize   Origin Snap%  Move Log Copy%  Convert
      LogVol00    VolGroup00  -wi-ao  64.22G                                      
      LogVol01    VolGroup00  -wi-ao   4.00G                                      
      lv_activemq vg_activemq -wi-a-  19.99G                                      
      lv_export   vg_export   -wi--- 499.99G                                      
      lv_hyperic  vg_hyperic  -wi-ao  47.69G                                      
      lv_postfix  vg_postfix  -wi-ao   1.91G   

-   Creare il filesystem di tipo ext3, ext4 o del formato desiderato.

<!-- -->

    [root@cw-spmi-mgm02 mpath]# mkfs.ext3 /dev/vg_activemq/lv_activemq 
    mke2fs 1.39 (29-May-2006)                                          
    Filesystem label=
    OS type: Linux
    Block size=4096 (log=2)
    Fragment size=4096 (log=2)
    2621440 inodes, 5240832 blocks
    262041 blocks (5.00%) reserved for the super user
    First data block=0
    Maximum filesystem blocks=4294967296
    160 block groups
    32768 blocks per group, 32768 fragments per group
    16384 inodes per group
    Superblock backups stored on blocks:
            32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
            4096000

    Writing inode tables: done
    Creating journal (32768 blocks): done
    Writing superblocks and filesystem accounting information: done

    This filesystem will be automatically checked every 24 mounts or
    180 days, whichever comes first.  Use tune2fs -c or -i to override.

-   Ora eseguire il tuning del filesystem per non far eseguire l'fsck forzato ogni 24 mount o 180 giorni. Inoltre si imposteranno alcune opzioni aggiunte per supportare le acl.

<!-- -->

    [root@cw-spmi-mgm02 mpath]# tune2fs -c0 -i0 -o acl,user_xattr /dev/vg_activemq/lv_activemq
    tune2fs 1.39 (29-May-2006)
    Setting maximal mount count to -1
    Setting interval between checks to 0 seconds

-   Al termine delle attività bisognerà ricordarsi di smontare il filesystem (se verrà smontato), dopo di che disabilitare il VG con il comando vgchange con l'opzione "-an" e poi rimuovere il tag.

    [root@cw-spmi-mgm02 mpath]# vgchange -an vg_activemq
      0 logical volume(s) in volume group "vg_activemq" now active
    [root@cw-spmi-mgm02 mpath]# vgchange --deltag mgmnode02 vg_activemq
      Volume group "vg_activemq" successfully changed
    [root@cw-spmi-mgm02 mpath]# vgs -a -o+tags
      VG          #PV #LV #SN Attr   VSize   VFree VG Tags
      VolGroup00    1   2   0 wz--n-  68.22G    0
      vg_activemq   1   1   0 wz--n-  19.99G    0
      vg_export     1   1   0 wz--n- 499.99G    0
      vg_hyperic    1   1   0 wz--n-  47.69G    0  mgmnode02
      vg_postfix    1   1   0 wz--n-   1.91G    0  mgmnode02

-   Se il nuovo fielsystem non verrà usato dal cluster, ma dovrà essere montato sui due sistemi, per non rifare sempre questa procedura si dovrà modificare il file di configurazione del LVM per poter far attivare il nuovo VG.

<!-- -->

-   Se il VG verrà utilizzato dal cluster, l'attivazione dei volumi verrà permessa dal LVM se è stato inserito il tag nel "volume\_list" del file di configurazione del LVM.
    Se manca ciò, la modifica sarà da apportare su tutti i nodi del cluster.

<Categoria:LVM>
