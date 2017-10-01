Alcuni aiuti e suggerimenti di base per chi ha appena iniziato ad usare Linux: editor di testo, installazione di hardware e programmi, problemi col video.

Consigli per neofiti
--------------------

Questa guida si propone di dare alcune informazioni di base utili a chi inizia a utilizzare Linux per la prima volta.
Raccoglie alcuni dei problemi più comuni di cui si è parlato qui nel forum fedoraonline e alcune spiegazioni su come intervenire per risolverli, o almeno iniziare a capire qual è il problema.
Può essere utile leggere oltre a questa guida anche la guida [Primi passi nel terminale](Primi_passi_nel_terminale "wikilink").

Il terminale e l'ambiente grafico
---------------------------------

Sebbene la maggior parte degli utenti utilizzi principalmente l'ambiente grafico quando lavora col proprio computer, Linux è nato con una interfaccia testuale, sempre accessibile anche quando l'ambiente grafico è in funzione, e indispensabile per risolvere situazioni di emergenza. Dalla semplice interfaccia a riga di comando si ha il pieno controllo del sistema. Si può accedere al terminale dall'ambiente grafico stesso tramite un apposito menu, oppure con la combinazione di tasti **ctrl+alt+f1**. ctrl+alt+f7 torna alla modalità grafica. (Inoltre si possono attivare operazioni diverse aprendo diversi terminali con ctrl+alt+f2 +f3 e così via)

L'utente root
-------------

Linux è nato come sistema multiutente, l'utente amministratore, che ha il pieno controllo su tutte le funzioni è chiamato root. Alcuni comandi possono essere dati solo dall'utente root.
Un utente comune può assumere i diritti di root e quindi lanciare i programmi riservati o modificare le impostazioni del sistema con il comando **su** seguito da invio e poi digitando la password di root. Per tornare utente normale si scrive exit e si da invio.
Se scrivendo il nome di un comando (anche come root) appare il messaggio che il comando non esiste, molto probabilmente basterà aggiungere **/sbin/** davanti al nome del comando.
Infine si può diventare utente root con il comando **su -** (su spazio meno) in questo modo si avrà anche il path di root (il percorso in cui il sistema va a cercare i comandi) e non sarà, ad esempio, necessario aggiungere /sbin/ davanti al nome del comando.

I permessi
----------

Essendo nato come sistema multiutente, in Linux è possibile assegnare dei permessi ad ogni utente, in particolare quali file può leggere, modificare (e quindi anche cancellare) o eseguire. Inoltre ogni utente può appartenere a un gruppo di lavoro, e il gruppo, a sua volta potrà avere il permesso di usare alcuni file e non altri.
Per una guida sui permessi vedere qui: [Gestione dei permessi](Gestione_dei_permessi "wikilink")

File di testo
-------------

Praticamente tutte le caratteristiche di un sistema Linux possono essere gestite tramite "semplici" file di configurazione in formato testo.
Se si ha un problema con la propria installazione, spesso basta correggere il giusto file di configurazione e il problema si risolve.

Nano e Vi
---------

Una volta nel terminale, per correggere i propri file di configurazione si ha bisogno di un editor di testo, i due più comuni sono Nano e Vi. Ecco le funzioni minime per poterli utilizzare.

Prima però è bene fare sempre una copia del file che si va a modificare, si può fare con il comando **cp nomefile nomefile.copia**. Se fosse necessario ripristinare la vecchia copia del file che si è modificata, si può cancellare il file modificato con **rm nomefile** e poi fare una copia del file di riserva con **cp nomefile.copia nomefile**

Per arrivare a modificare un file di configurazione può essere necessario spostarsi nella directory in cui il file si trova, per fare questo si scrive **cd /percorso/al/file** (cd sta per change directory). Per tornare nelle directory home scrivere cd e invio.

### Nano

Per aprire un file con nano si scrive **nano nomefile**. Viene mostrato il contenuto del file di testo, si può scorrere con i tasti freccia o con PGSU e PGGIU per arrivare al punto da modificare, scrivere il parametro che serve e poi salvare con **ctrl+o**, dare invio per confermare e quindi sovrascrivere il file originale, e uscire con **ctrl+x**

### Vi

Vi è un po' più complicato, si può usarlo in caso non si avesse nano installato.
Per aprire un file scrivere **vi nomefile**, una volta dentro ci si può spostare con i tasti freccia o PGsu e PGGIU. Per passare al modo inserimento premere la lettera **i** e scrivere ciò che serve, per uscire dal modo inserimento premere **ESC**. Per salvare e uscire scrivere **:wq** e premere invio. Per uscire senza salvare (in caso di errori) scrivere **:q!** e premere invio.

Linux è "case sensitive"
------------------------

Significa che il sistema, nell'interpretare i comandi, tiene conto anche delle maiuscole e minuscole. Se ad esempio voglio spostarmi in una directory chiamata "Musica" devo scrivere **cd Musica**, se scrivo **cd musica** avrò un messaggio di errore che mi avvisa che il percorso indicato non esiste.

Problemi post installazione
---------------------------

Seguono alcuni esempi di temi trattati nel forum.

### Ho bisogno di altri programmi

Dopo l'installazione guidata, che termina con un certo numero di pacchetti standard di programmi, è possibile aggiungere alla propria Fedora tantissimo altro software, per gli usi più vari.
Per fare questo si usano i comandi yum (solo interfaccia testuale) e yumex (funzioni simili ma con interfaccia grafica). Per installare yumex va usato per forza yum la prima volta: con il comando **yum install yumex**.
yum e yumex cercano il software in alcuni siti web appositi, detti repository. Nella sezione guide si troveranno le istruzioni per utilizzare yum e per configurare i repository. yum e yumex possono essere anche usati periodicamente per aggiornare tutto il software installato, ad esempio tramite il comando yum update.

### Lo schermo non si vede o si vede male

Se lo schermo si vede tremolante, distorto, con linee alternate, incompleto, diviso in due o con immagini sdoppiate potrebbe essere un problema di risoluzione. In questi casi va corretto il file xorg.conf (il suo percorso completo /etc/X11/xorg.conf) in cui sono contenuti molti parametri riguardanti l'ambiente grafico, dallo schermo alle periferiche di input come mouse e tastiera.
Il file è organizzato in sezioni che hanno come titolo la caratteristica che regolano.

Ad esempio:

`# Xorg configuration created by system-config-display`
`Section "ServerLayout"`
`   Identifier     "single head configuration"`
`   Screen      0  "Screen0" 0 0`
`   InputDevice    "Keyboard0" "CoreKeyboard"`
`EndSection`
`Section "InputDevice"`
`   Identifier  "Keyboard0"`
`   Driver      "kbd"`
`   Option      "XkbModel" "pc105"`
`   Option      "XkbLayout" "it"`
`EndSection`
`Section "Monitor"`
`   Identifier   "Monitor0"`
`   ModelName    "LCD Panel 1024x768"`
`   HorizSync    31.5 - 48.5`
`   VertRefresh  40.0 - 70.0`
`   Option      "dpms"`
`EndSection`
`Section "Device"`
`   Identifier  "Videocard0"`
`   Driver      "i810"`
`EndSection`
`Section "Screen"`
`   Identifier "Screen0"`
`   Device     "Videocard0"`
`   Monitor    "Monitor0"`
`   DefaultDepth     24`
`   SubSection "Display"`
`       Viewport   0 0`
`       Depth     24`
`       Modes    "800x600" "640x480"`
`   EndSubSection`
`EndSection`

Può succedere che in un sistema appena installato non sia possibile usare l'ambiente grafico per la mancanza dei giusti driver della scheda video. In questo caso si può modificare a mano il file /etc/X11/xorg.conf e nella riga Driver della sezione "Device" inserire tra le virgolette **vesa**: un driver generico che potrebbe permettere comunque di usare l'ambiente a finestre finchè non si trova il driver adatto.
Se il sistema non dovesse riconoscere durante l'installazione la risoluzione del monitor, inoltre, si può intervenire manualmente inserendo la giusta risoluzione nella riga Modes inserendola tra virgolette in prima posizione.

### Fedora si avvia in modalità testo

Se Fedora non riconosce la scheda video all'avvio dell'installazione può darsi che tutta l'installazione avvenga in modalità testuale. A fine installazione potrebbe essere comunque possibile ripristinare l'ambiente grafico modificando xorg.conf ma Fedora continuerà a partire in modalità solo testo. Per impostare come standard l'avvio dell'ambiente grafico si può agire sul file /etc/inittab

Tra le prime righe di inittab (questo è un esempio) si trova:

`....`
`# Default runlevel. The runlevels used by RHS are:`
`#   0 - halt (Do NOT set initdefault to this)`
`#   1 - Single user mode`
`#   2 - Multiuser, without NFS (The same as 3, if you do not have networking)`
`#   3 - Full multiuser mode`
`#   4 - unused`
`#   5 - X11`
`#   6 - reboot (Do NOT set initdefault to this)`
`# `
`id:5:initdefault:`
`....`

**id:5:initdefault:** nel file riportato sopra, indica che la modilità standard di avvio è il runlevel 5 ossia X11, che sarebbe l'ambiente grafico.
In un sistema che parte automaticamente in modo solo testo, questa riga sarà **id:3:initdefault:**
Se so che nel mio sistema è installato un ambiente grafico, perchè l'ho scelto durante l'installazione, ma non parte, allora posso provare a sostituire il 5 al 3 nella riga di inittab.
Per fare la prova e vedere se l'ambiente grafico esiste, prima di modificare la riga posso provare a scrivere **startx** e dare invio, per vedere se parte il modo grafico. Poi posso sempre tornare alla modalità testo con ctrl+alt+F1 per apportare le modifiche. (Utile anche nel caso, possibile, in cui mi ritrovassi con lo schermo nero e il monitor in modalità risparmio energetico, perchè non riceve segnale dalla scheda video.)

### Ho una doppia installazione Fedora/Windows

Chi installa Fedora e Windows sullo stesso disco, potrebbe avere problemi all'avvio nella scelta tra i sue sistemi operativi. In questo caso una soluzione può essere quella di ripristinare il **bootloader** grub e/o la sua configurazione (tramite il file /boot/grub/grub.conf). Il bootloader è un codice che risiede in una particolare zona del disco, viene eseguito nelle prime fasi di avvio e permette il caricamento del resto del sistema.
Per ripristinare e aggiornare grub seguire l'apposita [guida](Reinstallare_Grub "wikilink").

Se si è installato Fedora su un hard disk e si vuole tornare a Windows, bisogna cancellare l'hard disk da Fedora e rimuovere le partizioni Linux, prima che il cd/dvd di installazione di Windows sia in grado di riconoscere il disco di nuovo.
Per fare questo si usa il comando **fdisk**, di cui si parla nella guida dischi e partizioni, le basi.
Ma non si possono riformattare e cancellare gli hard disk da cui si è partiti, quindi bisogna prima avviare da CD o DVD, oppure da una distribuzione live, che funzioni senza hard disk, da quel sistema si può cancellare l'hard disk che si andrò a riutilizzare.

### Ho installato un nuovo hardware, che fare?

Quando si installa del nuovo hardware questo può essere riconosciuto automaticamente da Fedora, oppure può aver bisogno dei giusti driver per essere utilizzato.
I comandi utili quando si ha a che fare con nuovo hardware sono **dmesg** - **/sbin/lspci** - **/sbin/lsusb** - **tail**
Verificando quali messaggi appaiono con questi comandi è possibile sapere se l'hardware è stato riconosciuto senza problemi, se ha bisogno di moduli aggiuntivi per poter funzionare, e quali sono le sue caratteristiche, per cercare eventuali driver messi a punto per Linux.

dmesg
-----

elenca i messaggi del kernel (il nucleo di Linux, che si occupa di comunicare con le periferiche) i messaggi appaiono nell'ordine in cui vengono generati, quindi se collego una penna USB e voglio vedere cosa è sucesso, in genere, scrivendo dmesg basta leggere le ultime righe.

/sbin/lspci e /sbin/lsusb
-------------------------

Servono rispettivamente per elencare le periferiche PCI (le schede aggiuntive interne, ma se già se ne è aggiunta una da soli non si ha bisogno di questa precisazione) e le periferiche USB come webcam, modem, acquisizione video ecc.
Ai comandi /sbin/lspci e /sbin/lsusb possono essere aggiunte delle opzioni per avere un elenco più dettagliato aggiungendo l'opzione -v.
Tra le righe che risultano è importante la coppia di parametri separata dai duepunti. Questa coppia indica il produttore ed è utile per cercare i driver tramite google ad esempio.

Ad esempio dopo aver connesso un adattatore bluetooth su porta USB il comando dmesg restituisce

`...`
`ip_tables: (C) 2000-2006 Netfilter Core Team`
`Netfilter messages via NETLINK v0.30.`
`nf_conntrack version 0.5.0 (1849 buckets, 14792 max)`
`...`
`usb 2-1: new full speed USB device using uhci_hcd and address 2`
`usb 2-1: configuration #1 chosen from 1 choice`
`Bluetooth: Core ver 2.11`
`NET: Registered protocol family 31`
`Bluetooth: HCI device and connection manager initialized`
`Bluetooth: HCI socket layer initialized`
`Bluetooth: HCI USB driver ver 2.9`
**`usbcore:` `registered` `new` `interface` `driver` `hci_usb`**

e il comando /sbin/lsusb

`Bus 002 Device 003: ID `**`0a5c:200a`**` Broadcom Corp. `
`Bus 002 Device 001: ID 0000:0000  `
`Bus 001 Device 001: ID 0000:0000 `

</pre>
</code>

</div>
In questo caso il driver incorporato in Fedora (provato con Fedora7) è sufficiente a utilizzare l'adattatore. In caso non lo fosse stato, cercando i valori 0a5c:200a in google, e cercando un po' tra i risultati si sarebbe potuto arrivare a sapere se esistono i driver o se per caso il nostro hardware proprio non è supportato. I driver potrebbero essere disponibili su qualche sito di sviluppatori, a volte sul sito stesso del produttore (ma in questo caso piuttosto che arrivarci tramite google conviene collegarcisi direttamente e cercare in base al modello del prodotto).
Cosa accade se si inserisce dell'hardware non direttamente supportato.
Inseriamo un adattatore USB per la TV digitale terrestre dmesg riporta:

`usb 2-2: USB disconnect, address 4`
`usb 2-2: new full speed USB device using uhci_hcd and address 5`
`usb 2-2: configuration #1 chosen from 1 choice`
`dvb-usb: found a 'Twinhan USB2.0 DVB-T receiver (TwinhanDTV Alpha/MagicBox II)' in cold state, will try to load a firmware`
`'''vb-usb: did not find the firmware file. (dvb-usb-vp7045-01.fw) '''Please see linux/Documentation/dvb/ for more details on firmware-problems. (-2)`
`dvb_usb_vp7045: probe of 2-2:1.0 failed with error -2`
`usbcore: registered new interface driver dvb_usb_vp7045`

L'ultima riga dice che un driver è stato caricato, ma un messaggio qualche riga più in alto dice che non è stato possibile caricare il firmware, quindi la periferica ancora non può funzionare. Cercando **dvb-usb-vp7045-01.fw** su internet tramite google è possibile scaricare il file giusto e salvandolo in /lib/firmware al prossimo inserimento sarà trovato e l'adattatore potrà essere usato.

Quanto detto sopra vale anche per le altre periferiche USB come modem e webcam.

tail
----

Il comando tail serve a leggere le ultime righe di un file di testo, con l'opzione -f resta "in ascolto" per le modifiche a quel file.
In Fedora il file /var/log/messages registra ciò che accade durante lo svolgimento delle varie operazioni.
Quindi il comando **tail -f /var/log/messages** può essere usato, ad esempio, per osservare cosa succede all'inserimento di una nuova periferica USB. Dalle nuove righe che compaiono sullo schermo al collegamento della periferica si possono avere informazioni utili alla sua installazione.

In questa guida si sono trattate un po' di informazioni di base, che permetteranno di capire alcune cose che nei messaggi del forum a volte vengono date per scontate. Se si ha bisogno di aiuto su un argomento specifico cercare anche nei vecchi messaggi del forum tramite la funzione cerca. Sono già stati trattati molti argomenti e potrebbe esserci anche quello che interessa, e al quale si cerca una risposta il prima possibile.

<Categoria:Sistema>
