Introduzione
------------

-   Ti sei deciso di installare Fedora ma non sai come fare?
-   Hai appena installato Fedora e non hai idea come procedere?
-   Hai voglia di provare Fedora ma non sai a cosa andrai incontro?
-   Ti interessa Linux ma ti sembra tutto arabo?

Per tutte queste domande una risposta è sicuramente valida: **è normale!**
Infatti, quando ci si avvicina per la prima volta al mondo Linux i dubbi e le perplessità iniziali possono essere molteplici. Un file system diverso, un'installazione diversa e una configurazione del sistema molto più curata nei dettagli, spesso diventano ostacoli insormontabili.
Tuttavia un passaggio da altri sistemi operativi a Linux Fedora è più semplice di quello che si pensa, con il suggerimento di non fare confronti con altri S.O. ma di ripartire da zero. Vedrai che in questo modo la missione diventerà presto un successo.

Prima di addentrarci in alcuni aspetti fondamentali del tuo nuovo sistema operativo, però, vediamo un po' di storia.

Linux, un po' di storia
-----------------------

### Il Kernel

Spesso quando si parla di Linux si intende un sistema operativo completo, come nel nostro caso Fedora. Questo, però, non è del tutto esatto, perchè con Linux si intende solamente il kernel (cuore) del sistema, ovvero la parte che si occupa della gestione del processore, della memoria e delle componenti hardware. Per comunicare con il sistema invece si ha bisogno di un'interfaccia utente, che può essere testuale (una shell) oppure grafica (la cosiddetta GUI – Graphic User Interface).

### GNU/Linux

Tutte le distribuzioni che si trovano in circolazione e che permettono un avvicinamento meno difficoltoso all'ambiente Desktop, devono gran parte del loro successo al progetto GNU, che poi ha trovato in GNU/Linux il binomio perfetto. GNU (che significa “GNU is not Unix” - GNU non è Unix) nasce come sistema operativo completamente libero, utilizzando la licenza GPL (General Public Licence) che sancisce e protegge le libertà fondamentali che permettono l'uso e lo sviluppo collettivo e naturale del software.
Vengono creati programmi per ogni necessità informatica, ma per diventare un sistema operativo vero e proprio mancava ancora una parte importante, un kernel che potesse gestire la parte “hardware”. Quando nel 1991 Linus Torvalds scrisse il primo kernel e lo rilasciò liberamente era arrivato il momento della nascita di un nuovo sistema operativo, che venne chiamato GNU/Linux; finalmente si era aperta la strada per entrare nel mercato Desktop.

### Il software libero

Una delle caratteristiche fondamentali, che ha contribuito al successo del kernel Linux e di conseguenza delle applicazioni e del software legato ad esso, è il fatto che viene rilasciato l'intero codice sorgente, in modo che possa essere modificato e sviluppato dalla comunità. A differenza del software proprietario, in cui il codice sorgente rimane blindato, il software libero stimola la condivisione delle conoscenze; un aspetto importante che ha portato presto al software Open Source.

Fedora che cos'è?
-----------------

Fedora è un sistema operativo basato su Linux che presenta gli ultimissimi software liberi ed open source. Prende il suo nome da un cappello degli anni '20, logo molto noto della società che sponsorizza il progetto, ovvero Red Hat.
L'uso, la modifica e la distribuzione di Fedora è sempre libera per chiunque e per sempre. E' creata da un insieme di persone in tutto il mondo che lavorano come una comunità: il Fedora Project.
Il progetto Fedora cerca di seguire 2 principi fondamentali:

-   Fedora significa rapido progresso di contenuti liberi e software Open Source
-   Fedora crede nel motto “una volta libero, sempre libero”

Il ciclo di vita di una release (versione) di Fedora è di 6 mesi, il che significa che ci sono due rilasci stabili ogni anno e che di conseguenza Fedora è una delle distribuzioni Linux più all'avanguardia per quanto riguarda il software a bordo. Allo stesso modo, quindi sempre per un anno, una versione *n* viene supportata e mantenuta dalla comunità. Dopodichè il mantenimento si sposta alla release *n+1*.

Fedora funziona su tutti i tipi di hardware e può essere utilizzata nei più svariati modi, sia esso Desktop, Netbook, Laptop o un Server.
Infine c'è da sottolineare che Fedora come desktop predefinito utilizza GNOME. (vedi capitolo successivo)

Il Desktop di default: GNOME
----------------------------

L'installazione è stata terminata con successo e al primo login ci si trova davanti una scrivania nuova: GNOME (**G**NU **N**etwork **O**bject **M**odel **E**nvironment). Un Desktop Environment sconosciuto, che già dal primo impatto è molto diverso rispetto alle interfacce grafiche alle quali probabilmente si era abituato. <img src="gnome_base.jpg" title="fig:Gnome dopo la prima installazione si presenta così. Se così non fosse, verificare il corretto funzionamento dei driver grafici, c&#39;è un suggerimento più avanti" alt="Gnome dopo la prima installazione si presenta così. Se così non fosse, verificare il corretto funzionamento dei driver grafici, c&#39;è un suggerimento più avanti" width="400" />

<img src="gnome_app.jpg" title="fig:Le applicazioni presenti possono essere visualizzati anche per categoria" alt="Le applicazioni presenti possono essere visualizzati anche per categoria" width="400" /> Si nota fin da subito che è un Desktop pulito, privo di icone e menu. Quello che si vede si chiama **Gnome-Shell**, una scrivania interattiva, e portando il mouse in alto a sinistra si capirà subito perchè.
Toccare l'angolo superiore sinistro equivale al click su "Attività"; le finestre aperte verranno minimizzate e sul Desktop compariranno al centro. A sinistra si avrà un menu di avvio veloce, altamente configurabile, a destra ci saranno le aree di lavoro. Cliccando in alto su "Applicazioni si potranno vedere e scegliere le applicazioni installate sul proprio sistema, come nell'immagine a sinistra.
Riportando il mouse nell'angolo superiore sinistro si potrà tornare alle finestre aperte o, se non ci fossero, alla schermata iniziale.
Come per il cosiddetto "hot corner" in alto a sinistra, esiste un altro "angolo magnetico" in basso a destra. Portando il mouse in quella posizione apparirà una barra inferiore di sfondo nero, sulla quale potrai leggere le applicazioni in background, i messaggi di sistema oppure le funzionalità chat. <img src="gnome_utente.jpg" title="fig:Il menu utente sembra non avere il pulsante per spegnere la macchina" alt="Il menu utente sembra non avere il pulsante per spegnere la macchina" width="250" /> Tornando sul pannello superiore si noteranno delle icone a destra, tra cui il volume, la rete e la gestione della batteria. Seguendo il proprio nome utente, con un click si apre il menu indicato a destra.
A prima vista sembra non esserci il pulsante per spegnere la macchina, ma premendo il tasto <ALT> si vedrà che la voce "Sospendi" cambia in "Spegni". In alternativa esiste un'estensione che fa apparire in modo permanente e senza premere il tasto ALT le voci "Iberna" e "Spegni".
Alcune particolarità nell'utilizzo di Gnome-Shell:

-   **Tasto "Win":** Equivale al hot corner in alto a sinistra dello schermo
-   **ALT+F2:** si aprirà una linea di comando, inserendo "r" e premendo <Invio> per esempio si riavvia Gnome-Shell
-   **Ctrl+Alt+Freccia su/giù:** si passa da un Desktop virtuale (area) all'altro

<img src="gnome_sistema.jpg" title="fig:Molte cose si possono configurare direttamente da qui" alt="Molte cose si possono configurare direttamente da qui" width="250" /> All'interno del menu utente esiste un'altra voce importante, le *Impostazioni di Sistema*, dove si possono impostare lo schermo, la rete, il mouse, tastiera, la stampante e molto altro. Queste sono, a grandi linee, le cose basilari del Desktop di default. Naturalmente c'è molto altro da sapere su Gnome, dalle personalizzazioni alle estensioni disponibili, ma è possibile anche installare ulteriori pacchetti di amministrazione. Piano piano si imparerà a modificare l'aspetto di Gnome lavorando semplicemente sui file CSS e a tal proposito si può trovare un supporto nella [ guida avanzata sulla configurazione di Gnome](Gnome-Shell_e_le_sue_estensioni "wikilink").

Per adesso è bene esplorare il più possibile il nuovo Desktop, ricordando che finchè si è loggati come utente normale non si potranno arrecare danni al sistema. Quando invece viene chiesta la password di root (=amministratore) biogna prestare molta attenzione, perchè ogni cambiamento fatto da amministratore è potenzialmente pericoloso per la stabilità del sistema stesso.
Alcuni aspetti, come Nautilus, il file manager, saranno familiari, altri invece necessiteranno di un po' più di tempo per essere assimilati. Il file system, per esempio, è sicuramente molto diverso da tutti gli altri sistemi operativi, ma non per questo nasconde ostacoli insormontabili.

Strumenti di sistema: primi dubbi
---------------------------------

### Installazione delle applicazioni aggiuntive

Fedora, come tutte le distribuzioni Linux, è un vero sistema multi-utente, nel senso che è in grado di gestire un'infinità di utenti, attribuendo al solo amministratore (root) i permessi di installazione di applicativi, di modifiche su file di configurazione ecc.
Detto questo la prima differenza rispetto alle macchine con sistemi operativi Microsoft sta proprio in questa distinzione netta tra utente e amministratore, che di fatto su Windows spesso sono la stessa persona. Non è solo una necessità di un sistema multi-utente, ma chiude le porte a moltissimi malware e cavalli di troia, che non avendo i permessi di root non riescono ad arrecare danni significativi al sistema.

Fedora è un sistema rpm-based, il che vuol dire che per l'installazione di pacchetti software si avvale di formati RPM (**R**ed Hat **P**ackage **M**anager). <img src="PackageKit.jpg" title="fig:PackageKit è il gestore grafico di pacchetti RPM di Fedora" alt="PackageKit è il gestore grafico di pacchetti RPM di Fedora" width="300" /> Per gestire il processo di installazione/disinstallazione Fedora si avvale di PackageKit, uno strumento grafico che si trova in *Applicazioni &gt; Srumenti di Sistema &gt; Aggiungi/rimuovi software*.
L'utilizzo di PackageKit è molto intuitivo:

-   A sinistra si può cercare il pacchetto o farsi elencare un gruppo di applicazioni
-   Sulla destra verranno visualizzati i songoli pacchetti del gruppo e il loro stato (installato o no)

Se si fa click su un pacchetto, in basso verrà visualizzata una breve descrizione e la sua dimensione. si potrà selezionare o deselezionare il pacchetto mettendo o togliendo il classico "baffo" verde. Questa operazione può essere ripetuta per tutte le applicazione che si desidera installare o disinstallare qualcosa.
Terminata questa operazione bisogna soltanto confermare tutto con "Applica". Il sistema a questo punto verifica tutte le dipendenze, ovvero i pacchetti aggiuntivi che sono necessari per il corretto funzionamento dell'applicazione stessa.
Alla fine di tutti i controlli verrà chiesta la *password di root* e l'operazione comincerà, elencando le applicazioni e le dipendenze che sono state installate o disinstallate. Con un po' di pratica si vedrà presto che installare applicazioni nuove con PackageKit è davvero molto facile.
Le applicazioni installate saranno disponibili immediatamente nel menu *Applicazioni* visto durante il piccolo excursus su Gnome. Verranno automaticamente inserite nella categoria di competenza, da dove si possono lanciare con un semplice click.

### I Repository, ovvero, la banca dati

Tutti i pacchetti RPM disponibili per Fedora sono raccolti in una specie di grande banca dati, i cosiddetti [repository](:Categoria:Repository "wikilink"). Sono questi server che Fedora, tramite la GUI PackageKit, interroga per reperire informazioni su un determinato pacchetto o gruppo di applicazioni, e allo stesso modo verifica se sono disponibili degli aggiornamenti. Infatti, forse lo si avrà già notato, il sistema è preimpostato per verificare giornalmente la disponibilità di aggiornamenti e di comunicarli tramite la barra inferiore. Se si vorrà si potranno installare con un semplice click. Questa impostazione può essere modificata da *Sistema &gt; Preferenze &gt; Aggiornamento Software*.
Fedora ha già a bordo i repository "ufficiali", ma ne esistono molti altri. Il motivo per cui Fedora fornisce solo i suoi repository è facile intuirlo:
Fedora, come già detto prima, utilizza solamente software libero e privo di licenza proprietaria. Motivo per cui molti plugin o applicativi non sono presenti. Ecco perchè cui vale la pena installare almeno altri due repository.

#### RPMFusion

Questi repository, che si distinguono in *free* e *non-free*, rappresentano l'unione di alcuni repository già molto forniti precedentemente, motivo per cui dopo questa fusione contengono un'infinità di software.
Per installarli si può seguire la pagina di [RPMFusion](http://rpmfusion.org/Configuration), ma si può anche consultare la nostra guida dedicata all'installazione dei repository [RPMFusion](RPMFusion "wikilink").

### Articoli consigliati

Non è possibile inserire tutte le informazioni in un'unica guida, per cui si consiglia fortemente, oltre alle guide già citate, di leggere anche gli articoli sulle seguenti tematiche:

-   [ Driver video per la scheda grafica ATI](Installazione_Driver_ATI "wikilink")
-   [ Driver video per la scheda grafica NVidia](Installazione_Driver_NVidia "wikilink")
-   [ Installazione del plugin Flash](Flash_plugin "wikilink")
-   [ Installazione dei codec audio e video (mp3, avi, wma, DivX,...)](Multimedia_Player_e_codecs "wikilink")
-   e molto altro...

Il Terminale
------------

Fino ad ora, volutamente, non si è ancora toccato il cosiddetto *terminale*, un emulatore di shell presente in *Applicazioni &gt; Strumenti di Sistema &gt; Terminale*.
E' importante sapere che con il terminale è possibile eseguire qualsiasi tipo di operazione, ma per semplicità d'uso all'inizio spesso si privilegia l'ambiente grafico per muoversi e per controllare il sistema. Nelle pagine del wiki, però, si troveranno spesso dei richiami a output o input in un terminale, motivo per cui è utile confrontarsi fin dall'inizio con questo strumento.
Una volta aperto, il terminale si presenta così:

`[fol@localhost ~]$`

Il terminale indica il nome utente (fol), il nome della macchina (localhost), la posizione in cui ci si trova (**~** equivale alla propria home directory) e infine dice come si è loggati (**$** indica che si è loggati come utente normale).
Qualche esempio:

`# dnf install firefox`

oppure

`$ lspci`

-   il simbolo **\#** indica che l'operazione deve essere eseguita come **root** (amministratore);
-   il simbolo **$** indica che l'operazione deve essere eseguita come **utente**.

Per passare, subito dopo l'apertura del terminale, da utente normale a root, basterà digitare:

`[fol@localhost ~]$ su -`
`password di root`
`[root@localhost ~]#`

Conclusioni
-----------

Hai appena visto una piccolissima parte di quello che è Fedora, ma ora sei in grado di affrontare le guide presenti sul wiki per approfondire gli argomenti che più ti interessano. Continua a leggere il wiki e in caso di dubbi o problemi chiedi aiuto sul [Forum](http://forum.fedoraonline.it/).
Non tutto filerà sempre liscio all'inizio, ma non demordere, perchè l'esperienza che acquisisci, anche nei momenti di difficoltà, è enorme.
In bocca al lupo e **Benvenuto su Fedora Online!**

<Categoria:Installazione>
