Questo articolo spiega come configurare un server DNS per una rete locale privata, in modo da poter usare dei DNS esterni per la navigazione su internet e poi la definizione degli host interni sempre sullo stesso sistema.
Inoltre ci sono alcuni consigli per migliorare le prestazioni del proprio server DNS. Il servizio DNS viene svolto tramite BIND 9.x su Fedora 14/15. \_\_TOC\_\_

Configurazione caching DNS locale
---------------------------------

Un DNS (Domain Name System) permette di avere un'associazione tra indirizzi IP e nomi convenzione uomo come le definizione dei siti internet. Questo server non fa altro che associare i diversi hosts ai loro indirizzi IP e viceversa. Per poter implementare questo tipo di servizio all'interno di una rete locale è possibile utilizzare il pacchetto BIND (Berkeley Internet Name Domain, in precedenza Berkeley Internet Name Daemon), che viene fornito come il software Unix per DNS più utilizzato. Con questa configurazione verrà configurato un proxy DNS server, che inoltrerà le richieste di lookup verso dei server DNS pubblici e manterrà una cache delle richieste già svolte in modo da fornirle ai client che ne richiedono la definizione. Per prima cosa installare i pacchetti necessari sul proprio server via yum.

`[root@cellopc-mini /]# yum install -y bind bind-chroot bind-libs bind-utils`

I file di configurazione se viene installato il pacchetto bind-chroot sono spostati sotto il direttorio /var/named/chroot per questioni di sicurezza. Si dovrà qundi copiare tutti i file forniti con i samples sotto questo direttorio.

`[root@cellopc-mini /]# rsync -avSA /usr/share/doc/bind-9.7.2/samples/etc/ /var/named/chroot/etc/`
`[root@cellopc-mini /]# rsync -avSA /usr/share/doc/bind-9.7.2/samples/var/named/ /var/named/chroot/var/named/`

Dopo di che verificare che la comunicazione sulla porta 53 dei server DNS pubblici funzioni correttamente. Nell'esempio verranno utilizzati due server DNS pubblici ospitati da Google.

`[root@cellopc-mini etc]# nc -z 8.8.8.8 53`
`Connection to 8.8.8.8 53 port [tcp/domain] succeeded!`
`[root@cellopc-mini etc]# nc -z 8.8.4.4 53`
`Connection to 8.8.4.4 53 port [tcp/domain] succeeded!`

Ora si dovrà modificare la configurazione del file named.conf per le proprie esigenze eseguendo prima un backup del file di conf.

`[root@cellopc-mini ~]# cd /var/named/chroot/etc/`
`[root@cellopc-mini etc]# cp named.conf named.conf.orig`

Dopo di che verrà editato il file in modo da disabilitare l'ascolto sulla porta 53 per il protocollo IPV6 e poi verrà aggiunta la direttiva "forward", per inoltrare le richieste verso dei server DNS pubblici (indirizzi specificati nella direttiva "forwarders").

`[root@cellopc-mini etc]# diff -ub named.conf.orig named.conf`
`--- named.conf.orig    2010-07-19 15:34:15.000000000 +0200`
`+++ named.conf    2010-12-22 13:45:29.963726004 +0100`
`@@ -9,7 +9,7 @@`
`options {`
`     listen-on port 53 { 127.0.0.1; };`
`-    listen-on-v6 port 53 { ::1; };`
`+    //listen-on-v6 port 53 { ::1; };`
`     directory     "/var/named";`
`     dump-file     "/var/named/data/cache_dump.db";`
`         statistics-file "/var/named/data/named_stats.txt";`
`@@ -25,6 +25,9 @@`
`     bindkeys-file "/etc/named.iscdlv.key";`
`     managed-keys-directory "/var/named/dynamic";`
`+`
`+    forward first;`
`+    forwarders { 8.8.8.8; 8.8.4.4; };`
`};`

Inoltre si potrà specificare l'indirizzo o la lista di indirizzi dove il servizio named eseguirà il bind sulla porta 53, in modo da poter mettere in ascolto su più indirizzi il proprio server. Si dovrà specificare nella direttiva "listen on" all'interno delle parentesi graffe, separando ogni indirizzo da un ";".

`[root@cellopc-mini etc]# vim named.cond`
`...`
`     listen-on port 53 { 127.0.0.1; 192.168.10.1; 192.168.10.2 }`
`...`

E' possibile settare la direttiva "forward" in due modalità:

-   FORWARD ONLY: La richiesta viene passata al DNS server del proprio provider (o quello che abbiamo impostato), se lui non ha risposta restituirà un errore.
-   FORWARD FIRST: Prima la richiesta viene passata al DNS del proprio provider, se questo non ha risposta vengono interrogati i root server. Conviene impostarlo a "forward first" sia perché in genere il DNS del proprio provider risponde più velocemente degli altri (anche avendo una buona cache), sia per generare meno traffico inutile in Internet.

Dopo aver verificato che la configurazione sia corretta si potrà verificare la sintassi dei file tramite il comando "named-checkconf".

`[root@cellopc-mini ~]# chmod 644 /var/named/chroot/etc/named.conf`
`[root@cellopc-mini etc]# named-checkconf -z -t /var/named/chroot/`
`zone cello.local/IN: loaded serial 2011011901`

Se la sintassi è corretta startare il servizio named se non è attivo, e nel caso sia già attivo eseguire il reload dalla configurazione.

`[root@cellopc-mini ~]# service named restart`
`Stopping named:                                            [  `<span style="color: #007700">`OK`</span>`  ]`
`Starting named:                                            [  `<span style="color: #007700">`OK`</span>`  ]`

Editare il file di configurazione dei server DNS sul proprio sistema (il file /etc/resolv.conf), impostando come unico nameserver l'indirizzo 127.0.0.1.

`[root@cellopc-mini ~]# vim /etc/resolv.conf`
`nameserver 127.0.0.1`

Provando ora a richiedere la risoluzione del sito www.google.it la prima volta e campionando il tempo, la richiesta sarà di qualche secondo (nel nostro esempio quasi 8 secondi).

`[root@cellopc-mini ~]# time nslookup www.google.it`
`Server:        127.0.0.1`
`Address:    127.0.0.1#53`
`Non-authoritative answer:`
`www.google.it    canonical name = www.google.com.`
`www.google.com    canonical name = www.l.google.com.`
`Name:    www.l.google.com`
`Address: 74.125.87.99`
`Name:    www.l.google.com`
`Address: 74.125.87.104`
`real    0m7.718s`
`user    0m0.009s`
`sys    0m0.016s`

Verificando le successive volte il tempo di esecuzione sarà di pochi millisecondi, perchè la lookup successiva è stata mantenuta in cache.

`[root@cellopc-mini ~]# time nslookup www.google.it`
`Server:        127.0.0.1`
`Address:    127.0.0.1#53`
`Non-authoritative answer:`
`www.google.it    canonical name = www.google.com.`
`www.google.com    canonical name = www.l.google.com.`
`Name:    www.l.google.com`
`Address: 74.125.87.104`
`Name:    www.l.google.com`
`Address: 74.125.87.99`
`real    0m0.024s`
`user    0m0.012s`
`sys    0m0.008s`

Attivare poi il servizio named al boot per mantenere il servizio DNS in caso di riavvii del sistema.

`[root@cellopc-mini ~]# chkconfig named on`

Per poter poi permettere le richieste di lookup interne è possibile configurare la direttiva "allow-query", specificando la lista di reti (o singoli hosts interni) che possono svolgere le richieste al nostro server DNS. Risulta utile introdurre anche la direttiva "acl", che permette di creare dei gruppi di sottoreti che possono essere richiamate con facilità poi all'interno del file. Nell'esempio è stato creato il gruppo ACL "allowed\_nets" che poi sarà richiamato successivamente negli hosts che possono eseguire le lookup.

`[root@cellopc-mini etc]# diff -ub named.conf.old named.conf`
`--- named.conf.old    2010-12-23 13:30:18.129356667 +0100`
`+++ named.conf    2010-12-23 13:53:00.546357036 +0100`
`+acl allowed_nets { 192.168.10.0/24; 192.168.11.0/24; };`
`+`
`-    allow-query     { localhost; };`
`+    allow-query     { localhost; allowed_nets; };`
`     recursion yes;`

Dopo le modifiche eseguire il reload del servizio named per far caricare le nuove configurazioni.

`[root@cellopc-mini ~]# service named reload`

Configurazione internal DNS
---------------------------

Dopo aver configurato un proxy DNS per una rete locale è possibile creare un servizio DNS per una rete locale ed un suo dominio associato. In questo modo la risoluzioni all'interno del dominio "cello.local" verranno prese dalla configurazione interna, mentre tutto il resto verrà demandato al DNS esterno.
Nella configurazione del DNS verrà introdotta la direttiva "view" che permette di avere una configurazione separata in base al client che vengono intercettate dalle direttive "match-clients" e "match-destinations". Solitamente esistono le viste "internal" ed "external" che mantengono separate le configurazioni e verranno applicate le diverse opzioni in base al match degli indirizzi.

`[root@cellopc-mini named]# vim /var/named/chroot/etc/named.conf`
`view "internal"`
`{`
`...`
`};`

Come già detto in precedenza le clausole "match-clients" e "match-destinations" verificano se gli IP sorgenti delle richieste o destinatari fanno parte della lista passata all'interno delle direttive. Nel nostro esempio viene passato localhost e due subnet internet utilizzate dal nostro server per servire le richieste di lookup da alcune macchine virtuali. E' possibile aggiungere altre reti.

`[root@cellopc-mini named]# vim /var/named/chroot/etc/named.conf`
`view "internal"`
`{`
`        match-clients           { localhost; 192.168.10.0/24; 192.168.11.0/24; };`
`        match-destinations      { localhost; 192.168.10.0/24; 192.168.11.0/24; };`
`...`
`        recursion yes;`
`        include "/etc/named.root.key";`
`...`
`};`

Ora per ogni view sarà possible creare delle "zone", cioè suddividere per ogni dominio un file di configurazione separato dove sono contenuti tutti i record degli host risolvibili dal proprio DNS. Dato che si ha un dominio chiamato "cello.local" ci sarà una zone chiamata "cello.local" che definirà come master server del dominio il nostro server (con la direttiva "type" settata a "master" e poi specificato il nome del file di configurazione presente sotto il direttorio /var/named/chroot/var/named.

`[root@cellopc-mini named]# vim /var/named/chroot/etc/named.conf`
`view "internal"`
`...`
`        zone "cello.local" {`
`                type master;`
`                file "cello.local.zone.db";`
`        };`
`...`
`};`

I file \*.zone.db contengono tutti tipi di record e la loro associazione. Questo file viene usato sia per la risoluzione diretta che inversa degli indirizzi sul proprio server DNS. Il contenuto del file cello.local.zone.db sul proprio server DNS conterrà tutte le informazioni per il dominio interno specificato nella zona configurata. Per prima cosà verranno specificate le entry:
\* $ORIGIN : specifica il nome del dominio utilizzato e configurato nella zone del file named.conf e viene richiamato in tutte le entry dove il dominio non viene specificato. Per esempio se viene settata la direttiva in questo modo "$ORIGIN cello.local.", se viene inserita la entry "www" senza specificare alcun dominio, il DNS la comporrà come "www.cello.local.".

-   $TTL : identifica il time to live delle richieste, cioè il periodo di tempo impostato per considerare le informazioni passate dal DNS server valide. Solitamente il valore viene espresso in secondi (impostandolo a 86400 secondi si mantiene il TTL ad un giorno).

`[root@cellopc-mini named]# vim /var/named/chroot/var/named/cello.local.zone.db `
`$ORIGIN cello.local.`
`$TTL 86400`
`...`

Le prime rige della configurazione contengono le informazioni della zona cioè il record SOA (Start of Autority) ed indicato il nameserver principale del dominio ed alcuni parametri per la validità dei dati. A differenza degli altri tipi di record DNS, questo record viene espresso su più righe ma è da considerarsi come una singola riga di configurazione. Nella prima parte del SOA viene specificato i server DNS principali della zona (solitamente lo stesso server DNS che si sta configurando). Successivamente vengono riportati questi altri valori:

-   serial : espresso solitamente nel formato "YYYYMMDDNN" identifica un numero che deve essere modifica ad ogni aggiornamento della configurazione, in modo che i server DNS secondari aggiornino la configurazione in caso di modifiche.
-   refresh : espresso in secondi identifica l'intervallo di tempo prima che il server DNS esegua un controllo di evenutali modifiche nei file di configurazione delle zone e ne esegua il caricamento
-   retry : espresso in secondi identifica l'intervallo di tempo prima che il server DNS secondario in caso di mancata connettività con il primario, ritenti di ripristinare il collegamento.
-   expire : espresso in secondi identifica l'intervallo di tempo prima che il server DNS secondario in caso di mancata connettività con il primario, consideri non più validi i dati in precedenza forniti.
-   minimum : espresso in secondi identifica l'intervallo di tempo che viene utilizzato dai server DNS esterni per considerare valide le informazioni fornite dal server DNS stesso. Questo valore nella versiond BIND 9.x viene sovrascritto dal $TTL.

`[root@cellopc-mini named]# vim /var/named/chroot/var/named/cello.local.zone.db`
`...`
`@               IN      SOA     cellopc-mini.cello.local. ns.cello.local. (`
`                                2011011901 ; serial`
`                                21600 ; refresh after 6 hours`
`                                3600 ; retry after 1 hour`
`                                604800 ; expire after 1 week`
`                                86400 ) ; minimum TTL of 1 day`
`...`

Ora si dovranno definire il record NS (Name server) cioè il DNS considerato autorevole e quindi principale del proprio dominio. In questo caso sarà lo stesso DNS che verrà risolto come "ns.cello.local.". Sotto verrà subito aggiunta una nuovo record DNS di tipo A cioè associabile ad un indirizzo IP (IPv4). Infatti la struttura di ogni record della zona sono:

-   prima colonna : nome o indirizzo con cui viene svolta la lookup
-   seconda colonna : TTL del singolo record DNS
-   terza colonna : classe del record DNS (IN = internet).
-   quarta colonna : tipo di record DNS
-   quinta : indirzzo o nome che viene associato al termine della lookup.

`[root@cellopc-mini named]# vim /var/named/chroot/var/named/cello.local.zone.db`
`...`
`                86400   IN      NS              ns.cello.local.`
`ns        86400   IN      A       192.168.10.1`
`...`

In questo modo quando si cercherà di risolvere l'hostname ns.cellolocal verrà associato all'indirizzo 192.168.10.1. E' ora possibile inserire altri record per popolare il proprio server in base alla struttura della subnet utilizzata.

`[root@cellopc-mini named]# vim /var/named/chroot/var/named/cello.local.zone.db`
`...`
`server01    86400   IN    A    192.168.10.2`
`server02    86400   IN    A    192.168.10.3`
`...`

Nel caso si utilizzi un server web con Virtualhost configurati, risulta utile il record CNAME che non fa altro che puntare ad un altro record ad esempio di tipo A. Infatti in questo esempio viene definito il record per l'host "cellopc-mini" che ospita Apache con il VirtualHost "cellowiki". Basterà aggiungere un record di tipo CNAME facendolo puntare all'hostname definito nel precedente record A e il gioco sarà fatto

`[root@cellopc-mini named]# vim /var/named/chroot/var/named/cello.local.zone.db`
`...`
`cellopc-mini    86400   IN    A    192.168.10.1`
`cellowiki    86400   IN      CNAME       cellopc-mini.cello.local.`
`...`

La configurazione di esempio completa sarà la seguente:

`[root@cellopc-mini ~]# cat /var/named/chroot/var/named/cello.local.zone.db `
`$ORIGIN cello.local.`
`$TTL 86400`
`@               IN      SOA     cellopc-mini.cello.local. ns.cello.local. (`
`                                2011011901 ; serial`
`                                21600 ; refresh after 6 hours`
`                                3600 ; retry after 1 hour`
`                                604800 ; expire after 1 week`
`                                86400 ) ; minimum TTL of 1 day`
`                86400   IN      NS              ns.cello.local.`
`ns        86400   IN      A       192.168.10.1`
`cellopc-mini    86400   IN    A    192.168.10.1`
`cellowiki    86400   IN      CNAME       cellopc-mini.cello.local.`
`server01    86400   IN    A    192.168.10.2`
`server02    86400   IN    A    192.168.10.3`

Verificare la sintassi dei file di configurazione tramite il comando named-checkconf.

`[root@cellopc-mini ~]# named-checkconf -z`
`zone localhost.localdomain/IN: loaded serial 0`
`zone localhost/IN: loaded serial 0`
`zone 1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa/IN: loaded serial 0`
`zone 1.0.0.127.in-addr.arpa/IN: loaded serial 0`
`zone 0.in-addr.arpa/IN: loaded serial 0`

Se tutto è corretto eseguire il riavvio del proprio server DNS ed impostare in locale il proprio /etc/resolv.conf in modo che punti al DNS locale, eseguendo una ricerca per il dominio impostato nella zona.

`[root@cellopc-mini ~]# service named restart`
`Stopping named:                                            [  `<span style="color: #007700">`OK`</span>`  ]`
`Starting named:                                            [  `<span style="color: #007700">`OK`</span>`  ]`

`[root@cellopc-mini ~]# vim /etc/resolv.conf`
`nameserver 127.0.0.1`
`search cello.local`

Tramite il comando nslookup si potranno fare delle query verso il DNS per capire se la propria configurazione è corretta.

`[root@cellopc-mini ~]# nslookup cellopc-mini`
`Server:        127.0.0.1`
`Address:    127.0.0.1#53`
`Name:    cellopc-mini.cello.local`
`Address: 192.168.10.1`
`[root@cellopc-mini ~]# nslookup server01`
`Server:        127.0.0.1`
`Address:    127.0.0.1#53`
`Name:    server01.cello.local`
`Address: 192.168.10.2`

Ora si dovrà configurare la risoluzione inversa sulla propria subnet, in modo da poter rintracciare l'host che sta utilizzando un determinato indirizzo. Il tipo di record utilizzato sarà il PTR, che permette di far puntare un indirizzo IP ad un indirizzo canonico sul DNS. Il file di configurazione delle zone inverse utilizza la nomenclatura "in-addr.arpa" specifica per la risoluzione degli indirizzi IP. Il nome del file di conf sarà: "<subnet>.in-addr.arpa.zone.db" come ad esempio "10.168.192.in-addr.arpa". L'inizio del file di configurazione sarà ancora formato dai record SOA e NS.

`[root@cellopc-mini etc]# vim /var/named/chroot/var/named/10.168.192.in-addr.arpa.zone.db `
`$ORIGIN 10.168.192.in-addr.arpa.`
`$TTL 86400`
`@               IN      SOA     cellopc-mini.cello.local. ns.cello.local. (`
`                                1000 ; serial`
`                                21600 ; refresh after 6 hours`
`                                3600 ; retry after 1 hour`
`                                604800 ; expire after 1 week`
`                                86400 ) ; minimum TTL of 1 day`
`                86400   IN      NS              ns.cello.local.`
`...`

Ora si dovranno inserire i record di tipo PTR puntando all'indirizzo sulla rete che viene utilizzato dal record specificato

`....`
`1     IN      PTR     cellopc-mini.cello.local.`
`2     IN      PTR     server01.cello.local.`
`3     IN      PTR     server02.cello.local.`
`...`

Dopo aver inserito tutte le entry si dovrà modificare il file di configurazione principale named.conf inserendo nella vista "internal" anche la zona inversa.

`[root@cellopc-mini etc]# vim/var/named/chroot/etc/named.conf`
`...`
`view "internal"`
`{`
`     ...`
`        zone "10.168.192.in-addr.arpa" {`
`                type master;`
`                file "10.168.192.in-addr.arpa.zone.db";`
`        };`
`      ...`
`};`
`...`

Al termine delle modifiche eseguire ancora il check sulla sintassi dei file di configurazione e poi eseguire il restart del servizio named per caricare le modifiche.

`[root@cellopc-mini etc]# named-checkconf -z -t /var/named/chroot/`
`zone cello.local/IN: loaded serial 2011011901`
`zone 10.168.192.in-addr.arpa/IN: loaded serial 1000`
`zone 11.168.192.in-addr.arpa/IN: loaded serial 1000`

`[root@cellopc-mini etc]# service named restart`
`Stopping named:                                            [  `<span style="color: #007700">`OK`</span>`  ]`
`Starting named:                                            [  `<span style="color: #007700">`OK`</span>`  ]`

Provando ad eseguire ora delle risoluzioni su indirizzi IP interni, si dovrà verificare che la lookup venga svolta correttamente dal proprio DNS.

`[root@cellopc-mini etc]# nslookup 192.168.10.1`
`Server:        127.0.0.1`
`Address:    127.0.0.1#53`
`1.10.168.192.in-addr.arpa    name = cellopc-mini.cello.local.`
`[root@cellopc-mini etc]# nslookup 192.168.10.2`
`Server:        127.0.0.1`
`Address:    127.0.0.1#53`
`2.10.168.192.in-addr.arpa    name = server01.cello.local.`

E' possibile creare più file di configurazione per la risoluzione interna, in modo da censire in modo più puntuale dei server, che si attestano su più LAN differenti. Modificare quindi il file di configurazione per la risoluzione diretta della zona, inserendo i nuovi host.

`[root@cellopc-mini etc]# vim /var/named/chroot/var/named/cello.local.zone.db `
`...`
`server01-admin  86400   IN    A    192.168.11.2`
`server02-admin  86400   IN    A    192.168.11.3`
`...`

Configurare il file di risoluzione inversa con gli host attestati sulla subnet e definiti nella configurazione della rioluzione diretta.

`[root@cellopc-mini etc] vim /var/named/chroot/var/named/11.168.192.in-addr.arpa.zone.db `
`$ORIGIN 11.168.192.in-addr.arpa.`
`$TTL 86400`
`@               IN      SOA     cellopc-mini.cello.local. ns.cello.local. (`
`                                1000 ; serial`
`                                21600 ; refresh after 6 hours`
`                                3600 ; retry after 1 hour`
`                                604800 ; expire after 1 week`
`                                86400 ) ; minimum TTL of 1 day`
`                86400   IN      NS              ns.cello.local.`
`1     IN      PTR     cellopc-mini.cello.local.`
`2     IN      PTR     server01-admin.cello.local.`
`3     IN      PTR     server02-admin.cello.local`

Modificare il file di configurazione named.conf inserendo nella vista internal anche la zona inversa appena creata, in modo da renderla disponibile ai client che svolgeranno le query.

`[root@cellopc-mini etc]# vim /var/named/chroot/etc/named.conf`
`....`
`view "internal"`
`{`
`        ....`
`        zone "11.168.192.in-addr.arpa" {`
`                type master;`
`                file "11.168.192.in-addr.arpa.zone.db";`
`        };`
`        ...`
`};`
`...`

Ora eseguire il check sulla configurazione e poi eseguire il restart del servizio named.

`[root@cellopc-mini etc]# named-checkconf -z -t /var/named/chroot/`
`zone cello.local/IN: loaded serial 2011011901`
`zone 10.168.192.in-addr.arpa/IN: loaded serial 1000`
`zone 11.168.192.in-addr.arpa/IN: loaded serial 1000`
`[root@cellopc-mini etc]# service named restart`
`Stopping named:                                            [  `<span style="color: #007700">`OK`</span>`  ]`
`Starting named:                                            [  `<span style="color: #007700">`OK`</span>`  ]`

Verificare che svolgendo delle lookup sulla nuova subnet con risoluzione inversa o diretta venga svolto tutto in modo corretto.

`[root@cellopc-mini etc]# nslookup server01-admin`
`Server:        127.0.0.1`
`Address:    127.0.0.1#53`
`Name:    server01-admin.cello.local`
`Address: 192.168.11.2`
`[root@cellopc-mini etc]# nslookup 192.168.11.2`
`Server:        127.0.0.1`
`Address:    127.0.0.1#53`
`2.11.168.192.in-addr.arpa    name = server01-admin.cello.local.`

Configurazione cache DNS per forwarder DNS
------------------------------------------

Se si utilizza un forwarder DNS con BIND 9.x e si naviga molto in internet, in alcuni casi si possono avere dei problemi durante lo stop del servizio named, perchè la dimensione della cache è troppo grande. Il file della cache viene specificanto nel parametro "dump-file" nel file "named.conf".

`[root@cellopc-mini ~]# vim /var/named/chroot/etc/named.conf`
`...`
`options {`
`...`
`    dump-file     "/var/named/data/cache_dump.db";`
`...`
`};`

Un piccolo wokraround è quello di ripulire la cache tramite il comando "rndc flus" (per maggirori dettagli vedere la pagina [ Pulizia cache di proxy DNS](#Pulizia_cache_di_proxy_DNS "wikilink") con BIND 9.x) prima dello stop, ma si potrebbe eseguire un piccolo tuning sulla cache tramite i seguenti parametri:

-   max-cache-size : definisce la dimensione massima (in byte/K/M) del file di cache specificato nel paramtro "dump-file"
-   max-cache-ttl : definisce il TTL per mantenere valide le richieste positive dai DNS esterni in cache. Il parametro viene espresso in secondi
-   max-ncache-ttl : definisce il TTL per mantenere valide le richieste negative dai DNS esterni in cache. Il parametro viene espresso in secondi
-   cleaning-interval : Intervallo di tempo per la rimozione delle chiavi espirate. Il parametro viene espresso in minuti.

`[root@cellopc-mini ~]# vim /var/named/chroot/etc/named.conf`
`...`
`options {`
`...`
`    dump-file     "/var/named/data/cache_dump.db";`
`....`
`    allow-query     { localhost; allowed_nets; };`
`    recursion yes;`
`...`
`    forward first;`
`    forwarders { 8.8.8.8; 8.8.4.4; };`
`    /* Definisce la dimensione massima della cache (contenuta in dump-file). */    `
`    max-cache-size 10M;`
`    /* Definisce quanti secondi mantenere in cache le risposte positive dai DNS esterni */`
`    max-cache-ttl 86400;`
`    /* Definisce quanti secondi mantenere in cache le risposte negative dai DNS esterni */`
`        max-ncache-ttl 60;`
`    /* Intervallo di tempo per la rimozione delle chiavi espirate (in minuti) */`
`    cleaning-interval 10;`
`...`
`};`
`...`

Dopo la modifica eseguire il riavvio del servizio named per applicare le modifiche.

`[root@cellopc-mini ~]# service named restart`

Pulizia cache di proxy DNS
--------------------------

Quando si installa un proxy DNS server con BIND le lookup svolte verso DNS pubblici vengono salvate in locale per ridurre le richieste verso internet, e velocizzare i tempi di risposta. Per ripulire la cache che viene mantenuta su disco si potrà semplicemente riavviare il demone named in modo da far ricreare la cache

`[root@cellopc-mini ~]# service named restart`

Oppure è possibile sfruttuare il comando rndc, che permette di invocare alcune operazioni sul demone named, senza dover forzatamente riavviare. Richiamando il comando rndc con l'opzione "flush", verrà svuotata la cache per tutte le zone sotto il controllo di named.

`[root@cellopc-mini ~]# rndc flush`

Dopo la pulizia le prime lookup inviare verso un server pubblico saranno un pochino lente (qualche secondo) ma poi verranno mostrate in tempi in ordine di millisecondi

<Categoria:Sistema>
