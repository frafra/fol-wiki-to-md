\_\_TOC\_\_

In RHEL, per rendere più performanti alcune funzionalità di LVM2 con le periferiche multipath (periferiche in cui esiste più di un collegamento fisico tra la CPU e la memoria di massa), sono state apportate delle modifiche al file /etc/lvm/lvm.conf.

Preferred\_names
----------------

È stato aggiunto nel parametro preferred\_names, la lista di espressioni regolari sotto ripotarta, per rendere più visibili l'output dei comandi come pvscan, perchè al posto di restitutire il path /dev/dm-n, verrà mostrato un path più intuitivo.

    [root@node01 init.d]# pvscan                                              
      PV /dev/dm-5                      lvm2 [972.65 MB]        

Apportare dunque la modifica al file di configurazione, modificando:

`preferred_names = [ ]`

in:

`preferred_names = [ "^/dev/mpath/", "^/dev/[hs]d" ]`

Dopo la modifica l'output dei comandi come pvs o pvscan sarà similare a questo.

    [root@node01 boot]# pvs
      PV                  VG   Fmt  Attr PSize   PFree  
      /dev/mpath/mpath0p1      lvm2 --   972.65M 972.65M

Filters
-------

La seconda modifica riguarda il filtro impostato, per non eseguire uno scan continuo di block device non in uso.
Nel parametro filter è stato passato il controllo di tutti i block device che riguardano i device interni (/dev/cciss) e dei device multipath (/dev/multipath), escludendo i singoli path fisici dei dischi, perchè nelle configurazioni ghost degli storage LVM riscontrerebbe degli errori.
Nel file /etc/lvm/lvm.conf modificare:

`filter = [ "a/.*/" ]`

in:

`filter = [ "a|^/dev/cciss/.*|", "a|^/dev/mpath/.*|", "r|.*|" ]`

Note
----

Per ogni modifica al file di configurazione di LVM2, bisognerà ricreare l'immagine del ramdisk, in modo da applicare la modifiche.

    [root@node01 init.d]# cd /boot/
    [root@node01 boot]# cp initrd-2.6.18-128.el5.img initrd-2.6.18-128.el5.img.orig
    [root@node01 boot]# mkinitrd -v -f initrd-2.6.18-128.el5.img 2.6.18-128.el5
    Creating initramfs                                                         
    Looking for deps of module ehci-hcd                                        
    Looking for deps of module ohci-hcd                                        
    Looking for deps of module uhci-hcd                                        
    Looking for deps of module ext3: jbd                                       
    Looking for deps of module jbd                                             
    Looking for driver for device hdb1                                         
    Looking for deps of module ide:m-disk                                      
    Looking for deps of module pci:v00008086d00007111sv00000000sd00000000bc01sc01i8a: scsi_mod libata ata_piix 
    Looking for deps of module scsi_mod                                                                        
    Looking for deps of module sd_mod: scsi_mod                                                                
    Looking for deps of module libata: scsi_mod                                                                
    Looking for deps of module ata_piix: scsi_mod libata                                                       
    Looking for driver for device hda2                                                                         
    Looking for deps of module ide:m-disk                                                                      
    Looking for deps of module pci:v00008086d00007111sv00000000sd00000000bc01sc01i8a: scsi_mod libata ata_piix 
    Looking for deps of module ahci: scsi_mod libata                                                           
    Looking for deps of module ide-disk                                                                        
    Looking for deps of module dm-mod                                                                          
    Looking for deps of module dm-mirror: dm-mod dm-log                                                        
    Looking for deps of module dm-log: dm-mod                                                                  
    Looking for deps of module dm-zero: dm-mod                                                                 
    Looking for deps of module dm-snapshot: dm-mod                                                             
    Looking for deps of module dm-mem-cache                                                                    
    Looking for deps of module dm-region_hash: dm-mod dm-log                                                   
    Looking for deps of module dm-message                                                                      
    Looking for deps of module dm-raid45: dm-message dm-mod dm-mem-cache dm-log dm-region_hash                 
    Using modules:  /lib/modules/2.6.18-128.el5/kernel/drivers/usb/host/ehci-hcd.ko /lib/modules/2.6.18-128.el5/kernel/drivers/usb/host/ohci-hcd.ko /lib/modules/2.6.18-128.el5/kernel/drivers/usb/host/uhci-hcd.ko /lib/modules/2.6.18-128.el5/kernel/fs/jbd/jbd.ko /lib/modules/2.6.18-128.el5/kernel/fs/ext3/ext3.ko /lib/modules/2.6.18-128.el5/kernel/drivers/scsi/scsi_mod.ko /lib/modules/2.6.18-128.el5/kernel/drivers/scsi/sd_mod.ko /lib/modules/2.6.18-128.el5/kernel/drivers/ata/libata.ko /lib/modules/2.6.18-128.el5/kernel/drivers/ata/ata_piix.ko /lib/modules/2.6.18-128.el5/kernel/drivers/ata/ahci.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-mod.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-log.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-mirror.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-zero.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-snapshot.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-mem-cache.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-region_hash.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-message.ko /lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-raid45.ko                                                                                                                              
    /sbin/nash -> /tmp/initrd.jQ3151/bin/nash                                                                                                                    
    /sbin/insmod.static -> /tmp/initrd.jQ3151/bin/insmod                                                                                                         
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/usb/host/ehci-hcd.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/ehci-hcd.ko' [elf32-i386]                
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/usb/host/ohci-hcd.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/ohci-hcd.ko' [elf32-i386]                
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/usb/host/uhci-hcd.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/uhci-hcd.ko' [elf32-i386]                
    copy from `/lib/modules/2.6.18-128.el5/kernel/fs/jbd/jbd.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/jbd.ko' [elf32-i386]                                    
    copy from `/lib/modules/2.6.18-128.el5/kernel/fs/ext3/ext3.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/ext3.ko' [elf32-i386]                                 
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/scsi/scsi_mod.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/scsi_mod.ko' [elf32-i386]                    
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/scsi/sd_mod.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/sd_mod.ko' [elf32-i386]                        
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/ata/libata.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/libata.ko' [elf32-i386]                         
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/ata/ata_piix.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/ata_piix.ko' [elf32-i386]                     
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/ata/ahci.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/ahci.ko' [elf32-i386]                             
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-mod.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-mod.ko' [elf32-i386]                          
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-log.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-log.ko' [elf32-i386]                          
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-mirror.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-mirror.ko' [elf32-i386]                    
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-zero.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-zero.ko' [elf32-i386]                        
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-snapshot.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-snapshot.ko' [elf32-i386]                
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-mem-cache.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-mem-cache.ko' [elf32-i386]              
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-region_hash.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-region_hash.ko' [elf32-i386]          
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-message.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-message.ko' [elf32-i386]                  
    copy from `/lib/modules/2.6.18-128.el5/kernel/drivers/md/dm-raid45.ko' [elf32-i386] to `/tmp/initrd.jQ3151/lib/dm-raid45.ko' [elf32-i386]                    
    /sbin/lvm.static -> /tmp/initrd.jQ3151/bin/lvm                                                                                                               
    /etc/lvm -> /tmp/initrd.jQ3151/etc/lvm                                                                                                                       
    `/etc/lvm/lvm.conf' -> `/tmp/initrd.jQ3151/etc/lvm/lvm.conf'                                                                                                 
    /sbin/dmraid.static -> /tmp/initrd.jQ3151/bin/dmraid                                                                                                         
    /sbin/kpartx.static -> /tmp/initrd.jQ3151/bin/kpartx                                                                                                         
    Adding module ehci-hcd                                                                                                                                       
    Adding module ohci-hcd                                                                                                                                       
    Adding module uhci-hcd                                                                                                                                       
    Adding module jbd                                                                                                                                            
    Adding module ext3                                                                                                                                           
    Adding module scsi_mod                                                                                                                                       
    Adding module sd_mod                                                                                                                                         
    Adding module libata                                                                                                                                         
    Adding module ata_piix                                                                                                                                       
    Adding module ahci                                                                                                                                           
    Adding module dm-mod                                                                                                                                         
    Adding module dm-log                                                                                                                                         
    Adding module dm-mirror                                                                                                                                      
    Adding module dm-zero                                                                                                                                        
    Adding module dm-snapshot                                                                                                                                    
    Adding module dm-mem-cache                                                                                                                                   
    Adding module dm-region_hash                                                                                                                                 
    Adding module dm-message                                                                                                                                     
    Adding module dm-raid45                         

Nelle ultime versioni di Fedora e RedHat non è più presente initrd, ma initramfs, per questo si dovrà utilizzare il comando **dracut** per eseguire l'aggiornamento.

<Categoria:LVM>
