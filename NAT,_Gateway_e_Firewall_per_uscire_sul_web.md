Impostare una macchina con due schede di rete da usare come filtro per le connessioni a Internet.

Questa guida permette di configurare una macchina Fedora con due schede di rete da usare come NAT, Gateway e Firewall.
La Linux box su cui è stata testata è la seguente: Pentium2 233MHz (avete letto bene: duecentotrentatrè), 196Mb di RAM, FedoraCore5 (kernel 2.6.18) e senza interfaccia grafica.
L'installazione di Fedora è ridotta al minimo, senza grafica e senza pacchetti "da ufficio", basta anche un HardDisk da 8Gb

I passi da seguire sono questi:
(I meno esperti possono trovare in appendice un glossario e alcune spiegazioni)

1.  Installare Fedora e configurare le due schede di rete (meglio se durante la fase di installazione stessa) con due diverse classi di indirizzi IP

*Esempio:* una **eth0** che si affaccerà sul web, con l'indirizzo **192.168.0.1 oppure configurata tramite dhcp per quei provider che lo richiedono** (come Fastweb), l'altra, **eth1** con **192.168.1.1** che si affaccerà sulla rete interna, da rendere privata rispetto all'indirizzo IP pubblico assegnato dal provider.

<li>
**Collegare eth0 al router** (che dovrà essere sulla stessa classe di indirizzi IP es. 192.168.0.254) **o all'HAG** (se configurato con dhcp) e verificare che la macchina "veda" il web.

</li>
Se non c'è interfaccia grafica nè un bowser da lanciare, si può provare con un '''ping www.fedoraonline.it ''', se risponde, allora è connessa a Internet e risolve i nomi.

<li>
**Collegare eth1 allo switch** su cui convergeranno anche tutti i PC della rete interna che si vuole far sì che escano su Internet.

</li>
<li>
Abilitare l'IP forwarding nel kernel

</li>
<li>
Abilitare il NAT

</li>
Per mettere in pratica i punti 4 e 5, copio e incollo di seguito tutto il file **/etc/rc.d/rc.local** della macchina su cui ho provato la procedura descritta in questa guida.
Una volta inseriti in /etc/rc.d/rc.local i comandi verranno eseguiti in automatico ad ogni avvio del sistema.
**Se si hanno già altre impostazioni in rc.local, NON sostituire il file con questo riportato**, ma aggiungere solo in coda tutte le righe da echo...(compresa) alla fine.

`#!/bin/sh`
`#`
`# This script will be executed *after* all the other init scripts.`
`# You can put your own initialization stuff in here if you don't`
`# want to do the full Sys V style init stuff.`
`touch /var/lock/subsys/local`
`echo 1 >/proc/sys/net/ipv4/ip_forward `
`/sbin/iptables -P FORWARD ACCEPT`
`/sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`
`/sbin/iptables -A INPUT -i eth1 -s 192.168.1.0/255.255.255.0 -j ACCEPT`
`#/sbin/iptables -A INPUT -p udp -i eth0 -s 0/0 --dport 4672 -j ACCEPT`
`#/sbin/iptables -A INPUT -p tcp -i eth0 -s 0/0 --dport 5901 -j ACCEPT`
`#/sbin/iptables -A INPUT -p tcp -i eth0 -s 0/0 --dport 6881:6889 -j ACCEPT`
`/sbin/iptables -A INPUT -p tcp -i eth0 -m state -s 0/0 --dport 1:65535 --state INVALID,NEW -j DROP`
`/sbin/iptables -A INPUT -p udp -i eth0 -m state -s 0/0 --state INVALID,NEW -j DROP`
`/sbin/iptables -A INPUT -p icmp -i eth0 -m state -s 0/0 --state INVALID,NEW -j DROP`

La configurazione che ho riportato include anche alcune regole per un firewall di base, che permette di: ignorare tutte le richieste dalla rete esterna che tentano una nuova connessione e che non siano risposte a connessioni già stabilite, ignorare tutte le richieste con protocollo udp e tutti i ping dall'esterno.
Per applicare le regole e rendere funzionante il tutto è possibile riavviare la macchina, oppure dare da root il comando /etc/rc.d/rc.local
Chi già ha un firewall iptables funzionante e con altre regole saprà che le regole vengono applicate in ordine gerarchico e che dovrà intercalarle nel giusto ordine alle regole già esistenti.

<li>
Impostare il server Fedora con le due schede di rete come gateway (indirizzo dell'esempio 192.168.1.1) per tutti i PC della rete interna.

</li>
A questo punto tutti i PC della rete interna dovrebbero poter collegarsi a Internet tramite il NAT/Gateway/Firewall

</ol>
Appendice
---------

### Glossario

#### DHCP (Dynamic Host Configuration Protocol)

un protocollo per configurare in automatico una scheda di rete. Il client DHCP, ossia il computer che deve configurarsi, cerca in rete un server DHCP, il quale gli assegnerà un indirizzo valido per un certo intervallo di tempo (lease time).

#### Firewall

un filtro per escludere o ammettere connessioni in entrata o in uscita da una rete o da una singola macchina.

#### iptables

comando per gestire il firewall in Fedora, ha moltissime funzioni per filtrare il traffico di rete in base, ad esempio, agli indirizzi di provenienza e/o destinazione dei pacchetti di dati.

#### NAT (Network Address Translation)

operazione tramite la quale un nodo della rete "maschera" l'indirizzo IP dei pacchetti che gli giungono e li inoltra come se fossero pacchetti originati da esso stesso; lo stesso nodo si occuperà poi, al ritorno dei pacchetti di risposta, di smistarli di nuovo ai nodi originali di provenienza.

#### Gateway

viene chiamato così un apparato hardware dedicato (in genere il router ADSL che permette il collegamento a Internet), oppure un nodo configurato via software, affinchè si occupi di trasferire pacchetti di dati tra reti di diverse classi (tipicamente tra una rete domestica di classe C 192.168.0.x/255.255.255.0 e la rete pubblica Internet)

#### Essere root

root è l'utente amministratore della macchina, gli è permesso modificare tutte le configurazioni. Per alcune nozioni di base su root e sull'uso di alcuni comandi vedere la guida 'primi passi nel terminale': <http://www.fedoraonline.it/modules/wfsection/article.php?articleid=93> La spiegazione sarebbe troppo lunga da includere qui.

### Approfondimento

#### Spiegazioni per il file /etc/rc.d/rc.local

Riporto di seguito le righe necessarie alla configurazione della macchina NAT/Gateway/Firewall con alcune spegazioni.

`(1) echo 1 >/proc/sys/net/ipv4/ip_forward `
`(2) /sbin/iptables -P FORWARD ACCEPT`
`(3) /sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`
`(4) /sbin/iptables -A INPUT -i eth1 -s 192.168.1.0/255.255.255.0 -j ACCEPT`
`(5) #/sbin/iptables -A INPUT -p udp -i eth0 -s 0/0 --dport 4672 -j ACCEPT`
`(6) #/sbin/iptables -A INPUT -p tcp -i eth0 -s 0/0 --dport 5901 -j ACCEPT`
`(7) #/sbin/iptables -A INPUT -p tcp -i eth0 -s 0/0 --dport 6881:6889 -j ACCEPT`
`(8) /sbin/iptables -A INPUT -p tcp -i eth0 -m state -s 0/0 --dport 1:65535 --state INVALID,NEW -j DROP`
`(9) /sbin/iptables -A INPUT -p udp -i eth0 -m state -s 0/0 --state INVALID,NEW -j DROP`
`(10)/sbin/iptables -A INPUT -p icmp -i eth0 -m state -s 0/0 --state INVALID,NEW -j DROP`

(1) modifica un parametro del kernel per far sì che i pacchetti di dati che arrivano ad una scheda di rete vengano inoltrati all'altra. Per ripristinare il valore di default dare il comando (come root) echo 0 &gt;/proc/sys/net/ipv4/ip\_forward.

(2) imposta iptables per accettare tutti i pacchetti che vengono inoltrati

(3) imposta iptables per mascherare (-j MASQUERADE) tutti i pacchetti che escono (-o) dalla scheda di rete eth0

(4) imposta iptables per accettare tutto ciò che arriva su eth1 e che ha come provenienza la nostra rete interna, considerata affidabile.

(5)-(7) queste righe sono commentate (=hanno il \# davanti) e quindi le regole non vengono appplicate, le ho lasciate solo come esempio se dovete aprire qualche specifica porta per accedere a servizi che girano sul nodo che fa da gateway. Ad esempio la righa (6) apre la porta per il server VNC per gestire da remoto il nodo (in particolare da Internet, dato che tutte le connessioni dalla rete interna vengono accettate).
Se devo essere onesto, non so come reindirizzare ulteriormente le porte in caso che i servizi siano su macchine della rete interna. Credo che ci sia bisogno di agire sulle proprietà di POSTROUTING di iptables, ma non conosco i comandi.

(8)-(10) tre semplici regole per ignorare (-j DROP) i pacchetti in arrivo su eth0 (-i eth0) (la scheda esposta a Internet) da qualsiasi sorgente (-s 0/0) e con vari protocolli (-p tcp, -p udp, -p icmp) e che siano in uno stato (--state) NEW o INVALID, ossia richieste di nuova connessione o non rispondenti a connessioni verso l'esterno attivate dal nodo (NAT/Gateway/Firewall) stesso.

### Curiosità

In modo forse un po' presuntuoso io battezzerei una macchina così configurata come **NGF-box** dato che è una Linux box che fa da (N)at, (G)ateway e (F)irewall, ho cercato un po' su google e non mi pare che il nome esista già.

Se anche voi, come me, siete fanatici di nomi evocativi per i nodi della vostra rete, non sarebbe una cattiva idea chiamare questo nodo Giano, oppure Janus: l'antica divinità romana che custodiva le porte e i passaggi.

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink")
