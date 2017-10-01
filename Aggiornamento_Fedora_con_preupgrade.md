Introduzione
------------

Esistono vari modi per aggiornare il sistema da una release di Fedora all'altra. In questo piccolo howto ci si vuole focalizzare sull'aggiornamento tramite *Preupgrade*, che tra quelle disponibili è l'unica che effettivamente aggiorna il sistema agli ultimi pacchetti disponibili, perché si connette al [repository 'Fedora updates'](:Categoria:Repository "wikilink").

Preparazione del sistema
------------------------

Le operazioni che seguono vanno tutte date con i privilegi di root:

`$ su -`
`password`
`#`

Per poter passare da una versione di Fedora all'altra è necessario portare la vecchia release allo stato più aggiornato possibile. Di conseguenza la prima cosa da fare è un aggiornamento del sistema:

`# yum update`

L'aggiornamento può durare anche parecchio tempo, dipende dallo stato in cui si trovava la propria Fedora.
Una volta completato l'update è bene cancellare la cache di yum, per essere certi che non influisca nell'operazione di upgrade.

`# yum clean all`

Una volta riavviato ci si rilogga nel terminale come root per proseguire.

Operazioni preparative
----------------------

`# yum install preupgrade `

Siccome l'aggiornamento dalla versione 11 in poi, rispetto agli upgrade precedenti, richiede molto più spazio nella directory /boot, è necessario liberarne il più possibile. Per farlo si possono, a questo punto, eliminare tutti i kernel (se si ha una partizione /boot uguale o inferiore a 300MB) tranne l'ultimo, che si sta utilizzando.
Per ogni singolo kernel bisogna cancellare i seguenti file:

`# cd /boot`
`# ls`
`# rm -rf System.map-2.6.x.x-x.fc15.i586`
`# rm -rf vmlinuz-2.6.x.x-x.fc15.i586`
`# rm -rf initrd-2.6.x.x-x.fc15.i586.img`

Questa operazione va ripetuta per ogni versione di kernel, alla fine dovrebbero rimanere soltanto i file relativi al kernel in uso, ovvero l'ultimo.
Se non dovesse essere sufficiente liberare spazio cancellando i file inutili si può aumentare la partizione di /boot con [gparted](http://gparted.sourceforge.net/) oppure utilizzando una connessione via cavo (metodo descritto sul sito di [fedoraproject](https://fedoraproject.org/wiki/How_to_use_PreUpgrade#Method_2:_Trick_preupgrade_into_downloading_the_installer)).

L'aggiornamento
---------------

Completati tutti i preparativi si può partire con l'aggiornamento vero e proprio:

`# preupgrade`

Una volta digitato questo comando partirà una GUI che ti seguirà durante l'aggiornamento. Dopo il messaggio di benvenuto verrà chiesto di selezionare la versione da installare dopo l'aggiornamento. (in queste immagini per l'attuale mancanza a F16 viene proposto la Rawhide di Fedora Verne). <img src="Preupgrade1.png" title="fig:Preupgrade propone le versioni disponibili per l&#39;aggiornamento." alt="Preupgrade propone le versioni disponibili per l&#39;aggiornamento." width="350" /> Il sistema eseguirà tutti i controlli necessari per poi partire con il download dei pacchetti. E' bene sapere che durante questa fase un'eventuale uscita dal programma di aggiornamento non comprometterà nulla, e se si vuole si può riprendere il download anche successivamente dal punto in cui è stato interrotto. <img src="Preupgrade2.png" title="fig:Il controllo dello spazio, dei pacchetti ecc." alt="Il controllo dello spazio, dei pacchetti ecc." width="350" /> Una volta finito il download dei pacchetti viene nuovamente controllato il sistema e lo spazio nella directory */boot*. Se tutto va a buon fine verrà chiesto il riavvio del sistema. <img src="Preupgrade3.png" title="fig:Controllo eseguito con successo, riavviare." alt="Controllo eseguito con successo, riavviare." width="350" /> Una volta fatto il reboot viene eseguito l'upgrade vero e proprio. Infatti vengono installati tutti i pacchetti aggiornati alla versione successiva ed è facilmente intuibile che questa fase può durare molto, anche ore... <img src="Preupgrade4.png" title="fig:Installazione dei pacchetti della nuova release." alt="Installazione dei pacchetti della nuova release." width="350" /> Non appena l'aggiornamento sarà terminato ci si ritroverà davanti alla "nuova" schermata di login.

<Categoria:Installazione>
