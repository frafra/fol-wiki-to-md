Introduzione
------------

Questo documento tratta dei principali repository di terze parti di fedora, **RPMFusion**.
RPMFusion distingue tra programmi free e nonfree (nel senso di software "non libero", non nel senso di "non gratuito"), ciascuno con una locazione propria.

Il repo RPMFusion-free non dipende da nessun altro repository (se non quelli predefiniti e ufficiali di Fedora) e quindi può essere utilizzato senza RPMFusion-nonfree. Al contrario, RPMFusion-nonfree dipende anche da RPMFusion-free.

La guida espone due metodi differenti per l'installazione di tali repository.

Installazione tramite pacchetto rpm
-----------------------------------

Per i free di Fedora 22 per esempio, il pacchetto da scaricare è [questo](http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-22.noarch.rpm), mentre per i nonfree è [questo](http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-22.noarch.rpm). Si possono poi installare tramite installatore grafico semplicemente tramite doppio clic su tali files. Per altre versioni di Fedora fare riferimento alla [pagina ufficiale](http://rpmfusion.org/Configuration).

In caso di problemi in quest'ultimo passaggio, se non si volesse installare in locale entrambi i repo, è possibile farlo attingendo ai link sfruttando le potenzialità di dnf:

`# dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm`

Installazione manuale
---------------------

È, ovviamente, possibile inserire a mano i repo creando dei files di testo da inserire all'interno della directory */etc/yum.repos.d/*, che è esattamente cioè che fa il pacchetto rpm in automatico.

### RPMFusion-free

Usando nano (o qualsiasi editor si preferisca):

`# nano /etc/yum.repos.d/rpmfusion-free.repo`

Si apre il documento vuoto che deve essere così popolato:

`[rpmfusion-free]`
`name=RPM Fusion for Fedora $releasever - Free`
`#baseurl=http://download1.rpmfusion.org/free/fedora/releases/$releasever/Everything/$basearch/os/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=free-fedora-$releasever&arch=$basearch`
`enabled=1`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever)
`[rpmfusion-free-debuginfo]`
`name=RPM Fusion for Fedora $releasever - Free - Debug`
`#baseurl=http://download1.rpmfusion.org/free/fedora/releases/$releasever/Everything/$basearch/debug/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=free-fedora-debug-$releasever&arch=$basearch`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever)
`[rpmfusion-free-source]`
`name=RPM Fusion for Fedora $releasever - Free - Source`
`#baseurl=http://download1.rpmfusion.org/free/fedora/releases/$releasever/Everything/source/SRPMS/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=free-fedora-source-$releasever&arch=$basearch`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever)
`dopodichè si provvederà a creare il repo free-updates:`
`# nano /etc/yum.repos.d/rpmfusion-free-updates.repo`

da popolare così:

`[rpmfusion-free-updates]`
`name=RPM Fusion for Fedora $releasever - Free - Updates`
`#baseurl=http://download1.rpmfusion.org/free/fedora/updates/$releasever/$basearch/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=free-fedora-updates-released-$releasever&arch=$basearch`
`enabled=1`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever)
`[rpmfusion-free-updates-debuginfo]`
`name=RPM Fusion for Fedora $releasever - Free - Updates Debug`
`#baseurl=http://download1.rpmfusion.org/free/fedora/updates/$releasever/$basearch/debug/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=free-fedora-updates-released-debug-$releasever&arch=$basearch`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever)` `
`[rpmfusion-free-updates-source]`
`name=RPM Fusion for Fedora $releasever - Free - Updates Source`
`#baseurl=http://download1.rpmfusion.org/free/fedora/updates/$releasever/SRPMS/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=free-fedora-updates-released-source-$releasever&arch=$basearch`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora-$releasever)

### RPMFusion-nonfree

I repositori nonfree e nonfree-updates, rispettivamente devono essere creati così (al pari dei precedenti):

`# nano /etc/yum.repos.d/rpmfusion-nonfree.repo`

le cui istruzioni da inserire sono:

`[rpmfusion-nonfree]`
`name=RPM Fusion for Fedora $releasever - Nonfree`
`#baseurl=http://download1.rpmfusion.org/nonfree/fedora/releases/$releasever/Everything/$basearch/os/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=nonfree-fedora-$releasever&arch=$basearch`
`enabled=1`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever)` `
`[rpmfusion-nonfree-debuginfo]`
`name=RPM Fusion for Fedora $releasever - Nonfree - Debug`
`#baseurl=http://download1.rpmfusion.org/nonfree/fedora/releases/$releasever/Everything/$basearch/debug/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=nonfree-fedora-debug-$releasever&arch=$basearch`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever)
`[rpmfusion-nonfree-source]`
`name=RPM Fusion for Fedora $releasever - Nonfree - Source`
`#baseurl=http://download1.rpmfusion.org/nonfree/fedora/releases/$releasever/Everything/source/SRPMS/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=nonfree-fedora-source-$releasever&arch=$basearch`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever)
`ed il repositorio nonfree-updates:`
`# nano /etc/yum.repos.d/rpmfusion-nonfree-updates.repo`

con le seguenti istruzioni:

`[rpmfusion-nonfree-updates]`
`name=RPM Fusion for Fedora $releasever - Nonfree - Updates`
`#baseurl=http://download1.rpmfusion.org/nonfree/fedora/updates/$releasever/$basearch/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=nonfree-fedora-updates-released-$releasever&arch=$basearch`
`enabled=1`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever)
`[rpmfusion-nonfree-updates-debuginfo]`
`name=RPM Fusion for Fedora $releasever - Nonfree - Updates Debug`
`#baseurl=http://download1.rpmfusion.org/nonfree/fedora/updates/$releasever/$basearch/debug/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=nonfree-fedora-updates-released-debug-$releasever&arch=$basearch`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever)
`[rpmfusion-nonfree-updates-source]`
`name=RPM Fusion for Fedora $releasever - Nonfree - Updates Source`
`#baseurl=http://download1.rpmfusion.org/nonfree/fedora/updates/$releasever/SRPMS/`
`mirrorlist=http://mirrors.rpmfusion.org/mirrorlist?repo=nonfree-fedora-updates-released-source-$releasever&arch=$basearch`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever`](file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-nonfree-fedora-$releasever)

Conclusione
-----------

Seguite queste istruzioni si potranno installare molti più software non presenti nei normali repo di fedora, ad esempio i [codec](Multimedia_Player_e_codecs "wikilink") per la riproduzione di flussi dati, alcune [estensioni per gnome-shell](Estensioni_di_Gnome-Shell "wikilink") e molti altri programmi.
Per una lista completa di tutti i programmi disponibili da tutti i repo rpmfusion (che devono però già essere installati sul computer) si può fare così:

`$ dnf list available --disablerepo=* --enablerepo=rpmfusion-{free,free-updates,nonfree,nonfree-updates} |more`

Riferimenti
-----------

-   <http://www.rpmfusion.org/>

<Categoria:Repository> <Categoria:Dnf>
