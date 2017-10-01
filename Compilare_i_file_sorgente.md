Benché Fedora sia una distribuzione basata su pacchetti rpm (e sarebbe meglio installare sempre questi, magari con yum, quando se ne ha la possibilità) può capitare di dover compilare un programma partendo da sorgenti: ad esempio se il programma non è disponibile come rpm, oppure per personalizzarlo disabilitando o cambiando qualche funzionalità specifica.

Per la compilazione si avrà bisogno almeno degli strumenti di sviluppo di base, che si possono installare con:

`[root@hostname myhome]# yum groupinstall "Development Tools"`

più eventualmente altri (sviluppo di X, Gnome, KDE, ecc.).

I sorgenti di solito sono reperibili sotto forma di archivi compressi di questi tre tipi:

`programma-x.y.z.tgz`
`programma-x.y.z.tar.gz`
`programma-x.y.z.bz2`

Spostarsi nella directory che contiene l'archivio interessato ed estrarlo in una cartella rispettivamente con i comandi:

`[utente@hostname myhome]$ tar -xvzf programma-x.y.z.tgz`
`[utente@hostname myhome]$ tar -xvzf programma-x.y.z.tar.gz`
`[utente@hostname myhome]$ tar -xvjf programma-x.y.z.bz2`

Fatto questo spostarsi all'interno della cartella con

`[utente@hostname myhome]$ cd programma.x.y.z/`

Di solito all'interno di questa cartella sono presenti i file README e INSTALL che è sempre bene leggere perché potrebbero contenere istruzioni specifiche per la compilazione/installazione. In caso contrario la procedura generale è la seguente:

`[utente@hostname programma.x.y.z]$ ./configure`

A questo punto viene eseguito un controllo degli elementi del proprio sistema necessari alla compilazione/installazione del programma (configurazione). Se alla fine di questo processo sono riportati errori, probabilmente significa che sul proprio sistema manca qualcosa, in caso contrario si può procedere con

`[utente@hostname programma.x.y.z]$ make`
`[utente@hostname programma.x.y.z]$ su`
`Password:`
`[root@hostname programma.x.y.z]# make install`

Con questi comandi vengono compilati e installati sul sistema gli eseguibili.
Di default i pacchetti installati con questo sistema si vanno a posizionare nelle sottodirectory di /usr/local , ma si può anche decidere dove metterli al momento di configurare il pacchetto specificando:

`[utente@hostname programma.x.y.z]$ ./configure --prefix=/percorso/`

Per vedere invece una lista di tutte le impostazioni che è possibile scegliere prima di configurare e compilare:

`[utente@hostname myhome]$ ./configure --help`

Questa vuole essere soltanto una breve guida pratica, chi lo desidera potrà approfondire l'argomento.

[Categoria:Programmazione e Sviluppo](Categoria:Programmazione_e_Sviluppo "wikilink") <Categoria:Installazione>
