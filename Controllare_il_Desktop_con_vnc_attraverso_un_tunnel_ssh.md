Introduzione
------------

Con questa breve guida si vuole spiegare come aprire una connessione ad un desktop remoto utilizzando il client vncviewer, transitando per un tunnel crittografato ssh e utilizzando la compressione dei dati.

Requisiti
---------

Sul computer remoto da controllare è necessario che sia in ascolto il server vnc sulla porta 5900/tcp: per far ciò è possibile utilizzare "vino-server" del desktop Gnome dal menu *Sistema &gt; Preferenze &gt; Internet e rete &gt; Desktop Remoto* (oppure da shell: *$ vino-preferences*) mettendo il segno di spunta sulle relative voci secondo le proprie esigenze e attivando quantomeno l'opzione *Consentire agli altri utenti di visualizzare il proprio desktop*.

Fatto ciò si può verificare che effettivamente la porta 5900/tcp sia stata correttamente aperta:

`$ nmap -p 5900 localhost`
`Starting Nmap 4.52 ( `[`http://insecure.org`](http://insecure.org)` ) at 2008-03-08 12:16 CET`
`Interesting ports on Zod (127.0.0.1):`
`PORT     STATE SERVICE`
`5900/tcp open  vnc`

e che il processo sia attivo:

`$ ps -eaf | grep vino`
`zod  11713     1  0 12:15 ?        00:00:00 /usr/libexec/vino-server --oaf-activate-iid=OAFIID:GNOME_RemoteDesktopServer --oaf-ior-fd=51`

D'ora in poi ci si riferirà al computer da controllare, quello appunto su cui gira il server vnc (vino-server), chiamandolo PC\_IN\_PANNE e al computer che si collegherà ad esso per tele-controllarlo chiamandolo PC\_SOCCORSO.

Scenario 1
----------

`==============================================================================`
`SCENARIO N.1: PC_IN_PANNE è raggiungibile in ssh (porta tcp/22) da PC_SOCCORSO`
`==============================================================================`

Su PC\_SOCCORSO dare il seguente comando:

`$ ssh -C -c blowfish -f -L LOCAL_PORT:127.0.0.1:5900 USER@PC_IN_PANNE sleep 10 ; \`
`  vncviewer 127.0.0.1:LOCAL_PORT`

sostituendo:

-   LOCAL\_PORT con la porta locale che si vuole utilizzare allo scopo (ad esempio 9999)
-   USER@PC\_IN\_PANNE con delle credenziali esistenti per accedere in ssh al PC\_IN\_PANNE (esempio aiuto@pcinpanne.homeip.net)

Il comando sarà più o meno così:

`$ ssh -C -c blowfish -f -L 9999:127.0.0.1:5900 aiuto@pcinpanne.homeip.net sleep 10 ; \`
`  vncviewer 127.0.0.1:9999`

Breve sèiegazione delle opzioni sopra citate:

**-C -c blowfish** indica che il traffico ssh dovrà essere compresso. Si guadagna velocità a scapito dell'utilizzo della CPU. In caso di computers particolarmente datati è possibile togliere queste opzioni

**-f** indica che ssh deve andare in background. In pratica ssh stabilisce una connessione verso PC\_IN\_PANNE, si addormenta (sleep) 10 secondi e nel frattempo sul canale transitano i dati criptati vnc, che tengono aperta la connessione. Quando vncviewer verrà chiuso cadrà anche il tunnel ssh.

**-L 9999:127.0.0.1:5900** indica che la porta 9999 di PC\_SOCCORSO (127.0.0.1) viene mappata verso la porta 5900 (vino-server) del pc remoto (PC\_IN\_PANNE)

Scenario 2
----------

`=======================================================================================================`
`SCENARIO N.2: PC_IN_PANNE è dietro ad un firewall, ma PC_SOCCORSO è raggiungibile da PC_IN_PANNE in ssh`
`=======================================================================================================`

Su PC\_IN\_PANNE dare il seguente comando:

`$ ssh  -C -c blowfish -R REMOTE_PORT:localhost:5900 USER@PC_SOCCORSO`

sostituendo:

-   REMOTE\_PORT con la porta remota che si vuole utilizzare allo scopo (ad esempio 9999)
-   USER@PC\_SOCCORSO con delle credenziali esistenti per accedere in ssh a PC\_SOCCORSO (esempio grazie@pcsoccorso.homeip.net)

Il comando sarà più o meno così:

`$ ssh -C -c blowfish -R 9999:localhost:5900 grazie@pcsoccorso.homeip.net`

Da PC\_SOCCORSO sarà quindi possibile collegarsi a PC\_IN\_PANNE con:

`$ vncviewer localhost:REMOTE_PORT`

che nell'esempio significa:

`$ vncviewer localhost:9999`

Anche in questo caso *-C -c blowfish* indica la compressione e può essere omesso in caso di computers con processori lenti.
L'opzione *-R* di ssh serve invece a creare un *Reverse Tunnel*: il collegamento ssh infatti viene iniziato da PC\_IN\_PANNE, ma farà in modo che su PC\_SOCCORSO venga mappata la porta 9999/tcp verso il tunnel stesso (e quindi verso la porta 5900 di vino-server)

Poiché il collegamento ssh da PC\_IN\_PANNE a PC\_SOCCORSO è finalizzato alla sola apertura del suddetto tunnel, non è necessario che l'utente collegato (nell'esempio "grazie") abbia a disposizione una shell.

Su PC\_SOCCORSO si può ad esempio creare il seguente banale programma *mio\_messaggio.c*:

`#include `<stdio.h>
`int main(void)`
`{`
` printf("\n---------------------------------------------------------------\n");`
` printf("Reverse SSH Tunnel attivato\n");`
` printf("Il tunnel rimarrà attivo finchè questa finestra rimarrà aperta\n");`
` printf("---------------------------------------------------------------\n");`
` printf("Chiudere questa finestra se si desidera disattivare il tunnel\n");`
` printf("---------------------------------------------------------------\n");`
` while (getchar() !='\n');`
` return 0;`
`}`

compilarlo e copiarlo in /bin/ con

`$ cc mio_messaggio.c`
`$ cp a.out /bin/mio_messaggio`

e utilizzare quindi il file binario così generato al posto della shell di default per l'utente in questione, indicandolo nel file /etc/passwd:

`...`
`grzie:x:600:600:utente reverse tunnel `[`ssh:/home/grazie:/bin/mio_messaggio`](ssh:/home/grazie:/bin/mio_messaggio)

In tal modo l'utente che si collegherà da PC\_IN\_PANNE non potrà "girovagare" per il disco di PC\_SOCCORSO, non avendo a disposizione una shell:

`$ ssh grazie@pc_soccorso`
`grazie@pc_soccorso's password:`
`Last login: Sat Mar  8 12:40:58 2008 from XX.ZZ.WW.AA`
`---------------------------------------------------------------`
`Reverse SSH Tunnel attivato`
`Il tunnel rimarrà attivo finchè questa finestra rimarrà aperta`
`---------------------------------------------------------------`
`Chiudere questa finestra se si desidera disattivare il tunnel`
`---------------------------------------------------------------`

Aggiornamento alla guida
------------------------

E' possibile aprire il "reverse tunnel ssh" utilizzando il client [putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/).
Per l'installazione:

`# yum install putty`

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink")
