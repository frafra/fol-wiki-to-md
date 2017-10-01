\_\_TOC\_\_

Introduzione
------------

Queste sono le operazioni primarie per poter "utilizzare" il modem Pirelli di Alice, visto che ancora oggi molti utenti hanno difficoltà nella sua "configurazione".
Una volta connessi sia nel caso del cavo ethernet che con wireless, il primo test da effettuare è un ping:

`$ ping 192.168.1.1`

Se andrà a buon fine si può passare al passo successivo.

Creazione di una connessione xDSL
---------------------------------

Creare una connessione di tipo xDSL come segue:

`# system-config-network`

Creare una nuova connessione: **Nuovo --&gt; Collegamento xDSL**

`Nome fornitore accesso : Alice`
`User : aliceadsl`
`Password: aliceadsl`

Una volta creata, mettere la spunta sulla nuova connessione e verrà avviata in automatico ad ogni riavvio del sistema.
Se ancora persistono problemi si può procedere in questo modo:
Aggiungere 2 stringhe ad un file di configurazione, ma prima di renderlo permanente testare se in questo modo si risolvono i problemi. Per testarlo digitare i seguenti comandi da root:

`$ su - (ricorda il trattino)`
`# echo 0 > /proc/sys/net/ipv4/tcp_window_scaling`
`# echo 0 > /proc/sys/net/ipv4/tcp_ecn`

Successivamente si riavvia il servizio network:

`$ su -`
`# service network restart`

Ora si può provare a caricare una pagina web abbastanza pesante, controllando se la carica completamente. Provare ad effettuare anche:

`# yum update`

Se durante l'aggiornamento non si riscontrano problemi, procedere a rendere tutto automatico ad ogni avvio di sistema:

`# gedit /etc/sysctl.conf`

Cercare la seguente parte di testo:

`# Uncomment the next line to enable TCP/IP SYN cookies`
`# This disables TCP Window Scaling (http://lkml.org/lkml/2008/2/5/167)`

Ed aggiungere subito dopo le sequenti stringhe:

`#net.ipv4.tcp_syncookies=1`
`net.ipv4.tcp_window_scaling = 0`
`net.ipv4.tcp_ecn= 0`

Salvare il file, riavviare la macchina ed ora tutto dovrebbe funzionare.

Ovviamente questa guida non è altro che un sunto di ciò che si può trovare nel forum ringraziando tutti coloro che hanno aiutato nell'impresa di fare funzionare questa specie di "modem" dato in dotazione da Alice.

Riferimenti
-----------

-   <http://aiuto.alice.it/multimedia/manuali/modem_adsl.html>
-   <http://aiuto.alice.it/informazioni/modemadsl/generico.html>

<Categoria:Hardware>
