\_\_TOC\_\_

Introduzione
------------

Il repo Remi è creato e mantenuto da Remi Collet, appassionato di Fedora. I pacchetti con i quali è diventato famoso sono firefox5, mysql-workbench, php-oci8, php-fpm..., ma ultimamente include tutti i componenti di un sistema [LAMP](LAMP "wikilink"), mozilla e le ultime versioni del software per Fedora.
Il repo è disponibile per le versioni di Fedora dalla 10 compresa in poi.

Installazione
-------------

In ogni caso è necessario installare la chiave GPG:

`rpm --import `[`http://rpms.famillecollet.com/RPM-GPG-KEY-remi`](http://rpms.famillecollet.com/RPM-GPG-KEY-remi)

### Installazione automatica

Per ogni versione di Fedora è necessario inserire il numero esatto, come evidenziato in questi esempi: Per **Fedora 16** Verne

`# yum install --nogpgcheck `[`http://rpms.famillecollet.com/remi-release-16.rpm`](http://rpms.famillecollet.com/remi-release-16.rpm)

Per **Fedora 15** Lovelock

`# yum install --nogpgcheck `[`http://rpms.famillecollet.com/remi-release-15.rpm`](http://rpms.famillecollet.com/remi-release-15.rpm)

Per **Fedora 14** Laughlin

`# yum install --nogpgcheck `[`http://rpms.famillecollet.com/remi-release-14.rpm`](http://rpms.famillecollet.com/remi-release-14.rpm)

### Installazione manuale

Si può facilmente creare un file */etc/yum.repos.d/remi.repo* digitando da root:

`# gedit /etc/yum.repos.d/remi.repo`

e inserire le seguenti righe:

`[remi]`
`name=Les RPM de remi $releasever - $basearch`
`#baseurl=`[`http://rpms.famillecollet.com/fedora/$releasever/remi/$basearch/`](http://rpms.famillecollet.com/fedora/$releasever/remi/$basearch/)
`mirrorlist=`[`http://rpms.famillecollet.com/fedora/$releasever/remi/mirror`](http://rpms.famillecollet.com/fedora/$releasever/remi/mirror)
`enabled=0`
`gpgcheck=1`
`gpgkey=`[`http://rpms.famillecollet.com/RPM-GPG-KEY-remi`](http://rpms.famillecollet.com/RPM-GPG-KEY-remi)

Salvare e chiudere.
Il repo è pronto per l'uso, ma non è attivo di default (consigliato). Se si volesse installare dei pacchetti provenienti dal repo di Remi è necessario attivarlo per la singola operazione:

`# yum --enablerepo=remi install nome_pacchetto`

Riferimenti
-----------

-   [Sito RPM di Remi Collet](http://rpms.famillecollet.com/)

<Categoria:Repository>
