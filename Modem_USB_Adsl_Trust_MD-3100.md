La guida che segue è frutto dell'utilizzo delle molte indicazioni trovate in altre guide sintetizzate con elementi di esperienza diretta e correzioni varie necessarie.

I componenti richiesti per l'installazione sono i seguenti:

1.  Il sorgente del proprio kernel. Se non lo si possiede lo si può scaricare dal sito della propria distro, in questo caso <http://mirror.eas.muohio.edu/fedora/linux/core/5/i386//os/Fedora/RPMS/>
2.  Le vecchie guide indicavano di scaricare il "nuovo" ATM. Con Fedora Core 5 non occorre perché l’Atm di Fedora va benissimo e l’ATM che si scaricherebbe è vecchio di 2 anni e darebbe errore nella ricompilazione del kernel con conseguente fallimento della operazione.
3.  Il driver per Windows del modem TRUST MD-3100.

Si può iniziare l'installazione del modem.

Installazione del kernel
------------------------

1.  Scompattare il file rpm del sorgente del proprio kernel o dall'interfaccia grafica oppure da terminale con il comando:
        $ rpm -ivh kernel-2.6.15-1.2054_FC5.src.rpm

    (per veder la propria versione del kernel digitare *uname-r*)

2.  Poi digitare
        $ rpmbuild -bp --target=noarch /usr/src/redhat/SPECS/kernel-2.6.spec
        il sorgente si trova qui
        /usr/src/redhat/BUILD/kernel-2.6.15/

3.  A questo punto prima di compilare bisogna abilitare alcune opzioni del kernel. Eseguire il comando da terminale in modalità root:
        $ make menuconfig

    oppure se correttamente installato

        $ make xconfig

    per usufruire dell'interfaccia grafica.

4.  Andare sotto la voce Device *Drivers &gt; USB support &gt; USB DSL modem support* ed attivate USB DSL modem support & Conexant AccessRunner USB support.
    Questo attiverà anche il supporto per hotplug ed il caricatore per i firmware (dalla ver 2.6.15 del kernel è sicuramente tutto integrato).
5.  Andare sotto la voce Networking support -&gt; PPP support e configurare come di seguito
        PPP support
         PPP sync tty < potrebbero volerci
         PPP async tty < tutti e due
         PPP deflate < non obbligatorio
         PPP BSD-Compression < non obbligatorio
         PPP over ATM

6.  Andare sotto la voce Networking option e configurare come di seguito
        Asyncronous Transfer Mode
         Classical IP over ATM
         Do NOT send ICMP if no neighbour

    Cmq dovrebbe essere già abbastanza settato.

7.  A questo punto eseguire
        $ make clean

    per ripulire da precedenti compilazioni.

8.  Eseguire poi
        $ make bzImage

    per dare inizio alla compilazione del kernel. La compilazione impiega circa 10-15 minuti dipende dal processore.

9.  Poi eseguire
        $ make modules

    per la compilazione dei moduli. La compilazione impiega circa 2 ore su un Celeron 500.

10. Poi eseguire
        $ make modules_install

    per copiare i moduli nella cartella /lib/modules/\[versione del kernel\].

11. Poi eseguire
        $ make install

    per copiare l’immagine del kernel nella cartella /boot e via di seguito nelle altre cartelle.

Installazione del driver del modem
----------------------------------

1.  Ora rimanendo sempre nella cartella dei sorgenti del proprio kernel, andare a prendere l'utility per estrarre il firmware dal cvs e poi compilarlo. Digitare i seguenti comandi da terminale impostato come root.
        $ cvs -z3 -d:pserver:anonymous@cvs.sourceforge.net:/cvsroot/accessrunner co -P utils
         cd utils
         make

    ..questo ovviamente se si ha la fortuna di poter accedere alla rete. Il caso più ricorrente è quello in cui si dispone del vecchio modem 56Kbps. Basta configurarlo con un driver linux generico anche a 9.600 bps, tanto l'operazione per scaricare l'utility dura 5 secondi. Poi il modem 56 K se non lo si usa per i fax si può pure buttare dalla finestra. (Guardare se passa qualcuno prima di gettarlo…se lo si colpisce si sarà responsabili per danni).

2.  Copiare i file presi sopra in una qualsiasi Cartella
3.  Estrarre dal driver di windows il file CnxEtU.sys e copiarlo nella Cartella. Ora da terminale eseguire il seguente comando
        $ ./cxacru-fw CnxEtU.sys cxacru-fw.bin

    Verrà creato il file "cxacru-fw-bin" che altro non sarebbe che il firmware del nostro modem.

4.  Copiare il file "cxacru-fw.bin" sotto la cartella /lib/firmware.
5.  N.B. Nel caso, una volta caricato il firmware, si riceve il messaggio:
        cxacru 1-1:1.0: poll status: error -5

    significa che occorre una versione più recente del proprio firmware. Bisogna quindi cercare una versione aggiornata anche da produttori diversi da quello del modem in proprio possesso.

6.  A questo punto il driver del proprio modem dovrebbe già essere in funzione e il led ADSL del proprio modem dovrebbe lampeggiare per cercare la sincronizzazione con la linea.
7.  Una volta agganciato il segnale ADSL, scrivere da terminale
        $ cat /proc/net/atm/cxacru:0

    appariranno di seguito queste informazioni

        ADSL USB MODEM (usb-0000:00:07.2-1)
         MAC: xx:yy:zz:bla bla bla
         AAL5: tx 9363 ( 0 err ), rx 14299 ( 0 err, 0 drop )
         Line up

    Il driver del modem è perfettamente funzionante

Impostazione della connessione ADSL
-----------------------------------

Prima di iniziare bisogna sapere:

1.  la propria "userid" e "password" che di solito per Telecom Alice sono "userid=aliceadsl" e "password=aliceadsl"
2.  VPI e VCI del proprio provider che nel caso di Telecom Alice sono 8 e 35.
3.  IP e DNS del proprio provider nel caso di una connessione con IP statico.

### Iniziare con la configurazione

1.  Creiamo il file “adsl” nella cartella /etc/ppp/peers/ e scriviamoci al suo interno quello di seguito:

<!-- -->

    lock
     debug
     kdebug 1
     noauth
     maxfail 3
     ipparam ppp0
     noipdefault
     usepeerdns
     defaultroute
     noaccomp
     noccp
     nobsdcomp
     nodeflate
     nopcomp
     novj
     novjccomp
     persist
     plugin /usr/lib/pppd/2.4.3/pppoatm.so 8.35
     user aliceadsl

<li>
Aprire il file */etc/ppp/pap-secrets* ed inserire il proprio userid e password come di seguito:

</li>
`# Secrets for authentication using PAP`
`# client server secret IP addresses`
`aliceadsl * aliceadsl`
`####### redhat-config-network will overwrite this part!!! (begin) #####`
`####### redhat-config-network will overwrite this part!!! (end) #######`

<li>
Aprire il file /etc/ppp/chap-secrets ed inserire il proprio userid e password come di seguito:

</li>
`# Secrets for authentication using PAP`
`# client server secret IP addresses`
`aliceadsl * aliceadsl`
`####### redhat-config-network will overwrite this part!!! (begin) #####`
`####### redhat-config-network will overwrite this part!!! (end) #######`

<li>
A questo punto scrivere da terminale

</li>
`$ /usr/sbin/pppd call adsl`

ed il gioco è fatto.
Ora se si apre mozilla o firefox e si è eseguito senza errori la procedura, navigare regolarmente. Io poi mi sono fatto un collegamento sul Desktop poiché ogni volta che accendo il computer, occorre rieseguire */usr/sbin/pppd call adsl* per avviare la connessione.

<li>
Controllare su /var/log/messagges se appaiono scritte del genere

</li>
`Jun 3 00:07:40 localhost pppd[5101]: Plugin /usr/lib/pppd/2.4.3/pppoatm.so loaded.`
`Jun 3 00:07:40 localhost kernel: CSLIP: code copyright 1989 Regents of the University of California`
`Jun 3 00:07:40 localhost kernel: PPP generic driver version 2.4.2`
`Jun 3 00:07:40 localhost pppd[5101]: PPPoATM plugin_init`
`Jun 3 00:07:40 localhost pppd[5101]: PPPoATM setdevname_pppoatm - SUCCESS:8.35`
`Jun 3 00:07:40 localhost su(pam_unix)[5095]: session closed for user root`
`Jun 3 00:07:40 localhost pppd[5126]: pppd 2.4.2 started by root, uid 0`
`Jun 3 00:07:40 localhost pppd[5126]: Using interface ppp0`
`Jun 3 00:07:40 localhost pppd[5126]: Connect: ppp0 <--> 8.35`
`Jun 3 00:07:40 localhost pppd[5126]: Warning - secret file /etc/ppp/pap-secrets has world and/or group access`
`Jun 3 00:07:43 localhost pppd[5126]: Warning - secret file /etc/ppp/pap-secrets has world and/or group access`
`Jun 3 00:07:43 localhost pppd[5126]: PAP authentication succeeded`
`Jun 3 00:07:43 localhost pppd[5126]: local IP address 82.59.0.222`
`Jun 3 00:07:43 localhost pppd[5126]: remote IP address 192.168.100.1`
`Jun 3 00:07:43 localhost pppd[5126]: primary DNS address 80.17.212.208`
`Jun 3 00:07:43 localhost pppd[5126]: secondary DNS address 151.99.125.1`

<li>
Controllare su /etc/resolv.conf se i dns sono corretti altrimenti si dovranno inserire a mano.

</li>
`; generated by /sbin/dhclient-script`
`search pool8251.interbusiness.it`
`nameserver 80.17.212.208`

</ol>
Per chi ha libero adsl nel file *resolv.conf* deve scrivere:

`search libero.it`
`nameserver 193.70.192.25`
`nameserver 193.70.152.25`

Perciò il comando per connettersi sarà:

`$ /usr/sbin/pppd call adsl`

Il comando per disconnettersi sarà:

`$ killall pppd`

<Categoria:Hardware>
