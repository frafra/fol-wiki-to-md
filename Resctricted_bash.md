\_\_TOC\_\_

Introduzione
------------

Per limitare un utente, in modo che possa lanciare solo una serie limitata di comandi e non si vuole utilizzare il sudo, è possibile creare una shell ristretta che limiti le funzionalità che questo utente potrà usare. Le restricted bash (o rbash) sono installate di default sui sistemi ubuntu ma su distribuzioni come Fedora, Red Hat o CentOS bisognerà applicare un piccolo workaround per poter utilizzare queste bash.

Installazione
-------------

Nell'esempio ci sarà un gruppo *rgroup* ed un utente *ruser* che utilizzerà le restricted bash.

`[root@localhost /]# groupadd rgroup`
`[root@localhost /]# useradd -g rgroup -d /home/ruser -m -s /bin/bash ruser`
`[root@localhost /]# passwd ruser`
`Changing password for user ruser.`
`New UNIX password:`
`BAD PASSWORD: it is too short`
`Retype new UNIX password:`
`passwd: all authentication tokens updated successfully.`

Per prima cosa eseguire un symlink tra la shell */bin/bash* e la nuova shell */bin/rbash* per poter creare la nuova tipologia di bash.

`[root@localhost /]# ln -s /bin/bash /bin/rbash`
`[root@localhost /]# ls -l /bin/rbash`
`lrwxrwxrwx 1 root root 9 Mar 20 13:53 /bin/rbash -> /bin/bash`

Inserire la nuova shell all'interno dell'elenco di shell di sistema contenuta nel file */etc/shells*.

`[root@localhost /]# echo "/bin/rbash" >> /etc/shells`

Con il comando chsh è possibile cambiare la shell di default in uso da un utente. Con l'opzione -l è possibile visualizzare la lista delle shell disponibili sul sistema, mentre con le opzioni -s si modificherà la shell. Nel nostro esempio all'utente ruser associamo la shell rbash creata in precedenza.

`[root@localhost /]# chsh -l`
`/bin/sh`
`/bin/bash`
`/sbin/nologin`
`/bin/tcsh`
`/bin/csh`
`/bin/ksh`
`/bin/rbash`
`[root@localhost /]# chsh -s /bin/rbash ruser`
`Changing shell for ruser.`
`Shell changed.`

Configurazione
--------------

Nel file *.bash\_profile* di ogni utente è settato il percorso dove trovare i diversi comandi, e in questo caso si dovrà limitare l'accesso a questi percorsi settando un percorso personalizzato, dove convogliare i soli comandi utili e non altri. Per questo si dovrà creare la directory bin sotto la home che verrà utilizzata come path directory. Per questo modificare la variabile PATH dell'utente inserendo il nuovo percorso per rintracciare i comandi.

`[ruser@localhost ~]$ echo $PATH`
`/usr/kerberos/bin:/usr/local/bin:/bin:/usr/bin:/home/ruser/bin`
`[root@localhost /]# mkdir -p /home/ruser/bin`
`[root@localhost /]# cat /home/ruser/.bash_profile`
`# .bash_profile`
`# Get the aliases and functions`
`if [ -f ~/.bashrc ]; then`
`        . ~/.bashrc`
`fi`
`# User specific environment and startup programs`
`PATH=$HOME/bin`
`export PATH`

Modificare i proprietari dei file *.bashrc* e *.bash\_profile* per non permettere agli utenti di modificare il path dei comandi, che è stato impostato in precedenza.

`[root@localhost /]# chown root:root /home/ruser/.bash_profile`
`[root@localhost /]# chown root:root /home/ruser/.bashrc`

Ora per ogni comando che si vuole far usare all'utente ristretto, basterà creare un symlink tra il path assoluto del comando sotto il direttorio *$HOME/bin* che utilizziamo come path directory dell'utente.

`[root@localhost /]# ln -s /usr/bin/tail /home/ruser/bin/`
`[root@localhost /]# ln -s /bin/tar /home/ruser/bin/`
`[root@localhost /]# ln -s /bin/more /home/ruser/bin/`
`[root@localhost /]# cd /home/ruser/bin/`
`[root@localhost bin]# ls -l`
`total 0`
`lrwxrwxrwx 1 root root  8 Mar 23 09:03 cat -> /bin/cat`
`lrwxrwxrwx 1 root root  9 Mar 23 09:03 more -> /bin/more`
`lrwxrwxrwx 1 root root 13 Mar 23 09:02 tail -> /usr/bin/tail`
`lrwxrwxrwx 1 root root  8 Mar 23 09:03 tar -> /bin/tar`

Se si vuole permettere l'uso di alcune directory si può creare dei direttorio sotto la home e poi eseguire dei symlink come fatto con i comandi. L'utente infatti non potrà uscire al di fuori della sua home directory ne lanciare comandi che inizino con /, infatti:

`[ruser@localhost ~]$ cd /home`
`-rbash: cd: restricted`
`[ruser@localhost ~]$ /bin/sh`
`` -rbash: /bin/sh: restricted: cannot specify `/' in command names ``

<Categoria:Sistema>
