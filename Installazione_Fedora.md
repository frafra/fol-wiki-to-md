Introduzione
------------

Questa guida si propone di trattare l'installazione della release ***Fedora 20 "Heisenbug"*** su un personal computer utilizzando il metodo di installazione da DVD.
Tutte le versioni di Fedora sono liberamente scaricabili e vengono messe a disposizione dal [FedoraProject](http://fedoraproject.org/it/get-fedora-all). Scaricare la versione DVD.
Per maggiori informazioni su come creare un CD/DVD bootabile, consultare la [documentazione ufficiale del FedoraProject](http://docs.fedoraproject.org/it-IT/Fedora/17/html/Burning_ISO_images_to_disc/index.html).
Per creare invece una Usb bootabile seguire [queste istruzioni](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB/it).

Per illustrare il processo di installazione, è stata utilizzata una macchina virtuale con [Boxes](https://wiki.gnome.org/Boxes).
Inoltre la capacità dei dischi riprodotti nelle immagini è puramente indicativa; gli hard disk attuali permettono un partizionamento personalizzato per qualsiasi utilizzo.

Avvio dell'installazione
------------------------

Per l'installazione occorre inserire il disco ed eseguire il boot da DVD.
L'avvio si presenta simile a quello per l'installazione di Fedora 19.
Il countdown viene interrotto premendo un tasto qualsiasi e le frecce, su e giù, permettono di scorrere tra le tre selezioni principali.

-   *Install Fedora 20*: che permette di iniziare subito l'installazione;

<img src="install_f20_01.png" title="Schermata di avvio" alt="Schermata di avvio" width="400" />

-   *Test this media & Install Fedora 20*: esegue un test del supporto prima di iniziare l'installazione
-   *Troubleshooting*

La voce Troubleshootings (in italiano "Risoluzione dei problemi") permette di selezionare le seguenti azioni:

-   *Install Fedora in basic graphics mode*: tramite questa opzione, per chi avesse problemi hardware in particolare sulla scheda video, verrà fatto caricare il [driver vesa](http://it.wikipedia.org/wiki/Video_Electronics_Standards_Association);
-   *Rescue a Fedora system*: opzione utile per coloro che necessitano di "mettere mano" ad una installazione già presente di fedora sul disco. Tramite questa opzione anaconda cerca la partizione di fedora e tenta di darne un accesso \[<http://it.wikipedia.org/wiki/Chroot>‎ chroot\] all'interno; si può, ad esempio, [reinstallare Grub2](Reinstallare_Grub "wikilink") oppure modificare i file di una installazione esistente;
-   *Run a memory test*: per fare un test della memoria RAM del sistema;
-   *Boot from local drive*: per eseguire il boot dal MBR del primo disco rigido;
-   *Return to main menù*: per ritornare al menù principale.

In tutte le azioni è possibile premere il tasto tab per inserire eventuali opzioni; inoltre sono tutte selezionabili, oltre che con le frecce, anche con la lettera che sullo schermo viene indicata di colore diverso rispetto al resto del testo.
Con il tasto "Esc", invece, si torna al passaggio precedente.

Se dopo il controllo il supporto viene definito integro, si può scegliere la lingua da utilizzare durante il processo di installazione. Dopo aver selezionato la lingua, è suffciente cliccare su "Continua" per impostare automaticamente la tastiera secondo la lingua selezionata.

Riepilogo Installazione
-----------------------

La schermata successiva presenta il *Riepilogo Installazione*, formato da tre categorie principali: **Localizzazione**, **Software** e **Sistema**, con le relative sottocategorie.
Si nota subito che in alcune sottocategorie ci possono essere dei triangoli gialli; questi simboli avvertono di completare i vari passaggi prima di procedere con l'installazione. Normalmente l'unico segnale di avvertenza è nella *Destinazione di installazione*.
<img src="install_f20_02.png" title="fig:Riepilogo installazione con avvertenza sulla voce &quot;Destinazione di Installazione&quot;." alt="Riepilogo installazione con avvertenza sulla voce &quot;Destinazione di Installazione&quot;." width="800" />

Localizzazione
--------------

Nel sottomenù *Localizzazione* sono presenti le voci *Data & Ora*, *Tastiera* e *Supporto Lingua* che dovrebbero essere già impostate correttamente se si è scelta correttamente la propria lingua. Se le voci non fossero corrette cliccarci sopra e modificarle secondo i propri bisogni.

### Data & Ora

In questa sezione è possibile calibrare il fuso orario (avendo scelto la lingua italiana) su Roma oppure scegliere di impostare l'orario tramite la rete utilizzando un server NTP.

### Tastiera

Nella sezione *Tastiera* è possibile scegliere il layout della tastiera selezionando la lingua desiderata. Dalla stessa schermata è possibile aggiungere o togliere un determinato layout di tastiera.

### Supporto Lingua

In questa sezione è possibile aggiungere delle lingue addizionali all'installazione.

Software
--------

Il sottomenu *Software* fornisce le seguenti due voci:

### Sorgente Installazione

La sorgente di installazione è di default il dvd; modificando le opzioni di questa sezione è possibile selezionare come sorgente un file .iso di un dvd oppure un mirror nella rete. E' inoltre possibile selezionare di eseguire gli ultimi aggiornamenti e aggiungere dei Repository aggiuntivi.
Durante questa guida viene usato il dvd come sorgente di installazione senza installare gli aggiornamenti più recenti.
Dopo le scelte cliccare sul tasto *Fatto* in alto a sinistra per tornare al *Riepilogo Installazione* e proseguire nella configurazione del processo di installazione.

### Selezione Software

Nella sezione Selezione del Software è possibile scegliere quale ambiente Desktop installare (Gnome, Kde, XFCE, LXDE, ecc.) e, opzionalmente, quali add-ons o altre applicazioni, tra quelli presenti nel dvd, installare (per es. "Libreoffice", "Strumenti di Amministrazione" e molti altri).
<img src="install_f20_03.png" title="fig:Selezione Software" alt="Selezione Software" width="800" />
Dopo le scelte cliccare sul tasto *Fatto* in alto a sinistra per tornare al *Riepilogo Installazione* e proseguire nella configurazione del processo di installazione.

Sistema
-------

La sezione Sistema contiene le voci: *Configurazione Rete* e *Destinazione Installazione*, quest'ultima si dovrà selezionare per partizionare il sistema. Tutti i dispositivi connessi al sistema verranno identificati e si potranno selezionare per l'installazione.
Nella finestra *Dischi Locali Standard* sono presenti tutti i dispositivi connessi ed è possibile selezionare quali dischi includere nel processo di partizionamento e quali invece ignorare completamente.

### Destinazione di Installazione

Aprendo la sezione dischi saranno mostrati i vari dischi rilevati da Anaconda.

Nella sezione *Dischi Locali Standard* Scegliere il disco o i dischi sui quali si vuole installare Fedora

Nella sezione *Dischi specializzati e di rete* è possibile selezionare ulteriori dischi che non fanno parte dei dischi standard del nostro sistema, se non si hanno dischi speciali non è necessario impostare nulla in questa sezione.

Dopo aver selezionato i dischi che ci interessano per l'installazione è possibile selezionare il **Sommario completo del disco e del bootloader** cliccando sul relativo pulsante posto in basso a sinistra, con questo strumento è possibile ricontrollare tutti i dischi che verranno interessati dall'installazione di Fedora 20 ed è possibile scegliere su quale disco installare il bootloader, selezionando il disco e cliccando su *Imposta come dispositivo di boot*, oppure è possibile non installare il bootloader su un determinato disco selezionandolo e cliccando su *Non installare il bootloader*. Per uscire dal sommario del disco e del bootloader cliccare sul pulsante *Chiudi* nella relativa finestra.

Dopo la scelta dei dischi per proseguire nel processo di installazione partizionamento dei dischi, cliccare sul pulsante *Fatto* in alto a sinistra.

A questo punto verrà aperta la finestra *OPZIONI DI INSTALLAZIONE*, nella quale: si potrà scegliere di affidarsi al partizionamento automatico scegliendo *Configura automaticamente l'installazione di Fedora sui dischi selezionati e torna al menu principale*; oppure scegliere di effettuare il partizionamento manuale dei dischi, scegliendo *Controlla/Modifica le partizioni del disco prima di continuare*. In entrambe le scelte di partizionamento (automatico o manuale) è possibile scegliere lo schema delle partizioni scegliendo nel menu a tendina tra: *Partizione Standard*, *BTRFS*, *LVM* oppure *Thin provisioning LVM*.

Se si vuole criptare con password le partizioni su cui è installata Fedora selezionare l'opzione *Cifrare i dati. La passphrase sarà scelta in seguito.*

Se abbiamo dimenticato di agiungere dei dischi è possibile selezionare *Annulla e aggiungi altri dischi*.

Di seguito il dettaglio delle operazioni da eseguire nel processo di installazione in base alla scelta di effettuare un Partizionamento Automatico, oppure un Partizionamento Manuale:

#### Partizionamento Automatico

Se si sceglie il partizionamento automatico si dovrà soltanto scegliere il relativo tipo di partizione, ovvero *Partizioni Standard*, *LVM* oppure *BTRFS*.

Cliccando sul pulsante *Continua* posto in basso a destra si può tornare alla schermata principale del *Riepilogo Installazione*.
<img src="install_f20_04.png" title="fig:Opzioni di installazione" alt="Opzioni di installazione" width="800" />

#### Partizionamento Manuale

Selezionando invece *Controlla/Modifica le partizioni del disco prima di continuare* nella finestra *Opzioni di installazione* e cliccando sul pulsante *Continua*, si viene introdotti al partizionamento manuale, dove vi è la lista di tutte le partizioni già presenti sui dischi scelti in precedenza. Da qui si può scegliere se creare automaticamente un punto di mount cliccando sull'opzione *Clicca qui per crearli automaticamente*, oppure si potrà cliccare nel riquadro in basso il pulsante **+** per creare ulteriori punti di mount.
<img src="install_f20_05.png" title="fig:Partizionamento Manuale" alt="Partizionamento Manuale" width="800" />
Per ogni partizione si può scegliere manualmente il punto di mount, o formattare una partizione già esistente e scegliere il tipo di filesystem preferito, criptare la partizione e cambiarne l'etichetta.

Nel riquadro sottostante si vede come è possibile aggiungere o togliere i vari punti di mount nella propria installazione. Si può ad esempio aggiungere una partizione /home separata cliccando nella casella di selezione una qualsiasi partizione vuota, oppure anche sovrascriverne una esistente; quindi nelle caselle delle opzioni a destra bisogna specificare:

-   il *Punto di Mount*, che può essere /home, /tmp, /var, ecc;
-   l*'Etichetta*, il nome da dare alla partizione, che può anche essere lasciata vuota;
-   la *Capacità Desiderata*, ovvero la grandezza che si desidera dare alla partizione.
-   il *Tipo dispositivo*, che può essere Partizione Standard, LVM, oppure BTRFS e si può scegliere di criptare o meno la partizione;
-   il *Filesystem*, che normalmente è ext4, si può modificare con la relativa scelta per formattare o meno la partizione che si seleziona.

Per ogni modifica ad una singola partizione cliccare su *Aggiorna impostazioni* per memorizzare le modifiche.

Se non siamo soddisfatti del partizionamento che abbiamo creato cliccare sul pulsante *Reimposta tutto* posto in basso a destra per resettare le impostazioni di partizionamento.

Una volta terminate le modifiche alle partizioni cliccare sul pulsante *Fatto* in alto a sinistra, si aprirà un'altra finestra relativa al *Riepilogo delle Modifiche*, cliccare ancora su *Accetta Modifiche* per scrivere su disco le nuove partizioni e tornare alla schermata principale *RIEPILOGO INSTALLAZIONE*
<img src="install_f20_06.png" title="fig:Partizionamento Manuale 2" alt="Partizionamento Manuale 2" width="800" />
Se non si desidera vedere un esempio di partizionamento manuale si può proseguire direttamente al paragrafo [Avvio dell'installazione su disco](#Avvio_dell'installazione_su_disco "wikilink")

##### **Esempio di Partizionamento Manuale**

Segue un esempio pratico di partizionamento manuale.
Si parte dalla situazione, molto comune, di avere già installato un Dual Boot con un sistema operativo MS Windows in una partizione primaria, un altro sistema GNU/Linux già installato e presente in una partizione primaria e una o più partizioni logiche vuote e disponibili ad ospitare una nuova installazione di Fedora.

La tabella delle partizioni potrebbe quindi presentarsi in questo modo:

  
- sda1 installazione preesistente di MS Windows;

- sda2 partizione di recovery di MS Windows;

- sda3 partizione estesa

- sda4 partizione di swap

- sda5 partizione / di una distro Linux già installata

- sda6 partizione vuota

- sda7 partizione vuota

- sda8 partizione /home (contenente la /home della distro già installata)

Nell'esempio si vede come installare la directory / di Fedora in sda6 e la /home condivisa in sda8.

Facendo riferimento all'immagine **Opzioni di Installazione** selezionare la spunta su *Passare al partizionamento personalizzato dei dischi* e cliccare sul pulsante *Continua* uscirà la schermata relativa al *Partizionamento Manuale* con elencate tutte le partizioni presenti sul disco nella colonna a sinistra.

Ora si passa a preparare la partizione /. Dalla lista delle partizioni cliccare sulla partizione sda6. Verrà aperta sulla destra una nuova lista di opzioni come da immagine precedente, **Partizionamento manuale 2**.

-   Nella casella *Punto di Mount* inserire: **/** che rappresenta la directory radice del futuro sistema fedora 20;
-   Nella casella *Etichetta* si può inserire ad esempio l'etichetta: **fedora20** oppure lasciare il campo vuoto, è indifferente;
-   Lasciare invariato il campo *Capacità desiderata* che utilizzerà di default tutto lo spazio disponibile nella partizione;

<!-- -->

-   Nel menu a tendina *Tipo Dispositivo* selezionare **Standard Partition**;
-   Nel menu a tendina *File system* selezionare **ext4**, per avere un filesystem moderno adatto per un sistema desktop tradizionale;
-   Mettere la spunta nella casella *Riformatta* per formattare nuovamente la partizione nel caso in cui non si fosse sicuri che sia completamente vuota;

Cliccare sul pulsante *Aggiorna impostazioni* per memorizzare le impostazioni sulle partizioni e procedere con l'impostazione della partizione successiva.

Ora si può preparare la partizione /home. Dalla lista delle partizioni cliccare sulla partizione sda8:

-   Nella casella *Punto di Mount* inserire: **/home** che rappresenta la directory /home del proprio sistema;
-   Nella casella *Etichetta* lasciare il campo vuoto;
-   Lasciare invariato il campo *Capacità desiderata* che utilizzerà di default tutto lo spazio disponibile nella partizione.

<!-- -->

-   Nel menu a tendina *Tipo Dispositivo* selezionare **Standard Partition**;
-   Nel menu a tendina *File System* selezionare **ext4**;
-   **Non bisogna mettere** la spunta nella casella *Riformatta*, poiché questo è il caso di una /home condivisa con un altro sistema operativo; in caso di formattazione tutti i dati presenti verrebbero irrimediabilmente distrutti;

Cliccare sul pulsante *Aggiorna impostazioni* per memorizzare le impostazioni sulle partizioni e procedere con l'impostazione della partizione successiva.

Infine si prepara la partizione di swap se si necessita di una partizione [swap](http://it.wikipedia.org/wiki/Swap_%28informatica%29); dalla lista delle partizioni cliccare sulla partizione denominata "swap" (in questo caso sda4): sarà aggiunta in automatico al mount point della nuova installazione.

Le modifiche alle partizioni sono terminate, si può tornare al *Riepilogo Installazione* cliccando sul pulsante *Fatto* in alto a sinistra.

### Configurazione Rete

Nella configurazione di rete (Network Configuration) è possibile aggiungere la propria connessione, di qualunque tipo essa sia, utilizzando la modalità integrata di Network Manager.

Avvio dell'installazione su disco
---------------------------------

Quando la schermata **Riepilogo Installazione** non presenta più nessun triangolo giallo di avvertimento è possibile procedere all'installazione vera e propria cliccando sul pulsante *Avvia installazione* posto in basso a destra.
<img src="install_f20_07.png" title="fig:Riepilogo di Installazione completato" alt="Riepilogo di Installazione completato" width="800" />

Durante il processo di installazione si possono inserire le *Impostazioni Utente*: verrà richiesto di inserire la password di root e di creare un utente. È sempre buona regola scegliere una password molto robusta per l'utente root, da almeno da una decina di caratteri, sia alfanumerici che simboli speciali.
<img src="install_f20_08.png" title="fig:Inizio dell&#39;installazione su disco" alt="Inizio dell&#39;installazione su disco" width="800" />

Creazione Utente
----------------

Nella schermata di creazione utente bisogna inserire il nome reale, il nome dell'utente e la relativa password utente. Se viene spuntata la casella *Imposta questo utente come amministratore* l'utente appena creato avrà appunto i privilegi di amministratore, cioè verrà aggiunto al gruppo wheel; sostanzialmente all'utente è permesso l'uso del comando *sudo*.
Il comando sudo su fedora è disabilitato di default, dato che permette a qualsiasi utente normale del sistema di operare come fosse root e questo è un grave rischio per la sicurezza. È possibile attivarlo comunque durante l'installazione selezionando la casella relativa.
Viene inoltre richiesto di inserire la password utente che servirà per accedere durante la sessione di lavoro.

Nella sezione *Avanzato* è possibile effettuare una Configurazione utente avanzata, potendo scegliere di creare una directory per il relativo utente nella posizione che si desidera, scegliere di specificare manualmente un ID utente e specificare manualmente un ID gruppo, è infine possibile inserire manualmente l'utente che si è creato in un determinato gruppo.
<img src="install_f20_09.png" title="fig:Creazione Utente" alt="Creazione Utente" width="800" />
Alla fine dell'installazione viene richiesto di riavviare il computer. Bisognerà estrarre il supporto utilizzato durante l'installazione (dvd, cd, live-usb, ecc...) e si avrà davanti il primo avvio di Fedora 20; nel caso si abbia installato il Desktop Environment Gnome si verrà "salutati" da una schermata di benvenuto. <img src="install_f20_10.png" title="fig:Primo avvio di Fedora 20 Gnome" alt="Primo avvio di Fedora 20 Gnome" width="800" />

Per problemi sorti durante l'installazione cercare all'interno del forum discussioni con problemi simili e, nel caso mancasse, aprire una discussione specificando che supporto si è utilizzato, quali "passi" differenti dalla guida si sono seguiti, e qualsiasi informazione possa servire ad aiutare alla soluzione.
Enjoy.
<Categoria:Installazione>
