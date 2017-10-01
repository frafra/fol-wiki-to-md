Se si usa una stampante all'interno di una rete con PC Windows la si può configurare come stampante di rete.

Dopo aver configurato Samba e aver controllato che la rete funzioni passare alla configurazione della stampante.
Si suppone di avere una HP970C collegata alla propria macchina con Fedora, per iniziare aprire il printconf-gui e digitare la password di root:

`$ printconf-gui`

Cliccare su ***NUOVO***:

![](print0.jpg "print0.jpg")

Inserire il nome della nostra stampante (HP970C) e cliccare su AVANTI.

![](print1.jpg "fig:print1.jpg") ![](print2.jpg "fig:print2.jpg")

Viene chiesto di selezionare la stampante dalla lista e il tipo di coda (locale), procedere con *OK*. Viene visualizzata una schermata con un breve riassunto della propria configurazione, premere *TERMINA* e la configurazione locale è terminata.

Ora che si è configurata la stampante localmente si passa alla vera configurazione di Samba. Per fare questo aprire il file /etc/samba/smb.conf e nella sezione generale e quella delle stampanti inserire i seguenti parametri:

`#Nella sezione [global]`
`load printers = yes`
`printing = cups`
`printcap name = cups`

`#Nella sezione [printers]`
`comment = Stampante HP930C`
`path = /var/spool/samba`
`browseable = no`
`guest ok = yes`
`writable = yes`
`printable = yes`
`public = yes`
`printer admin = root`
`use client driver = yes`
`print command = lpr -r -o raw -P %p %s`
`lpq command = lpstat -o %p`
`lprm command = cancel %p-%j`

Prima di riavviare il servizio de-commentare la riga in /etc/cups/mime.convs:

`#application/octet-stream application/vnd.cups-raw 0 -`

Stessa cosa anche per la riga in /etc/cups/mime.types:

`#application/octet-stream`

Far ripartire i servizi SMB e CUPS e la configurazione del server è fatta:

`# /sbin/service smb restart`
`# /sbin/service cups restart`

Ora bisogna configurare il client; ripartire da printconf-gui e cliccare su NUOVO.
Dare un nome alla stampante per identificarla in rete:

![](print3.jpg "print3.jpg")

Ora scegliere la coda selezionando Windows Rete (SMB), comparirà il nome del proprio PC, cliccare sulla freccettina nera e sulla propria stampante HP970C:

![](print4.jpg "print4.jpg")

Ora selezionare il fornitore della stampante e il modello, dare OK e ci si ritrova davanti al riassunto della configurazione. Premendo su TERMINA si è concluso.

![](print5.jpg "fig:print5.jpg") ![](print6.jpg "fig:print6.jpg")

Naturalmente bisogna aggiungere la stampante anche sulla macchina Windows, cercandola con la funzione apposita nel menu di Aggiungi Stampante e installando il driver per Windows.

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink") <Categoria:Stampanti>
