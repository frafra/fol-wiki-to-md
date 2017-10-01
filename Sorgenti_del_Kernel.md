Compilare il kernel è un'operazione molto delicata, ma con le giuste precauzioni e calma si possono ottimizzare le prestazioni del proprio sistema. Cercare di avere sempre un kernel funzionante (la versione prima) a disposizione, potrebbe essere fondamentale. Per installare le sorgenti su Fedora viene richiesto:

1.  Aver installato qt-devel
2.  Aver installato gcc
3.  Sapere che kernel abbiamo
4.  Le sorgenti del nostro kernel

Quindi si inizia (procedura per l'architettura x86):
Per poter installare il pacchetto delle sorgenti verrà richiesto il pacchetto di sviluppo qt-devel e il compilatore gcc, quindi si installano con Yum:

`# yum install qt-devel`
`# yum install gcc`

Dopodiché si guarda che versione del kernel è installata:

`# uname -r`
`2.6.10-1.741_FC3`

Ora bisogna andare nella sezione [Downloads](http://www.fedoraonline.it/modules/mydownloads/) e scaricare il pacchetto adatto per il proprio kernel (nel nostro caso [questo](http://download.fedora.redhat.com/pub/fedora/linux/core/updates/3/SRPMS/kernel-2.6.10-1.741_FC3.src.rpm)). Tornare nel terminale e digitare dalla posizione dove lo si è scaricato:

`# rpm -Uvh kernel-2.6.10-1.741_FC3.src.rpm`
`preparing...##################(100%)`
`kernel-2.6.10......##################(100%)`

Spostarsi nella directory /usr/src/redhat/SPECS e modificare il file kernel-2.6.spec con un editor qualsiasi (anche MC) in modo da avere i valori dei seguenti parametri del file kernel-2.6.spec in questo modo:

`# cd /usr/src/redhat/SPECS`
`%define buildup 0`
`%define buildsmp 0`
`%define buildsource 1`
`%define builddoc 0`

Salvare il file e costruire il proprio RPM:

`[root@localhost SPECS]# rpmbuild --target i686 -ba kernel-2.6.spec`

Ora serve un po' di pazienza, lasciare che Fedora lavori e non interrompere assolutamente la procedura. Quando la compilazione sarà completa bisogna solamente installare il pacchetto, spostarsi nella directory degli RPMS di i686 e lanciare l'installazione:

`# cd /usr/src/redhat/RPMS/i686`
`# rpm -Uvh kernel-sourcecode-2.6.10-1.741_FC3.root.i686.rpm`
`Preparing... ####################### [100%]`
`1:kernel-sourcecode ...################# [100%]`

Fatto! In questo modo si sono installate le sorgenti; andate a verificarne la presenza in /usr/src/linux.

`# cd /usr/src/linux`
`# ls`
`linux-2.6.10-1.741_FC3.root  redhat`

[Categoria:Programmazione e Sviluppo](Categoria:Programmazione_e_Sviluppo "wikilink")
