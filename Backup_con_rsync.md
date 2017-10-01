Introduzione
------------

La perdita dei dati del proprio computer o di qualsiasi supporto di memorizzazione è un evento che non sempre può essere preventivato. Per evitare questi spiacevoli inconvenienti è importante eseguire un backup periodico di tutti i documenti importanti.

Nella seguente guida verrà proposta la procedura di backup della propria cartella utente attraverso il comando *rsync*.

Installazione
-------------

Rsync è presente nei repository ufficiali di fedora e può essere installato con il gestore dei pacchetti dnf

`# dnf install rsync`

Backup
------

Rsync è un potente strumento di sincronizzazione dati che può essere usato come alternativa a *cp* ed offre la possibilità di creare il backup dei propri documenti con semplici comandi. Di seguito verranno esposti alcuni esempi che soddisfano le necessità più comuni.

Il comando per effettuare il backup della propria home (definita in bash dalla variabile **$HOME**) e salvarlo nella cartella */destinazione/* è

`$ rsync -aAXvz $HOME /destinazione/`

dove le opzioni *-aAX* permettono di preservare completamente la struttura della *$HOME*, *-v* è la modalità *verbose* e *-z* comprime i file durante il trasferimento.

Un aspetto interessante di *rsync* consiste nel fatto che le sucessive esecuzioni andranno ad aggiornare unicamente i file che sono stati modificati. I file obsoleti non più presenti nella *$HOME*, possono essere cancellati aggiungendo l'opzione *--delete*

`$ rsync --delete -aAXvz $HOME /destinazione/`

Rsync può essere usato connettendosi via ssh ad un server remoto specificando la porta tramite l'opzione *-p*

`$ rsync -aAXvz -e ssh $HOME user_remoto@host_remoto:/destinazione/remota/`
`$ rsync -aAXvz -e "ssh -p 22" $HOME user_remoto@host_remoto:/destinazione/remota/`

Per ripristinare il backup sarà sufficente invertire sorgente e destinazione

`$ rsync -aAXvz /sorgente/ $HOME`

Riferimenti
-----------

-   [Sito ufficiale](http://rsync.samba.org/)
-   [Man page](http://linux.die.net/man/1/rsync)
-   [Documentazione Archlinux](https://wiki.archlinux.org/index.php/Full_system_backup_with_rsync)

<Categoria:Sistema>
