Questa non vuol essere una guida passo-passo di una installazione ma un canovaccio da seguire nel caso si voglia configurare ex-novo una qualunque scheda wireless a prescindere dal tipo.
E' indirizzata appunto ad utenti che hanno problemi nella configurazione della propria wireless.
Ultimamente ho utilizzato uno schema mentale del genere, in vari thread del nostro forum, per dare una mano ad utenti in difficoltà, spesso con esiti positivi.
Questa guida non vuole essere esaustiva, ma, vuole cercare di affrontare i problemi più comuni per cui mi scuso fin d'ora delle imprecisioni in essa contenute.
Spero, inoltre, dopo questa prima stesura di pubblicarne una più completa e corretta.

Premessa
--------

Si userà la linea di comando e non le interfacce grafiche ( networkmanager, wifi-radar, wlassistant etc) per cinque motivi validi:

1.  le interfacce grafiche non permettono un uso totale del sistema
2.  le interfacce grafiche non sempre funzionano correttamente con tutte le schede ( ad esempio NetworkManager in F8 sta dando parecchi problemi a molti utenti)
3.  le interfacce grafiche non fanno altro che lanciare degli script shell e allora tanto vale fare se la cosa ed avere il controllo della situazione.
4.  è più facile descrivere cosa si sta facendo, ed interrompere la procedura in caso di errore per chiedere un aiuto specifico sul problema che si è presentato
5.  la linea di comando è un mezzo di grande potenza e flessibilità e permetterà di fare esattamente ciò che si prevede.

Materiali
---------

Oltre alla propria scheda e al computer dove si vuole installarla, si ha la necessità di avere un computer collegato alla rete web, naturalmente può essere il computer stesso sul quale si andrà ad agire perché magari è dotato di connessione via cavo.
Questa ipotesi è particolarmente utile ed efficiente pertanto se il proprio computer non è dotato di connessione via cavo si invito a dotarlo di un simile dispositivo almeno temporaneamente, e assumeremo nel prosieguo che si avrà risolto questo problema.

Convenzioni
-----------

Per ottenerli da interfaccia grafica -&gt; strumenti di sistema -&gt; terminale

`$ su -`
`password:(inserite la password di root)`

non dimenticare il - "trattino" dopo "su" altrimenti si avranno i poteri root ma ambiente utente.

Se si sono dubbi su di un comando o sulla sua sintassi, oppure il sistema informa che il comando è sconosciuto o non eseguibile ( tutti gli umani sbagliano ), usare le pagine man:

`$ man nome_comando`

Ho indicato con nomi di fantasia alcune periferiche e moduli, per essere più generico possibile, quindi attenzione a non usare questi nomi nella realtà.

REPERIRE INFORMAZIONI
---------------------

### La prima cosa da fare è reperire informazioni

Dare il comando:

`# lspci`

l'output potrebbe essere una cosa del genere:

`00:00.0 Host bridge: VIA Technologies, Inc. VT8377 [KT400/KT600 AGP] Host Bridge (rev 80)`
`00:01.0 PCI bridge: VIA Technologies, Inc. VT8237 PCI Bridge`
`00:0a.0 Ethernet controller: Atheros Communications, Inc. AR5212 802.11abg NIC (rev 01)`
`00:0f.0 IDE interface: VIA Technologies, Inc. VT82C586A/B/VT82C686/A/B/VT823x/A/C PIPC Bus Master IDE (rev 06)`
`00:10.0 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1.1 Controller (rev 81)`
`00:10.1 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1.1 Controller (rev 81)`
`00:10.2 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1.1 Controller (rev 81)`
`00:10.4 USB Controller: VIA Technologies, Inc. USB 2.0 (rev 86)`
`00:11.0 ISA bridge: VIA Technologies, Inc. VT8237 ISA bridge [KT600/K8T800/K8T890 South]`
`00:11.5 Multimedia audio controller: VIA Technologies, Inc. VT8233/A/8235/8237 AC97 Audio Controller (rev 60)`
`00:13.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8139/8139C/8139C+ (rev 10)`
`01:00.0 VGA compatible controller: ATI Technologies Inc RV280 [Radeon 9200 SE] (rev 01)`
`00:00.0 Host bridge: VIA Technologies, Inc. VT8377 [KT400/KT600 AGP] Host Bridge (rev 80)`
`00:01.0 PCI bridge: VIA Technologies, Inc. VT8237 PCI Bridge`
`00:0a.0 Ethernet controller: Atheros Communications, Inc. AR5212 802.11abg NIC (rev 01)`

oppure più lungo.

La linea del tipo:

`01:04.0 Network controller: Pinco-Pallina Comunications PPC1452 802.11g (rev 05)`

oppure:

`00:0a.0 Ethernet controller: Pinco-Pallina Comunications PPC1452 802.11g (rev 04)`

è quello che interessa (ripeto: ho usato nomi di fantasia e la scheda in questione naturalmente non esiste).
Se ci sono dubbi tenere presente che il protocollo standard della connessione wifi è: 802.11 e può essere di diversi tipi: a,b,g,... etc.

Se la linea non c'è e l'hardware è collegato al sistema allora il problema è molto più grave e bisognerà attendere o che venga rilasciato un kernel che la "veda" o che venga pubblicata una guida specifica, oppure si è così esperti che leggere questa guida è inutile.

Ora quello che bisogna fare è di cercare le informazioni in rete tramite \[<http://www.google.it/linux>. www.google.it/linux.\]
Una ottima idea è quella di associare alle parole chiave "Pinco-Pallina 1452", cioè il chip wireless montato sulla scheda e il numero tipo, la parola "fedora 8" e/o la versione kernel, che è possibile ottenere con il comando:

`$ uname -r`

Fare attenzione alle date delle informazioni che si andranno a raccogliere, perché il proprio Sistema Operativo si evolve continuamente, quindi ciò che tre mesi fa era valido spesso ora non lo è più.

### Cosa bisogna cercare

Fondamentalmente una sola cosa: il nome del modulo kernel che gestisce la scheda e le informazioni sul suo funzionamento.
Googleando a dx e a sx si riesce ad appurare che la scheda Pinco-Pallina PPC1452 è gestita dal modulo: PP14WF.
Fare attenzione che questa ultima cosa sia vera altrimenti si perderà solo tempo, l'informazione DEVE essere SICURA.
Il modulo PP14wf deve essere quello che gestisce esattamente il proprio hardware e NON un hardware similare.
La grande varietà di chip wifi presenti sul mercato fa si che una periferica dello stesso produttore e con lo stesso nome ma versione differente (rev 05) o (rev 04), possa avere un chip diverso.
Chip differenti avranno, probabilmente, periferiche con lo stesso nome ma con bus di comunicazione differente, ad esempio schede pci, usb, oppure pcmcia.
Quindi fare molta attenzione a questo fatto.
Esistono siti che indicano la compatibilità dei chip wifi con determinati moduli, fatene uso, selezionando i più aggiornati.
Se si è particolarmente bravi o fortunati la propria ricerca si esaurisce in pochi minuti.
Tenere presente che se si arriva a sapere qual è il modulo, il più è fatto.
Sapere che esiste il modulo che la gestisce e non bisogna fare altro che montare, configurare adeguatamente modulo, periferica e rete wireless.

Una volta trovato il modulo, ci si può trovare di fronte a diverse possibilità:

1.  Il modulo in questione è già presente nel kernel che si ha a disposizione.
      
    In questo caso vuol dire che gli sviluppatori del kernel hanno avuto il tempo per implementarlo o grazie al produttore che ha messo a disposizione le specifiche dell'hardware oppure a specifici progetti della comunità.

2.  Il modulo è stato implementato esternamente al kernel e va "iniettato" mediante una procedura di compilazione ed installazione.
      
    In questo caso il chip è particolarmente nuovo e gli sviluppatori del kernel non hanno avuto ancora il tempo di inserire il modulo che lo gestisce dopo averlo opportunamente testato, oppure il produttore ha rilasciato un modulo con software closed.

3.  Il modulo è, non solo "esterno" al kernel, ma va gestito con software particolare.
      
    Questo può essere il caso in cui non esistono moduli kernel specifici e bisogna rivolgersi a dei software particolari (ad esempio ndiswrapper) che riescano a risolvere comunque il problema.

Per il momento intendo occuparmi della prima ipotesi, la più semplice, successivamente descriverò nelle Appendici [A](#Appendice_A "wikilink") e [B](#Appendice_B "wikilink") come comportarsi nelle altre due.

### Come verificare che il modulo sia presente nel nostro kernel

Dare il comando

`# modprobe -l pp14wf`

( ripeto ancora: il modulo pp14wf in realtà non esiste )

Se la risposta del sistema è di questo tipo:

`/lib/modules/2.6.23.1-49.fc8/kernel/drivers/net/wireless/pp14wf.ko`

vuol dire che è presente, se risponde col prompt \# vuol dire che non è presente.
Se è presente si può proseguire, se non è presente bisogna trovarlo e installarlo cioè ci si trova nell'ipotesi che va "iniettato" perché per qualche motivo non è stato inglobato nel kernel della nostra Fedora, ad esempio potrebbe, anche, trattarsi di un modulo "proprietario" cioè non prodotto dalla Community e quindi non distribuito ufficialmente, pertanto saltare temporaneamente questa parte ed andare all'[Appendice A](#Appendice_A "wikilink").

INSTALLARE IL MODULO
--------------------

### Controllare quali siano le proprie periferiche di comunicazione

Dare i comandi:

`# ifconfig`

si avrà come risposta una cosa del genere:

`eth0      Link encap:Ethernet  HWaddr 00:13:8F:F3:37:4E  `
`          inet addr:192.168.1.65  Bcast:192.168.1.255  Mask:255.255.255.0`
`          inet6 addr: fe80::213:8fff:fef3:374e/64 Scope:Link`
`          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1`
`          RX packets:20549 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:15213 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:1000 `
`          RX bytes:26450306 (25.2 MiB)  TX bytes:1144627 (1.0 MiB)`
`          Interrupt:17 Base address:0x2000 `
`lo        Link encap:Local Loopback  `
`          inet addr:127.0.0.1  Mask:255.0.0.0`
`          inet6 addr: ::1/128 Scope:Host`
`          UP LOOPBACK RUNNING  MTU:16436  Metric:1`
`          RX packets:5568 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:5568 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:0 `
`          RX bytes:2754748 (2.6 MiB)  TX bytes:2754748 (2.6 MiB)`

La prima periferica è una ethernet via cavo la cui descrizione è piuttosto intuitiva:

`HWaddr 00:13:8F:F3:37:4E ---> indirizzo fisico detto anche mac-address`
`inet addr:192.168.1.65 ---> indirizzo ip- internet protocoll ( `**`fondamentale,` `ogni` `periferica` `network` `DEVE` `avere` `un` `ip,` `se` `non` `è` `presente` `non` `potrà` `mai` `funzionare`**`)`
`RX bytes:26450306 (25.2 MiB)  TX bytes:1144627 (1.0 MiB) ---> il numero di byte ricevuti e trasmessi.`

Gli altri parametri non interessano, almeno per il momento.
L'interfaccia denominata "lo" è l'interfaccia di loopback, molto speciale, essa NON va mai toccata, a meno che non si sa cosa si sta facendo.
Se è presente solo la loopback vuol dire che non si possiede, almeno per il momento, interfacce network.

Poi dare:

`# iwconfig`

il cui output dovrebbe essere:

`lo        no wireless extensions.`
`eth0      no wireless extensions.`

questo significa che non si hanno interfacce wifi disponibili.

Copiare gli output da qualche parte e tenerli a portata di mano per confrontarli con i successivi.

### Montare il modulo

Per prima cosa verificare che non sia già montato:

`# lsmod|grep pp14wf`

( il simbolo | è una "pipe") se il sistema risponde una cosa del genere:

`pp14wf                135049  0 `
`ieee80211              30985  1 pp14wf`

allora è già montato, ciò significa che i servizi di autoconfigurazione ( kuzdu, hal, etc ) hanno funzionato in maniera eccellente, individuando l'hardware e caricando autonomamente il modulo nel kernel, e non bisogna procedere al montaggio, saltare la lettura successiva andando al paragrafo [Alias](#Alias "wikilink").

Se non lo è allora lo si monta:

`# modprobe pp14wf`

se il sistema risponde con il prompt allora il modulo è stato montato con successo e si può verificare questa cosa con il comando:

`# lsmod|grep pp14wf`

### Alias

All'atto del montaggio del modulo dovrebbe comparire il nome della periferica che viene gestita dal modulo, si può verificare questo con:

`# dmesg|grep pp14wf`

dmesg è il comando che visualizza i messaggi del kernel a seguito di un evento e dovrebbe dare un output del genere:

`[   52.675396] PP14WF: Vendor = 0x1814, Product = 0x0301 `
`[   53.473722] PP14WF: RfIcType= 3`

ed altro.
La periferica avrà assegnato dal sistema un alias (nome simbolico) del tipo eth1, ra0, wlan0 o altre sigle, naturalmente il proprio sistema permette la personalizzazione dell'alias se in modprobe non si utilizzano opzioni particolari l'alias sarà quello predefinito.
Potremo visualizzare il nome simbolico con il comando:

`# iwconfig`

il cui output produce:

`lo no wireless extensions.`
`eth0 no wireless extensions.`
`pw0 unassociated ESSID:off/any Nickname:""`
`Mode:Managed Channel=0 Access Point: Not-Associated`
`Bit Rate:0 kb/s Tx-Power:16 dBm`
`Retry short limit:7 RTS thr:off Fragment thr:off`
`Encryption key:off`
`Power Management:off`
`Link Quality:0 Signal level:0 Noise level:0`
`Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:0`
`Tx excessive retries:0 Invalid misc:0 Missed beacon:0`

spendiamo qualche parola sul significato di quest'ultimo.

-   pw0 unassociated --&gt; il nome simbolico della periferica wifi che useremo sarà proprio pw0 voi lo sostituirete con il vostro alias -
-   (unassociated) --&gt; la periferica non è attiva ( per il momento )
-   ESSID --&gt; il nome della rete wifi - off nessuno
-   Mode --&gt; il tipo di connessione Managed di solito si utilizza questo per gran parte delle connessioni wifi del client remoto
-   Channel = 0 --&gt; canale della comunicazione - nessuno
-   Access Point : Not - Associated --&gt; l'access point non è "agganciato"
-   Encryption key:off --&gt; chiave di criptazione off

gli altri parametri sono intuitivi.

Ora che il modulo è stato caricato siamo pronti per la...

CONFIGURAZIONE DELLA PERIFERICA E DELLA RETE WIRELESS
-----------------------------------------------------

In questa fase utilizzerò ip statici e non dinamici (dhcp).
Farò anche l'ipotesi che il proprio access point sia collegato ad un router (cosa assai probabile) e che il proprio provider non sia fastweb ( poi lo spiego ).
Ci occorreranno le seguenti informazioni sulla rete:

1.  indirizzo ip da usare per la propria periferica (spesso le piccole reti usano gli indirizzi del tipo 192.168.1.2 e si userà questo)
2.  indirizzo del gateway, ovvero il cancello che permetterà di uscire dal proprio nido nel turbinio del web (spesso il router ha come indirizzo gateway 192.168.1.1 e si userà questo)
      
    Per sapere queste cose consultare il manuale oppure la pagina di configurazione del proprio router.

3.  la chiave wpa o wep se la propria rete è criptata (supponiamo che sia wpa e la chiave sia "speriamochecelafaccio")

se queste ipotesi e il possesso di queste informazioni non sono verificate è inutile continuare a leggere.

### Fermare i servizi

Bisogna prestare la massima attenzione al fatto che non ci siano servizi o demoni che possano interferire con i comandi.
Quindi si suggerisce di mettere a terra tutti quei servizi che possano dare fastidio o interferire durante il proprio lavoro:

`# service NetworkManager stop`
`# service NetworkManagerDispatcher stop`
`# service wpa_supplicant stop`
`# service wifi-radar stop`

e quant'altro si è installato tentando la fortuna.
Anzi li renderei non avviabili al boot in maniera predefinita e resetterei il sistema, questa cosa la si può fare tranquillamente da interfaccia grafica - sistema -&gt; amministrazione -&gt; servizi -&gt; eliminare la spunta sui servizi menzionati, salvare e riavviare la macchina, naturalmente poi si dovrà replicare il caricamento del modulo ([capitolo precedente](#INSTALLARE_IL_MODULO "wikilink")).

### Cominciamo

I comandi fondamentali che si andranno ad usare sono:

1.  ifconfig
2.  iwconfig
3.  iwlist
4.  iwpriv
5.  route

e le loro innumerevoli opzioni.

Si comincia con:

`#iwlist pw0 scanning`

che produrrà un output del tipo:

`pw0      Scan completed :`
`          Cell 01 - Address: 00:13:5G:53:D6:00`
`                    ESSID:"la_nostra_wifi"`
`                    Protocol:IEEE 802.11bg`
`                    Mode:Master`
`                    Frequency:2.437 GHz (Channel 6)`
`                    Encryption key:on`
`                    Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s; 6 Mb/s`
`                              12 Mb/s; 24 Mb/s; 36 Mb/s`
`                    Quality:77  Signal level:0  Noise level:0`
`                    IE: WPA Version 1`
`                        Group Cipher : TKIP`
`                        Pairwise Ciphers (2) : TKIP CCMP`
`                        Authentication Suites (1) : PSK`

La cosa che si può dire ora è che la scheda funziona e il modulo per il momento fa il suo dovere.
Copiasi da qualche parte questo output e tenerselo a portata di mano.
Dalla lettura dello stesso si deduce:

1.  il mac-address dell'access-point - Address: 00:13:5G:53:D6:00
2.  il nome della nostra rete - ESSID:"la\_nostra\_wifi"
3.  il protocollo - IEEE 802.11bg
4.  la criptazione wpa è attiva e il tipo della stessa cioè tkip-psk

Copiasi queste informazioni da qualche parte e procedere.

L'output potrebbe essere più lungo nel caso ci siano altre reti wifi nelle vicinanze, fare attenzione a selezionare la propria, si commetterebbe un illecito ad effettuare un collegamento ad una rete se non siete autorizzati (di solito punisco, in maniera assai dura, chi tenta una connessione alla mia rete wifi, e voi non sapete dove mi trovo, quindi...fare attenzione).

### Esplorare il proprio modulo

Dare, ora, il comando:

`# iwpriv pw0 --all`

l'output di quest'ultimo dovrebbe dire quali comandi "privati" accetta il modulo pp14wf, il sistema potrebbe rispondervi:

`pw0      Available read-only private ioctl :`
`pw0      get_power:Power save level: 6 (Off)`
`pw0      get_preamble:auto (0)`
`pw0      get_crc_check:CRC checked (1)`

ciò significa che il modulo non accetta parametri in ingresso ma solo in lettura ( read-only ) , ovvero è in grado di dare informazioni sul suo funzionamento.
Se invece si legge anche la parola "set" vuol dire allora che il modulo accetta parametri che possono essere definiti dall'utente.
In quest'ultimo caso, fermasi, occorre assolutamente conoscere quali parametri possono essere settati e quale è la sintassi corretta.
Di solito, l'output dice solo quanti sono i comandi in questione e una descrizione molto sommaria di essi, del resto poco utilizzabile.
Dare i seguenti comandi:

`# updatedb`

questo serve per aggiornare il database dei files presenti sul proprio filesystem, attendere la fine dell'operazione, poi dare:

`# locate pw0`

dalla lista di output dei files potrebbe saltar fuori un qualche file di documentazione del modulo (doc), essi di solito si trovano in /usr/share/doc.
Se si hanno i sorgenti del kernel montati sul proprio sistema, che vengono sistemati in una directory del tipo /usr/src/kernels/2.6.\*\*\*\*, potrebbe essere una buona idea andare a guardare i file sorgenti del proprio modulo pp14wf.
Anche se non si conosce il C, si troveranno nel file di nostro interesse i commenti degli sviluppatori e certe volte sono così chiari che si avranno tutte le informazioni che si necessitano.
Se l'output non segnala nulla di interessante allora bisogna usare [www.google.it/linux](http://www.google.it/linux), inserire nella ricerca il nome del modulo pp14wf e il comando iwpriv.
Google risponderà sicuramente con qualcosa di utile, selezionare le informazioni da siti di tipo "istituzionali" se non si trova nulla, guardare anche i forum, fermarsi se si incontra qualcosa del genere:

`iwpriv pw0 set AuthMode=WPAPSK`
`iwpriv pw0 set EncrypType=TKIP`
`iwpriv pw0 set WPAPSK="mypasskey"`

sono i comandi che si stavano cercando.

Fare una ricerca approfondita, cercare di sapere con certezza quanti, quali e che tipo di sintassi hanno questi comandi iwpriv, se l'esistenza di qualche comando di questo genere sfugge, non si potrà, probabilmente, configurare adeguatamente la propria wifi.
Fare attenzione che schede e/o moduli diversi, anche se apparentemente similari, potrebbero avere comandi iwpriv completamente differenti.
In taluni casi ci si potrebbe trovare di fronte comandi iwpriv con parametri esadecimali.

Ora bisogna cercare un'altra informazione e cioè bisogna capire se i comandi iwpriv sono sufficienti al modulo per gestire la criptazione oppure no.
Ci sono moduli che riescono a gestirla senza dover usare un servizio particolare chiamato wpa\_supplicant altri, anche usando i comandi iwpriv, ne hanno bisogno.
Appurare questo fatto e quando si è in possesso di questa informazione passare al [punto successivo](#Configurare_il_servizio_wpa_supplicant "wikilink") se si è saputo che il modulo per gestire la criptazione ha bisogno di wpa\_supplicant, saltate al punto [Finalmente](#Finalmente "wikilink") se non ne ha bisogno.
Vale sempre la regola di controllare le date delle informazioni, un modulo ultima versione potrebbe non avere bisogno di wpa\_supplicant, mentre la versione precedente si, quindi, fare attenzione.

### Configurare il servizio wpa\_supplicant

Dare il seguente comando

`# gedit /etc/wpa_supplicant.conf`

si aprirà un editor di testo che permetterà di scrivere il file di configurazione di wpa\_supplicant.
Inserire le seguenti linee:

`network={`
`ssid="la_nostra_wifi"`
`psk="speriamochecelafaccio"`
`key_mgmt=WPA-PSK`
`proto=WPA`
`pairwise=CCMP TKIP`
`}`

salvare e chiudere il file.

### Finalmente

Ora che tutto è a disposizione, si è pronti al grande passo, dare i seguenti comandi:

`# ifconfig pw0 down                ( disattivare il proprio dispositivo per sicurezza)`
`# iwconfig pw0 essid "la_nostra_wifi"      ( dichiarare a quale rete si intende connettersi)`
`# iwconfig pw0 mode Managed            ( stabilire con quale tipo di connessione )`
`# iwconfig pw0 ap 00:13:5G:53:D6:00        ( indicare l'indirizzo fisico del proprio access point)`

naturalmente bisogna sostituire i parametri corretti del proprio sistema.

Ora per abilitare il traffico criptato bisogna aver trovato nelle ricerche precedenti tre possibilità in alternativa tra loro:

1.  Il proprio modulo pp14wf è autosufficiente e gestisce la criptazione direttamente con il comando iwconfig, in questo caso date i seguenti:
2.  wpa\_passphrase la\_nostra\_wifi speriamochecelafaccio

il sistema risponderà con queste stringhe:

`network={`
`        ssid="la_nostra_wifi"`
`        #psk="speriamochecelafaccio"`
`        psk=5ee6feba943837827347kfj9dfjd33dd532c6ae54c4c57e63955d4535771fcb1673e`
`}`

prendere questa lunga stringa esadecimale 5ee6feba943837827347kfj9dfjd33dd532c6ae54c4c57e63955d4535771fcb1673e, che non è niente altro che la propria password "speriamochecelafaccio" criptata e sostituirla alla parola "chiave" del comando successivo:

`# iwconfig  pw0 key chiave             (impostare la chiave wpa)`
`# ifconfig pw0 192.168.1.2 netmask 255.255.255.0 up    ( attivare il dispositivo indicando ip e netmask )`

<li>
Il vostro modulo pp14wf gestisce la criptazione con i comandi iwpriv , in questo caso date quelli che avete trovato nelle ricerche precedenti, ad esempio:

</li>
`# iwpriv pw0 set AuthMode=WPAPSK`
`# iwpriv pw0 set EncrypType=TKIP`
`# iwpriv pw0 set WPAPSK="speriamochecelafaccio"`
`# ifconfig pw0 192.168.1.2 netmask 255.255.255.0 up    ( attiviamo il dispositivo indicando ip e netmask )`

<li>
Il vostro modulo pp14wf gestisce la criptazione con l'ausilio del servizio wpa\_supplicant, in questo caso

</li>
`# ifconfig pw0 192.168.1.2 netmask 255.255.255.0 up            ( attiviamo il dispositivo indicando ip e netmask )`
`# wpa_supplicant -Dwext -ipw0 -c/etc/wpa_supplicant.conf -dd -B        (lanciamo il servizio)`

dove:
il codice wext è per un modulo generico, potrebbe essere necessario verificare se è obbligatorio utilizzare per il nostro modulo un codice specifico.
il codice pw0 è l'alias della nostra interfaccia
il percorso /etc/wpa\_supplicant.conf è il file di configurazione del servizio, controllate che il percorso sia esatto
il codice -dd -B sono opzioni che lanciano il servizio come demone in background.

Dare ora il comando:

`# route add default gw 192.168.1.1 dev pw0`

che indica alla periferica l'instradamento al gateway predefinito.

Dare i seguenti comandi:

`# ifconfig`
`# iwconfig`

si avrà nell'ordine i seguenti output:

Per ifconfig

`eth0      Link encap:Ethernet  HWaddr 00:13:8F:F3:37:4E  `
`          inet addr:192.168.1.65  Bcast:192.168.1.255  Mask:255.255.255.0`
`          inet6 addr: fe80::213:8fff:fef3:374e/64 Scope:Link`
`          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1`
`          RX packets:20549 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:15213 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:1000 `
`          RX bytes:26450306 (25.2 MiB)  TX bytes:1144627 (1.0 MiB)`
`          Interrupt:17 Base address:0x2000 `
`lo        Link encap:Local Loopback  `
`          inet addr:127.0.0.1  Mask:255.0.0.0`
`          inet6 addr: ::1/128 Scope:Host`
`          UP LOOPBACK RUNNING  MTU:16436  Metric:1`
`          RX packets:5568 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:5568 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:0 `
`          RX bytes:2754748 (2.6 MiB)  TX bytes:2754748 (2.6 MiB)`
`pw0       Link encap:Ethernet  HWaddr 00:1A:70:A5:79:77  `
`          inet addr:192.168.1.2  Bcast:192.168.1.255  Mask:255.255.255.0`
`          inet6 addr: fe80::21a:70ff:fea5:7977/64 Scope:Link`
`          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1`
`          RX packets:0 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:1000 `
`          RX bytes:661468 (645.9 KiB)  TX bytes:294138 (287.2 KiB)`
`          Interrupt:11`

controllare che l'inet addr di pw0, cioè l'ip, sia quello giusto

Per iwconfig

`lo        no wireless extensions.`
`eth0      no wireless extensions.`
`pw0       PP14WF Wireless  ESSID:"la_nostra_wifi"  Nickname:""`
`          Mode:Managed  Frequency:2.462 GHz  Access Point: 00:13:5G:53:D6:00   `
`          Bit Rate=54 Mb/s   `
`          RTS thr:off   Fragment thr:off`
`          Encryption key:1172-AFCA-3811-6455-1B09-6283-EE5E-A5D4   Security mode:open`
`          Link Quality=82/100  Signal level:-51 dBm  Noise level:-79 dBm`
`          Rx invalid nwid:  Rx invalid crypt:0  Rx invalid frag:0`
`          Tx excessive retries:0  Invalid misc:0   Missed beacon:0`

controllare nell'ordine che:

1.  il primo codice corrisponda al modulo pp14wf, ciò significa che il modulo è associato alla periferica.
      
    A volte il proprio modulo dipende da altri e potrebbe, invece di essere presente pp14wf, esserci uno di quelli presenti nell'output di lsmod|grep pp14wf .

    Se non c'è nulla oppure c'è scritto "unassociated", bisogna controllare di nuovo il caricamento del modulo, qualcosa non è andato per il verso giusto.

2.  l'essid corrisponda alla propria wifi, questo significa che è stata selezionata la propria rete
3.  l'access point sia quello giusto, ciò significa che il dispositivo ha "agganciato" l'access point. Se non c'è l'indirizzo, controllare di aver dato quello giusto.
4.  Encryption key non sia né off né una sequenza di zeri, in questo caso la criptazione non è corretta cioè si è sbagliato qualcosa nella determinazione del metodo e dei comandi di criptazione del traffico.
5.  il link quality, cioè la qualità del collegamento, sia alto.
      
    Se è basso o addirittura zero, allora o ci si trova a grande distanza dall'access point oppure si può pensare che il modulo che si è montato non è quello corretto.

6.  il noise, cioè il rumore rispetto al segnale sia più basso

se i punti su menzionati non sono realizzati, il collegamento non verrà stabilito.
A volte è necessario indicare anche altri parametri mediante iwconfig, ad esempio utilizzando l'opzione **channel** per specificare il canale oppure **modu** per indicare il tipo di protocollo 802.11a/b/g da utilizzare.

</ol>
Se qualcosa non corrisponde è inutile andare avanti ripercorrere i passi eseguiti e cercare di capire dove si è sbagliato.
Se tutto è in ordine si può provare a dare un:

`# ping -I pw0 192.168.1.1 -c 10`

se il sistema risponde in questo modo

`64 bytes from 192.168.1.1: icmp_seq=1 ttl=255 time=3.62 ms`
`64 bytes from 192.168.1.1: icmp_seq=2 ttl=255 time=0.791 ms`
`64 bytes from 192.168.1.1: icmp_seq=3 ttl=255 time=0.793 ms`
`64 bytes from 192.168.1.1: icmp_seq=4 ttl=255 time=0.793 ms`
`64 bytes from 192.168.1.1: icmp_seq=5 ttl=255 time=0.793 ms`
`64 bytes from 192.168.1.1: icmp_seq=6 ttl=255 time=0.697 ms`
`64 bytes from 192.168.1.1: icmp_seq=7 ttl=255 time=0.783 ms`
`64 bytes from 192.168.1.1: icmp_seq=8 ttl=255 time=0.786 ms`

allora la connessione con il proprio router wifi funziona correttamente.
Se il ping risponde in maniera diversa c'è qualche inesattezza sulla configurazione di rete , probabilmente o negli indirizzi o nell'instradamento, ed è inutile andare avanti, ripercorrere i passi eseguiti e cercare di capire dove si è sbagliato.
Prima di ritornare ai passi precedenti, fare una operazione molto semplice:
Appuntasi i comandi che sono necessari, spegnere il sistema, riaccendere, ridare i comandi, attendere almeno 60 secondi, provare a pingare.
A volte si sono dati, senza ricordarsene, dei comandi che hanno "sporcato" la configurazione, la procedura suggerita restituisce un sistema "pulito".

Se invece il ping è in ordine, provare a dare un:

`# ping -I pw0 www.google.it -c 10`

se la risposta è simile alla precedente allora si può stare tranquilli, altrimenti bisogna intervenire sul file /etc/resolv.conf in questo modo:

`# gedit /etc/resolv.conf`

ed inserire la/le linee:

`nameserver xxx.xxx.xxx.xxx`

dove xxx.xxx.xxx.xxx è l'indirizzo ip del DNS (domain name server), quasi sempre i router hanno anche il servizio DNS e quindi è sufficiente inserire 192.168.1.1 altrimenti bisogna usare i DNS del proprio provider.

Se si vuole provare in maniera completa la scheda, mettere a terra la eth0:

`# ifdown eth0`

aprire il proprio browser preferito e controllare che la navigazione sia corretta.

Ora si è sicuri che la propria scheda funzioni perfettamente.

Se si vuole far ripartire la eth0:

`# ifup eth0`

### Rendere le modifiche permanenti

Il metodo più efficiente ed elegante è quello di creare il file /etc/sysconfig/network-scripts/ifcfg-pw0, e su questo lascio al gusto di scoprire come si fa.
Il metodo più veloce da implementare, ma meno elegante, è questo:
Aprire il file:

`# gedit /etc/rc.local`

inserire in esso tutti i comandi che hanno permesso di configurare la propria wifi (senza il cancelletto \#), salvare e chiudere.
Ora il sistema allo startup configurerà in automatico la rete wireless.
Non dimenticare, eventualmente, di rendere non attivabile al boot la eth0, cosa che si può fare tranquillamente da interfaccia grafica.

Suggerimenti di carattere generale
----------------------------------

-   Fare uso di [www.google.it/linux](http://www.google.it/linux) per individuare le informazioni mancanti o insufficienti.
-   Nel momento in cui sorge una problematica e non si riesce a risolvere, si può chiedere aiuto nel forum.
      
    Fatelo con chiarezza, indicando con dovizia di particolari, cosa si intende fare, cosa si sta utilizzando, quale hardware si sta attivando, quale modulo si sta installando e quant'altro possa essere utile, riportando eventualmente i messaggi di errore che il sistema comunica.

-   Non siate parsimoniosi nelle informazioni, siate invece specifici, precisi, diretti.
-   Se volete una risposta risolutiva, ponete un quesito esaustivo.

Appendice A
-----------

Come iniettare un modulo nel kernel
-----------------------------------

### Usare Yum

Il modulo pp14wf potrebbe essere presente sui repository della nostra distribuzione, pertanto invito a configurarli mediante le guide presenti sul sito, come ad esempio per fedora 8: [<http://www.fedoraonline.it/modules/smartsection/item.php?itemid=138>](http://www.fedoraonline.it/modules/smartsection/item.php?itemid=138). Evitare repository "esotici" o poco noti, potrebbero installare moduli non perfettamente testati o addirittura non funzionanti, rendendo il sistema instabile.

Si consiglia caldamente di utilizzare solo quelli proposti.
Dare il seguente comando:

`# yum --enablerepo=nome_del_repository list *pp14wf*`

inserendo via via i nomi dei vari repository che si sono configurati.
Se ad un certo punto yum segnalerà di aver trovato qualcosa controllare con:

`# yum --enablerepo=nome_del_repository info *pp14wf*`

se è quello che si sta cercando.
Individuato il pacchetto, supponiamo sia ad esempio: pp14wk-kmod.i386, allora lo installarlo:

`# yum --enablerepo=nome_del_repository install pp14wk-kmod`

Fare attenzione che a volte è necessario, oltre ad installare il pacchetto relativo al modulo, installare firmware e/o moduli kernel aggiuntivi, fare una ricerca approfondita sulla questione.
Se si hanno difficoltà con yum si può usare la sua interfaccia grafica yumex, si può installare quest'ultimo con:

`# yum install yumex`

si troverà l'applicazione nel menù degli strumenti di sistema, il cui utilizzo è molto intuitivo.

Una volta iniettato il modulo nel kernel andare [qui](#Come_verificare_che_il_modulo_sia_presente_nel_nostro_kernel "wikilink").

### Installare i moduli da sorgente

Se la ricerca con yum non ha dato i suoi frutti, allora occorre iniettare il modulo mediante una compilazione.
La cosa più difficile è individuare il progetto della comunità che se ne occupa, faccio un esempio:
Per i chip Ralink il progetto di riferimento è:[<http://rt2x00.serialmonkey.com/wiki/index.php?title=Main_Page>](http://rt2x00.serialmonkey.com/wiki/index.php?title=Main_Page) al cui interno si troveranno un gran numero di pacchetti tar, ognuno riferito ad un particolare chip.
Scegliere con cura e solo dopo esserne sicuri, scaricare il pacchetto di vostro interesse.
Non andare a casaccio si perderebbe solo del tempo.
Scompattare, anche da interfaccia grafica, spostasi nella directory creata dalla scompattazione ( cd /home/utente/percorso ) e cosa ASSOLUTAMENTE necessaria **leggere la documentazione**.
Di solito i comandi che permettono di iniettare il modulo sono:

`$ ./configure`
`$ make`
`# make install`

Se si hanno segnalazioni di errore durante questa procedura i motivi possono essere molteplici.
Possono mancare librerie indispensabili, il pacchetto non può essere compilato con il compilatore in possesso ma con un altro di diversa versione, il pacchetto è indirizzato ad un'altra distribuzione o architettura, o altri cento motivi.
Se questa eventualità si presenta, chiedere un aiuto specifico alla comunità indicando con chiarezza il problema.
Se tutto prosegue senza intoppi, si dovrebbe dare sicuramente un :

`# depmod -a`

per ricostruire le dipendenze dei moduli, per questo problema fare comunque riferimento alla documentazione del modulo.
Se tutto è a posto andare [qui](#Come_verificare_che_il_modulo_sia_presente_nel_nostro_kernel "wikilink").

Appendice B
-----------

### Come utilizzare moduli kernel non specifici

Per il momento rimando alle guide del sito relative a ndiswrapper, madwifi, etc.. si integrerà successivamente questa sezione.

<Categoria:Hardware> <Categoria:Wi-Fi>
