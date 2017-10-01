Come preparare un RAID software con due dischi in mirroring

Questa guida descrive come **preparare un RAID software per utilizzare due dischi in mirroring** (ossia in copia continua tra loro) e avere la duplicazione dei dati. In pratica il sistema scriverà i dati sempre sui due dischi contemporaneamente, in caso di rottura di uno, si avrà una copia di riserva e il sistema sarà comunque utilizzabile anche con un solo disco funzionante. La situazione migliore è quella in cui si hanno due Hard Disk identici (stessa capacità, velocità, marca ecc.).

Gli esempi si riferiscono a dei dischi sata (sda e sdb), ma il tutto vale anche per dischi eide, basta sostituire a sda e sdb le sigle hda e hdb.
Tutte le operazioni per la preparazione del RAID andranno fatte al momento dell'installazione di Fedora, cancellando la struttura di partizioni proposta dall'installazione guidata e impostando a mano il RAID.

Per notizie di base su dischi e partizioni, e sull'utilizzo di alcuni comandi per la gestione dei dischi vedere la guida [Dischi e partizioni: le basi](http://doc.fedoraonline.it/Dischi_e_partizioni:_le_basi)

Creazione del set RAID
----------------------

1.  Al momento dell'installazione partizionare manualmente i dischi sda e sdb. (Assicurarsi che la partizione da 100Mb che verrà resa di boot risieda nei primi settori del disco).

Come tipo di filesystem per le partizioni scegliere "RAID software" E' possibile anche creare tutte le partizioni solo su uno dei dischi e poi usare l'opzione "RAID/clona partizioni" per riprodurre la stessa struttura sul secondo disco.

Di seguito è riportata la struttura dei due dischi, con partizioni di identiche dimensioni su entrambi.

`[/dev/sda]`
`/dev/sda1 RAID software 102`
`/dev/sda2 RAID software 30000`
`/dev/sda3 RAID software 1024`
`/dev/sda4 ESTESA 120000`
`/dev/sda5 RAID software 120000`
`[/dev/sdb]`
`/dev/sdb1 RAID software 102`
`/dev/sdb2 RAID software 30000`
`/dev/sdb3 RAID software 1024`
`/dev/sdb4 ESTESA 120000`
`/dev/sdb5 RAID software 120000`

<li>
Accoppiare le partizioni uguali in un **/dev/mdx**, scegliere RAID1, assegnargli un punto di mount e il tipo di filesystem con cui si vuole formattarlo

</li>
Nell'esempio di configurazione riportato di seguito, le due partizioni da 102Mb /dev/sda1 e /dev/sdb1 vengono accoppiate in /dev/md0 e viste dal sistema come una singola. Allo stesso modo le due partizioni da 30Gb (md2) e così via. Per il sistema il disco sarà in pratica uno solo /dev/md suddiviso nella varie partizioni di sistema.

`[Dispositivi RAID]`
`/device /punto_di_mount dimensioni_Mb`
`/dev/md3 /home 120000`
`/dev/md0 /boot 102`
`/dev/md1 swap 1024`
`/dev/md2 / 30000`

<li>
Proseguire normalmente con l'installazione: da adesso i due dischi vengono visti come uno solo e i dati vengono automaticamente duplicati.

</li>
<li>
Lo stato del set RAID

</li>
A fine installazione è possibile controllare lo stato del set RAID con il comando **cat /proc/mdstat** il simbolo \[UU\] indica che entrambe le partizioni del RAID sono funzionanti (UP), il simbolo \[\_U\] o \[U\_\] significa che una delle due non funziona.

</ol>
Sostituzione di un disco
------------------------

Dopo aver sostituito un disco danneggiato, ricreare su di esso la stessa struttura delle partizioni e riassociarle al set RAID.
Le partizioni possono essere ricreate manualmente una per una con **fdisk** oppure clonate dal disco sano con **sfdisk -d /dev/sda | sfdisk /dev/sdb** (\*) (sda è il disco sano con i dati da duplicare, sdb il disco sostituito, naturalmente è di *fondamentale importanza fare attenzione* ad indicare il giusto disco sorgente da clonare).
Per sapere la struttura del disco sano, nel caso fosse necessario ricrearla manualmente con fdisk: (come utente root) **fdisk -l /dev/sda** (fdisk meno elle minuscola).
Con il comado cfdisk (che però NON E' nell'installazione standard di Fedora) è possibile creare partizioni in modalità 'semi-grafica' spostandosi con i testi freccia all'interno di un menu.

Con il comando (da dare come root) **mdadm** è possibile marcare come 'faulty' (difettoso), rimuove e aggiungere partizioni al set RAID.
Una partizione può essere rimossa (*mdadm --remove /dev/md0 /dev/sdb1*) solo se è faulty \[U\_\], per marcarla manualmente come faulty, usare *mdadm --fail /dev/md0 /dev/sdb1*.

Infine:

`mdadm --add /dev/md0 /dev/sdb1`

aggiunge la partizione *sdb1* di un nuovo disco al device *md* di un set RAID esistente e che magari si è danneggiato. Ripetere il comando per tutte le partizioni sostituendo via via le giuste corrispondenze tra le partizioni del deivce md e le partizioni del nuovo disco.

Dopo l'aggiunta della nuova partizione inizia la duplicazione automatica dei dati (E' possibile seguirla con **cat /proc/mdstat** ).
E' possibile aggiungere tutte le partizioni senza attendere che la ricostruzione della prima sia terminata: le partizioni verranno messe in coda (si vede DELAYED con *cat /proc/mdstat*), ma in questo caso *la macchina NON VA RIAVVIATA* finché non è finita la ricostruzione di tutte le partizioni, altrimenti i dati non vengono duplicati.

Se i comandi dati come utente root non funzionano subito (appare un messaggio che dice che il comando non esiste) ridare lo stesso comando facendolo precedere da **/sbin/**

RAID sta per: Redundant Array of Independent Disks (insieme ridondante di dischi indipendenti). Esistono vari 'livelli RAID' a seconda del numero di dischi che compongono un 'set' e del modo in cui i dischi vengono utilizzati. Il tipo 'mirroring' descritto qui è chiamato anche RADI1.

La partizione di swap non contiene dati fondamentali, ma solo dati temporanei usati dal sistema. Nella guida viene messa nel set RAID anche la partizione di swap, ma potrebbe anche essere lasciata fuori, su una partizione non replicata.
Io di solito imposto il RAID nel modo indicato nella guida e non ho mai avuto problemi.

<Categoria:Sistema>
