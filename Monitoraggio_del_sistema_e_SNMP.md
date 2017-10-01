Introduzione
------------

In questa guida vedremo come tenere sotto controllo le risorse del nostro sistema, sia con gli strumenti di cui Fedora (e linux in generale) dispone di default, ma anche con un tool aggiuntivo "graficamente" più accattivante!

Controllo dei processi
----------------------

### Utilizzo di ps

Il comando **ps** ci da la possibilità di visualizzare informazioni riguardanti i processi in esecuzione. Questo comando produce in output una lista statica, ovvero un elenco dei processi in esecuzione nel momento in cui lanciamo il comando. Mentre invece se vogliamo che il nostro output sia una lista costantemente aggiornata di processi dobbiamo affidarci al comando **top**, che vedremo tra poco. Il modo più comune di utilizzare il comando ps è con le opzioni **ax**:

`[draven@copernico ~]$ ps -ax`

Il comando con queste opzioni ci rilascia le seguenti informazioni:

-   L’elenco dei processi in esecuzione sul sistema, inclusi quelli generati da altri utenti;
-   L’id di ogni singolo processo (PID);
-   Il terminale associato ad ogni singolo processo (TTY);
-   Lo stato di ogni singolo processo (STAT);
-   Da quanto tempo ogni singolo processo sta usando la CPU (TIME);
-   Il nome del file eseguibile che genera ogni singolo processo (COMMAND).

`  PID TTY      STAT   TIME COMMAND`
`    1 ?        Ss     0:04 /usr/lib/systemd/systemd --switched-root --system --deserialize 19`
`    2 ?        S      0:00 [kthreadd]`
`    3 ?        S      0:01 [ksoftirqd/0]`
`    5 ?        S<     0:00 [kworker/0:0H]`
`    7 ?        S      0:00 [rcu_sched]`
`    8 ?        S      0:00 [rcuos/0]`
`    9 ?        S      0:00 [rcu_bh]`
`   10 ?        S      0:00 [rcuob/0]`
`   11 ?        S      0:00 [migration/0]`
`   12 ?        S      0:00 [watchdog/0]`
`   13 ?        S<     0:00 [khelper]`
`   14 ?        S      0:00 [kdevtmpfs]`
`   15 ?        S<     0:00 [netns]`

L’aggiunta dell’opzione u (ps –aux) al comando ps ci rilascia in output lo stesso elenco di processi ma con informazioni più dettagliate:

-   Tutte le informazioni rilasciate dalle opzioni –ax;
-   L’username dell’utente che ha generato il processo (USER);
-   La percentuale di cpu e memoria utilizzati da ogni singolo processo (%CPU e %MEM);
-   La memoria virtuale utilizzata espressa in kilobyte (VSZ);
-   La memoria fisica utilizzata espressa in kilobyte (RSS);
-   La data o l’ora in cui il processo si è avviato.

`[draven@copernico ~]$ ps -aux`
`USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND`
`root         1  0.0  0.5  26776  5760 ?        Ss   12:28   0:04 /usr/lib/systemd/systemd --switched-root --system --deserialize 19`
`root         2  0.0  0.0      0     0 ?        S    12:28   0:00 [kthreadd]`
`root         3  0.0  0.0      0     0 ?        S    12:28   0:01 [ksoftirqd/0]`
`root         5  0.0  0.0      0     0 ?        S<   12:28   0:00 [kworker/0:0H]`
`root         7  0.0  0.0      0     0 ?        S    12:28   0:00 [rcu_sched]`
`root         8  0.0  0.0      0     0 ?        S    12:28   0:00 [rcuos/0]`
`root         9  0.0  0.0      0     0 ?        S    12:28   0:00 [rcu_bh]`
`root        10  0.0  0.0      0     0 ?        S    12:28   0:00 [rcuob/0]`
`root        11  0.0  0.0      0     0 ?        S    12:28   0:00 [migration/0]`
`root        12  0.0  0.0      0     0 ?        S    12:28   0:00 [watchdog/0]`
`root        13  0.0  0.0      0     0 ?        S<   12:28   0:00 [khelper]`
`root        14  0.0  0.0      0     0 ?        S    12:28   0:00 [kdevtmpfs]`
`root        15  0.0  0.0      0     0 ?        S<   12:28   0:00 [netns]`

Possiamo anche utilizzare il comando ps in combinazione con grep per controllare se è in esecuzione un determinato processo:

`[draven@copernico ~]$ ps -ax | grep sshd`

### Utilizzo di top

Volendo avere in output una lista che sia, diciamo così, real time, dovremmo avvalerci del comando top. Questo comando però oltre a restituire l’elenco dei processi, ci da anche informazioni riguardanti il sistema in generale: l’uptime, l’utilizzo della cpu e della memoria, il numero totale dei processi in esecuzione, ecc.

`[draven@copernico ~]$ top`
`top - 14:14:37 up  1:45,  3 users,  load average: 0,00, 0,07, 0,15`
`Tasks: 180 total,   1 running, 179 sleeping,   0 stopped,   0 zombie`
`%Cpu(s):  0,0 us,  0,3 sy,  0,0 ni, 99,7 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st`
`KiB Mem :  1026312 total,    32820 free,   606760 used,   386732 buff/cache`
`KiB Swap:   839676 total,   752164 free,    87512 used.   380068 avail Mem`
`  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND`
` 3829 root      20   0       0      0      0 S  0,3  0,0   0:00.31 kworker/0:0`
` 4898 draven    20   0   15712   3952   2952 S  0,3  0,4   0:00.10 sshd`
`    1 root      20   0   26776   5760   2812 S  0,0  0,6   0:04.86 systemd`
`    2 root      20   0       0      0      0 S  0,0  0,0   0:00.00 kthreadd`
`    3 root      20   0       0      0      0 S  0,0  0,0   0:01.40 ksoftirqd/0`
`    5 root       0 -20       0      0      0 S  0,0  0,0   0:00.00 kworker/0:0H`
`    7 root      20   0       0      0      0 S  0,0  0,0   0:00.94 rcu_sched`
`    8 root      20   0       0      0      0 S  0,0  0,0   0:00.47 rcuos/0`
`    9 root      20   0       0      0      0 S  0,0  0,0   0:00.00 rcu_bh`
`   10 root      20   0       0      0      0 S  0,0  0,0   0:00.00 rcuob/0`
`   11 root      rt   0       0      0      0 S  0,0  0,0   0:00.00 migration/0`
`   12 root      rt   0       0      0      0 S  0,0  0,0   0:00.04 watchdog/0`
`   13 root       0 -20       0      0      0 S  0,0  0,0   0:00.00 khelper`
`   14 root      20   0       0      0      0 S  0,0  0,0   0:00.00 kdevtmpfs`
`   15 root       0 -20       0      0      0 S  0,0  0,0   0:00.00 netns`

Controllo della memoria
-----------------------

Per controllare lo stato della memoria utilizziamo il comando **free**, che ci dà i valori di ram utilizzata e libera. Questo comando visualizza informazioni riguardanti sia la memoria fisica che la swap.

`[draven@copernico ~]$ free`
`              total        used        free      shared  buff/cache   available`
`Mem:        1026312      604108       35344        1944      386860      382768`
`Swap:        839676       87444      752232`

I valori numerici riportati sono kilobytes, per una visualizzazione più vicina all'utente potremmo usare il comando free con l'attributo **-m** che ci darà le stesse informazioni ma espresse in megabytes.

Controllo dell'hard disk
------------------------

Per controllare il nostro hard disk possiamo farci aiutare da due comandi, **df** e **du**. Il comando **df** visualizza le informazioni riguardanti lo spazio utilizzato sull'hard disk di sistema:

`[draven@copernico ~]$ df`
`File system                       1K-blocchi   Usati Disponib. Uso% Montato su`
`/dev/mapper/fedora_copernico-root    6751000 4439500   1945524  70% /`
`devtmpfs                              503844       0    503844   0% /dev`
`tmpfs                                 513156     252    512904   1% /dev/shm`
`tmpfs                                 513156     692    512464   1% /run`
`tmpfs                                 513156       0    513156   0% /sys/fs/cgroup`
`tmpfs                                 513156      96    513060   1% /tmp`
`/dev/sda1                             487652   96691    361265  22% /boot`
`tmpfs                                 102632      28    102604   1% /run/user/1000`

Il dettaglio di queste informazioni si riferisce a:

-   File System
-   1K-blocchi = grandezza della partizione
-   Usati = quanto spazio è utilizzato
-   Disponib. = quanto spazio è ancora utilizzabile
-   Uso% = spazio utilizzato in percentuale
-   Montato su = punto di mount del file system

Anche in questo caso (come per la memoria) le grandezze sono espresse in blocchi da 1 kilobyte, per renderne più semplice la lettura possiamo utilizzare il comando df con l'opzione **-h**.

Il comando **du**, digitato all'interno di una directory, ci fornisce un report con l'elenco dei file contenuti all'interno della directory dove ci troviamo e, soprattutto, la dimensione di ogni singolo file. Anche per il comando du, come per df, possiamo utilizzare l'opzione **-h**.
Oltre a questa però, abbiamo un'altra opzione interessante, ovvero **-s**. Con quest'ultima, verrà omesso l'elenco dei file e verrà restituito solo il valore totale delle dimensioni dei file contenuti nella directory.

Informazioni sull'hardware
--------------------------

I comandi che il sistema ci mette a disposizione per ottenere informazioni sull'hardware sono i seguenti:

-   **lspci** = fornisce un elenco di tutti i componenti PCI presenti nel sistema
-   **lspcmcia** = fornisce un elenco di tutti i componenti PCMCIA presenti nel sistema
-   **lsusb** = fornisce informazioni sui bus usb utilizzati e sui device che vi sono collegati
-   **lscpu** = fornisce informazioni riguardanti il processore presente nel sistema (architettura, modello, cache, ecc.)

Monitoraggio con SNMP
---------------------

L**'SNMP**, al secolo **Simple Network Management Protocol**, è un protocollo di rete comunemente utilizzato per il monitoraggio di apparati di rete e di qualsiasi dispositivo che supporta il protocollo stesso. Il più delle volte il protocollo SNMP può essere definito come una tecnologia **client-server**, nel senso che è concepito per funzionare con due componenti: un "**manager**", componente che effettua richieste snmp per ottenere informazioni e un "**managed object**", ovvero il device che deve essere monitorato. Ponendoci però l'obiettivo di monitorare il nostro sistema, nessuno ci vieta di implementare entrambi sullo stesso host, che da ora in poi chiameremo **localhost** (macchina locale, pc o workstation o server che sia).

La prima cosa che faremo sarà quindi installare due tools sulla nostra Fedora, che la renderanno sia un manager che un managed object. I tool sono rispettivamente **MRTG** e **NET-SNMP**. Il primo è un software che si occuperà di effettuare richieste snmp in locale e di generare delle pagine html contenenti dei grafici di andamento; il secondo è un demone che si metterà in ascolto sulla nostra Fedora in attesa di richieste provenienti dal manager (MRTG) tramite protocollo snmp. Installiamo questi tool con il seguente comando (ricordatevi che queste installazioni e configurazioni necessitano di permessi amministratore per poter essere eseguite):

`[draven@copernico ~]# dnf install mrtg net-snmp net-snmp-utils`

Completata l'installazione, per prima cosa avviamo il demone snmp con il seguente comando:

`[draven@copernico ~]# systemctl start snmpd`

(se si vuole avere il servizio attivo ad ogni riavvio della macchina, *ripetere* il comando precedente sostituendo start con **enable**. Per maggiori informazioni si veda [questa](Gnome-Shell#Servizi "wikilink") sezione).

Tra le utils dell'snmp che abbiamo installato c'è **snmpconf**, che ci facilita la configurazione del protocollo tramite una procedura guidata:

`[draven@copernico ~]$ snmpconf`
`The following installed configuration files were found:`
`   1:  ./snmpd.conf`
`   2:  /etc/snmp/snmpd.conf`
`   3:  /etc/snmp/snmptrapd.conf `
`Would you like me to read them in?  Their content will be merged with the`
`output files created by this session.`
`Valid answer examples: "all", "none","3","1,2,5"`
`Read in which (default = all):`

Elenco di seguito la sequenza da digitare per una configurazione minimale all'interno dei menu dell'snmpconf:

-   digitare all
-   digitare 2 (selezionare il file **snmpd.conf**)
-   digitare 1 (selezionare **Access Control Setup**)
-   digitare 3 (selezionare **SNMPv1/SNMPv2c read-only access community name**)
-   digitare **public** (il nome della community snmp)
-   digitare **localhost** (il nome host del managed object)
-   premere invio per non specificare restrizioni
-   digitare **finished** (per uscire dal sottomenu Access Control Setup)
-   digitare **finished** (per uscire dal menu di configurazione)
-   digitare **quit** (per uscire dal tool snmpconf)

A questo punto la nostra Fedora è ufficialmente un managed object, possiamo accertarci di questo grazie al seguente comando:

`[draven@copernico ~]$ snmpwalk -v2c -c public localhost system`

Continuiamo la nostra configurazione concentrandoci sul manager (MRTG), per far lavorare quest'ultimo dobbiamo generare un file di configurazione, tramite il seguente comando:

`[draven@copernico ~]$ cfgmaker –-global 'WorkDir: /var/www/mrtg' –-output /etc/mrtg/mrtg.cfg public@localhost`

Vediamo cosa abbiamo scritto:

-   cfgmaker = richiamiamo il tool dell'MRTG che genera i file di configurazione
-   –global 'WorkDir: /var/www/mrtg' = definiamo una variabile globale WorkDir ovvero diciamo all'MRTG che la sua directory di lavoro per il salvataggio di pagine e files da ora in poi sarà /var/www/mrtg
-   –output /etc/mrtg/mrtg.cfg = definiamo il percorso e il nome del file di configurazione che stiamo creando
-   public@localhost = public è la community snmp che utilizzeremo e con localhost diciamo all'MRTG che dovrà "autointerrogarsi" in locale

------------------------------------------------------------------------

NOTA: *Nelle varie configurazioni abbiamo incontrato due termini che meritano un minimo di spiegazione per i meno esperti, ovvero "public" e "community". Sostanzialmente un insieme di device monitorati da snmp appartengono ad una comunità (community). La comunità non è altro che un identificativo a garanzia di sicurezza, in pratica un managed object risponde solo alle richieste snmp di un manager della stessa comunità. Il termine public deriva dal fatto che, di base, le community possono essere di sola lettura e di lettura/scrittura, dove, di default (possono essere cambiate), viene utilizzato public per le community di sola lettura e private per le community di lettura/scrittura.*

------------------------------------------------------------------------

Il cfgmaker ci ha quindi creato un file di configurazione nel percorso specificato, analizziamo il contenuto di questo file che, sostanzialmente è composto da tre tipi di informazioni:

`# Created by`
`# /bin/cfgmaker --global "WorkDir: /var/www/mrtg" --output /etc/mrtg/mrtg.cfg public@localhost`
`### Global Config Options`
`#  for UNIX`
`# WorkDir: /home/http/mrtg`
`#  or for NT`
`# WorkDir: c:\mrtgdata`
`### Global Defaults`
`#  to get bits instead of bytes and graphs growing to the right`
`Options[_]: growright, bits`
`EnableIPv6: no`
`WorkDir: /var/www/mrtg`

-   La prima parte del file contiene informazioni di carattere globale, con quale comando è stato generato il file, quale è il percorso della WorkDir e una Option da decommentare se vogliamo che i grafici vengano visualizzati da destra verso sinistra e in bits.

`######################################################################`
`# System: copernico`
`# Description: Linux copernico 3.17.4-301.fc21.i686 #1 SMP Thu Nov 27 19:32:52 UTC 2014 i686`
`# Contact: Root `<root@localhost>` (configure /etc/snmp/snmp.local.conf)`
`# Location: Unknown (edit /etc/snmp/snmpd.conf)`
`######################################################################`

-   La seconda parte è completamente commentata perchè puramente informativa e deriva dal fatto che nel momento in cui il cfgmaker crea il file fa una prima richiesta snmp al managed object per sapere: Nome Host, Descrizione, un contatto di riferimento e la location del sistema.

<!-- -->

-   La terza parte (la più importante) è quella relativa a tutto ciò che di quel dato sistema vogliamo monitorare. Di default, nella suddetta prima richiesta snmp, l'mrtg prende informazioni riguardanti solo le interfacce di rete, tra poco vedremo come implementare anche il controllo di cpu e ram. Quindi in un sistema più o meno classico, con una sola scheda di rete, i pezzi di configurazione saranno due, uno per la scheda di rete e uno per l'interfaccia di loopback. Quest'ultimo pezzo lo troveremo interamente commentato, questo perchè il creatore del pacchetto mrtg ha stabilito di default che probabilmente a nessuno interessi monitorare il traffico locale! Ecco come si presenta la configurazione delle interfacce all'interno del file:

![](Configurazionemrtg.png "Configurazionemrtg.png")

Naturalmente tutte le informazioni descrittive possono essere modificate a piacere per rendere migliore il dettaglio della pagina html generata da mrtg. A questo punto riporto di seguito i pezzi di configurazione da aggiungere al file mrtg nel caso in cui vogliamo monitorare anche l'andamento della ram e del processore:

![](Configurazionemrtg2.png "Configurazionemrtg2.png")

Completato il file di configurazione mrtg dobbiamo generare una pagina html index che faccia da collante per le altre pagine html di dettaglio, che invece saranno generate automaticamente da mrtg. Il comando da eseguire per generare la index è il seguente:

`indexmaker -output=/var/www/mrtg/index.html /etc/mrtg/mrtg.cfg`

------------------------------------------------------------------------

NOTA: *Come avrete notato la directory dove stiamo generando le nostre pagine html con i grafici di andamento si trova sotto il percorso /var/www/, dove questo percorso è generalmente utilizzato come directory root di un server web. Ora c'è da dire che le pagine generate da mrtg sono in formato html e quindi non hanno bisogno di essere interpretate da un server web ma possono essere visualizzate localmente con un semplice browser. l'implementazione di un server web ci darebbe la possibilità di puntare ai grafici mrtg anche da altri host della stessa rete, in questo caso tramite l'indirizzo http://ip-fedora/mrtg/index.html. Chiaramente non è questa la guida adatta per dilungarci nell'installazione e la configurazione di un server web.*

------------------------------------------------------------------------

A questo punto non ci resta che far lavorare il nostro mrtg, il comando per avviare mrtg è il seguente:

`[draven@copernico ~]$ env LANG=C /bin/mrtg /etc/mrtg/mrtg.cfg`

Ma se vogliamo automatizzare il processo per fare in modo che ogni x minuti mrtg richieda informazioni al demone snmp, possiamo semplicemente dare in pasto a **cron** la seguente stringa, il comando per editare cron e schedulare un processo è **crontab -e**.

`*/5 * * * * root LANG=C LC_ALL=C /usr/bin/mrtg /etc/mrtg/mrtg.cfg --lock-file /var/lock/mrtg/mrtg_l --confcache-file /var/lib/mrtg/mrtg.ok`

Qui di seguito potete vedere un esempio di grafico generato da mrtg:

![](Esempiomrtg.png "Esempiomrtg.png")

Riferimenti
-----------

-   Pagina ufficiale del progetto [SNMP](http://www.net-snmp.org/);
-   Pagina su [wikipedia](https://it.wikipedia.org/wiki/Simple_Network_Management_Protocol) relativa a SNMP.

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink")
