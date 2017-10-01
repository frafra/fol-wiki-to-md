Introduzione
------------

In questa guida vengono descritte le partizioni di sistema create durante l'installazione, e più in generale vengono fornite notizie di base sul partizionamento e il montaggio di dischi.
Le informazioni qui riportate derivano da ricerche che ho fatto quando mi trovavo a dover risolvere un qualche problema riguardo i dischi, e da risposte ricevute a domande che ho fatto qui sul forum.

Partizionare il disco serve a dividerlo in porzioni separate da usare per scopi diversi.
Con il partizionamento automatico effettuato durante l'installazione di Fedora su una tipica macchina con un singolo hard disk, il disco viene diviso in tre parti: una partizione di boot, una root ( / ) e una di swap.

Esistono tre tipi di partizione: primaria, estesa e logica. Ogni hard disk può avere un massimo di tre partizioni primarie e una estesa, la partizione estesa a sua volta fa da contenitore per un massimo di 12 partizioni logiche.

Inoltre il partizionamento automatico delle ultime versioni di Fedora prepara il disco (o i dischi) avviando una gestione particolare chiamata Logical Volume Manager (LVM), ma in questa guida verrà considerato solo come preparare manualmente le partizioni.

Punti di mount (mount point)
----------------------------

Ogni partizione può avere un suo punto di mount: immaginando che l'hard disk (HD) sia un albero e i dati in esso contenuti siano foglie, il punto di mount indica il punto di innesto di un ramo sull'albero e da lì parte un path (percorso) che arriva fino ai dati.
Una volta "montata", una partizione (o forse sarebbe più esatto dire il file system in essa contenuto) è vista dal sistema come un'estensione dell'HD, come una directory, anche se se si trova fisicamente su un disco diverso da quello di avvio, magari aggiunto in un secondo tempo rispetto alla prima installazione del sistema.

Il punto di mount della partizione di boot (che conterrà i dati necessari alle prime fasi di avvio del sistema) sarà */boot*.
Il punto di mount della partizione che contiene tutti gli altri file di sistema e che conterrà anche i vari file di log, e le applicazioni installate sarà **/** (slash, o radice, root in inglese, ma da non confondere con l'utente root).
La partizione di swap non ha bisogno di un punto di mount.

Dimensione e funzione delle partizioni
--------------------------------------

La partizione di **boot** deve trovarsi fisicamente nei primi settori del disco (deve partire dal settore 1) e basta che sia grande 500Mb: è però consigliabile impostare la boot ad almeno 1Gb per evitare problemi delle ultime versioni di fedora al momento del preupgrade. Conterrà i file necessari alle prime fasi di avvio del sistema.

La partizione di **swap** serve come contenitore temporaneo per dati che il sistema sta utilizzando, ma che non riesce a immagazzinare nella memoria RAM. Sui sistemi più vecchi, con meno di 32 Mb di RAM era consigliabile creare una partizione di swap di dimensioni doppie rispetto alla quantità di RAM, mentre con le macchine attuali, che hanno grandi quantità di RAM è possibile lavorare bene anche con una partizione di swap delle stesse dimensioni della RAM fisica.

La partizione **/** (root), come già accennato, è la partizione "principale" del disco, qui verrà installato il sistema operativo con tutti i suoi file e directory di sistema. Se si decide di non creare altre partizioni, alla partizione **/** può essere assegnato tutto lo spazio rimanente del disco, dopo aver sottratto i 100Mb per /boot e lo spazio di swap. Nell'installazione standard automatizzata di Fedora viene installata all'interno di **/** anche la directory */home*, nella quale verranno archiviati tutti i dati e le impostazioni personali dei vari utenti (Desktop, preferenze dei programmi, ecc.).

Formattazione
-------------

La formattazione prepara il disco per la scrittura dei dati, creando una struttura che servirà a organizzare i file e tener traccia delle loro proprietà e permessi.

In genere le partizioni di */boot* e **/** vengono formattate con il filesystem ext3 la partizione di swap va formattata con li suo filesystem di tipo swap.
I vari tipi di formattazione (ext3, ext2, reiser, FAT e decine di altri tipi) differiscono tra loro per varie caratteristiche e per il modo in cui i dati vengono organizzati e identificati.

E' infine possibile preparare e formattare al momento dell'installazione di Fedora anche altre partizioni per suddividere il disco come più ci fa comodo.
In particolare potrebbe essere utile fare una partizione separata che conterrà tutti i nostri dati, in questo modo, se fosse necessario reinstallare il sistema operativo e riformattare l'hard disk sarà possibile riformattare solo le partizioni di boot, di swap e la radice, senza toccare i file che resteranno sulla partizione separata.
Per il punto di mount della partizione aggiuntiva è possibile scegliere il nome che si vuole (ad es. /dati), alla conclusione dell'installazione /dati sarà a tutti gli effetti una directory (si può capire che è una partizione a sè e non una semplice directory perchè contiene una directory chiamata lost&found creata dal sistema operativo stesso).

Identificazione di hard disk e partizioni
-----------------------------------------

Fedora e molte altre distribuzioni Linux identificano gli HD installati e le partizioni presenti su di essi tramite una sigla formata da lettere e numeri.
Il criterio è il seguente:

-   le prime due lettere indicano il tipo di disco (hd per dischi ide, sd per dischi scsi, sata, e per i pendrive USB),
-   la terza lettera indica il canale su cui il disco è fisicamente collegato alla scheda madre e se si tratta di un disco master o slave,
-   infine un numero indica la partizione (e di conseguenza anche il suo tipo).

Ogni HD installato viene visto dal sistema come un "device" e ha un suo file corrispondente nella directory /dev, per effettuare operazioni su quel disco, bisogna indicarlo al sistema (come argomento di un comando) tramite il suo percorso /dev/hdxx (o /dev/sdxx)

Ad esempio: se un disco è identificato dal sistema come **hda** significa che è un disco ide (hd) e che è il master primario (a) le partizioni su quel disco sono identificate da numeri 1,2,3 per le tre partizioni primarie che può contenere, da 5 in poi per le partizioni logiche all'interno della estesa (che avrebbe il 4).

Un disco slave primario è identificato come **hdb**, un master secondario **hdc**, e uno slave secondario **hdd** (la stessa identificazione vale, oltre che per gli HD anche per lettori/masterizzatori CD e DVD)

Un device sarà, ad esempio, /dev/sda e per montare una penna USB con sopra un'unica partizione sda1 si usa il comado **mount -t auto /dev/sda1 /punto/di/mount**.

Comandi utili
-------------

Un elenco di comandi utili per visualizzare i dischi installati e le loro partizioni, vanno scritti in una finestra di terminale.

### df -h

Fa un elenco dello spazio disponibile su disco riportando le partizioni e la loro percentuale di utilizzo

`Filesystem         Dimens. Usati Disp. Uso% Montato su`
`/dev/hda2              73G   29G   41G  42% /`
`/dev/hda1              99M   15M   80M  16% /boot`
`tmpfs                 315M     0  315M   0% /dev/shm`

### dmesg | grep hd

Cerca tra i messaggi del kernel tutte le righe in cui compare la stringa "hd", utile per sapere come viene identificato ad es. un nuovo disco appena collegato.
Se si cerca un nuovo disco scsi o un nuovo pendrive usare sd invece di hd, come nell'esempio che segue, in cui è stato collegato un pendrive USB (/dev/sda) da 1Gb, che ha sopra una partizione /dev/sda1

`SCSI device sda: 2071808 512-byte hdwr sectors (1061 MB)`
`sda: Write Protect is off`
`sda: Mode Sense: 03 00 00 00`
`sda: assuming drive cache: write through`
`SCSI device sda: 2071808 512-byte hdwr sectors (1061 MB)`
`sda: Write Protect is off`
`sda: Mode Sense: 03 00 00 00`
`sda: assuming drive cache: write through`
` sda: sda1`
`sd 0:0:0:0: Attached scsi removable disk sda`

### fdisk -l

va dato come utente root **/sbin/fdisk -l** riporta l'elenco dei dischi e le loro partizioni.
Indicando un particolare device, verrà riportato l'elenco solo per quello (es. /sbin/fdisk -l /dev/hda riporta le partizioni del solo disco primario)

`Disk /dev/hda: 81.9 GB, 81964302336 bytes`
`255 heads, 63 sectors/track, 9964 cylinders`
`Units = cylinders of 16065 * 512 = 8225280 bytes`
`   Device Boot      Start         End      Blocks   Id  System`
`/dev/hda1   *           1          13      104391   83  Linux`
`/dev/hda2              14        9833    78879150   83  Linux`
`/dev/hda3            9834        9964     1052257+  82  Linux swap / Solaris`

Il comando fdisk serve anche a creare partizioni su un nuovo HD appena installato: una volta identificato il nuovo disco (ad es. hdb, un disco slave sul canale primario) è possibile partizionarlo con fdisk scrivendo da utente root **/sbin/fdisk /dev/hdb** partirà l'interfaccia testuale del comando fdisk, con le istruzioni a video.

### mkfs

Comando per formattare le partizioni con filesystem Linux.
Va dato da utente root.
 Se si vogliono fare prove procurasi un secondo disco o un pendrive, e formattare quello.

Di seguito è riportata la formattazione di un pendrive USB, ma le operazioni sono pressochè le stesse per aggiungere un nuovo HD.

1.  /sbin/fdisk -l /dev/sda

Disk /dev/sda: 1060 MB, 1060765696 bytes

`33 heads, 62 sectors/track, 1012 cylinders`
`Units = cylinders of 2046 * 512 = 1047552 bytes`

`   Device Boot      Start         End      Blocks   Id  System`

Nessuna partizione presente sul pendrive, creiamone una.

<li>
/sbin/fdisk /dev/sda

</li>
`Command (m for help): m                              `**`nota` `(1)`**
`Command action`
`   a   toggle a bootable flag`
`   b   edit bsd disklabel`
`...`
`   m   print this menu`
`   n   add a new partition`
`   o   create a new empty DOS partition table`
`...`
`   v   verify the partition table`
`   w   write table to disk and exit`
`   x   extra functionality (experts only)`
`Command (m for help): n                              `**`nota` `(2)`**
`Command action`
`   e   extended`
`   p   primary partition (1-4)`
`     `**`scelto` `p`**
`Partition number (1-4):                                   `**`scelto` `1`**
`First cylinder (1-1012, default 1):                 `**`premuto` `invio`**
`Using default value 1`
`Last cylinder or +size or +sizeM or +sizeK (1-1012, default 1012):      `**`premuto` `invio`**
`Using default value 1012`

Per uscire da fdisk salvando le modifiche apportate, premere w. Per uscire senza salvare premere q.

<li>
/sbin/mkfs -t ext3 /dev/sda1

</li>
per formattare la partizione appena creata

`mke2fs 1.39 (29-May-2006)`
`Etichetta del filesystem=`
`Tipo SO: Linux`
`Dimensione blocco=4096 (log=2)`
`Dimensione frammento=4096 (log=2)`
`129536 inode, 258811 blocchi`
`12940 blocchi (5.00%) riservati per l'utente root`
`Primo blocco dati=0`
`Maximum filesystem blocks=268435456`
`8 gruppi di blocchi`
`32768 blocchi per gruppo, 32768 frammenti per gruppo`
`16192 inode per gruppo`
`Backup del superblocco salvati nei blocchi: `
`        32768, 98304, 163840, 229376`
`Scrittura delle tavole degli inode: fatto                           `
`Scrittura delle informazioni dei superblocchi e dell'accounting del filesystem: fatto`
`Questo filesystem verrà automaticamente controllato ogni 32 mount, o`
`180 giorni, a seconda di quale venga prima. Usare tune2fs -c o -i per cambiare.`

Il pendrive adesso è formattato, montiamolo.

<li>
mount -t auto /dev/sda1 /usr/Condivisa/media/usb/

</li>
(deve già esistere la directory in cui montarlo, in questo caso /usr/Condivisa/media/usb)

<li>
df -h

</li>
e controlliamo il nuovo "spazio disco" sul nostro sistema

`Filesystem         Dimens. Usati Disp. Uso% Montato su`
`/dev/hda2              73G   29G   41G  42% /`
`/dev/hda1              99M   15M   80M  16% /boot`
`tmpfs                 315M     0  315M   0% /dev/shm`
`/dev/sda1             996M  1,3M  944M   1% /usr/Condivisa/media/usb`

per smontare il pendrive prima di sfilarlo dalla presa USB

`umount /dev/sda1`

### mkdosfs

Comando per formattare le partizioni con filesystem FAT32 di Windows, la cosa curiosa e anche molto utile è che questo comando (diversamente dalla formattazione effettuabile da Windows) permette di formattare anche dischi di dimensioni maggiori di 32Gb senza suddividerli in partizioni più piccole.

### /etc/fstab

fstab è un file di configurazione che si trova nella directory /etc e che riporta le informazioni sui filesystem da montare automaticamente all'avvio, i loro punti di mount e i permessi. E' possibile leggere il contenuto di /etc/fstab con **cat /etc/fstab**.
Una volta aggiunto un nuovo HD, per far si che il sistema lo monti così come fa di solito con l'HD principale, occorre modificare il file /etc/fstab aggiungendo una riga con il device da montare, il punto di mount e alcune opzioni che riguardano i permessi con cui il disco (o la singola partizione) sarà montato.
Suggerimento: /etc/fstab viene letto in fase di avvio del sistema. Se ho appena aggiunto una riga per montare un nuovo disco e non posso o non voglio riavviare, con il comando **mount -a** "forzo" il mount di ciò che si trova in fstab. Se con questo comando il nuovo device non viene montato con le giuste opzioni, allora è necessario riavviare.

Se il device che abbiamo visto nell'esempio precedente fosse il nostro nuovo HD e volessimo farlo montare ad ogni avvio per averlo sempre disponibile dovremmo modificare il file /etc/fstab.

`LABEL=/1                /                       ext3    defaults        1 1`
`LABEL=/Condiviso        /Condiviso              ext3    defaults        1 2`
`LABEL=/boot1            /boot                   ext3    defaults        1 2`
`devpts                  /dev/pts                devpts  gid=5,mode=620  0 0`
`tmpfs                   /dev/shm                tmpfs   defaults        0 0`
`proc                    /proc                   proc    defaults        0 0`
`sysfs                   /sys                    sysfs   defaults        0 0`
`LABEL=SWAP-hda5         swap                    swap    defaults        0 0`

aggiungendo in fondo la riga

`/dev/sda1               /Condiviso/mount/usb    ext3    rw,user         0 0`

Nella prima colonna va il nome del device, nella seconda il punto di mount, nella terza il tipo di filesystem, nella quarta le opzioni di mount (in questo caso rw per permettere lettura e scrittura e user per permettere anche a tutti gli utenti di usarlo. Le ultime due colonne servono a indicare al sistema operativo in che ordine e se eseguire il controllo diagnostico del filesystem.

</ol>
Manuali
-------

Ognuno dei comandi a cui si è accennato ha molte opzioni, per avere a video spiegazioni dettagliate di tutte le opzioni e delle particolarità di ognuno, usare **man nomecomando**, per stamparle leggete la guida [Stampare le pagine man](Stampare_le_pagine_man "wikilink"). Se state usando per la prima volta i comandi da terminale leggete [Primi passi nel terminale](Primi_passi_nel_terminale "wikilink"). Per modificare i file di configurazione come */etc/fstab* è necessario usare un editor di testo, ad esempio **vi**.

<Categoria:Sistema>
