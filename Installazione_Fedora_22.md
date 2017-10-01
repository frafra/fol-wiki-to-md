Introduzione
------------

Lo scopo della presente guida è quella di esplorare l'installazione della release 22 di Fedora, nella **variante Workstation**. L'immagine ISO utilizzata è quella proposta di default dal sito ufficiale del Fedora Project. Per maggiori informazioni su come creare un supporto CD/DVD avviabile, è consigliabile seguire le [istruzioni](http://docs.fedoraproject.org/it-IT/Fedora/17/html/Burning_ISO_images_to_disc/index.html) ufficiali. Se si preferisce invece utilizzare una Pendrive USB, occorre consultare [questa](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB/it) pagina (anche se al momento non risulta pienamente aggiornata).

Per illustrare il processo di installazione, è stata utilizzata una macchina virtuale creata con [virt-manager](https://virt-manager.org/). La capacità del disco fisso rappresentato è puramente indicativa. Anche il partizionamento è stato illustrato a titolo esemplificativo e non deve essere inteso come unico metodo valido e consigliato. Le ampie dimensioni di storage delle unità odierne – e la grande varietà di sistemi operativi presenti - consentono all'utente di intraprendere strade diverse, compatibilmente con le esigenze personali. Ulteriori informazioni a riguardo, possono essere reperite all'interno della [documentazione](http://docs.fedoraproject.org/en-US/Fedora/22/html/Installation_Guide/index.html) del Fedora Project.

Avvio dell'installazione
------------------------

Per l'installazione occorre inserire il supporto e modificare le opzioni del **BIOS/UEFI** per effettuare il boot con esso. È presente un conto alla rovescia per l'avvio della Live: è possibile agire su tale countdown premendo un tasto qualsiasi. Le frecce (su e giù) permettono di navigare nel menù e invio di confermare l'opzione scelta. Le selezioni sono le seguenti:

-   **Start Fedora Live**: fa partire l'esecuzione del sistema operativo installato sul supporto
-   **Troubleshooting**: offre strumenti per la risoluzione di problemi.

Quest'ultima voce elenca le seguenti procedure:

-   **Start Fedora Live in basic graphics mode**: esegue il sistema utilizzando i driver video generici Vesa, utili nel caso in cui la modalità standard evidenzi problemi grafici
-   **Test this media & start Fedora Live**: testa la consistenza relativa al supporto adoperato per l'installazione
-   **Run a memory test**: valuta l'affidabilità della RAM del computer
-   **Boot from local drive**: richiama il boot-loader installato sull'hard disk del computer senza quindi procedere alla nuova installazione di Fedora
-   **Return to main menu**: visualizza nuovamente il menù precedente

Ultimato l'avvio del sistema operativo Live, un'utile schermata propone di partire subito con l'installazione vera e propria di Fedora. Se il computer non è connesso ad Internet per mezzo di un cavo Ethernet, è consigliato configurare preliminarmente le **opzioni di rete** e avviare il processo solo in un momento successivo (tramite l'apposita icona reperibile nell'insieme delle applicazioni).

<img src="fedora22inst_2.png" title="fig:Troubleshooting." alt="Troubleshooting." width="200" /> <img src="fedora22inst_3.png" title="fig:Finestra di benvenuto." alt="Finestra di benvenuto." width="200" /> <img src="fedora22inst_1.png" title="fig:Schermata di avvio." alt="Schermata di avvio." width="600" />

La primissima videata di **Anaconda** – il software che si preoccuperà di installare il sistema – offre l'opportunità di selezionare la **lingua preferita**. È opportuno ricordare che l'etichetta presente in alto a destra, riguardante il layout della tastiera, non è modificabile. Sarà successivamente possibile configurare anche questo aspetto.

<img src="fedora22inst_4.png" title="fig:Scelta della lingua." alt="Scelta della lingua." width="600" />

Riepilogo Installazione
-----------------------

La schermata successiva presenta il **"riepilogo di installazione"**, composto da quattro categorie fondamentali (tastiera, data e ora, destinazione d'installazione, rete). In base all'idioma scelto, l'applicazione dovrebbe esser riuscita a determinare layout e fuso orario corretti. Se così non fosse o se l'utente volesse personalizzare ulteriormente questo aspetto, è possibile accedere ai relativi menù. I triangoli arancioni evidenziano invece le voci che devono essere ancora ultimate prima di poter procedere con i passaggi finali.

<img src="fedora22inst_5.png" title="fig:Riepilogo installazione." alt="Riepilogo installazione." width="600" />

Disposizione della tastiera
---------------------------

Il menù relativo alla **disposizione della tastiera**, consente di scegliere quali layout includere nel sistema. Una casella di testo consente inoltre di verificarne il funzionamento associato.

<img src="fedora22inst_8.png" title="fig:Aggiunta disposizione della tastiera." alt="Aggiunta disposizione della tastiera." width="200" /> <img src="fedora22inst_7.png" title="fig:Opzioni di cambio disposizione." alt="Opzioni di cambio disposizione." width="200" />
<img src="fedora22inst_6.png" title="fig:Disposizione della tastiera." alt="Disposizione della tastiera." width="600" />

Per aggiungere, togliere o ordinare i vari schemi, occorre agire tramite i tasti presenti appena sotto l'apposita lista. Tramite il tasto **Opzioni**, è inoltre facile scegliere quali combinazioni utilizzare per cambiare la configurazione.

Ora & Data
----------

Corredata da un elegante e utile planisfero, la categoria relativa all'orologio consente di selezionare il **fuso orario**.

<img src="fedora22inst_10.png" title="fig:Server NTP." alt="Server NTP." width="200" />
<img src="fedora22inst_9.png" title="fig:Ora &amp; Data." alt="Ora &amp; Data." width="600" />

È possibile fare in modo che Fedora sincronizzi l'ora tramite Internet. Un'opzione consente inoltre di aggiungere host personalizzati da usare come Server NTP.

Rete & Nome Host
----------------

Il compito dell'interfaccia qui proposta è essenzialmente quello di attribuire un **hostname**, ossia un nome identificativo con cui gli altri computer distingueranno il nostro all'interno di una comunicazione, nel caso di condivisioni basate su rete. Per configurare il collegamento ad Internet invece, occorre servirsi degli strumenti offerti dall'ambiente desktop della Live (Gnome 3, nel caso dell'edizione Workstation di Fedora).

<img src="fedora22inst_20.png" title="fig:Rete &amp; Nome Host." alt="Rete &amp; Nome Host." width="600" />

Destinazione d'installazione
----------------------------

La sezione chiamata **"Destinazione d'installazione"**, è senza dubbio la più importante di tutto il processo. Configurare partizioni, cifratura, bootloader e supporti interessati è scopo delle funzionalità qui proposte.

<img src="fedora22inst_12.png" title="fig:Dischi di rete." alt="Dischi di rete." width="200" /> <img src="fedora22inst_13.png" title="fig:Sommario completo disco e bootloader." alt="Sommario completo disco e bootloader." width="200" /> <img src="fedora22inst_11.png" title="fig:Destinazione d&#39;installazione." alt="Destinazione d&#39;installazione." width="600" />

Per prima cosa, conviene scegliere le unità da utilizzare come destinazione, inserendo eventuali dischi di rete, se necessario. Per quanto riguarda il layout di partizionamento, le alternative sono due: agire manualmente o demandare il compito ad Anaconda, il quale opterebbe per la soluzione LVM. Nel caso in cui lo spazio sia insufficiente, il software proporrà il ridimensionamento delle partizioni esistenti. All'occorrenza, è inoltre possibile cifrare i dati applicando una password da digitare all'avvio del sistema e scegliere la destinazione del boot loader Grub.

### Partizionamento manuale

Il wizard dedicato al layout che si andrà a creare, permette di creare le partizioni, scegliendo per prima cosa, dall'apposito menù a tendina, il tipo di schema da utilizzare:

-   **LVM**: consente di organizzare il sistema all'interno di volumi logici. Tale tipo di partizionamento aggiunge flessibilità in caso di modifiche alle partizioni, ma può essere considerato sovrabbondante nel caso di sistemi Workstation.
-   **BTRFS**: destinato a diventare il file system predefinito, offre interessanti novità ma non è ancora considerato maturo come l'ecosistema ext.
-   **Partizioni standard**: offre l'opportunità di creare partizioni di tipo standard. Se non sono presenti esigenze particolari, è consigliato l'utilizzo di questa opzione, abbinata al file system di tipo 'ext4'.

<img src="fedora22inst_16.png" title="fig:Aggiunta di un punto di mount." alt="Aggiunta di un punto di mount." width="200" /> <img src="fedora22inst_17.png" title="fig:Configurazione di un punto di mount." alt="Configurazione di un punto di mount." width="200" /> <img src="fedora22inst_18.png" title="fig:Riepilogo delle modifiche." alt="Riepilogo delle modifiche." width="200" /> <img src="fedora22inst_15.png" title="fig:Partizionamento manuale." alt="Partizionamento manuale." width="600" />
Lo scopo del menù qui descritto, è quello di gestire gli schemi relativi ai dischi selezionati. Una volta sceltane la tipologia, occorre creare i diversi tipi di mount in modo automatico oppure procedere all'aggiunta manuale. Per ogni elemento, è possibile personalizzare capacità desiderata, file system ed – opzionalmente - etichetta. La [documentazione ufficiale del Fedora Project](http://docs.fedoraproject.org/en-US/Fedora/22/html/Installation_Guide/sect-installation-gui-manual-partitioning-recommended.html), consiglia la creazione delle seguenti partizioni:

-   **/boot**: contiene i file necessari all'avvio del sistema. 500Mb sono sufficienti.
-   **/**: contiene cartelle e file relativi al sistema operativo e ai programmi installati. È consigliabile una dimensione compresa tra i 10 e i 20gb
-   **swap**: è la memoria virtuale che viene sfruttata dal sistema in caso di saturazione di quella di tipo fisico. La dimensione deve essere decisa in base all'ammontare di RAM del sistema. Se la memoria è meno di 2gb, allora occorre includere una partizione di swap di dimensioni doppie rispetto ad essa. Se la RAM va dai 2 agli 8gb, la swap può eguagliarne la capacità in termini di giga-bytes.
-   **/home**: contiene file e directory appartenenti agli utenti. Conviene sfruttare lo spazio rimanente (allocando almeno 10gb). Avere tale partizione separata è utile per preservare i dati personali nel caso in cui si opti per una successiva nuova installazione di Fedora.

Come specificato dall'interfaccia, la conferma applicata al riepilogo proposto da Anaconda, non implica un'immediata applicazione dei cambiamenti previsti.

##### **Esempio di Partizionamento Manuale**

Segue un esempio pratico di partizionamento manuale.
Si parte dalla situazione, molto comune, di avere già installato un Dual Boot con un **sistema operativo MS Windows** in una partizione primaria, un altro **sistema GNU/Linux** situato in un'altra partizione primaria e una o più partizioni logiche vuote e disponibili ad ospitare una nuova installazione di Fedora.

La tabella delle partizioni potrebbe quindi presentarsi in questo modo:

  
- sda1 installazione preesistente di MS Windows;

- sda2 partizione di recovery di MS Windows;

- sda3 partizione estesa

- sda4 partizione di swap

- sda5 partizione / di una distro Linux già installata

- sda6 partizione vuota

- sda7 partizione vuota

- sda8 partizione /home (contenente la /home della distro già installata)

Nell'esempio si vede come installare la directory **/** di Fedora in **sda6** e la **/home** condivisa in **sda8**.

Facendo riferimento all'immagine **Destinazione d'installazione**, selezionare l'opzione **Configurerò le partizioni** e cliccare sul pulsante **Fatto** presente nella parte superiore sinistra dell'interfaccia. La schermata successiva sarà quella relativa al **Partizionamento Manuale**, che elenca, all'interno della colonna sinistra, tutte le partizioni presenti sul disco.

Si può cominciare con la partizione /. Dalla lista delle partizioni cliccare sulla partizione sda6. Verrà aperta sulla destra una nuova lista di opzioni come da immagine **Configurazione di un punto di mount**.

-   Nella casella **Punto di Mount** inserire: **/** che rappresenta la directory radice del futuro sistema Fedora;
-   Nella casella **Etichetta** è possibile inserire a piacere un identificativo per la partizione oppure mantenere vuoto il campo;
-   **Capacità desiderata** va lasciato vuoto, in modo che venga utilizzato tutto lo spazio disponibile nella partizione;

<!-- -->

-   Nel menu a tendina **Tipo Dispositivo** selezionare **Partizione standard**;
-   Nel menu a tendina **File system** scegliere **ext4**, per avere un filesystem moderno e adatto ad un sistema desktop tradizionale;
-   È opportuno cosiderare la spunta sulla scelta **Riformatta** nel caso in cui la partizione non sia completamente vuota;

Infine, cliccare sul pulsante **Aggiorna impostazioni** per memorizzare le modifiche applicate e procedere con l'impostazione del punto di mount successivo.

Ora si può preparare la partizione /home. Dalla lista delle partizioni cliccare sulla partizione sda8:

-   Nella casella **Punto di Mount** inserire: **/home**
-   Nella casella **Etichetta** lasciare il campo vuoto;
-   Lasciare invariato il campo **Capacità desiderata** che utilizzerà di default tutto lo spazio disponibile nella partizione.

<!-- -->

-   Nel menu a tendina **Tipo Dispositivo** selezionare **Partizione standard**;
-   Nel menu a tendina **File system** selezionare **ext4**;
-   **Non bisogna apporre** la spunta sulla casella **Riformatta**, poiché questo è il caso di una /home condivisa con un altro sistema operativo; in caso di formattazione tutti i dati presenti verrebbero infatti irrimediabilmente distrutti;

Cliccare sul pulsante **Aggiorna impostazioni** per salvare i nuovi cambiamenti e procedere.

Infine, nel caso in cui si necessiti di una partizione di [swap](http://it.wikipedia.org/wiki/Swap_%28informatica%29), è opportuno crearla. Dalla lista cliccare sulla partizione denominata "swap" (in questo caso sda4). Essa sarà aggiunta in automatico ai punti di montaggio della nuova installazione.

Il nuovo layout è completo e terminato; si può tornare al **Riepilogo Installazione** cliccando sul pulsante **Fatto**, situato in alto a sinistra.

Avvio dell'installazione su disco
---------------------------------

Non appena il riepilogo non sottolinea più la presenza di impostazioni mancanti, per concludere l'installazione di Fedora, è sufficiente azionare l'apposito bottone blu **"Avvia installazione"**.

<img src="fedora22inst_19.png" title="fig:Riepilogo d&#39;installazione completo." alt="Riepilogo d&#39;installazione completo." width="600" />
Durante il processo vero e proprio, una barra d'avanzamento fornisce dettagli relativi alle azioni compiute dall'installer. A questo punto, è da considerare l'eventualità di creazione di una password di root – l'utente avente i privilegi più elevati all'interno di Fedora – e di un utente standard. Se quest'ultimo non viene previsto a questo stadio, in seguito al boot del sistema installato, sarà comunque possibile una sua aggiunta tramite la comoda interfaccia di benvenuto chiamata 'gnome-initial-setup'. Anaconda rende tuttavia già disponibili alcune personalizzazioni di tipo avanzato (gruppi di appartenenza, home directory, ID).

<img src="fedora22inst_22.png" title="fig:Impostazione password di root." alt="Impostazione password di root." width="200" /> <img src="fedora22inst_24.png" title="fig:Creazione utente standard." alt="Creazione utente standard." width="200" /> <img src="fedora22inst_25.png" title="fig:Configurazione utente avanzata." alt="Configurazione utente avanzata." width="200" /> <img src="fedora22inst_21.png" title="fig:Esecuzione dell&#39;installazione." alt="Esecuzione dell&#39;installazione." width="600" />
In seguito al completamento dell'installazione - e della configurazione - dei pacchetti previsti dall'edizione Workstation, basterà terminare Anaconda e procedere al **riavvio del computer**.

<img src="fedora22inst_30.png" title="fig:Riavvio del computer (1)." alt="Riavvio del computer (1)." width="200" /> ![tight|200px|Riavvio del computer (2).](fedora22inst_31.png "fig:tight|200px|Riavvio del computer (2).") <img src="fedora22inst_29.png" title="fig:Installazione completata." alt="Installazione completata." width="600" />

Utilizzo del nuovo sistema operativo
------------------------------------

Prima della riaccensione della macchina, è opportuno **rimuovere correttamente il dispositivo esterno** contenente il sistema Live, in modo tale da evitare di avviare nuovamente il processo di installazione.

Se è stato creato un utente, il sistema lo evidenzierà all'interno di **Gdm**, il gestore degli accessi di Gnome. Una volta correttamente effettuato il log-in, le finestre di **gnome-initial-setup** elencheranno alcuni passaggi finali per perfezionare l'esperienza d'utilizzo.

<img src="fedora22inst_32.png" title="fig:Gdm." alt="Gdm." width="200" /> <img src="fedora22inst_34.png" title="fig:gnome-initial-setup – Digitazione." alt="gnome-initial-setup – Digitazione." width="200" /> <img src="fedora22inst_33.png" title="fig:gnome-initial-setup – Lingua." alt="gnome-initial-setup – Lingua." width="600" /> <img src="fedora22inst_35.png" title="fig:gnome-initial-setup – Privacy." alt="gnome-initial-setup – Privacy." width="200" /> <img src="fedora22inst_36.png" title="fig:gnome-initial-setup – Account online." alt="gnome-initial-setup – Account online." width="200" /> <img src="fedora22inst_37.png" title="fig:gnome-initial-setup – Fedora pronta all&#39;uso." alt="gnome-initial-setup – Fedora pronta all&#39;uso." width="600" />

Successivamente, sarà la volta della **guida di Gnome**, che è consigliato consultare sopratutto nel caso in cui non si abbia una sufficiente dimestichezza con tale ambiente desktop. All'interno della documentazione di Fedora Online sono presenti altre pagine utili, come ad esempio:

-   [Gnome-Shell](Gnome-Shell "wikilink"): dettagli riguardanti l'interfaccia utente di Gnome.
-   [Nautilus\_scripts\_e\_personalizzazioni](Nautilus_scripts_e_personalizzazioni "wikilink"): personalizzazioni relative al gestore di file e cartelle predefinito.

<img src="fedora22inst_38.png" title="fig:Primi passi." alt="Primi passi." width="600" />
Ed infine, eccolo qui! Il desktop predefinito della nostra nuova Fedora è finalmente **pronto per essere utilizzato**!

<img src="fedora22inst_39.png" title="fig:Il desktop Gnome." alt="Il desktop Gnome." width="600" />

<Categoria:Installazione>
