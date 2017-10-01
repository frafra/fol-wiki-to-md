`# yum install tftp-server system-config-netboot-cmd dchp`

-   Verificare che la directory */tftpboot* sia la stessa dalla quale il tftp-server fornisce i files. Nelle ultime versione il tftp-server fornisce i files partendo da */var/lib/tftpboot*; è perciò necessario modificare nella sua *conf* sotto */etc/xinet.d/tftp* la voce server\_args in modo che contenga il valore corretto passato al parametro *-s*. Dopo di che attivare il servizio tftp.

`# vim /etc/xinetd.d/tftp`
`# default: off`
`# description: The tftp server serves files using the trivial file transfer \`
`# protocol. The tftp protocol is often used to boot diskless \`
`# workstations, download configuration files to network-aware printers, \`
`# and to start the installation process for some operating systems.`
`service tftp`
`{`
`socket_type = dgram`
`protocol = udp`
`wait = yes`
`user = root`
`server = /usr/sbin/in.tftpd`
`server_args = -s /tftpboot`
`disable = yes`
`per_source = 11`
`cps = 100 2`
`flags = IPv4`
`}`

`# chkconfig tftp on`
`# chkconfig --list tftp`
`tftp on`

-   Creare le directory che conterranno i contenuti del dvd d'installazione e i file di kickstart, che permettono un'installazione automatica senza dover eseguire i passi via intefaccia grafica.

`# mkdir -p /dati/install/kickstars`
`# mkdir -p /dati/install/rhel5.3-x86`

-   Esportare via NFS le directory appena create, modificando il file */etc/exports* e poi eseguendo il restart del servizio.

`# vim /etc/exports`
`/dati/install/kickstarts *(no_root_squash,no_subtree_check,ro)`
`/dati/install/rhel5.3-x86 *(no_root_squash,no_subtree_check,ro)`
`# service nfs restart`
`Shutting down NFS mountd: [ OK ]`
`Shutting down NFS daemon: [ OK ]`
`Shutting down NFS quotas: [ OK ]`
`Shutting down NFS services: [ OK ]`
`Starting NFS services: [ OK ]`
`Starting NFS quotas: [ OK ]`
`Starting NFS daemon: [ OK ]`
`Starting NFS mountd: [ OK ]`
`# showmount -e 192.168.11.1`
`Export list for 192.168.11.1:`
`/dati *`
`/dati/install/rhel5.3-x86 *`
`/dati/install/kickstarts *`

-   Montare in locale la iso del DVD del sistema operativo e fare una copia completa del suo contenuto, all'interno della directory esportata via NFS che conterrà i file d'installazione.

`# mkdir -p /mnt/rhel5.3DVD`
`# mount -o loop /dati/rhel-server-5.3-i386-dvd.iso /mnt/rhel5.3DVD`
`# df -k /mnt/rhel5.3DVD/`
`Filesystem 1K-blocks Used Available Use% Mounted on`
`/dev/loop0 2943222 2943222 0 100% /mnt/rhel5.3DVD`
`# rsync -avSA /mnt/rhel5.3DVD/ /dati/install/rhel5.3-x86/`
`sending incremental file list`
`./`
`.discinfo`
`.treeinfo`
`...sent 3012581465 bytes received 48380 bytes 8546467.65 bytes/sec`
`total size is 3012018364 speedup is 1.00`

-   Ora bisogna impostare il server DHCP per assegnare indirizzi fissi ad ogni client e da qui passare le informazioni, per poter recuperare il kickstart ed eventuali file di configurazione. Nel file */etc/dhcpd.conf* configurare una sottorete (es 192.168.11.0), ed un eventuale range di ip da assegnare (192.168.11.20/50).

Per ogni client che dovrà essere installato verrà messa una regola per assegnare un indirizzo fisso in base alla scheda di rete collegata al sistema. E' stata introdotta anche una parte di PXE Specification, che in caso di richiesta da un PXEClient passa la directory tftp dove sono contenuti i file di configurazione e l'indirizzo ip del server che esporta in dati (nel nostro caso il server dove stiamo eseguendo le modifiche).

1.  cat /etc/dhcpd.conf

<!-- -->

    #
    # DHCP Server Configuration file.
    # see /usr/share/doc/dhcp*/dhcpd.conf.sample
    # see 'man 5 dhcpd.conf'
    #

    ddns-update-style interim;
    ignore client-updates;

    subnet 192.168.11.0 netmask 255.255.255.0 {

    option subnet-mask 255.255.255.0;

    range 192.168.11.20 192.168.11.50;
    default-lease-time 21600;
    max-lease-time 43200;

    #PXE-specific configuration directives...
    if substring (option vendor-class-identifier, 0, 9) = "PXEClient" {
    filename "linux-install/pxelinux.0";
    next-server 192.168.11.1;
    }

    host prova1 {
    option host-name "prova1";
    hardware ethernet 00:0C:29:29:E0:CE;
    fixed-address 192.168.11.21;
    }
    }

`# service dhcpd restart`
`Shutting down dhcpd: [ OK ]`
`Starting dhcpd: [ OK ]`

-   Ora bisognerà copiare i files *vmlinuz* e *initrd.img* dal dvd appena copia alla directory del tftpboot. Creare per prima cosa una directory sotto */tftpboot/linux-install* che contenga i file della versione del sistema operativo da installare. Dopo di che fare la copia dei file dalla iso montata in precedenza sotto questo direttorio (i files sono nella directory isolinux).

`# mkdir -p /tftpboot/linux-install/rhel5.3-x86`
`# cp /mnt/rhel5.3DVD/isolinux/vmlinuz /tftpboot/linux-install/rhel5.3-x86`
`# cp /mnt/rhel5.3DVD/isolinux/initrd.img /tftpboot/linux-install/rhel5.3-x86`

-   Sotto la directory /tftpboot/linux-install/pxelinux.cfg/ vengono messi i file di configurazione per il boot. Essi vengono richiesti dal bootloader *pxelinux.0* al *tftp-server* in un ordine specifico, partendo dal dettaglio maggiore al minor dettaglio. E' presente il file default che verrà caricato per ultimo. Editare questo file come nell'esempio sotto riportato.

Sotto la label 0 bisognerà passare il percorso del file *vmlinuz* e *initrd.img*, ed il percorso verrà inteso come la directory sotto /tftpbot/linux-install dove sono contenute i file copiati in precedenza. Quindi il percorso sarà formato dalla directory che fa riferimento al sistema operativo ed il nome del file copiato. Anche per initrd.img bisognerà passare il percorso sotto /tftpbot/linux-install, il method nfs con l'indirizzo ip del server che esporta via nfs ed il percorso dove trovare i dati.

`# vim /tftpboot/linux-install/pxelinux.cfg/default`

    default local
    timeout 100
    prompt 1
    display msgs/boot.msg
    F1 msgs/boot.msg
    F2 msgs/general.msg
    F3 msgs/expert.msg
    F4 msgs/param.msg
    F5 msgs/rescue.msg
    F7 msgs/snake.msg

    label local
    localboot 0

    label 1
    kernel rhel5.3-x86/vmlinuz
    append initrd=rhel5.3-x86/initrd.img ramdisk_size=9216 method=nfs:192.168.11.1:/dati/install/rhel5.3-x86 ip=dhcp

-   Ora eseguire il boot da rete sul client aspettando che ricerchi un server DHCP dalla scheda di rete attestata sulla rete utilizzata per l'installazione. Verrà mostrato poi il RedHat Installer. Da qui selezionando **0** si eseguirà il boot dalla macchina locale, mentre con il label impostato nel file sotto */tftpboot/linux-install/pxelinux.cfg/default*, verrà lanciato il kernel da rete (nel caso descritto qui opzione **1**).
-   E' possibile anche utilizzare i file di kickstart per automatizzare le fasi di installazione. Questo file viene generato da Anaconda (si trova sotto */root/anaconda-ks.cfg*), con estensione ks e permette il settaggio di diverse informazioni sul partizionamento, configurazione di rete. Dopo aver creato il file di kickstart, copiarlo all'interno della share nfs denominata kickstarts.

`# cat /dati/install/kickstarts/rhel5.3-x86.ks`

    # Kickstart file automatically generated by anaconda.
    install
    text
    reboot
    nfs --server=192.168.11.1 --dir=/dati/install/rhel5.3-x86/
    key --skip
    lang en_US.UTF-8
    keyboard it2
    network --device eth0 --bootproto dhcp
    network --device eth1 --onboot no --bootproto dhcp
    rootpw --iscrypted $1$ndSeUyMS$RVA3AENYbbwes9JwPFAx/.
    firewall --disabled
    authconfig --enableshadow --enablemd5
    selinux --disabled
    timezone Europe/Rome
    skipx
    bootloader --location=mbr --driveorder=sda
    # The following is the partition information you requested
    # Note that any partitions you deleted are not expressed
    # here so unless you clear all partitions first, this is
    # not guaranteed to work
    clearpart --linux --drives=sda
    part /boot --fstype ext3 --size=100 --ondisk=sda
    part pv.2 --size=0 --grow --ondisk=sda
    volgroup VolGroup00 --pesize=32768 pv.2
    logvol swap --fstype swap --name=LogVol01 --vgname=VolGroup00 --size=1504
    logvol / --fstype ext3 --name=LogVol00 --vgname=VolGroup00 --size=8576

    %packages
    @office
    @editors
    @text-internet
    @dialup
    @core
    @base
    @games
    @java
    @legacy-software-support
    @graphics
    @printing
    @sound-and-video
    @admin-tools
    @graphical-internet
    emacs
    kexec-tools
    fipscheck
    device-mapper-multipath
    libsane-hpaio

-   Nel file di configurazione sotto */tftpboot/linux-install/pxelinux.cfg/* bisognerà modificare il caricamento dell'immagine del sistema operativo. Dopo *l'initrd.img* bisognerà sostitutire il campo *method*, con il campo *ks*, passando il percorso del file kickstart che viene esportato via nfs e verrà utilizzato per l'installazione.

Se si ha un sistema con più schede di rete si dovrà indicare la schede di rete usata dall'host per recuperare le informazioni da nfs (quindi la scheda di rete attestata sulla stessa rete del server che riceve un ip dal DHCP) alla variabile ksdevice. Se si ha uno storage collegato e non si vuole che venga riconosciuto come device, si dovrà impostare anche il valore *nostorage*.

`# vim /tftpboot/linux-install/pxelinux.cfg/default`

`default local`
`timeout 100`
`prompt 1`
`display msgs/boot.msg`
`F1 msgs/boot.msg`
`F2 msgs/general.msg`
`F3 msgs/expert.msg`
`F4 msgs/param.msg`
`F5 msgs/rescue.msg`
`F7 msgs/snake.msg`
`label local`
`localboot 0`
`label 1`
`kernel rhel5.3-x86/vmlinuz`
`append initrd=rhel5.3-x86/initrd.img ramdisk_size=9216 ks=`[`nfs:192.168.11.1:/dati/install/kickstarts/rhel5.3-x86.ks`](nfs:192.168.11.1:/dati/install/kickstarts/rhel5.3-x86.ks)` ksdevice=eth1`

-   Ora eseguire il boot da rete sul client aspettando che ricerchi un server DHCP dalla scheda di rete attestata sulla rete utilizzata per l'installazione. Verrà mostrato poi il RedHat installer. Da qui selezionando 0 si eseguirà il boot dalla macchina locale, mentre con il label impostato nel file sotto */tftpboot/linux-install/pxelinux.cfg/default*, verrà lanciato il kernel da rete (nel caso specifico opzione **1**) e poi i passi dell'installazione completati in automatico.

<Categoria:Installazione>
