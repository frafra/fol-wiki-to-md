\_\_TOC\_\_

Introduzione
------------

Le estensioni rappresentano la vera novità di Gnome Shell: esattamente come per Firefox, attraverso esse è possibile aggiungere funzionalità altrimenti non presenti nel sistema. Tutto ciò, va ricordato, senza necessità preliminari di installare pacchetti aggiuntivi (salvo rare eccezioni).
Per fare degli esempi, quindi, è possibile sia aggiungere un'icona per le previsioni meteo sulla barra superiore, esattamente come con i widget per gnome-panel, xfce e lxde, sia re-implementare l'effetto *Coverflow* fornito da compiz, alla pressione di alt-tab. Il tutto in pochi secondi e senza dover riavviare il sistema.

Lo scopo di questa guida, dunque, è di fornire un elenco dettagliato e aggiornato delle varie estensioni disponibili, presentandone gli effetti e gli eventuali pregi o difetti.

Case testing
------------

Allo scopo di testare le varie estensioni, anche su configurazioni di sistema diverse, è stata dunque creata una Live USB. La versione in uso, in linea di massima, verrà aggiornata quanto prima all'uscita di ogni nuova release.

La versione di fedora in uso per testare queste estensioni è:

<div class="center" style="width:auto; margin-left:auto; margin-right:auto;">
**Fedora 18 / Gnome 3.6 (25 marzo 2013)**

</div>
Repositories e siti
-------------------

In un mondo perfetto le estensioni sarebbero scaricabili e installabili tutte allo stesso modo, da un'unica fonte.
Sfortunatamente però non è così. L'utente si trova dunque, suo malgrado, a doversi barcamenare tra varie fonti e diversi metodi di installazione. Di seguito, un elenco dei repositories e siti da cui è possibile scaricare le estensioni recensite, con rispettivi metodi di installazione.

### Repo Ufficiale Fedora

I repository rappresentano il primo approccio per tutti coloro che vengono a contatto con le estensioni per la prima volta. Nei repo è possibile reperire un assortimento di estensioni di base, che non modificano radicalmente l'esperienza d'utilizzo.

-   Metodo di Installazione: Tramite Packagekit o Yum (il nome di base dei pacchetti è *gnome-shell-extension-\[nome estensione\]*).
-   Note: Le estensioni presenti nei repo passano per lo stesso processo di verifica e testing dei pacchetti di Fedora. Dunque non vengono aggiornate su base giornaliera, ma in base alla versione stabile rilasciata. In linea di massima, comunque, sono solitamente le più affidabili (o comunque le meno probabili che causino crash al sistema, date i controlli che subiscono).

La cartella di default di queste estensioni è */usr/share/gnome-shell/extensions*

#### A

**AlternateTab**

`yum install gnome-shell-extension-aternate-tab`

-   Descrizione: Ripristina il funzionamento classico di alt-tab, senza raggruppare le applicazioni
-   Commento: Indispensabile per i nostalgici di Gnome 2, ripristina alt-tab ad una modalità più familiare. Dal menù impostazioni (selezionabile solo tramite Extensions Shortcuts o dal menù impostazioni di un'altra estensione) è possibile impostare la visualizzazione delle anteprime, delle sole icone dei programmi o di un misto di entrambe. Inoltre è possibile selezionare se visualizzare le finestre di tutti i desktop o solamente quelle dello spazio attivo.
-   Note: In alternativa, sul [Sito ufficiale delle estensioni di GNOME-Shell](#Sito_ufficiale_delle_estensioni_di_GNOME_Shell "wikilink"), è disponibile [Windows Alt-Tab](https://extensions.gnome.org/extension/38/windows-alt-tab/) che ha la stessa identica funzione (salvo qualche lieve variazione grafica nel menù di configurazione).

**Applications Menu**

`yum install gnome-shell-extension-apps-menu`

-   Descrizione: Aggiunge a fianco al pulsante "attività" un classico menù applicazioni.
-   Commento: Solamente per nostalgici di gnome 2 o utenti che non si ritrovano con il nuovo menù applicazioni di Gnome Shell. A gusti.

**Automove Windows**

`yum install gnome-shell-extension-auto-move-windows`

-   Descrizione: Consente di impostare il workspace di default per ogni applicazione
-   Commento: Anche in questo caso, si tratta di un'estensione che va a gusti.
    Da un lato è utile non dover spostare le applicazioni ogni volta che le si carica, dall'altro può diventare scomodo, ad esempio, se si deve avviare solamente un'applicazione impostata per il workspace 5. In quel caso si avranno 4 desktop vuoti, un quinto con un unica applicazione, e un sesto nuovamente vuoto, rendendo così necessario spostarsi fino al workspace necessario. Il menù di impostazioni, comunque, permette di selezionare il numero di workspace, l'unico segreto è quello di non esagerare (ad esempio impostando un'applicazione per il workspace 25).

#### D

**Dock**

`yum install gnome-shell-extension-dock`

-   Descrizione: Aggiunge una barra dock a scomparsa, sul lato destro dello schermo, che clona il contenuto del dash.
-   Commento: Notevolmente migliorata dalle prime release, Dock consente di gestire le applicazioni del dash in modo veloce senza dover ricorrere per forza all'overview (l'andare in alto a sinistra su "attività"). Accorpata con qualche estensione per rimuovere il dash da quest'ultima, può indubbiamente cambiare in maniera radicale la modalità d'uso del sistema, a patto che l'estensione rimanga aggiornata e funzionante ad ogni nuova release di Gnome-Shell. Utile, ma opinabile.
-   Note: A differenza di quanto possibile con il dash nell'overview, qui non è consentito il riordino delle icone.

#### I

**Indic onscreen keyboard**

`yum install gnome-shell-extension-iok`

-   Descrizione: Aggiunge alla barra superiore un pulsante per abilitare o disabilitare la tastiera a schermo Indic
-   Commento: Indic è una tastiera a schermo per le lingue indoarie, quindi in sé non ha molta utilità per l'utente europeo. Tuttavia la completezza della tastiera virtuale (che a differenza di eekboard comprende i tasti funzione) e del layout inglese potrebbero renderla appetibile a qualche 'smanettone'. Ma è comunque un ipotesi alquanto remota. Inoltre da segnalare che, a differenza di eeekboard, non è possibile utilizzare indic come tastiera a scomparsa. La finestra rimane quindi indipendente (anche se preimpostata per essere sempre in primo piano).
-   Note: Nessun difetto particolare, tranne forse l'icona di stato che non è particolarmente integrata col tema di default.

#### M

**Monitor Status Indicator**

`yum install gnome-shell-extension-xrandr-indicator`

-   Descrizione: Aggiunge alla barra superiore un pulsante per gestire le impostazioni del monitor
-   Commento: Altra estensione semplicissima, permette di scegliere l'angolo di rotazione del monitor (normale, 90°. 180°. 270° gradi) e fornisce un collegamento rapido alla scheda "Schermo" nel pannello di controllo. Utile per chi abbia un monitor ruotabile o un netbook (a patto che scheda video e drivers supportino la rotazione, ovviamente).
-   Note: Da ricordare che la rotazione dello schermo non implica automaticamente la rotazione del touchpad / mouse, e che quindi potrebbe capitare di dover gestire un touchpad con gli assi invertiti. Da installare a patto che sia pronti a gestire le periferiche di puntamento in condizioni disagiate.

#### N

**Native Window Placement**

`yum install gnome-shell-extension-native-window-placement`

-   Descrizione: Cambia la disposizione delle finestre nell'overview, organizzandole a seconda della loro dimensione e della loro posizione sul desktop.
-   Commento: Con ogni probabilità, l'intenzione dell'autore/autrice è di fornire un overview che rispetti il posizionamento e la dimensione delle finestre sul desktop. Questo, però, rende l'organizzazione dell'overview meno ordinata, alle volte sovrapponendo le etichette delle finestre alle anteprime stesse. È sicuramente un estensione che va a gusti, ma niente di fondamentale.

#### S

**System Monitor**

`yum install gnome-shell-extension-systemMonitor`

-   Descrizione: Aggiunge nella parte sinistra della barra notifiche due grafici relativi all'uso di memoria e processore.
-   Commento: Per i fanatici del controllo è sicuramente un estensione interessante. Cliccando sui grafici è possibile visualizzare la scheda di "Risorse" di Gnome-system-monitor. Non molto comoda per computer dotati di processori multicore e multithread, in quanto il grafico è veramente troppo piccolo per poterci ricavare qualcosa (e a questo punto è meglio farsi una scorciatoia di tasti per avviare gnome-system-monitor). Anche qui, da valutare caso per caso.

#### W

**Windows Navigator**

`yum install gnome-shell-extension-windowsNavigator`

-   Descrizione: Consente di selezionare le finestre in overview tramite tastiera.
-   Commento: Utile in quanto aggiunge una funzionalità non presente, ma forse non comodissima. Una volta entrati nell'overview è possibile premere alt per visualizzare dei numeri a fianco alle preview delle applicazioni. Premendo il numero rispettivo viene dato focus alla finestra in questione. Stessa cosa è possibile fare con i workspace, sostituendo alt con ctrl (perciò ctrl+2 per il secondo workspace, ctrl+3 per il terzo, etc..). Dicevamo non comodissima, perchè a conti fatti è comunque più veloce cliccare col mouse sulla preview desiderata che premere alt, leggere i numeri e selezionare quello desiderato. Comunque, un'estensione che può avere la sua utilità, a patto di trovarsi a gestire un numero limitato di finestre per workspace.

**Workspace indicator**

`yum install gnome-shell-extension-workspace-indicator`

-   Descrizione: Aggiunge un selettore per i workspace dinamici sulla barra superiore
-   Commento: Estensione molto semplice, nessun fronzolo, fa esattamente quanto promesso. I workspace sono identificati per numero.

### Repo RpmFusion

Nei repository RpmFusion attualmente è presente una sola estensione, ovvero Weather Broadcast. Ciò ovviamente non preclude la possibilità che altre ne vengano aggiunte in futuro.

-   Metodo di Installazione: Lo stesso dei repo ufficiali (Packagekit o Yum), a patto ovviamente di avere [installato precedentemente i repo specifici](RPMFusion "wikilink").
-   Note: Anche qua vale la stessa precisazione fatta coi repo ufficiali.

**Weather Broadcast**

`yum install gnome-shell-extension-weather`

-   Descrizione: Aggiunge alla barra superiore un pulsante che visualizza condizioni meteo e temperatura.
-   Commento: Di certo non fondamentale, si tratta comunque di un'estensione utile ed altamente configurabile. Allo stato attuale è possibile aggiungere più località tra cui scegliere, impostare le unità di misura desiderate (pressione, temperatura e intensità del vento), scegliere la posizione del pulsante sul pannello (destra, sinistra, centro) e configurare l'aspetto generale del menu. Consigliata.

### [Sito ufficiale delle estensioni di GNOME Shell](https://extensions.gnome.org)

Il sito ufficiale di Gnome per le estensioni, per certi versi, ricalca la pagina degli addon per Firefox.
Aggiornato costantemente da centinaia e centinaia di sviluppatori, fornisce estensioni per tutti i gusti, complete di descrizione, commenti ed un'immagine esplicativa. Inoltre, attraverso di esso è possibile gestire le estensioni installate nel sistema e verificare la presenza di eventuali aggiornamenti (vedi [qua](https://extensions.gnome.org/local/)).

-   Metodo di Installazione: Ogni estensione ha una propria pagina. Cliccando sopra ad un "pulsante" di switch on/off, a patto di usare Firefox o Chrome, è possibile installare e abilitare le estensioni desiderate in pochi secondi, o disabilitarle se non volessimo usarle.
    Diverso discorso va fatto per la disinstallazione, al momento possibile solamente dalla [pagina di riepilogo](https://extensions.gnome.org/local/) delle estensioni installate.
-   Note: Differentemente dalle estensioni dei repo, queste vengono aggiornate costantemente. Questo ovviamente include sia release stabili che release beta.
    Inoltre, essendo un sito generico per tutte le distribuzioni che fanno uso di Gnome-Shell, è possibile che alcune estensioni non siano compatibili con Fedora.
    Si raccomanda, dunque, di leggere sempre attentamente descrizione e commenti per verificare eventuali incompatibilità o bug.

==== A ==== **Activities Configurator**([link](https://extensions.gnome.org/extension/358/activities-configurator/))

-   Descrizione: Consente di modificare funzionamento e aspetto del pulsante "Attività"
-   Commento: Non fondamentale, ma interessante. Una volta installata, sostituisce il pulsante "Attività" con un'icona del pacchetto Gnome. Cliccandoci sopra con il tasto destro è possibile modificare le opzioni. Si può modificare l'etichetta del pulsante o rimuoverla del tutto (sono supportate le lettere accentate), cambiare l'icona o rimuoverla, impostare la spaziatura per icona e etichetta, variare la sensibilità in millisecondi dell'hot-corner, rimuovere completamente l'hot-corner (Altamente sconsigliato) o il pulsante attività, impostare il colore di sfondo della barra superiore e l'eventuale trasparenza. Inoltre è una delle poche estensioni a disporre di un tasto "README". Può non essere utile, ma è consigliato provarla almeno una volta per capire se possa servire o no.
-   Note: Il menù di configurazione dispone di un pulsante "Rilevamento dei conflitti", per evitare che altre estensioni rubino la posizione sulla barra al pulsante attività.

**All-In-One Places** ([link](https://extensions.gnome.org/extension/299/all-in-one-places/))

-   Descrizione: Aggiunge alla barra superiore un pulsante per le cartelle preferite
-   Commento: Fornisce un funzionamento simile a quello dell'estensione Places Menu, ma con delle modifiche interessanti e una maggiore configurabilità. È possibile scegliere quali voci di menù visualizzare, se renderle collegamenti a tendina o già espanse, il numero di documenti recenti da visualizzare, la dimensione dell'icona, l'eventuale etichetta da visualizzare a fianco al pulsante, se posizionare il pulsante a destra o a sinistra, e altre impostazioni. Particolarmente utile se si deve aprire velocemente una posizione (sul sistema o remota) senza dover per forza passare da nautilus, o da una scorciatoia per avviarlo.
-   Note: Sfortunatamente, al momento l'estensione funziona solo con Gnome 3.4 (Fedora 17).

==== B ==== **Brightness Control** ([link](https://extensions.gnome.org/extension/231/brightness-control/))

-   Descrizione: Aggiunge alla barra superiore un menù per la regolazione della luminosità dello schermo (ove possibile)
-   Commento: Classico caso di un'estensione semplice ma fondamentale per molti.
    Tramite il suo pulsante è possibile cambiare in tempo reale la luminosità senza dover per forza entrare nel pannello di controllo o usare le combinazioni di tasti preimpostate. Particolarmente funzionale il fatto che sia stata ideata allo stesso modo dell'icona del volume, ragion per cui è possibile aumentare o diminuire la luminosità semplicemente posizionando il puntatore sull'icona e "scrollando" con la rotellina del mouse / touchpad. Inoltre il menù di configurazione consente di impostare la persistenza delle impostazioni anche in seguito al riavvio del sistema.
    Consigliata a chiunque abbia avuto noie con il controllo luminosità.
-   Note: Unica pecca, tramite persistenza non è possibile impostare un comportamento diverso a seconda che il sistema sia alimentato a batteria o a corrente (caso per il quale rimane necessaria la modifica di /etc/rc.d/rc.local)

==== C ==== **Caffeine** ([link](https://extensions.gnome.org/extension/517/caffeine/))

-   Descrizione: Aggiunge un pulsante alla barra superiore per abilitare o disabilitare il timeout di screensaver e autosuspend.
-   Commento: Considerato che alcuni programmi spesso non supportano correttamente la comunicazione con dbus per informare il sistema che sono attualmente in funzione, caffeine risulta spesso fondamentale per tutti quegli utenti che usano principalmente fedora per la visione / ascolto di file e flussi multimediali.
    Ma non solo. Tramite la gui di configurazione è possibile selezionare i programmi per i quali caffeine deve autoavviarsi senza richiedere intervento dell'utenza. Inoltre, caffeine non sovrascrive le impostazioni del sistema, garantendo così al riavvio che screensaver e autosuspend funzionino come prestabilito.
-   Note: Su gnome 3.4 (Fedora 17) c'è un bug riguardante le notifiche: ogni volta che caffeine entra in funzione, alla barra viene aggiunta un icona, che non si disabilita in automatico. Questo può portare la barra notifiche ad assumere una lunghezza spropositata. Il bug, comunque, non è presente in Gnome 3.6 (Fedora 18)

**Coverflow Alt-Tab** ([link](https://extensions.gnome.org/extension/97/coverflow-alt-tab/))

-   Descrizione: Sostituisce il task switcher di default (quello che appare alla pressione di alt-tab, appunto) con l'effetto coverflow di Compiz.
-   Commento: È un estensione difficile da inquadrare. Da un lato ha il pregio di essere molto gradevole a vedersi, ma dall'altro può scombussolare chi sia ormai abituato ad usare il task-switcher di default, soprattutto perchè non raggruppa in automatico le finestre provenienti da una stessa applicazione (anche se è possibile visualizzarle lo stesso premendo alt+tasto presente sopra il tab). Per il resto, la configurazione tasti rimane identica: tenendo premuto alt è possibile navigare tra le preview con le frecce direzionali. In più, premendo "q" (sempre con alt premuto) è possibile chiudere direttamente l'applicazione selezionata.
-   Note: L'effetto visivo può essere 'pesante' per il sistema, particolarmente per schede grafiche di nuova generazione prive di drivers abbastanza rodati (o per vecchi chip che proprio 'non ce la fanno')

==== D ==== **Desktop Scroller** ([link](https://extensions.gnome.org/extension/561/desktop-scroller-all-sides-for-gnome-36/))

-   Descrizione: Consente all'utente di cambiare velocemente spazio di lavoro, semplicemente azionando lo scroll del mouse / touchpad sui lati esterni dello schermo.
-   Commento: Oltre ad essere utile, può fungere da "boss-mode" consentendo di passare velocemente da un desktop all'altro senza bisogno di ricorrere all'overview o a più 'percettibili' combinazioni di tasti (ctrl+alt+frecce). È configurabile, direttamente da gnome-tweak-tool, per ognuno dei quattro lati dello schermo e funziona anche nell'overview.
-   Note: Non funziona su gnome 3.4, per il quale sono disponibili due diverse versioni, una per il lato destro [1](https://extensions.gnome.org/extension/136/desktop-scroller/) e una per il lato sinistro [2](https://extensions.gnome.org/extension/235/desktop-scroller-left-and-overview-version/) (non configurabili).

==== E ==== **Extensions Shortcuts** ([link](https://extensions.gnome.org/extension/525/extension-shortcuts/))

-   Descrizione: Aggiunge alla barra superiore un pulsante per gestione e configurazione delle estensioni di Gnome-Shell
-   Commento: Decisamente fondamentale per chi ama 'smanettare' con le estensioni. Il menù integrato permette di:

1.  collegarsi alla pagina delle estensioni installate in locale
2.  collegarsi ad extensions.gnome.org per cercare nuove estensioni
3.  aprire il menù di configurazione delle estensioni
4.  avviare gnome-tweak-tool
5.  aprire in nautilus la cartella delle estensioni
6.  riavviare la shell (ovvero alt+r)
7.  avviare looking glass.

==== F ==== **Favorites Menu** ([link](https://extensions.gnome.org/extension/115/favorites-menu/))

-   Descrizione: Aggiunge alla barra superiore un menù con i collegamenti alle applicazioni attualmente nel dash (ma solo le preferite)
-   Commento: Anche qui, una semplice aggiunta di valore meramente estetico. Fornisce le stesse funzioni dell'estensione Dock, tranne per il comportamento dei collegamenti. Infatti, cliccando sul collegamento di un programma già avviato, l'estensione non rimanda all'istanza attualmente in corso ma ne apre una nuova.
    Non fornisce collegamenti ai programmi attualmente in corso ma non presenti nei preferiti.
-   Note: Tra le opzioni c'è "use gnome-shell-extensions-prefs only". Settare quell'opzione significa che le preferenze non saranno più direttamente disponibili dal menù, ma solamente dal menù impostazioni generale delle estensioni (accessibile solo da gnome-tweak-tool o dall'estensione Extensions-Preferences)

==== G ==== **gTile** ([link](https://extensions.gnome.org/extension/28/gtile/))

-   Descrizione: Sintetizzando, consente di impostare lo spazio occupato da una finestra, sullo schermo, secondo una griglia.
-   Commento: Sicuramente più facile a vedersi che a dirsi. L'installazione aggiunge un pulsante alla barra superiore, alla cui pressione viene visualizzata una griglia. Selezionando un numero di riquadri, di questa griglia, è possibile dire al sistema di ridimensionare la finestra attualmente in focus di tanti riquadri quanti ve ne sarebbero se lo schermo fosse suddiviso secondo la suddetta griglia. Per cui, ad esempio, se la griglia fosse 4x4, selezionando solo i 4 riquadri centrali la finestra verrebbe ridimensionata al centro dello schermo, alta e larga esattamente metà dello spazio disponibile (non tenendo conto della barra superiore). Sono disponibili 4 diverse griglie di default (2x2, 3x2, 4x4, 6x6), un pulsante per suddividere equamente lo schermo in base al numero di finestre e un ultimo per dare un intero lato alla finestra attiva e suddividere le restanti sul lato opposto. Inoltre è possibile selezionare se chiudere automaticamente gTile una volta completato il ridimensionamento e se attivare l'animazione. Di utilità opinabile, rimane comunque una modalità di gestione delle finestre affascinante.
-   Note: Purtroppo, al momento le configurazioni di griglia personalizzate sono possibili solamente editando manualmente il file extension.js.
    Al momento l'estensione NON FUNZIONA con Gnome 3.6 (Fedora 18).

==== H ==== **Hide Top Bar** ([link](https://extensions.gnome.org/extension/545/hide-top-bar/))

-   Descrizione: Nasconde la barra superiore.
-   Commento: Semplice ma efficace. Una volta installata, senza necessità di riavviare la Shell, nasconde la barra superiore in tutte le modalità che non siano l'overview. È interessante notare come, nonostante la mancanza di barra e pulsante dedicato, l'hot corner in alto a sinistra rimanga inalterato. Utile a chi voglia recuperare spazio sul desktop.

==== I ==== **Icon Hider** ([link](https://extensions.gnome.org/extension/351/icon-hider/))

-   Descrizione: Aggiunge alla barra superiore un pulsante per nascondere/visualizzare le icone in essa presenti.
-   Commento: Utile estensione, che consente di scegliere quali elementi della barra superiore visualizzare. Funziona con ogni icona/menù/pannello/pulsante: è dunque possibile nascondere il menù utente, l'orologio, il pulsante attività, le icone del tray (volume, rete, accesso facilitato, bluetooth, layout di tastiera) ma soprattutto qualunque elemento aggiuntivo fornito da altre estensioni. Consigliata a chi non voglia perdere tempo a cercare più estensioni per nascondere ogni singolo elemento.
-   Note: Non esente da bug: una volta installata, l'estensione ha impostato di default la visualizzazione di tutte le icone disponibili, comprese quelle che erano state precedentemente disattivate, e stessa cosa è successa alla rimozione. Va comunque detto che per ripristinare la visualizzazione 'regolare' della barra è stato sufficiente riavviare la shell.

#### M

**Maximus** ([link](https://extensions.gnome.org/extension/354/maximus/))

-   Descrizione: Rimuove la barra del titolo dalle finestre massimizzate (e non solo).
-   Commento: Il tema predefinito di GNOME-Shell (Adwaita) si nota da subito per una peculiarità: la barra del titolo, nelle finestre, è decisamente più alta rispetto allo stile di Metacity / GNOME 2. Ora, ad alcuni questo può risultare comodo, ma ad altri (ad esempio gli utenti net/notebook, con limitato spazio desktop) meno. Maximus, risolve questo problema, nascondendo la barra del titolo su tutte le finestre che siano state massimizzate. Tramite il menù di configurazione, inoltre è possibile configurare lo stesso comportamento per le finestre massimizzate solo da un lato (ovvero, super+freccia destra e super+freccia sinistra) e quali finestre / applicazioni massimizzate, invece, decorare normalmente. Consigliato agli utenti net/notebook
-   Note: Ovviamente, se la barra del titolo è nascosta, si deve ricorrere ad altri metodi per spostare le finestre. In GNOME 3.6, questo è possibile di default tenendo premuti il tasto super (invece che ALT, come in precedenza) e il pulsante destro del mouse. Da segnalare che si tratta di un opzione configurabile tramite Gnome-Tweak-Tool.

==== P ==== **Panel Settings** ([link](https://extensions.gnome.org/extension/208/panel-settings/))

-   Descrizione: Consente di configurare le opzioni di visibilità della barra superiore.
-   Commento: L'installazione di questa estensione aggiunge al menù utente in alto a destra, delle opzioni di configurazione della visibilità della barra superiore. Più nel dettaglio, se visualizzare la barra normalmente, solo al passaggio del mouse o solo nell'overview, la posizione della suddetta (sopra o sotto), e l'eventuale trasparenza. Potrebbe essere utile, una volta risolti i numerosi conflitti (vedi sotto).
-   Note: Conflitti, si diceva. Innanzitutto, l'estensione non è ancora pienamente compatibile con GNOME 3.6, quindi l'installazione è possibile solamente scaricando l'estensione da [github](https://github.com/eddiefullmetal/gnome-shell-extensions) e decomprimendola nella cartella utente (il metodo classico dal sito delle estensioni, invece, fallisce clamorosamente). Inoltre, una volta installata, entra in conflitto con la nuova disposizione della barra notifiche, che viene così spostata di 3 centimetri in alto, non più attaccata al lato inferiore dello schermo ma in mezzo ad esso. Di conseguenza, non si consiglia l'installazione fino a che non sarà totalmente garantita la compatibilità con Fedora 18 (e GNOME 3.6 in generale)

**Places Status Indicator** ([link](https://extensions.gnome.org/extension/8/places-status-indicator/))

-   Descrizione: Aggiunge alla barra superiore un menù per le cartelle preferite
-   Commento: Semplice e senza fronzoli, fa esattamente quello che promette. Una versione più avanzata è All-In-One Places, decisamente più configurabile e dotata di un pulsante per la gestione del Cestino.
-   Note: Invece di posizionare l'icona a destra come la maggiorparte delle altre estensioni, Places Status Indicator la posiziona a sinistra, a fianco al pulsante attività. Si potesse scegliere dove tenerla (senza dover editare il file dell'estensione) sarebbe meglio.

**Pulseaudio Shortcuts** ([link](https://extensions.gnome.org/extension/109/pulse-audio-shortcuts/))

-   Descrizione: Aggiunge al pulsante del volume, nella barra superiore, un sottomenù per l'avvio rapido dei programmi di Gestione di Pulseaudio.
-   Commento: Estensione forse meno utile di quello che possa sembrare. Beneficia realmente solamente coloro che debbono barcamenarsi costantemente tra diverse periferiche audio e livelli di volume variabili. Rimane comunque un aggiunta interessante e altamente configurabile. I programmi attualmente supportati sono Pulseaudio Equalizer, Pulseaudio Volume Control (pavucontrol), Pulseaudio Preferences (paprefs), Pulseaudio Manager (paman), qpaeq (vecchia gui per l'equalizzazione di Pulseaudio) e Gstreamer-Properties
-   Note: Dalle opzioni è possibile disattivare i collegamenti ai programmi non attualmente installati.

==== S ==== **Sticky Notes** ([Link](https://extensions.gnome.org/extension/568/notes/))

-   Descrizione: Aggiunge al dash nell'overview, un pulsante per gestire note adesive.
-   Commento: Finalmente maturata al punto giusto rispetto alle versioni precedenti, l'estensione aggiunge alla lista applicazioni nel dash un pulsante che permette di creare, visualizzare e modificare piccole note adesive all'interno dell'overview (la cartella di default delle note è ~/.local/share/gnome-shell-notes). Si tratta pur sempre di un'estensione basilare, priva delle funzionalità avanzate di gnote o tomboy, ma può essere utile per salvare rapidamente brevi stringhe di testo. Consigliata.
-   Note: Lo scrolling non funziona ancora a dovere; una volta raggiunto il bordo inferiore l'immissione continua 'al di sotto' della nota. Va comunque segnalato che le funzioni taglia-copia-incolla (da tastiera) sono perfettamente utilizzabili. Compatibile solamente con GNOME 3.6 (Fedora 18) o superiori.

**Shade Inactive Windows** ([link](https://extensions.gnome.org/extension/650/shade-inactive-windows/))

-   Descrizione: Applica un effetto ombreggiato alle finestre inattive.
-   Commento: Altra funzione ereditata dal pesante ma pur sempre compianto Compiz, quest'estensione aggiunge un richiamo visivo alla finestra attiva, rendendo più scure tutte le finestre inattive. Particolarmente utile per chi ha impostato il focus al puntatore (invece che al click del mouse, come sarebbe di default). Difetta, purtroppo, di un menù di impostazioni (utile, ad esempio, per decidere dopo quanto oscurare la finestra, con quale livello di opacità, etc).

#### T

**Text Translator** ([link](https://extensions.gnome.org/extension/593/text-translator/))

-   Descrizione: Implementa una finestra di dialogo per effettuare traduzioni istantanee.
-   Commento: Quest'estensione si appoggia a Google translate o Yandex translate per effettuare traduzioni istantanee dei termini e delle frasi immesse dall'utente, senza necessità di avviare un browser. La finestra di dialogo è richiamabile usando il pulsante apposito nella barra superiore, oppure tramite macro. È possibile scegliere sia la lingua di origine che quella di destinazione (contestualmente alla disponibilità del provider di traduzione scelto). Le macro di default sono super-t per richiamare la finestra di dialogo, super-shift-t per tradurre direttamente dagli appunti e super-alt-t per tradurre da un testo selezionato (funzione che richiede l'installazione del pacchetto xclip, 45kb, disponibile nei repo Fedora). È infine possibile configurare l'estensione tramite un menù apposito. Ottima aggiunta per il sistema, andrebbe forse migliorata permettendo di aggiungere più providers di traduzione.
-   Note: Le impostazioni di default prevedono l'inglese come lingua d'origine e il russo come lingua di destinazione (e questo spiega l'uso di Yandex).

**Touchpad Indicator** ([link](https://extensions.gnome.org/extension/131/touchpad-indicator/))

-   Descrizione: Aggiunge alla barra superiore un icona per controllare i settaggi delle periferiche di puntamento (mouse / touchpad)
-   Commento: Estensione molto utile per chi deve passare velocemente da una periferica di puntamento all'altra, specie se su un portatile. Consente di disabilitare in automatico il touchpad non appena viene connesso un mouse. Inoltre, permette di scegliere il client di configurazione usato (xinput / synaptic / gconf).
-   Note: Non è esente da alcuni leggeri bug. Al riavvio può capitare, ad esempio, che l'icona di stato non sia aggiornata (sebbene il touchpad sia comunque disabilitato). Nulla di irrisolvibile, comunque.

**Trash** ([link](https://extensions.gnome.org/extension/48/trash/))

-   Descrizione: Aggiunge alla barra superiore un pulsante per la gestione del cestino.
-   Commento: Estensione semplice ma utile. Dal suo menù è possibile visualizzare il contenuto del cestino, svuotarlo o aprire la cartella in Nautilus. Manca solo di un menù di configurazione.
-   Note: Da segnalare che il pulsante rimane nascosto fino a quando nel cestino non è presente qualche file.

#### W

**Web Search Dialog** ([link](https://extensions.gnome.org/extension/549/web-search-dialog/))

-   Descrizione: Implementa una finestra di dialogo, richiamabile tramite macro, per effettuare ricerche nel web, con il browser di default.
-   Commento: Molto utile, permette di velocizzare di molto le operazioni di ricerca. Funziona sia che il browser sia gia in funzione che non (e in questo caso apre un'ulteriore scheda, senza rimpiazzare quelle già presenti). Le possibilità di configurazione sono elevatissime. È possibile impostare il motore di ricerca predefinito, aggiungerne di nuovi (richiamabili tramite l'immissione di parole chiave), aprire direttamente degli indirizzi, visualizzare i suggerimenti di ricerca, modificare la scorciatoia in uso, etc...
    Da segnalare il fatto che la finestra di dialogo sia direttamente a livello di shell (come ad esempio la finestra di alt+f2), quindi è visibile in qualunque caso.
-   Note: La scorciatoia di default (super+barra di spazio) può entrare in conflitto con quelle usate da altre estensioni. Fortunatamente è possibile modificarla nelle impostazioni (ad esempio con Alt+f3)

#### X

**Xmenusystem** ([link](https://extensions.gnome.org/extension/653/xmenusystem/))

-   Descrizione: Aggiunge nell'angolo in alto a sinistra, un menù con numerose opzioni di sistema.
-   Commento: Va dato atto che l'idea non è male. Tuttavia sembrerebbe male implementata, in quanto le opzioni fornite non sono nulla di particolarmente difficile da reperire (Dall'alto verso il basso: Dettagli del sistema, Aggiornamenti, Ubuntu Software Center, Pannello di controllo, Gnome Tweak tool, Monitor di sistema, Forza uscita, Spegni, Logout, Blocca lo schermo). Altamente opinable la scelta di inserire il pulsante per il software center di Ubuntu, senza fornire all'utente la possibilità di configurare quali voci far apparire e quali no. A conti fatti, un'estensione ancora acerba.

### [Il Blog di Finbarr P. Murphy](http://www.fpmurphy.com/gnome-shell-extensions/)

Sezione di un blog di un programmatore dedicata specificamente alle estensioni.

-   Metodo di Installazione: In questo caso, l'installazione va effettuata manualmente, scaricando i file desiderati dal sito e decomprimendoli all'interno della cartella estensioni nel profilo utente desiderato(~/.local/share/gnome-shell/extensions).
-   Note: Aggiornato regolarmente ma non frequentemente, le estensioni in esso presenti sono da considerarsi 'sperimentali'.

==== N ==== **No a11y** ([link](http://www.fpmurphy.com/gnome-shell-extensions/noa11y-3.6.0.tar.gz) - da installare manualmente)

-   Descrizione: Rimuove dalla barra superiore il pulsante per l'accesso universale
-   Commento: Esattamente quello che promette, niente di più niente di meno. Le opzioni di accesso universale rimangono comunque accessibili dal pannello di controllo
-   Note: Fornisce la stessa funzionalità dell'estensione "Remove Accessibility Icon" presente nei repo di Fedora. Con la differenza, però che allo stato attuale (19 gennaio) questa funziona, mentre Remove Accessibility Icon no.

==== R ==== **Remove User Menu Separators** ([link](http://www.fpmurphy.com/gnome-shell-extensions/removeusermenuseparators-3.6.0.tar.gz) - da installare manualmente)

-   Descrizione: Rimuove i separatori dal menù utente
-   Commento: Nessuna utilità, se non una semplice precisazione grafica. Rimuove dal menù utente in alto a destra, i tre separatori presenti (sopra e sotto "Impostazioni di sistema" e sopra "Spegni"). Comoda per risparmiare spazio.
-   Note: Curiosamente gli altri menu adiacenti (ad esempio "Volume") rimangono inalterati

==== S ==== **Start of week** ([Link](http://www.fpmurphy.com/gnome-shell-extensions/startofweek-3.6.0.tar.gz) - da installare manualmente)

-   Descrizione: Consente di cambiare il giorno di avvio della settimana, sul calendario nella barra superiore
-   Commento: Utilità dubbia, consente di impostare qualunque giorno da domenica a sabato, come primo giorno della settimana nel calendario, indipendentemente dalle impostazioni regionali. Manca di una gui per modificare agilmente le impostazioni.
-   Note: Per selezionare il giorno d'inizio settimana è necessario editare il file extension.js e modificare la riga "const START\_OF\_WEEK = \[n\]", dove \[n\] è il numero del giorno desiderato. "1" equivale a Domenica, "2" a Lunedì, "3" a Martedì e così via fino a "7", che è Sabato

==== W ==== **Weather** ([link](http://www.fpmurphy.com/gnome-shell-extensions/weather-3.6.0.tar.gz) - da installare manualmente)

-   Descrizione: Aggiunge alla barra superiore un pulsante per le condizioni meteo, temperatura, e previsioni fino a 5 giorni dopo.
-   Commento: Simile a Weather Broadcast (vedi [qui](#Repo_di_RpmFusion "wikilink")) ma radicalmente diversa, quest'estensione fa riferimento alle previsioni meteo del sito World Weather Online. Ragion per cui, per poterla usare è necessario avere una chiave API che ci identifichi all'interno del sito, ottenibile solamente con la registrazione del proprio indirizzo mail.
    Dalla sua ha comunque il fatto di poter disporre di ben 5 giorni di previsioni meteo. Sarebbe stata però più gradita una maggiore libertà d'uso. Scarsa configurabilità. Utile solo per coloro che necessitano di sapere le condizioni meteo con largo anticipo.
-   Note: Va comunque detto che non è difficile ottenere una chiave API con un indirizzo mail temporaneo (ad esempio da "10 minute mail") e che una volta verificato che l'indirizzo esista al momento della registrazione, la chiave diventa permanente.

Consigliate
-----------

Ovviamente, come s'è potuto vedere, ogni estensione può avere utilità diverse da caso a caso. Tuttavia, esistono alcune estensioni che, per le loro funzionalità, risultano vivamente consigliabili, se non altro per una questione di rapporto pregi-difetti. Di seguito un breve elenco delle estensioni consigliate per un utilizzo "classico" di GNOME-Shell:
\***Caffeine**

-   **Extensions Shortcuts**
-   **Places Status indicator** o **All-in-one Places**
-   **Sticky notes**
-   **Web Search Dialog**

Riferimenti
-----------

-   Pagina [FAQ](https://extensions.gnome.org/about/) del sito ufficiale delle Estensioni di gnome-shell.
-   [Blog](http://blog.fpmurphy.com/) di Finbarr P. Murphy.

[Categoria:Ambiente Desktop](Categoria:Ambiente_Desktop "wikilink")
