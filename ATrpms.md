\_\_TOC\_\_

Introduzione
------------

ATrpms fa parte dei repository di ***terze parti***. L'installazione è utile qualora si necessiti di pacchetti aggiuntivi in relazione alla multimedialità. Il repo è disponibile attualmente per le versioni da Fedora 12 compresa in poi, sia stabile che testing.

Installazione
-------------

In ogni caso è necessario installare la chiave GPG:

`rpm --import `[`http://packages.atrpms.net/RPM-GPG-KEY.atrpms`](http://packages.atrpms.net/RPM-GPG-KEY.atrpms)

### Configurazione manuale

Si può facilmente creare un file */etc/yum.repos.d/atrpms.repo* digitando da root:

`# gedit /etc/yum.repos.d/atrpms.repo`

e inserire le seguenti righe:

`[atrpms]`
`name=Fedora Core $releasever - $basearch - ATrpms`
`baseurl=`[`http://dl.atrpms.net/f$releasever-$basearch/atrpms/stable`](http://dl.atrpms.net/f$releasever-$basearch/atrpms/stable)
`gpgkey=`[`http://ATrpms.net/RPM-GPG-KEY.atrpms`](http://ATrpms.net/RPM-GPG-KEY.atrpms)
`enabled=0`
`gpgcheck=1`

Salvare e chiudere.
Il repo è pronto per l'uso, ma non è attivo di default (consigliato). Se si volesse installare dei pacchetti provenienti da ATrpms è necessario attivarlo per la singola operazione:

`# yum --enablerepo=atrpms install nome_pacchetto`

Riferimenti
-----------

-   [Sito ufficiale ATrpms](http://atrpms.net/)

<Categoria:Repository> <Categoria:Yum>
