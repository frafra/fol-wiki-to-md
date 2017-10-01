\_\_TOC\_\_

Introduzione
------------

JPackage è utile per l'installazione di pacchetti java. Il repo è disponibile attualmente per tutte le versioni di Fedora, sia stabile che testing.

Installazione
-------------

### Installazione automatica

`# yum install yum-priorities`
`# rpm -ivh `[`http://mirrors.dotsrc.org/jpackage/5.0/generic/free/RPMS/jpackage-release-5-4.jpp5.noarch.rpm`](http://mirrors.dotsrc.org/jpackage/5.0/generic/free/RPMS/jpackage-release-5-4.jpp5.noarch.rpm)

### Installazione manuale

Per l'installazione manuale della versione 5 è necessario crearsi il repo.file, da root:

`# gedit /etc/yum.repos.d/jpackage50.repo`

e inserire le seguenti righe:

`[jpackage50-generic]`
`name=JPackage (free), generic`
`baseurl=`[`http://mirrors.dotsrc.org/jpackage/5.0/generic/free/`](http://mirrors.dotsrc.org/jpackage/5.0/generic/free/)
`failovermethod=priority`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`http://www.jpackage.org/jpackage.asc`](http://www.jpackage.org/jpackage.asc)
` `
`[jpackage50-generic-nonfree]`
`name=JPackage (non-free), generic`
`baseurl=`[`http://mirrors.dotsrc.org/jpackage/5.0/generic/non-free/`](http://mirrors.dotsrc.org/jpackage/5.0/generic/non-free/)
`failovermethod=priority`
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`http://www.jpackage.org/jpackage.asc`](http://www.jpackage.org/jpackage.asc)

Salvare e chiudere.
Il repo è pronto per l'uso, ma non è attivo di default (consigliato). Se si volesse installare dei pacchetti provenienti da JPackage è necessario attivarlo per la singola operazione:

`# yum --enablerepo=jpackage install nome_pacchetto`

Riferimenti
-----------

-   [Sito ufficiale JPackage](http://www.jpackage.org/yum.php)

<Categoria:Repository>
