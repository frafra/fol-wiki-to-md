\_\_TOC\_\_

Introduzione
------------

VirtualBox è un applicativo commerciale proprietario multi-piattaforma per la virtualizzazione di sistemi operativi sviluppato da Oracle. Si possono riscontrare alcuni problemi con il supporto USB: purtroppo ancora non è stata prevista una configurazione totalmente automatica.

Installazione tramite repository RPMFusion
------------------------------------------

VirtualBox è disponibile all'interno dei repository [RPMFusion](RPMFusion "wikilink"). Per installarlo è sufficiente eseguire da terminale

`# yum install akmod-VirtualBox VirtualBox`

Installazione tramite repository Oracle
---------------------------------------

L'installazione di VirtualBox utilizzando i repository ufficiali Oracle è descritta nella guida [VirtualBox repo](VirtualBox_repo "wikilink").

Configurazioni
--------------

Di seguito viene illustrato come abilitare alcune funzionalità non presenti nella versione base di VirtualBox, tramite l'installazione degli appositi Extension Pack.

### Installazione del Extension Pack

L'installazione degli Extension Pack permette di estendere le funzionalità di VirtualBox base aggiungendo le seguenti caratteristiche

-   Supporto per i device virtuali USB 2.0 (EHCI).
-   Supporto per il VirtualBox Remote Desktop Protocol (VRDP)
-   Intel PXE boot ROM con supporto per la scheda di rete E1000
-   Il supporto sperimentale per PCI su host Linux

L'Extension Pack può essere scaricato dalla sezione download del [sito ufficiale](https://www.virtualbox.org/wiki/Downloads), facendo attenzione a scegliere la stessa versione di VirtualBox. Per installarlo sarà sufficiente eseguire il pacchetto appena scaricato con un doppio click.

### Aggiunta utente al gruppo

Per poter abilitare il controller USB 2.0 (EHCI), bisogna aggiungere il proprio utente al gruppo *vboxusers* (controllare che non sia già stato fatto in automatico, usando il comando *groups*), con il seguente comando:

`# gpasswd -a $(logname) vboxusers`

Per rendere effettiva la modifica, prima di riutilizzare VirtualBox, occorre riavviare il sistema host.

### Compattare un disco virtuale VDI di Virtualbox (guest: Windows)

Con un utilizzo regolare di una macchina virtuale il corrispondente file VDI (*Virtual Disk Image*) cresce continuamente di volume, anche qualora si liberasse dello spazio rimuovendo file all'interno del sistema guest, questo perché i file non vengono realmente eliminati nel nulla, ma lo spazio occupato nel file system viene semplicemente indicato come "sovrascrivibile", se necessario, dal sistema.
La procedura di compattazione del file vdi purtroppo non è banale e richiede una preparazione del sistema ospite. Infatti, per ridurre la dimensione del file vdi, occorre che lo spazio libero disponibile sul sistema guest sia marcazo a zero.
Per diminuire il peso di un hard disk virtuale di un sistema ospite Windows si procede quindi come segue:

1.  \[da guest\] Come operazione preliminare è necessario deframmentare il sistema guest con l'apposito tool disponibile su Windows all'interno del *Pannello di controllo*;
2.  \[da guest\] Installare il programma [sdelete](http://technet.microsoft.com/en-us/sysinternals/bb897443), un'applicativo creato da Microsoft con delle funzionalità utili;
3.  \[da guest\] Dalla finestra DOS (richiamabile attraverso Start - Esegui - *cmd*) settare a zero lo spazio libero con:
        sdelete -z

4.  \[da host linux\] Per concludere compattare lo spazio del disco virtuale con:
        $ VBoxManage modifyvdi /percorso/a/nomefile.vdi compact

La compattazione di un disco virtuale può ridurre lo spazio occupato anche di decine di gigabyte.

Riferimenti
-----------

-   [Home](https://www.virtualbox.org/) del programma VirtualBox;
-   [Guida in italiano](http://www.stenoweb.it/node/134) su come comprimere spazio di un hard disk virtuale;
-   [Guida in inglese](http://www.kaibader.de/compact-virtualbox-vdi-images/) su come comprimere spazio di un hard disk virtuale;
-   [Pagina](http://technet.microsoft.com/en-us/sysinternals/bb897443) del programma *sdelete*.

<Categoria:Virtualizzazione>
