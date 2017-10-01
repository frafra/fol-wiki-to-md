[Rilettura in corso](Rilettura_in_corso "wikilink")

Introduzione
------------

Segnalare un bug – baco, “difetto” nello sviluppo del software - è un ottimo modo per contribuire attivamente allo sviluppo del sistema operativo Fedora e dei pacchetti del parco applicativo che compongo la distribuzione. Non esiste infatti prodotto informatico esente da imperfezioni; l'apporto degli utenti risulta quindi fondamentale per accrescerne la qualità.

<img src="bugzilla_mainpage.png" title="Home Page di Bugzilla." alt="Home Page di Bugzilla." width="600" />

Il modo migliore per rendere consapevoli sviluppatori e manutentori quindi, è quello di aprire una segnalazione su [Red Hat Bugzilla](https://bugzilla.redhat.com/), la piattaforma di riferimento per l'ecosistema Red Hat.

Creazione account Bugzilla
--------------------------

Il primo passo, è ovviamente quello rappresentato dalla creazione di un account gratuito tramite [l'apposita pagina per la registrazione](https://bugzilla.redhat.com/createaccount.cgi). L'unico dettaglio richiesto è l'indirizzo e-mail, a cui verrà inviato un collegamento ipertestuale per l'attivazione: è consigliabile creare una casella di posta elettronica “ad-hoc” o comunque utilizzarne una differente rispetto a quella personale. I motivi sono sostanzialmente due:

-   Il contatto inserito non sarà celato, in modo da agevolare eventuali comunicazioni private – rare ma possibili – tra i diversi contributori.
-   In seguito ad ogni intervento che interesserà il report aperto, il sistema notificherà all'utente l'evoluzione della situazione tramite mail.

<img src="bugzilla_newaccount.png" title="Registrazione a Bugzilla." alt="Registrazione a Bugzilla." width="600" />

Tramite il link inviato automaticamente dal sistema, è opportuno inserire gli ultimi dettagli - nome reale, password, relativa convalida – e confermare per rendere l'account operativo. Va ricordato comunque che, essendo Fedora un progetto esteso a livello mondiale, è necessaria una certa dimestichezza con la lingua inglese, per poter interpretare correttamente richieste e commenti.

<img src="bugzilla_accountconfirmation.png" title="Registrazione a Bugzilla." alt="Registrazione a Bugzilla." width="600" />

Quando segnalare un bug
-----------------------

Spesso, quello che potrebbe all'apparenza sembrare un bug, è invece in realtà una caratteristica controversa del software o, più comunemente, un errore di configurazione dell'utente. Una lettura interessante sull'argomento è rappresentata dall'apposita [guida ufficiale](http://fedoraproject.org/wiki/Bugs_and_feature_requests/it). Prima di aprire una segnalazione, può essere utile consultare altre risorse, tra le quali:

-   **Il forum della comunità italiana Fedora Online**: il forum di [FOL](https://www.fedoraonline.it), frequentato da utenti italiani della distribuzione, racchiude al suo interno una raccolta di svariate problematiche e relative soluzioni. Può inoltre risultare utile l'apertura di un nuovo topic ad-hoc per permettere di inquadrare la situazione.
-   **AskFedora**: similarmente a quanto accade per l'ecosistema nostrano, questo [portale](https://ask.fedoraproject.org) di riferimento rappresenta il punto d'incontro per discussioni internazionali da cui è possibile attingere per reperire informazioni a riguardo del malfunzionamento riscontrato.
-   **IRC**: per avere un sostegno rapido e diretto, può essere utile porre una domanda veloce sulla chat maggiormente utilizzata dagli utenti di Fedora. I canali di riferimento sono *\#fedora-it* per il panorama italiano, *\#fedora* per quello internazionale e *\#fedora-qa* per discutere in merito della versione Rawhide o dei pre-rilasci. Un elenco completo di tutti i vari canali è presente [qui](https://fedoraproject.org/wiki/Communicating_and_getting_help/it#IRC).
-   **Mailing List**: le mailing list sono speciali indirizzi che rispediscono i messaggi che ricevono a tutti gli utenti iscritti. [Qui](https://fedoraproject.org/wiki/Communicating_and_getting_help/it#Mailing_Lists_degli_utenti) è possibile consultare la vasta gamma di liste appartenenti al Project.
-   **Motori di ricerca**: spesso bistrattati ed ignorati, in realtà possono fornire indicazioni soprattutto se affrontati in panorami esterni a Fedora. Forum di discussioni, pagine tecniche di sviluppatori e blog di appassionati possono risultare utili anche solo per una prima e sommaria raccolta di informazioni.

Se tuttavia non si ha la certezza assoluta ed inopinabile della presenza di un errore di programmazione, può comunque essere utile aprire un report per dialogare con i manutentori del pacchetto interessato. In un mondo aperto come quello Open Source, difficilmente essi ignorano richieste d'aiuto e si rendono spesso disponibili a indirizzare gli utenti verso la possibile soluzione.

Occorre assicurarsi però di non aprire una segnalazione a riguardo di una questione già nota. Per non occupare inutilmente dello spazio, rischiare di perdere tempo e frammentare l'attività, risulta fondamentale evitare la creazione di ulteriori duplicati. Se, da un lato, le [pagine dei bug comuni](https://fedoraproject.org/wiki/Common_bugs) possono aiutare, molto più importante, quasi obbligatoria, è una ricerca mirata e preliminare all'interno di Bugzilla. Sono sufficienti i passaggi qui di seguito illustrati.

Raggiungere la [home page di Bugzilla](https://bugzilla.redhat.com) e selezionare il collegamento [**Search**](https://bugzilla.redhat.com/query.cgi) presente nell'header.

Per usare la ricerca semplice, occorre inserire del testo e opzionalmente filtrare per **stato** e **prodotto**. Anche se tale funzione può risultare fruttifera, spesso conviene tuttavia optare per un'esplorazione più fine tramite il motore offerto da **“Advanced Search”**.

<img src="bugzilla_search1.png" title="Bugzilla – Ricerca semplice." alt="Bugzilla – Ricerca semplice." width="600" />

Ora è infatti possibile sfruttare impostazioni sicuramente più mirate come, per esempio, la scelta del componente. Va ricordato che l'utente può selezionare più elementi dalle liste, per personalizzare ulteriormente la richiesta. In seguito alla pressione del bottone **“Search”** e, dopo un breve lasso di tempo di attesa, il browser aggiornerà la pagina e mostrerà le **segnalazioni** più coerenti con i parametri impostati.

<img src="bugzilla_search3.png" title="fig:Ricerca per più componenti" alt="Ricerca per più componenti" width="200" /> <img src="bugzilla_search4.png" title="fig:In attesa..." alt="In attesa..." width="200" /> <img src="bugzilla_search2.png" title="fig:Bugzilla – Ricerca avanzata." alt="Bugzilla – Ricerca avanzata." width="600" />

Per consultare un **report**, è sufficiente cliccare sull'ID del bug, oppure sul valore della colonna **“Summary”**.

<img src="bugzilla_search5.png" title="Bugzilla – Risultato ricerca." alt="Bugzilla – Risultato ricerca." width="600" />

A questo punto, l'utente – se autenticato nel sistema e se lo ritiene opportuno – può partecipare all'evoluzione della situazione con semplici interventi:

-   Può commentare o aggiungere allegati, se potenzialmente funzionali alla risoluzione della problematica.
-   Può aggiungere il proprio contatto alla cosidetta **CC list** (semplicemente spuntando l'apposita casella e invocando il bottone **Save changes**), in modo da ricevere notifiche via mail a riguardo del report interessato.

<img src="gnomeabrt_16reportedbug1.png" title="Bugzilla – Consultazione di un report." alt="Bugzilla – Consultazione di un report." width="600" />

Segnalazione di bug (tramite browser)
-------------------------------------

Il modo più semplice e rapido per aprire un report e segnalare un problema, è quello di affidarsi all'interfaccia web di Bugzilla. I passaggi sono sostanzialmente i seguenti.

Per prima cosa, occorre effettuare il *login* assicurandosi di possedere un profilo attivato mediante la procedura descritta nella [sezione precedente](#Creazione_account_Bugzilla "wikilink") della presente guida.

<img src="bugzilla_login.png" title="Login a Bugzilla." alt="Login a Bugzilla." width="600" />

Cominciare quindi la creazione della segnalazione tramite il click sul pulsante **New**, situato nell'header della pagina, in alto a sinistra. Va scelta la classificazione giusta, nel nostro caso **Fedora**.

<img src="bugzilla_bugreport1.png" title="Classificazione per il bug." alt="Classificazione per il bug." width="600" />

Ora, occorre selezionare il prodotto adatto. Se si sta per segnalare un problema tecnico derivante dall'utilizzo del sistema operativo, si deve optare per il prodotto **Fedora**. Diverso può essere, per esempio, il caso di un errore rilevato nelle note di rilascio, per il quale conviene scegliere **Fedora Documentation**.

<img src="bugzilla_bugreport2.png" title="Tipologia di prodotto a cui il bug si riferisce." alt="Tipologia di prodotto a cui il bug si riferisce." width="600" />

Il momento cruciale dell'intero processo è quello della stesura vera e propria del report. Bugzilla presenta un form con alcuni dati da compilare.

1.  **Component**: prodotto oggetto della segnalazione, il quale evidenzia il comportamento scorretto che è stato rilevato. Cominciando a scrivere, un menù a tendina compare per facilitare l'inserimento. Se l'utente non è pienamente sicuro a riguardo della natura dell'inconveniente, può comunque selezionare un elemento a parer suo coerente con il problema. Il componente può essere successivamente variato da membri di alcuni team del Fedora Project;
2.  **Version**: versione di Fedora sulla quale si riscontra la presenza del bug;
3.  **Severity**: grado di criticità del problema. Non è un valore obbligatorio, ma può esser utile per evidenziare le questioni più prioritarie. Attualmente, è possibile scegliere tra:
    1.  **Urgent**: il bug rende l'intero sistema inusabile, oppure mina la sua sicurezza. È importante notare che una problematica riferibile soltanto a dell'hardware specifico - come ad esempio configurazioni particolari di schede video, ecc. - non è sufficientemente critica per essere etichettata come urgente;
    2.  **High**: il bug rende il programma inusabile, o riguarda problemi di licenza;
    3.  **Medium**: un vero e proprio bug che rende il programma – o parte di esso – più difficile da usare;
    4.  **Low**: problematiche meno urgenti, quali sottigliezze grafiche oppure bug riscontrati tramite l'utilizzo di configurazioni inusuali;

4.  **Hardware**: architettura del proprio processore, desumibile invocando *`$` `uname` `-m`* da un prompt del terminale;
5.  **OS**: la compilazione di questo campo, per report riguardanti Fedora, risulta di poca utilità effettiva. Può essere tranquillamente ignorato (alternativamente, è sufficiente selezionare 'Linux');
6.  **Summary**: titolo applicabile al report. Deve essere il più possibile preciso e conciso per facilitare le ricerche da parte di altri utenti di Bugzilla;
7.  **Description**: contenuto del messaggio allegato alla segnalazione. Bugzilla indica una traccia che, pur non essendo strettamente necessaria, conviene seguire per poter fornire importanti dettagli ai manutentori:
    1.  **Description of the problem**: descrizione che deve fornire quante più informazioni possibili a riguardo del problema. In un certo senso, è l'estensione più prolissa e dettagliata del campo **Summary**;
    2.  **Version-release number of selected component**: versione specifica dei pacchetti che causano l'inconveniente. Il comando *`$` `rpm` `-qa` `|` `grep` `nomeprogramma`* può aiutare ad identificare i dati richiesti da tale paragrafo;
    3.  **How reproducible**: frequenza con la quale si verifica il problema. Alcuni esempi:
        1.  **Happens every time**: la problematica si manifesta sempre quando si crea la situazione indicata dal paragrafo 'Steps to reproduce';
        2.  **Happens sometimes, but not always**: non è chiaro quale evento faccia scattare la problematica, che quindi appare manifestarsi occasionalmente;
        3.  **Haven't tried to reproduce it**: l'utente non ha provato a ricreare la situazione problematica;
        4.  **Tried, but couldn't reproduce it**: il bug si è manifestato una singola volta e non è facile da riprodurre;

8.  **Steps to reproduce**: sequenza di passi con la quale è possibile azionare gli eventi che innescano il comportamento scorretto del componente;
9.  **Actual results**: dettagli relativi all'effettiva manifestazione del problema (per esempio, crash, output errati, ecc.);
10. **Expected results**: al contrario del precedente punto, in tale paragrafo occorre specificare i risultati attesi, in un certo senso immaginando che l'applicazione interessata non sia affetta dal bug che si sta segnalando;
11. **Additional information**: eventuali informazioni non fondamentali, ma che possono comunque essere utili per il processo di risoluzione;
12. **Attachment**: opzionalmente, sono facilmente allegabili file dal proprio computer per chiarificare la situazione;
13. **Add External Bug**: se si è a conoscenza del fatto che il bug è stato segnalato su altre piattaforme all'infuori di Red Hat Bugzilla (quali potrebbero per esempio essere le pagine Github, il sito dell'upstream oppure report relativi ad altre distribuzioni), si possono agganciare tali link esterni al nuovo report.

<img src="bugzilla_bugreport3.png" title="Stesura del bug-report." alt="Stesura del bug-report." width="600" />

Segnalazione di bug (tramite gnome-abrt)
----------------------------------------

**ABRT** – ovvero [Automatic Bug Report Tool](https://github.com/abrt/abrt/wiki/ABRT-Project) – è un software di interesse fondamentale per il miglioramento della qualità del sistema operativo Fedora. Esso intercetta gran parte dei crash che possono verificarsi durante l'utilizzo, facilitando la predisposizione di informazioni tecniche per la compilazione di un bug report.

Preinstallato all'interno dell'edizione Workstation, **gnome-abrt** è un comodo frontend grafico perfettamente integrato con Gnome e con i diversi ambienti desktop della distribuzione. In questa sezione esamineremo i passaggi significativi per una corretta segnalazione, assumendo che l'utente abbia già un profilo Red Hat Bugzilla attivo.

Può capitare che, durante l'esecuzione, un programma incorra in un errore e che quest'ultimo sia catturato dallo strumento descritto in questo capitolo, generando una notifica. In Gnome 3.16, tali avvisi appaiono per qualche secondo centralmente - in corrispondenza del lato superiore dello spazio di lavoro – e vengono poi raggruppati all'interno del calendario.

<img src="gnomeabrt_1notify.png" title="fig:Notifica di ABRT all&#39;interno di Gnome" alt="Notifica di ABRT all&#39;interno di Gnome" width="200" /> <img src="gnomeabrt_2notify.png" title="fig:Testo notifica completo" alt="Testo notifica completo" width="200" /> <img src="gnomeabrt_3notify.png" title="fig:Rilevazione crash da parte di ABRT elencata assieme alle altre notifiche di Gnome" alt="Rilevazione crash da parte di ABRT elencata assieme alle altre notifiche di Gnome" width="600" />

Un semplice click sul tasto **segnala** – oppure sull'icona dell'apposita applicazione, contrassegnata da un'allarme – consente all'utente di raggiungere la **schermata principale di ABRT**.

<img src="gnomeabrt_4icon.png" title="fig:Icona di gnome-abrt da Gnome Shell." alt="Icona di gnome-abrt da Gnome Shell." width="200" /> <img src="gnomeabrt_10problemdetails.png" title="fig:Dettagli di un problema rilevato da ABRT" alt="Dettagli di un problema rilevato da ABRT" width="200" /> <img src="gnomeabrt_5problemlist.png" title="fig:Schermata principale di gnome-abrt" alt="Schermata principale di gnome-abrt" width="600" />

In seguito al primo avvio, conviene salvare le proprie credenziali per il **login automatico su Bugzilla**, per evitare di doverle scrivere ripetutamente. Per fare ciò, occorre navigare all'interno del menu di ABRT – su Gnome, accessibile selezionando l'icona presente nel pannello superiore – e scegliere l'elemento **Preferenze**. Nella scheda **Eventi**, è quindi possibile individuare la voce relativa alla piattaforma di Red Hat. È sufficiente completare la configurazione di base, inserendo **Nome utente** e **Password**.

<img src="gnomeabrt_8bzaccount3.png" title="fig:Configurazione evento Bugzilla" alt="Configurazione evento Bugzilla" width="200" /> <img src="gnomeabrt_9bzaccount4.png" title="fig:Inserimento credenziali Bugzilla" alt="Inserimento credenziali Bugzilla" width="200" /> <img src="gnomeabrt_6bzaccount1.png" title="fig:Menù di ABRT" alt="Menù di ABRT" width="600" />

All'interno della schermata principale, il tasto blu **Riporta**, permette di costruire il report vero e proprio. In seguito all'azionamento di tale bottone, verranno raccolte tutte le informazioni, grazie anche ad un'eventuale installazione di pacchetti aggiuntivi per il debugging. Lo stack trace può essere inviato ai server di Fedora per permettere ai manutentori di disporre di più dati utili. Anche se una ricerca via browser all'interno di Bugzilla è sempre raccomandata, in questa fase, ABRT è potenzialmente in grado di riconoscere se un bug simile è già stato segnalato. In quest'ultimo caso, l'utente sarà aggiunto alla rispettiva **CC list** e riceverà novità via mail in caso di sviluppi futuri.

<img src="gnomeabrt_11problemalreadyreported.png" title="fig:Problema già noto" alt="Problema già noto" width="200" /> <img src="gnomeabrt_13analyze2.png" title="fig:ABRT analizza il problema" alt="ABRT analizza il problema" width="200" /> <img src="gnomeabrt_12analyze1.png" title="fig:Invio dello stack trace" alt="Invio dello stack trace" width="600" />

La descrizione dell'evento problematico è il fulcro dell'intero processo. Per una corretta stesura, si consiglia la lettura del capitolo precedente, relativo alle segnalazioni via web.

<img src="gnomeabrt_14analyze3.png" title="Testo della segnalazione" alt="Testo della segnalazione" width="600" />

L'ultimo passaggio riguarda gli allegati. La scelta dipende sostanzialmente dalla caratteristica del componente; per esempio, in presenza di software di sistema, possono risultare utili variabili relativi all'ambiente. È sempre consigliabile optare *almeno* per **core\_backtrace**, **backtrace**, **comment** e **reason**. È bene ricordare che, con un semplice click, si ha l'opportunità di rivedere il contenuto di tali file. In caso di dubbio, si consiglia di selezionare più elementi possibili, per evitare di tralasciare dettagli importanti.

<img src="gnomeabrt_15analyze4.png" title="Scelta degli allegati" alt="Scelta degli allegati" width="600" />

In seguito alla conferma, ABRT provvederà all'apertura vera e propria del report all'interno di Red Hat Bugzilla ed evidenzierà all'utente il relativo codice identificativo, per una successiva consultazione tramite browser.

All'interno del sommario, è possibile reperire o modificare importanti dettagli, quali lo stato, l'assignee – ovvero la persona o il gruppo incaricati di risolvere la questione -, la versione di Fedora ecc. Nei giorni successivi alla segnalazione, converrà tenere monitorato il proprio indirizzo e-mail per poter rispondere prontamente alle eventuali richieste effettuate dai componenti del Fedora Project che interverranno.

<img src="bugzilla_mainpage.png" title="fig:Home Page di Bugzilla" alt="Home Page di Bugzilla" width="200" /> <img src="gnomeabrt_16reportedbug1.png" title="fig:Dettagli relativi al report" alt="Dettagli relativi al report" width="200" /> <img src="gnomeabrt_17reportedbug2.png" title="fig:Descrizione del report" alt="Descrizione del report" width="600" />

Flags relativi ad un bug-report
-------------------------------

In seguito all'intervento del manutentore del pacchetto interessato dal report dell'utente, oppure di un membro qualificato del Fedora Project, è possibile che venga variato lo stato – flag – dell'intera segnalazione. Per una lista comprensiva, e per comprendere l'intero ciclo di vita di un bug, si consiglia la lettura della pagina [BugStatusWorkflow](https://fedoraproject.org/wiki/BugZappers/BugStatusWorkFlow). Di seguito, si riportano e descrivono le principali etichette che possono essere applicate:

1.  **NEW**: stato primitivo di un report, assegnato automaticamente dal sistema appena esso viene riportato da un utente;
2.  **NEEDINFO**: flag assegnato per sottolineare la richiesta di un addetto, indirizzata ad uno o più partecipanti alla segnalazione. Esso sta ad evidenziare il fatto che, per proseguire nello studio del caso, l'assignee - persona che lavora alla risoluzione - ha bisogno di informazioni specifiche da un utente o da un altro operatore;
3.  **ASSIGNED**: utile per i manutentori, può essere utilizzato per assegnare il bug ad uno specifico membro di un gruppo. Una segnalazione, per esempio, che involve un componente del desktop Plasma, può inizialmente essere assegnata al KDE SIG. Successivamente, tale team ha poi la facoltà di incaricare una sola figura per la risoluzione;
4.  **MODIFIED**: tale etichetta viene usata quando una patch è pronta ed è stata inserita nei sistemi utilizzati dai manutentori, ma non è ancora presente nel pacchetto interessato;
5.  **VERIFIED**: il bug ha un fix confermato, reso finalmente disponibile in una successiva versione del pacchetto di riferimento. Tale nuova edizione, sta per entrare a far parte di un repository di test di Fedora. Workaround non ufficiali o patch manuali non applicate al componente non sono degne di nota per considerare una segnalazione come "*verified*";
6.  **ON\_QA**: il pacchetto aggiornato per sistemare la problematica riscontrata è stato inserito nel repository updates-testing. L'utente che ha segnalato il problema è invitato a provare l'aggiornamento e partecipare al processo di rilascio lasciando il proprio karma (commento, feedback) nel sistema [Bodhi](https://bodhi.fedoraproject.org/). Se la nuova versione riceverà un adeguato riscontro, oppure supererà un certo lasso di tempo senza evidenziare nuovi bug, allora essa verrà certificata come stabile;
7.  **CLOSED**: condizione applicabile ad un report chiuso perchè scartato oppure perchè risolto:
    1.  **CLOSED ERRATA**: il bug è stato risolto e incluso in un nuovo pacchetto del repository updates. “Errata” va utilizzato per una Fedora “Branched” (una versione 'numerata', come Fedora 22, ossia non una Rawhide);
    2.  **CLOSED RAWHIDE**: identica alla condizione precedente, ma in questo caso il nuovo pacchetto raggiungerà solamente i repository Rawhide;
    3.  **CLOSED NEXTRELEASE**: utilizzata quando il bug è stato risolto, ma il nuovo pacchetto verrà incluso in una versione Fedora successiva a quella della segnalazione;
    4.  **CLOSED INSUFFICIENT\_DATA**: il report viene chiuso a causa della mancanza di dati fondamentali o dell'insufficiente partecipazione dell'utente che l'ha aperto;
    5.  **CLOSED NOTABUG**: il problema viene chiuso perché non rappresenta un vero proprio difetto dal punto di vista software;
    6.  **CLOSED CANTFIX**: utilizzata sopratutto quando il software che possiede il bug proviene da sorgenti esterne non fa parte dei repository di Fedora;
    7.  **CLOSED WONTFIX**: tale etichetta viene applicata quando la versione di Fedora indicata nella segnalazione raggiunge l'End Of Life e non viene più mantenuta;
    8.  **CLOSED WORKSFORME**: utilizzata dal manutentore del pacchetto interessato, viene scelta quando una risoluzione viene confermata unilateralmente;
    9.  **CLOSED CURRENTRELEASE**: tale opzione viene indicata quando un bug viene scoperto all'interno della fase Alpha o Beta e risolto nel rilascio finale di Fedora;
    10. **CLOSED UPSTREAM**: usata dal manutentore del pacchetto quando ritiene che la problematica verrà risolta dall'upstream (ossia dal programmatore o dal gruppo che sviluppa il prodotto all'infuori di Fedora).

[Categoria:Progetto Fedora](Categoria:Progetto_Fedora "wikilink") [Categoria:Rilettura in corso](Categoria:Rilettura_in_corso "wikilink")
