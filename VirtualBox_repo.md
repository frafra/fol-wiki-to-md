\_\_TOC\_\_

Introduzione
------------

VirtualBox è un applicativo proprietario multipiattaforma per la virtualizzazione di sistemi operativi sviluppato da Oracle. Il repo è disponibile dalla versione Fedora 14 in poi.

Installazione
-------------

Si scarica il repo e lo si posiziona nella cartella /etc/yum.repos.d/, da root:

`# curl `[`http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo`](http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo)` -o /etc/yum.repos.d/virtualbox.repo`

Il repository è attivo di default ma bisogna installare alcune dipendenze necessarie per far girare VirtualBox:

`# yum install dkms binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel`

A questo punto si può installare l'ultima versione di VirtualBox (attualmente la 4.2.x):

`# yum install VirtualBox-4.2`

Configurazione
--------------

VirtualBox può essere configurato seguendo le istruzioni della guida [Installare e configurare Virtualbox](Installare_e_configurare_Virtualbox "wikilink")

Risoluzione problemi
--------------------

Può capitare che dopo un aggiornamento generico del sistema, VirtualBox non parta e lanci un pannello di allarme. Questo succede perché non sono stati aggiornati i moduli di VirtualBox (vboxdrv, vboxnetflt e vboxnetadp) dopo l'aggiornamento al nuovo kernel. Questa situazione può essere risolta installando il pacchetto *dkms*

`# yum install dkms`

Riferimenti
-----------

[Sito ufficiale VirtualBox](https://www.virtualbox.org/)

<Categoria:Yum> <Categoria:Repository> <Categoria:Virtualizzazione>
