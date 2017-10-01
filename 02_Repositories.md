\_\_TOC\_\_

Come aggiungere dei repositories extra
--------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Sostituisci il tuo vecchio file yum.conf con uno più recente

`cd /etc`
`mv -f yum.conf yum.conf.bak`
`wget `[`http://www.fedorafaq.org/samples/yum.conf`](http://www.fedorafaq.org/samples/yum.conf)
`rpm -Uvh `[`http://www.fedorafaq.org/yum`](http://www.fedorafaq.org/yum)

Aggiungi i repos di RPMforge
----------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come importare una chiave GPG](#Come_importare_una_chiave_GPG "wikilink")

Aggiungere un repo RPMforge è un'alternativa ai repos che vengono installati dai siti web delle fedorafaq. N.B.: Questi due gruppi sono mutuamente incompatibili e possono causare errori nelle tue installazioni se utilizzati insieme in updates automatici.

### freshrpms

`rpm -ivh `[`http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/5/freshrpms-release/freshrpms-release-1.1-1.fc.noarch.rpm`](http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/5/freshrpms-release/freshrpms-release-1.1-1.fc.noarch.rpm)

### dries

`gedit /etc/yum.repos.d/dries.repo`

Aggiungi le seguenti linee al nuovo file

`[dries]`
`name=Extra Fedora rpms dries - $releasever - $basearch`
`baseurl=`[`http://ftp.belnet.be/packages/dries.ulyssis.org/fedora/linux/$releasever/$basearch/dries/RPMS/`](http://ftp.belnet.be/packages/dries.ulyssis.org/fedora/linux/$releasever/$basearch/dries/RPMS/)
[`http://apt.sw.be/dries/fedora/fc5/$basearch/dries/RPMS/`](http://apt.sw.be/dries/fedora/fc5/$basearch/dries/RPMS/)
`failovermethod=priority`
`enabled=0`
`gpgcheck=1`

### newrpms

`gedit /etc/yum.repos.d/newrpms.repo`

Aggiungi le seguenti linee al nuovo file:

`[newrpms.sunsite.dk]`
`name=Fedora Core 5 i386 NewRPMS.sunsite.dk`
`baseurl=`[`http://newrpms.sunsite.dk/apt/redhat/en/$basearch/fc$releasever`](http://newrpms.sunsite.dk/apt/redhat/en/$basearch/fc$releasever)
[`http://newrpms.atrpms.net/apt/redhat/en/$basearch/fc$releasever`](http://newrpms.atrpms.net/apt/redhat/en/$basearch/fc$releasever)
`failovermethod=priority`
`enabled=0`
`gpgcheck=1`

Come importare una chiave GPG
-----------------------------

Ricorda che devi avere i privilegi di root per fare questo. Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

`rpm --import `[`http://freshrpms.net/packages/RPM-GPG-KEY.txt`](http://freshrpms.net/packages/RPM-GPG-KEY.txt)
`rpm --import `[`http://dries.ulyssis.org/rpm/RPM-GPG-KEY.dries.txt`](http://dries.ulyssis.org/rpm/RPM-GPG-KEY.dries.txt)
`rpm --import `[`http://newrpms.sunsite.dk/gpg-pubkey-newrpms.txt`](http://newrpms.sunsite.dk/gpg-pubkey-newrpms.txt)
`rpm --import /usr/share/doc/fedora-release-*/*GPG-KEY*`

<Categoria:Fedoraserver>
