Come fare per abbreviare l'inserimento dei comandi nella console? E se non ci si ricorda esattamente un comando che non consisteva di soltanto 4 lettere ma di più parole?
Si ha un tasto sulla tastiera che aiuta in questo, il "TAB".

Esempio:
Si vuole installare un pacchetto RPM che si è scaricato nella propria cartella /home/utente/downloads e attualmente ci si trova nella propria home, quindi si è in:

`[utente@localhost ~]$`

Ora per spostarsi nella cartella downloads scrivere:

`[utente@localhost ~]$ cd downloads`

Provare a inserire questo invece:

`[utente@localhost ~]$ cd d"TAB"`

Visto? Fedora autocompleta immediatamente la d a downloads (sempre che non ci siano più cartelle che inizino con la "d" - in questo caso le elencherà). In questo caso non si è guadagnato tanto tempo perché si sapeva esattamente il percorso e il nome della directory, ma se si era nella root directory e non ci ricordavamo il nome della cartella (download o downloads o downloading???).
Per ogni cartella che si inserisce quindi si può usare il tasto "TAB".

Stesso discorso vale per installare un pacchetto RPM che si ipotizza abbia il nome nomepacchetto-1.0-FC3.i386.rpm

Un nome lungo da digitare, usando di nuovo il tasto "TAB".

`# rpm -ivh n"TAB"`
`# rpm -ivh nomepacchetto-1.0-FC3.i386.rpm`

Si vede che Fedora ha autocompletato il pacchetto, basta dare "INVIO" per lanciare l'installazione.

Ora, come completare un comando, si suppone che si voglia eseguire i servizi, il comando da terminale in questo caso è abbastanza lungo e non ce lo si ricorda...si sa che inizia con system-.......

`$ system-"TAB"`
`system-cdinstall-helper          system-config-printer`
`system-config-authentication     system-config-printer-gui`
`system-config-boot               system-config-printer-tui`
`system-config-date               system-config-rootpassword`
`system-config-display            system-config-samba`
`system-config-httpd              system-config-securitylevel`
`system-config-keyboard           system-config-securitylevel-tui`
`system-config-language           system-config-services`
`system-config-mouse              system-config-soundcard`
`system-config-network            system-config-time`
`system-config-network-cmd        system-config-users`
`system-config-network-druid      system-control-network`
`system-config-nfs                system-install-packages`
`system-config-packages           system-logviewer`

Siccome ci sono più di un comando che iniziano con system- bisogna premere due volte il tasto "TAB" e viene fornito l'elenco, ora lo si vede, è "system-config-services". Digitare (la prima parte lo scrive già Fedora), fatto!

<Categoria:Sistema>
