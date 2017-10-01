Introduzione
------------

Fin dagli albori, il **Fedora Project** ha cercato di fornire alla propria utenza un metodo ufficialmente supportato per poter avanzare di versione senza ricorrere ad una nuova installazione pulita. Dato l'impatto e la delicatezza dell'operazione però, storicamente si è reso necessario lo sviluppo e il rinnovo nel tempo di diversi sistemi.

Lo scopo di questa guida è quello di descrivere lo strumento supportato a partire da Fedora 23, ossia un plugin di **Dnf** chiamato **system-upgrade**.

Nascita di system-upgrade
-------------------------

Dopo cinque rilasci di Fedora, e il confronto con i cambiamenti che le novità comportano, nel 2015 si decide di abbandonare il precedente prodotto chiamato **FedUp**. Il motivo è essenzialmente dovuto a scelte iniziali di design non più adattabili all'evoluzione del sistema operativo.

Il problema sostanziale è che, il vecchio applicativo, procedeva alla costruzione di un “*upgrade.img*” - una sorta di initramfs dedicato per l'operazione - che si basava su meccanismi non supportati e non documentati di [Systemd](http://www.freedesktop.org/wiki/Software/systemd/).

Le segnalazioni di alcuni bug non facilmente risolvibili hanno stimolato la nascita di un nuovo metodo più integrato con il **gestore di pacchetti [Dnf](http://dnf.baseurl.org/)**.

Preparazione del sistema
------------------------

Prima di partire, può essere utile consultare la [lista di bug](https://bugzilla.redhat.com/buglist.cgi?bug_status=NEW&bug_status=ASSIGNED&component=dnf-plugin-system-upgrade&order=Importance&query_format=advanced), riguardanti **system-upgrade**, attualmente aperti.

Le immagini illustrative dell'intera guida sono state reperite da una **macchina virtuale** contenente **Fedora 22 KDE**. Sono riportate qui a puro titolo esemplificativo: dato il prevalente utilizzo di interfacce di tipo testuale, l'utilizzo di un diverso ambiente Desktop (come Gnome) non si discosta in maniera rilevante.

Tutti i comandi del procedimento, devono essere impartiti da **root**. Per questo, è necessario effettuare il login come tale utente, tramite un **emulatore di terminale**.

`$ su -`

Al sistema vanno applicati gli ultimi aggiornamenti disponibili.

`# dnf upgrade`

<img src="dnf-plugin-system-upgrade_1.png" title="Aggiornamento del sistema." alt="Aggiornamento del sistema." width="600" />

Se non risulta essere già installato, il plugin per l'upgrade può ora essere reperito tramite **Dnf** (analogamente a qualsiasi altro programma).

`# dnf install dnf-plugin-system-upgrade`

<img src="dnf-plugin-system-upgrade_2.png" title="Installazione di dnf-plugin-system-upgrade" alt="Installazione di dnf-plugin-system-upgrade" width="600" />

L'ultimo passaggio per la preparazione del sistema, riguarda il **riavvio** dello stesso.

`# reboot`

Upgrade
-------

### Fase 1: download

La prima fase riguarda il download automatico dei pacchetti necessari per l'upgrade. Nel comando seguente, “versione\_da\_raggiungere” deve essere opportunamente sostituito con il numero del rilascio di Fedora di destinazione (esempio: se si desidera passare da Fedora 23 a Fedora 24, la stringa adatta sarà *`dnf` `system-upgrade` `download` `--releasever=24`*). Come evidenziato dall'immagine del terminale, talvolta è possibile che alcuni programmi abbiano problemi di dipendenze: il comportamento predefinito di Dnf è quello di lasciare tali applicativi fermi alla versione attuale per poter procedere comunque all'avanzamento. Il parametro **`--best`** (descritto nel paragrafo *Parametri "--best" e "--distro-sync"*), può essere usato dagli utenti avanzati per sovvertire questo comportamento.

`# dnf system-upgrade download --releasever=versione_da_raggiungere`

<img src="dnf-plugin-system-upgrade_3.png" title="Download pacchetti per avanzamento di versione." alt="Download pacchetti per avanzamento di versione." width="600" />

Alla fine del processo di scaricamento, devono essere importate le chiavi **gpg** relative ai nuovi repository: è sufficiente confermare digitando la lettera **s**, seguita dalla pressione del tasto **Invio**.

<img src="dnf-plugin-system-upgrade_4.png" title="Importazione chiavi gpg." alt="Importazione chiavi gpg." width="600" />

L'ultima operazione automatica di Dnf, in questa fase, riguarda un piccolo **test di transazione**, che si conclude nel giro di pochi minuti.

<img src="dnf-plugin-system-upgrade_5.png" title="Test di transazione." alt="Test di transazione." width="600" />

<img src="dnf-plugin-system-upgrade_6.png" title="Completamento fase di download." alt="Completamento fase di download." width="600" />

L'ultimo input utente necessario, è quello per **riavviare il sistema** in modo appropriato per procedere quindi **all'avanzamento di versione** vero e proprio.

`# dnf system-upgrade reboot`

<img src="dnf-plugin-system-upgrade_7.png" title="dnf system-upgrade reboot" alt="dnf system-upgrade reboot" width="600" />

### Fase 2: Upgrade vero e proprio

Diversamente a quanto avveniva con FedUp, la configurazione di Grub non è ancora stata toccata. Non sono presenti righe “System upgrade” o simili: occorre avviare **normalmente** il sistema non ancora aggiornato.

<img src="dnf-plugin-system-upgrade_8.png" title="Schermata di Grub" alt="Schermata di Grub" width="600" />

All'avvio, viene presto segnalata la partenza del meccanismo vero e proprio per l'avanzamento di versione. In questa fase, verranno installati tutti i pacchetti scaricati in precedenza. Con il tasto ESC è possibile esaminare il dettaglio del processo attraverso un'interfaccia di tipo testuale. Il tempo di esecuzione varia a seconda della mole di software presente.

<img src="dnf-plugin-system-upgrade_10.png" title="fig:Avvio dell&#39;upgrade del sistema (interfaccia testuale)" alt="Avvio dell&#39;upgrade del sistema (interfaccia testuale)" width="200" /> <img src="dnf-plugin-system-upgrade_11.png" title="fig:Aggiornamento in corso (interfaccia grafica)" alt="Aggiornamento in corso (interfaccia grafica)" width="200" /> <img src="dnf-plugin-system-upgrade_9.png" title="fig:Avvio dell&#39;upgrade del sistema (interfaccia grafica)" alt="Avvio dell&#39;upgrade del sistema (interfaccia grafica)" width="600" />

Successivamente, Dnf procederà alla pulizia dei pacchetti obsoleti (che sono stati appena sostituiti) e alla verifica di quelli nuovi. L'avanzamento di versione si avvia quindi verso la conclusione.

<img src="dnf-plugin-system-upgrade_13.png" title="fig:Pulizia pacchetti obsoleti" alt="Pulizia pacchetti obsoleti" width="200" /> <img src="dnf-plugin-system-upgrade_14.png" title="fig:Verifica nuovi pacchetti" alt="Verifica nuovi pacchetti" width="200" /> <img src="dnf-plugin-system-upgrade_12.png" title="fig:Aggiornamento in corso (interfaccia testuale)" alt="Aggiornamento in corso (interfaccia testuale)" width="600" />

Infine, il sistema si riavvierà nuovamente: se tutto è filato per il verso giusto, si avrà ora la nuova riga di Grub riguardante un kernel per la nuova versione di Fedora. Al completamento del boot, sarà quindi possibile utilizzare il nuovo rilascio.

<img src="dnf-plugin-system-upgrade_15.png" title="fig:Grub dopo upgrade" alt="Grub dopo upgrade" width="200" /> <img src="dnf-plugin-system-upgrade_16.png" title="fig:Login manager di KDE" alt="Login manager di KDE" width="200" /> <img src="dnf-plugin-system-upgrade_17.png" title="fig:Desktop di KDE" alt="Desktop di KDE" width="600" />

Fase di download: comandi aggiuntivi (facoltativi)
--------------------------------------------------

Gli utenti più esperti, possono trarre beneficio dall'utilizzo di alcuni parametri o comandi aggiuntivi.

### Parametri '--best' e '--distro-sync'

Per sincronizzare ed allineare in automatico la distribuzione, si può utilizzare il parametro *`--distro-sync`* (vedasi capitolo relativo alla *Rimozione dei pacchetti orfani*, all'interno della sezione “*Passaggi Post-Upgrade*”) direttamente all'avvio della *Fase di download*. Di seguito, si riporta un esempio riguardante l'avanzamento a Fedora 23.

`# dnf system-upgrade download --releasever=23 --distro-sync`

L'utilizzo di *--distro-sync* è utile nel caso in cui la versione precedente – nell'esempio, Fedora 22 – abbia del software troppo aggiornato rispetto a quanto presente nei repository del rilascio successivo. Solitamente, questo è dovuto alla presenza nel sistema di pacchetti provenienti dai repository di test *updates-testing* o *Rawhide*.

L'atteggiamento predefinito di Dnf, contrariamente agli strumenti del passato, è quello di procedere comunque all'upgrade nonostante l'eventuale presenza di pacchetti con problemi di dipendenze. Nel comportamento tipico quindi, tali rpm rimangono ancorati al rilascio precedente di Fedora. La decisione presa dagli sviluppatori ha perfettamente senso: in questo modo, non si blocca l'avanzamento, si mantiene il software in uno stato funzionante e non si rischia di compromettere il sistema. Se l'utente preferisce non avviare il processo nel caso in cui ci siano perplessità di questo genere, è sufficiente l'utilizzo del parametro **--best**. L'esempio successivo riguarda un ipotetico avanzamento a Fedora 23.

`# dnf system-upgrade download --releasever=23 --best`

### Monitorare lo stato del sistema durante l'effettivo upgrade

Durante la fase di download dei pacchetti, prima di riavviare il sistema con *`#` `dnf` `system-upgrade` `reboot`*, è possibile inserire il seguente input

`# systemctl add-wants system-update.target debug-shell.service`

Tale comando, permette all'utente di monitorare il sistema durante l'upgrade, abilitando una shell root nella console virtuale VT9 (accessibile con CTRL+ALT+F9). Per esempio, per l'avanzamento di versione dal rilascio 22 a Fedora 23, i passaggi completi per la preparazione saranno i seguenti:

`# dnf system-upgrade download --releasever=23`
`# systemctl add-wants system-update.target debug-shell.service`
`# dnf system-upgrade reboot`

Passaggi Post-Upgrade (facoltativi)
-----------------------------------

Per raffinare ulteriormente il processo di upgrade, e renderlo nella sostanza più simile ad una nuova installazione, può risultare utile una pulizia rispetto ai pacchetti non più presenti nella nuova versione di Fedora.

### Rimozione pacchetti orfani

Per prima cosa, assicurarsi di avere un sistema completamente in **sincronia** con i repository configurati

`# dnf distro-sync`

Solo successivamente, è possibile scoprire quali dei programmi installati, **non sono più presenti** nelle sorgenti attive.

`# dnf list extras`

In linea di massima, tutti i pacchetti elencati possono essere rimossi senza problemi. L'output del precedente comando **deve però essere correttamente interpretato** a seconda della situazione: esistono casi in cui si potrebbe avere del software non volutamente allineato a quanto previsto da Fedora. Ecco alcuni esempi:

1.  Dnf ovviamente riporta i vecchi **kernel**, in quanto essi non risultano essere più reperibili. In realtà però, mantenere – e quindi non disinstallare – diverse versioni degli stessi, rappresenta una buona pratica, per avere diverse alternative in caso di problemi al supporto hardware.
2.  Un'altra circostanza assai frequente, è rappresentata da programmi di **terze parti** o comunque provenienti da **sorgenti esterne** ora disabilitate. Tra gli esempi, si trovano Skype, i codec del repository Livna, driver grafici proprietari.
3.  Se alcuni programmi sono stati reperiti da **"updates-testing"**, verranno qui riportati in quanto “troppo aggiornati” rispetto a quanto previsto dai repository stabili.

I seguenti comandi consentono inoltre di effettuare ricerche mirate per poter valutare le diverse circostanze.

`$ dnf search nomepacchetto --releasever=versione_di_fedora`
`$ dnf info nomepacchetto --releasever=versione_di_fedora`

### Aggiornamento files '.conf'

Alcuni manutentori, potrebbero aver fornito file *.conf* aggiornati, assieme all'installazione di nuove versioni dei loro pacchetti. Per non sovrascrivere inavvertitamente eventuali impostazioni dell'utente, Dnf li rinomina aggiungendo l'estensione *.rpmnew*.

Per effettuare una ricerca nel sistema ed eliminare i file di configurazione non più attuali, è possibile servirsi di *rpmconf*, facilmente reperibile dai repository standard di Fedora.

`# dnf install rpmconf`

Il comando per l'avvio dell'applicativo è il seguente

`# rpmconf -a`

Se rpmconf trova un file aggiornato, varie scelte sono possibili:

-   *Y o I*: mantiene il nuovo file del manutentore
-   *N o O* mantiene il file obsoleto
-   *D*: mostra le differenze tra i due file
-   *M*: unisce i due file di configurazione
-   *Z*: sposta in background l'esecuzione di rpmconf per esaminare meglio la situazione
-   *S*: salta questo conflitto, senza prendere una decisione

<img src="dnf-plugin-system-upgrade_18.png" title="Esecuzione di rpmconf" alt="Esecuzione di rpmconf" width="600" />

Nel caso di un upgrade di Fedora, è bene quindi rispondere **Y** a tutte le richieste poste da rpmconf (**fatta ovviamente eccezione per i file modificati manualmente dall'utente**).

Casi particolari
----------------

### Salti di versione (esempio: da Fedora 21 a Fedora 23)

I cosiddetti “salti di versione”, rappresentano ad oggi una parte controversa e mai del tutto chiarita, a causa di una sorta di “vuoto legislativo” all'intero del Project.

Tecnicamente, questo tipo di aggiornamento dovrebbe funzionare, ma rimane comunque un processo non ufficialmente riconosciuto e quindi non consigliato. In passato, sono stati segnalati problemi dovuti alla mancanza di chiavi gpg, comunque aggirabili tramite l'opzione **--nogpgcheck**.

Risulta però conveniente optare per un'installazione pulita, oppure per un aggiornamento graduale (per esempio: da Fedora 21 a Fedora 22 e solo successivamente da Fedora 22 a Fedora 23).

### Da Fedora 21 a Fedora 22

Con l'arrivo della versione 0.5.0 di dnf-plugin-system-upgrade su Fedora 21, si consiglia di preferire tale programma a FedUp anche per l'upgrade verso Fedora 22.

I passaggi sono quelli descritti nei capitoli precedenti.

Metodi obsoleti (per aggiornamenti a rilasci precedenti a Fedora 23)
--------------------------------------------------------------------

<img src="Preupgrade4.png" title="Interfaccia grafica di preupgrade" alt="Interfaccia grafica di preupgrade" width="300" />

Con l'avvento di Fedora 9 (Sulphur), vede la luce il progetto **preupgrade**, affiancato al già esistente aggiornamento tramite dvd. Funzionante fino al rilascio 17, rimane ad oggi l'unico ad offrire una vera e propria interfaccia grafica. All'interno della documentazione di Fedora Online, è ancora presente la relativa pagina ([Aggiornamento\_Fedora\_con\_preupgrade](Aggiornamento_Fedora_con_preupgrade "wikilink")).

La nascita di Fedora 18 (Spherical Cow), porta invece alla ribalta **FedUp**, di cui conserviamo un tutorial ([Aggiornamento\_Fedora\_con\_FedUp](Aggiornamento_Fedora_con_FedUp "wikilink")). Dichiarato non supportato a partire dal rilascio 23, lascerà progressivamente spazio al plugin di Dnf, oggetto della presente guida.

Fonti
-----

[Changes for Fedora: DNF\_System\_Upgrades](https://fedoraproject.org/wiki/Changes/DNF_System_Upgrades)

[:Categoria:Installazione](:Categoria:Installazione "wikilink")
