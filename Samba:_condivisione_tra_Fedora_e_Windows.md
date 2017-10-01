Per condividere le risorse all'interno di una rete, nella quale ci sono anche macchine con Windows, si utilizza [Samba](http://samba.xsec.it/), un tool potentissimo che si installa digitando da root:

`# dnf install samba samba-common samba-client system-config-samba`

Il primo fornisce il "SMB/CIFS Server", per fornire la condivisione ai client, il secondo una serie di files utili sia al server che al client, il terzo invece fornirà un insieme di files utili al "SMB/CIFS File System" di Linux per avere l'accesso alle risorse condivise. Si precisa solamente che dopo l'avvento del *CIFS*, tutte le funzionalità di cui si ha bisogno, sono gestite dal kernel, non si avrà quindi bisogno di nulla altro.
L'ultimo pacchetto installato è la GUI che permette di configurare Samba in modo intuitivo. Questo è possibile anche direttamente tramite il file */etc/Samba/smb.conf*, che verrà trattato nella seconda parte della presente guida.

Per prima cosa bisogna attivare il servizio, lo si fa posizionandosi nel menu *Sistema &gt; Amministrazione &gt; Servizi* e selezionando i servizi SMB e NMB, li si avviano con il pulsante in alto a sinistra, si salvano per renderli attivi durante il prossimo boot, e si esce.
La stessa cosa è fattibile anche da terminale:

`# /sbin/chkconfig --level 2345 smb on`
`# /sbin/chkconfig --level 2345 nmb on`

Il primo servizio si occupa di gestire le risorse condivise sul server Samba per i client SMB/CIFS.
Il secondo (Naming Service Component) -non critico- fornisce funzionalità varie, come il WINS ai client windows e il servizio di browser per l'elezione in LAN.
Samba è in piedi e pronto per essere configurato.

Si ipotizzi una rete semplice tramite un Router. Di conseguenza la rete si articolerà nel seguente modo:
Il Router ha indirizzo 192.168.0.1, il Workgroup lo si chiamerà "rete".
Il PC su cui si lavorerà si chiama "roby", ma prima di proseguire bisogna fare 3 cosette:

1.  Salvarsi una copia di */etc/samba/smb.conf* come backup
2.  Impostare il firewall e settare Samba come servizio "fidato", come?

Andare in *Sistema &gt; Amministrazione &gt; Firewall* e dopo aver inserito la password di root mettere il baffo su Samba. Fatto!
Oppure si può direttamente dettare ad iptables le regole per le singole porte se si utilizzano IP fissi:.

`[root@localhost logs]# iptables -I RH-Firewall-1-INPUT -s 192.168.1.0/24 -p udp -m udp --dport 137 -j ACCEPT`
`[root@localhost logs]# iptables -I RH-Firewall-1-INPUT -s 192.168.1.0/24 -p udp -m udp --dport 138 -j ACCEPT`
`[root@localhost logs]# iptables -I RH-Firewall-1-INPUT -s 192.168.1.0/24 -p tcp -m tcp --dport 139 -j ACCEPT`
`[root@localhost logs]# iptables -I RH-Firewall-1-INPUT -s 192.168.0.0/24 -p tcp -m tcp --dport 445 -j ACCEPT`

Le prime due regole si occupano dell'nmbd, le altre dell'smbd.

<li>
Per quanto riguarda invece SELinux normalmente si consiglia di disabilitarlo, oppure di rivolgersi alla documentazione ad esso dedicata, specifica per Samba e le svariate problematiche che possono nascere.

</li>
Ora aprire il menu di configurazione andando in *Sistema &gt; Amministrazione &gt; Samba*.

![](smb7.jpg "smb7.jpg")

Andare in Preferenze-&gt;Impostazioni Server e inseriamo le impostazioni di base e sicurezza come sotto.

![](smb1.jpg "fig:smb1.jpg") ![](smb2.jpg "fig:smb2.jpg")

</ol>
Fatto questo si configurano gli utenti di Samba:
Andare in Preferenze-&gt;Utenti Samba e aggiungere un utente.

![](smb3.jpg "smb3.jpg")

In questo modo per accedere alle risorse condivise si inserirà l'utente ospite con la rispettiva password. In poche parole accedere alle risorse tramite l'alias 'utente'.
Ora bisogna specificare cosa condividere, per esempio la directory /Pubblici, alla quale bisogna dare i permessi 755 (per renderla accessibile anche agli altri utenti). Si veda l'inserimento della condivisione cliccando sul tasto 'Aggiungi condivisione'. Anche qui si inseriranno le impostazioni di base e di accesso.

![](smb4.jpg "fig:smb4.jpg") ![](smb5.jpg "fig:smb5.jpg")

Ora bisogna inserire la condivisione, se ne possono inserire altre, per semplicità qui si mette soltanto una.

![](smb8.jpg "smb8.jpg")

Per riavviare Samba con le nuove impostazioni bisogna riavviare il servizio andando in *Sistema &gt; Amministrazione &gt; Servizi*. Cliccare su *SMB* e premere 'Riavvia'.

![](smb10.jpg "smb10.jpg")

Vedere se è andato tutto a buon fine, digitando:

`$ smbclient -U% -L localhost`

L'output deve dare tutti gli utenti collegati, condivisioni, stampanti e il gruppo di lavoro con il master.
Per completezza si analizzerà anche il file */etc/samba/smb.conf*, aprendolo con un editor di testo. Si metteranno dei commenti tra parentesi, **NON** copiarli nel proprio *smb.conf*!!!
Innanzitutto il file, togliendo i mille commenti "inutili" (preceduti dal cancelletto \#) si divide in 3 sezioni principali:

-   GLOBAL SECTION: parametri di configurazione generale;
-   HOMES SECTION: contiene eventuali specificazioni sull'accesso alle directory "home";
-   PRINTERS SECTION: contiene eventuali dettagli sulla configurazione delle stampanti (che merita particolare attenzione, e perciò si tratterà meglio in una guida a parte)

`[global]                           (sezione di base con impostazioni principali)`
`   workgroup = rete           (gruppo di lavoro)`
`   netbios name = roby        (nome del nostro PC)`
`   server string = Samba Server    (descrizione del nostro PC)`
`   load printers = yes        (le opzioni cups e print sono per la stampante condivisa)`
`   printing = cups`
`   printcap name = cups`
`   cups options = raw`
`   log file = /var/log/samba/%m.log`
`   max log size = 50`
`   password server = None      (non abbiamo un password server)`
`   smb passwd file = /etc/samba/smbpasswd`
`   socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192`
`   os level = 34                (livello sistema operativo, a 34 siamo sicuri di diventare master nella rete)`
`   preferred master = yes       (vogliamo essere master? Sì)`
`   dns proxy = no               (non abbiamo un proxy)`
`   username map = /etc/samba/smbusers (dove sono gli utenti samba?)`
`   guest ok = yes               (ospiti accettati)`
`[printers]                           (la sezione dove configuro la stampante, sopra ho detto che uso CUPS)`
`   comment = HP Deskjet 970     (nome della mia stampante)`
`   path = /var/spool/samba`
`   browseable = no`
`   printable = yes`
`   guest ok = yes`
`   writable = yes`
`   public = yes`
`   printer admin = root`
`   use client driver = yes`
`   print command = lpr -r -o raw -P %p %s`
`   lpq command = lpstat -o %p`
`   lprm command = cancel %p-%j`
`[Pubblici]                        (ecco la sezione della nostra condivisione)`
`   comment = file condivisi       (la descrizione che abbiamo messo)`
`   path = /home/roby/Pubblici     (il percorso della nostra cartella)`
`        writeable = yes`
`   guest ok = yes                (ospiti ok)`
`   browseable = yes              (tutti possono sfogliare la cartella)`

A questo punto verificare se il proprio *smb.conf* è corretto (soprattutto se si sono fatte delle modifiche a mano).

`$ testparm`

Se non da nessun errore riavviare il servizio andando in *Sistema &gt; Amministrazione &gt; Servizi*. Fare click su SMB e premere 'Riavvia'. Altrimenti aspettare 60sec perché il file di Samba viene letto automaticamente ogni minuto!
Se è andato tutto bene come si spera, si troveranno le risorse condivise in Windows (ad esempio da ESEGUI, \\\\192.168.0.x, verrà chiesto l'accesso per l'autenticazione) - per chi utilizza IP fissi.
Nella propria Fedora si avranno vari strumenti grafici di gestione, tutti molto intuitivi, ognuno dei quali adatto alle proprie esigenze ed al Desktop che si predilige (sono ottimi sia *system-config-samba* che *smb4k*, ...).

Infine un consiglio sull'utilizzo di alcuni comodi (e trascurati) strumenti a riga di comando:

`$ smbstatus // offre il quadro sulla situazione attuale `
`$ smbclient // OTTIMO strumento per la connessione alle risorse`
`$ smbtar // comodo per il back-up dei dati ...`

Samba ora è in piedi e configurato per la propria rete, buon lavoro.

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink")
