\_\_TOC\_\_

Introduzione
------------

Ksplice è una nuova applicazione che permette di aggiornare in realtime il kernel senza dover riavviare per installare le nuove modifiche. Questo tool verifica le eventuali fix e le applica sfruttando un particolare meccanismo per inserire il nuovo codice, nella funzione attualmente contenuta nell'immagine del kernel caricata in memoria. Questo servizio è a pagamento per alcune distro, mentre per Fedora è gratuito (http://www.ksplice.com/news/20100831-fedora).

Verifiche sistema
-----------------

Per prima cosa verificare che la versione di Fedora attualmente installata sul sistema sia supportata da Ksplice, verificando sul sito di Ksplice all'URL <http://www.ksplice.com/pricing>

`[root@cellopc-mini ~]# cat /etc/issue`
`Fedora release 13 (Goddard)`

Dopo aver verificato che la versione di Fedora sia supportata, si dovrà per prima cosa scaricare il pacchetto rpm dal sito di Ksplice da installare manualmente in un secondo momento.

Installazione
-------------

`[root@cellopc-mini ~]# wget `[`http://www.ksplice.com/uptrack/dist/fedora/13/ksplice-uptrack.rpm`](http://www.ksplice.com/uptrack/dist/fedora/13/ksplice-uptrack.rpm)

Installare il pacchetto PyYAML necessario come dipendenza per l'installazione del pacchetto ksplice-uptrack.rpm e poi installare il pacchetto.

`[root@cellopc-mini ~]# yum install -y PyYAML`
`[root@cellopc-mini ~]# rpm -Uvh ksplice-uptrack.rpm`

Se si utilizza un proxy per accedere ad internet si dovrà modificare il file di configurazione `/etc/uptrack/uptrack.conf` inserendo le credenziali di accesso nella proprietà "https\_proxy" anche se è già esportata come variabile d'ambiente.

`[root@cellopc-mini uptrack]# cd /etc/uptrack/`
`[root@cellopc-mini uptrack]# cp uptrack.conf uptrack.conf.orig`
`[root@cellopc-mini uptrack]# diff -ub uptrack.conf.orig uptrack.conf`
`--- uptrack.conf.orig  2010-09-07 12:24:47.465388263 +0200`
`+++ uptrack.conf   2010-09-06 14:44:49.232748302 +0200`
`@@ -17,7 +17,7 @@`
`#`
`# You can also set this to "None" to force Uptrack not to use a proxy, even if`
`# one is set in the environment.`
`-https_proxy =`
`+https_proxy = `[`http://DOM`](http://DOM)` \usr01:passwd@192.168.10.1:8080`
`[Settings]`
`# Automatically install updates at boot time. If this is set, on`

Per richiamare l'interfaccia grafica si dovrà lanciare come utente non privilegiato (non root) il comando `uptrack-manager`. Da qui verrà aperta l'applet per l'aggiornamento delle componenti del kernel.

`[cello@cellopc-mini ~]$ uptrack-manager`

Cliccare su "Check" per verificare eventuali update dal repoistory fornito da KSplice. Altrimenti premere "Close" per uscire. Dopo aver selezionato gli update da installare, premere su "Install" per far partire il processo di aggiornamento a caldo del kernel.

<Categoria:Sistema>
