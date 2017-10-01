Introduzione
------------

Seguendo i passaggi di questa guida, si farà in modo che tutto ciò che verrà digitato in tutte le bash shell aperte sul proprio sistema (anche quelle di root), verrà loggato nel file /var/log/bash.log .
Per fare ciò occorrerà modificare il codice sorgente della bash.
(La procedura è stata testata su Fedora 11, bash-4.0-8.fc11.i586 ).

Configurazione
--------------

Inanzitutto, se non si ha ancora installato i pacchetti di sviluppo, procedere con:

`# yum groupinstall “Development Tools”`
`# yum install rpmdevtools`

Aprire un terminale root e dare:

`# rpmdev-setuptree`

A questo punto si dovrebbero avere gli strumenti per poter iniziare. Procurarsi i sorgenti della bash con yumdownloader:

`#  yumdownloader --source bash`

( nel caso di questa guida ha scaricato: bash-4.0-8.f11.src.rpm)

`# rpm -Uvh  bash-4.0-8.f11.src.rpm[/code]`

Aprire con un editor di testo il file bash.spec

`# vi /root/rpmbuild/SPECS/bash.spec`

Cercare dentro il file bash.spec la sezione **%install** e subito sotto aggiungere le seguenti stringhe:

`%install`
`     chmod o+w /var/log/shlogp`
`     touch /etc/init.d/S01bashlog`
`     chmod 755 /etc/init.d/S01bashlog`
`     echo "#!/bin/zsh">> /etc/init.d/S01bashlog`
`     echo "tail -f  /var/log/shlogp >> /var/log/bash.log &" >> /etc/init.d/S01bashlog`
`     touch /var/log/bash.log`
`     chmod 600 /var/log/bash.log`
`     ln -s /etc/init.d/S01bashlog /etc/rc1.d/S01bashlog`
`     ln -s /etc/init.d/S01bashlog /etc/rc2.d/S01bashlog`
`     ln -s /etc/init.d/S01bashlog /etc/rc3.d/S01bashlog`
`     ln -s /etc/init.d/S01bashlog /etc/rc4.d/S01bashlog`
`     ln -s /etc/init.d/S01bashlog /etc/rc5.d/S01bashlog[/quote]`

*Esc:wq!* (per salvare e chiudere il file con vi)

Spostarsi nella dir */root/rpmbuild/SOURCES* e scompattare *bash-4.0.tar.gz* per poter modificare il file *bashhist.c* contenuto nell archivio:

`# cd /root/rpmbuild/SOURCES`
`# gunzip bash-4.0.tar.gz`
`# tar xvf bash-4.0.tar`
`# rm -rf bash-4.0.tar`
`# cd bash-4.0`

Aprire con un editor di testo il file *bashhist.c*

`# vi /root/rpmbuild/SOURCES/bash-4.0/bashhist.c`

Cercare la sezione

`void`
`maybe_add_history (line)`
`     char *line;`
`{`
`  hist_last_line_added = 0;`

e farla diventare così:

`void`
`maybe_add_history (line)`
`char *line;`
`{`
`int should_add;`
`int pipefd, uid;`
`FILE *logfile;`
`HIST_ENTRY *temp;`
`/* istruzioni aggiuntive per loggare i comandi della shell dati dai singoli utenti */`
`uid = getuid();`
`logfile = fopen("/var/log/shlogp", "a");`
`fprintf(logfile, "[uid %d] %s\n", uid, line);`
`fclose(logfile);`
`hist_last_line_added = 0;`

*Esc:wq!* (Per salvare e chiudere il file con vi) Ora ricreare l'archivio ed eliminare la dir scompattata.

`# cd`
`# tar -cvf /root/rpmbuild/SOURCES/bash-4.0.tar /root/rpmbuild/SOURCES/bash-4.0`
`# gzip /root/rpmbuild/SOURCES/bash-4.0.tar`
`# rm -rf /root/rpmbuild/SOURCES/bash-4.0`

Ora creare i pacchetti.

`# rpmbuild -bb /root/rpmbuild/SPECS/bash.spec[/code]`

Attendere la fine del processo, che ci mette un pò di tempo, e se tutto è andato a buon fine l'operazione termina con un “exit 0”.
A questo punto rimuovere l'rpm bash di sistema e installare i pacchetti che sono appena stati creati:

`# rpm -e --nodeps bash`
`# rpm -ivh /root/rpmbuild/RPMS/i586/bash-4.0-8.fc11.i586.rpm `
`# rpm -ivh /root/rpmbuild/RPMS/i586/bash-debuginfo-4.0-8.fc11.i586.rpm `
`# rpm -ivh /root/rpmbuild/RPMS/i586/bash-doc-4.0-8.fc11.i586.rpm`

Dare un reboot. Aprire un terminale di root e dare:

`# tail -f /var/log/bash.log`

Contemporaneamente aprire un terminale utente e digitare dei comandi, se ci si sposta sul terminale root si vedrà che il comando tail fa comparire in tempo reale i comandi che sono stati dati nel terminale utente specificando anche l'uid.

[Categoria:Programmazione e Sviluppo](Categoria:Programmazione_e_Sviluppo "wikilink")
