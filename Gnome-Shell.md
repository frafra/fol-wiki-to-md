Introduzione
------------

Quello che attualmente si vede come Gnome-shell non è, e non sarà, la versione finale; molte funzioni non sono attive in questo momento e verranno implementate solo strada facendo, il che ha permesso al team di Fedora di compiere un atterraggio morbido, in seguito anche all'esperienza e lo scotto pagato con l'uscita di KDE 4.0 qualche anno fa.
Di conseguenza la configurazione e i consigli che seguono sono da considerare per quello che Gnome è in questo momento.

**Concetti:** Gnome-shell è quello che si vede sullo schermo, la shell grafica appunto, attraverso la quale si comunica con l'hardware. Essa richiede, per funzionare correttamente, l'installazione dei driver video ed è scritta in C e Javascript. Se si dovesse presentare qualche problema, Gnome lo comunica all'utente e lancia direttamente la modalità *fallback*, una sorta di Gnome 2.x, per non dover rinunciare alla grafica.

Modalità Fallback
-----------------

<img src="Gnome_fallback.jpg" title="fig:Fallback: l&#39;ancora di salvataggio se non si ha l&#39;accelerazione grafica." alt="Fallback: l&#39;ancora di salvataggio se non si ha l&#39;accelerazione grafica." width="350" /> La modalità chiamata *fallback* è una sorta di ancora di salvataggio nel caso Gnome non riesca ad avviare correttamente gnome-shell e debba utilizzare il driver grafico generico. Per chi proviene da Gnome 2.x si troverà di fronte un desktop familiare, il pannello in alto contiene i menu *Applicazioni* e *Risorse* e quello in basso le aree di lavoro utilizzate.
Per utilizzare Gnome-shell invece si necessita dell'accelerazione grafica, controllare con il comando sottostante se è attiva o no:

`$ glxinfo | grep direct`
`direct rendering: Yes`

Se la risposta è un *sì*, allora il problema non è la scheda grafica, se invece la risposta è *No* si legga come installare i driver della propria scheda video in [ questa categoria](:Categoria:Schede_grafiche "wikilink").
Una volta installato il driver corretto, se ne avete realmente bisogno, al prossimo avvio del server X GNOME shell verrà avviato.

Alternative alla Modalità Fallback di Gnome3
--------------------------------------------

Probabilmente però, la soluzione di installare i driver per la scheda video potrebbe non essere la soluzione, se, come scritto sul [sito ufficiale del progetto GNOME](https://live.gnome.org/GnomeShell/FAQ#What_led_to_the_decision_to_make_3D_acceleration_a_requirement_for_GNOME_Shell.3F), la macchina su cui si sta tentando di utilizzare il sistema, ha più di 4-5 anni.
In parole povere gli sviluppatori invitano a cambiare desktop; se vi eravate affezionati al caro vecchio gnome 2.x potrebbe essere l'occasione di provare Mate, un fork migliorato di gnome2, già presente nei repo ed installabile così

`# dnf install @mate-desktop`

quindi un semplice logout e login nel nuovo DE.
Altrimenti, se volete provare Cinnamon, un fork che prende le tecnologie introdotte da gnome3, digitate questo da root:

`# dnf install cinnamon`

e al prossimo login potrete provare cinnamon come desktop.
Se ancora questi ambienti desktop non vi soddisfano potete provare i sempreverdi lxde, xfce, fluxbox, e molti altri...

Considerazioni
--------------

Fin da subito si nota che si ha di fronte un desktop apparentemente "sconosciuto", nessun legame con Gnome 2.x, ed è proprio questo che spiazza molti utenti in un primo momento. L'abitudine e l'essere tradizionalisti in questo caso possono giocare dei brutti scherzi, perchè dopo un po' di prove ci si convince che questa shell grafica è molto potente e quando avrà tutte le funzionalità si ricorderà Gnome 2.x soltanto con un sorriso sulle labbra, pensando ai "vecchi tempi".
Gnome 3 mira anche a far cambiare le abitudini all'utente, nel senso che porterà ad utilizzare molto di più le aree di lavoro, mentre fino ad ora si lavorava su massimo 2 o forse 3 e si gestiva il tutto con i pulsanti ad icona. L'utilizzo delle aree invece renderà la navigazione più veloce e la lettura più immediata (le finestre potranno rimanere aperte nelle varie aree spostandosi facilmente da un area all'altra con *Ctrl+Alt+freccia* su o giù).
Gnome-shell è altamente personalizzabile, e lo sarà ancor di più quando sarà a pieno regime. Chi conosce le basi dei fogli di stile CSS non troverà nessuna difficoltà nel modificarli a proprio piacimento; inoltre nascono sempre più molti temi ed [estensioni](Estensioni_di_Gnome-Shell "wikilink") ad hoc per personalizzarlo.

Principali novità
-----------------

### Hot corner

Esistono due cosiddetti *hot corner*, degli angoli del monitor che al passaggio del mouse eseguono una determinata azione.
Il primo, quello più importante, è in alto a sinistra, e farà apparire una seconda scrivania, se così la si può chiamare. Tutte le finestre aperte verranno ridotte a miniature, e a sinistra apparirà una barra di avvio veloce, chiamata **dock**, che si potrà personalizzare a seconda delle proprie esigenze. Sul lato della schermata a destra ci sono, appena visibili, due aree di lavoro, che si amplieranno permettendo all'utente di scegliere in quale area "dirigersi". Noterete, sopra le miniature aperte, due pulsanti: uno, il pulsante *Finestre* sarà più marcato, in quanto state visualizzando le miniature. Premendo sul pulsante *Applicazioni* si aprirà un elenco di icone di tutti i programmi grafici avviabili, disposti in ordine alfabetico. Nella parte destra è possibile selzionare le applicazioni per "attinenza", visualizzando solo quelle pertinenti a quell'ambito. <img src="Gnome_base.jpg" title="fig:Gnome-Shell come appare dopo l&#39;installazione del sistema" alt="Gnome-Shell come appare dopo l&#39;installazione del sistema" width="400" /> Il secondo "Hot Corner" è quello in basso a destra, che farà apparire in trasparenza una barra in basso, dove verranno visualizzati i messaggi di sistema, gli aggiornamenti disponibili, e sostanzialmente è la barra dalla quale si può gestire la chat.

### Aree di lavoro

Apparentemente le aree di lavoro sono soltanto due, ma in realtà sono infinite. Ogni qualvolta viene aperta una nuova area verrà aggiunta un'altra vuota, immediatamente utilizzabile. Lo switch da un'area all'altra è molto veloce e permette di tenere molte applicazioni aperte senza dover saltare da una all'altra tramite la riduzione ad icona.

### Centro di controllo

Per chi fino a ieri era gnomista puro questa è davvero una novità, d'ora in poi non solo KDE ma anche Gnome ha un suo centro di controllo, dal quale è possibile impostare lo schermo, tastiera, mouse, rete, ecc..
Di contro, siccome si può impostare lo schermo e il monitor da qui, il famoso system-config-display è stato definitivamente mandato in pensione. <img src="Gnome_utente.jpg" title="fig:Per far apparire la voce &quot;Spegni&quot; basta premere " alt="Per far apparire la voce &quot;Spegni&quot; basta premere " width="200" /> <img src="Gnome_sistema.jpg" title="fig:Il centro di controllo è molto intuitivo" alt="Il centro di controllo è molto intuitivo" width="250" />

### Spegnimento PC

Chi a questo punto vorrà fare una pausa e, nel menu utente, cliccando sul proprio nome, cerca il tasto "Spegni" avrà un'altra sorpresa: il tasto sembra mancare!
Invece c'è, premendo il tasto **<ALT>** la voce *Sospendi* cambia in *Spegni*. Cliccando sopra con il mouse appare la finestra di spegnimento/riavvio del PC. Si vedrà più avanti che esiste un'estensione che rende definitiva questa opzione.

### Servizi

Benchè non dipenda direttamente da Gnome, un'altra novità inserita su Fedora fin dalla versione 15 è il nuovo gestore di servizi *systemd*, che di fatto ha sostituito *system-config-services*, benchè quest'ultimo attualmente è ancora disponibile, per un adeguamento "soft" degli utenti al nuovo sistema. Di conseguenza cambia anche il modo di gestione dei servizi stessi. La sintassi è:

`# systemctl start/stop/status/enable/disable nome_servizio.service `

Si utilizza:

-   **start**: per attivare il servizio nella sessione corrente;
-   **stop**: per disattivare il servizio nella sessione corrente;
-   **enable**: per far sì di attivare il servizio ad ogni esecuzione del kernel;
-   **disable**: per disattivare l'avvio automatico del servizio;
-   **status**: per avere informazioni sul servizio richiesto.

È presente anche una GUI per systemd, installabile tramite:

`# dnf install systemd-ui`

ed eseguibile quindi con:

`# systemadm`

Gnome Tweak Tool
----------------

Un'altra novità che si noterà durante la navigazione è la mancanza dei pulsanti "massimizza/minimizza" e "chiudi a icona" nella barra superiore delle finestre; è presente solamente una grande "X" per chiudere la finestra.
È un concetto che risulta difficile da digerire, ma che orienta l'utente al pensiero che gli sviluppatori di Gnome si pongono come obiettivo: utilizzare le aree di lavoro e le funzionalità che si possono dare a mouse e tastiera per personalizzare il comportamento delle finestre. Questo obiettivo lo si può raggiungere facilmente dalle impostazioni di sistema, in cui si possono impostare delle combinazioni di tasti per la personalizzazione dei movimenti delle finestre, ma ancor di più è utile l'utilizzo di Gnome Tweak Tool, uno comodo strumento che si installa così:

`# dnf install gnome-tweak-tool `

<img src="Gnome-tweak-02.png" title="fig:Gnome Tweak Tool è davvero potente e non dovrebbe mancare sul proprio Desktop." alt="Gnome Tweak Tool è davvero potente e non dovrebbe mancare sul proprio Desktop." width="400" /> Una volta installato l'applicativo si trova in *Applicazioni &gt; Accessori &gt; Strumento di Personalizzazione*; è uno strumento che non solo permette di impostare il comportamento delle finestre, ma anche di cambiare caratteri, impostare le icone sul desktop e di variare il tema utilizzato. Molto altro verrà ancora aggiunto a questo tool con il progresso di GNOME3.

Alcune funzioni molto interessante aggiunte a Gnome Tweak Tool su Fedora 18 sono:

-   La possibilità di aggiungere i pulsanti Minimizza e Massimizza sulla Titlebar; è sufficiente spostarsi su *Shell &gt; Arrangement of buttons on the titlebar* e dal menu a tendina scegliere quali pulsanti visualizzare.
-   Scegliere un'azione per il Pulsante Power; utile specialmente sui notebook, dal menu *Shell &gt; Power button action* è possibile scegliere alla pressione del tasto power di spegnere lo schermo, ibernare, sospendere, spegnere il pc, oppure aprire una finestra interattiva per la scelta.
-   Cambiare il tema delle finestre; dopo aver scaricato i temi che preferiamo da [gnome-look](http://http://gnome-look.org/) e dopo averli copiati nella cartella utente */home/nomeutente/.themes* ( o /usr/share/themes/ per renderli usabili da tutti gli utenti del sistema) possiamo poi selezionarli da gnome-tweak trovandoli in *Tema &gt; Tema Gtk+*
-   Scegliere il tema scuro per le finestre; da *Tema &gt; Abilitare il tema scuro per tutte le applicazioni* e posizionarlo su ON.

Un'altra caratteristica molto interessante di Gnome Tweak Tool è la possibilità di impostare e personalizzare la visualizzazione dei caratteri per l'ambiente desktop gnome. Nel menu *Tipi di carattere* è possibile regolare le impostazioni di *Hinting* e *Antialisiang*, una possibile regolazione che rende una visualizzazione gradevole e uniforme è regolare *Hinting* su Slight e *Antialiasing* su Rgba. Naturalmente molto dipende dai caratteri scelti per il proprio desktop e le caratteristiche del proprio monitor.

Tramite questo strumento si potranno inoltre gestire le estensioni di Gnome-Shell, di cui si parlerà nel prossimo capitolo e in maniera più approfondita nella guida dedicata alle Estensioni Gnome Shell.

Estensioni Gnome-Shell
----------------------

Tra gli aspetti più innovativi di Gnome rientra sicuramente la facilità di personalizzazione. Le varie sezioni del Desktop, le icone, la barra ecc. si possono modificare semplicemente tramite i fogli di stile (CSS).
Inoltre esistono alcune estensioni, e nel tempo ce ne saranno sempre di più, che rendono il Desktop ancora più immediato nel suo utilizzo. Esse sono gestibili, oltre che da Gnome-Tweak-Tool visto in precedenza, anche da terminale.

Le estensioni attualmente disponibili possono essere viste e installate tramite il sito <https://extensions.gnome.org/> e molte di esse sono già presenti nel repo fedora, basta dare da terminale

`$ dnf search gnome-shell-extension`

per visualizzare tutte quelle installabili tramite dnf.

Rimandando l'analisi dettagliata delle estensioni nella guida \[Estensioni\_di\_Gnome-Shell Estensioni di Gnome-Shell\], di seguito vediamo alcuni approfondimenti su qualche estensione, che possono essere installate sia dal sito gnome, sia da repo Fedora:

### Alternative-status-menu

Con questa estensione si rende permanente la visualizzazione della voce "Spegni" nel menu utente, senza dover premere il tasto <ALT> come indicato precedentemente.

`# dnf install gnome-shell-extensions-alternative-status-menu`

### Places-menu

Per avere un accesso più veloce a Nautilus e alle cartelle nei segnalibri potrebbe essere utile avere un'icona sul pannello superiore che faccia da scorciatoia.

`# dnf install gnome-shell-extensions-places-menu`

### Application-menu

Con questa estensione è possibile avere un menu delle applicazioni installate direttamente nel pannello superiore, divise per categoria, in uno stile simile a gnome 2.x:

`# dnf install gnome-shell-extensions-apps-menu`

Rendere Gnome-Shell simile a Gnome 2.x
--------------------------------------

Per i più malinconici è disponibile anche un pacchetto che non fa del tutto dimenticare Gnome 2.x.

Si può installare semplicemente da terminale.
Per Fedora 15:

`# dnf install --nogpgcheck `[`ftp://ftp.tigress.co.uk/fedora/15/tigress-utils/i386/gnome-shell-frippery-0.2.8-1.noarch.rpm`](ftp://ftp.tigress.co.uk/fedora/15/tigress-utils/i386/gnome-shell-frippery-0.2.8-1.noarch.rpm)

per Fedora 16:

`# dnf install --nogpgcheck `[`ftp://ftp.tigress.co.uk/fedora/16/tigress-utils/i386/gnome-shell-frippery-0.3.9-1.noarch.rpm`](ftp://ftp.tigress.co.uk/fedora/16/tigress-utils/i386/gnome-shell-frippery-0.3.9-1.noarch.rpm)

per Fedora 17:

`# dnf install --nogpgcheck `[`ftp://ftp.tigress.co.uk/fedora/17/tigress-utils/i386/gnome-shell-frippery-0.4.1-1.noarch.rpm`](ftp://ftp.tigress.co.uk/fedora/17/tigress-utils/i386/gnome-shell-frippery-0.4.1-1.noarch.rpm)

per Fedora 18:

`# dnf install --nogpgcheck `[`ftp://ftp.tigress.co.uk/fedora/18/tigress-utils/i386/gnome-shell-frippery-0.5.2-1.noarch.rpm`](ftp://ftp.tigress.co.uk/fedora/18/tigress-utils/i386/gnome-shell-frippery-0.5.2-1.noarch.rpm)

Questo pacchetto installa sei estensioni, eventualmente attivabili anche singolarmente:

-   *Bottom Panel*: aggiunge un pannello inferiore, con funzionalità simili a quello di gnome 2.x;
-   *Shut Down Menu*: sostituisce la voce "sospendi" con "arresta", che apre una finestra con tutte le opzioni di spegnimento, sospensione e ibernazione (similmente all'estensione "Alternative-status-menu");
-   *Move Clock*: sposta l'orologio a destra;
-   *Panel Favorites*: aggiunge al pannello superiore le icone per avviare direttamente le applicazione preferite;
-   *Applications Menu*: sostituisce il tasto "attività" in alto a sinistra con un menu "applicazioni" come quello di gnome 2.x. L'hot corner in alto a sinistra può essere disattivato o no tramite opzione selezionabile con clic destro;
-   *Static Workspaces*: permette di avere un numero fisso di aree di lavoro.

<img src="Gnome_gnome2.jpg" title="Nostalgia di Gnome 2? No problem." alt="Nostalgia di Gnome 2? No problem." width="350" />

Il tutto si completa da Gnome Tweak Tool:

-   nella scheda "Scrivania", attivando tutte le opzioni così da avere disponibili le icone sul desktop;
-   nella scheda "Shell", selezionando "all" nell'opzione "Arrangement of buttons on the titlebar" così da non avere solo il tasto di chiusura nelle finestre delle applicazioni.

Altri esempi di personalizzazione
---------------------------------

Come già detto, di personalizzazioni se ne possono fare tantissime e per fortuna ognuno ha le sue preferenze. Vediamo di seguito alcuni esempi per dimostrare cosa si può ottenere con minimi sforzi.

### Ridimensionare icone applicazioni

Le icone del menu principale delle applicazioni sono decisamente grandi ed è possibile regolare la loro grandezza in maniera semplice andando a modificare il file */usr/share/gnome-shell/theme/gnome-shell.css*. Di seguito una personalizzazione delle dimensioni icone che risulta particolarmente gradevole su monitor 15,6' con risoluzione 1366x768

`# nano /usr/share/gnome-shell/theme/gnome-shell.css`

Dopo aver aperto il file cerchiamo (nell'editor di testo Nano premendo ctrl+W) l'intestazione **/\* Application Launchers and Grid \*/** modificandola in questo modo:

`# /* Application Launchers and Grid */`
`  .icon-grid {`
`      spacing: 30px;`
`      -shell-grid-horizontal-item-size: 85px;`
`      -shell-grid-vertical-item-size: 85px;`
`  }`
`  .icon-grid .overview-icon {`
`      icon-size: 72px;`
`  }`

Ora salvate, uscite dall'editor, premete ALT+F2 e scrivete **r** per ricaricare le impostazioni della shell con le nuove modifiche.

### Togliere icone sul pannello Gnome Shell

Un'altra personalizzazione potrebbe essere quella di voler togliere delle icone che non ci interessano dal pannello superiore di Gnome Shell. Per esempio si potrebbe voler togliere l'icona *accessibility menu* perché non la riteniamo utile, ma l'esempio si può applicare a qualsiasi altra icona presente. Vediamo come editare il file /usr/share/gnome-shell/js/ui/panel.js andando a cercare la riga **const PANEL\_ITEM\_IMPLEMENTATIONS**:

`# nano /usr/share/gnome-shell/js/ui/panel.js`

e per rimuovere l'icona commentiamo con i caratteri **//** le icone che non ci interessano per eliminarle dal pannello, in questo caso *a11y: imports.ui.status.accessibility.ATIndicator*

`# const PANEL_ITEM_IMPLEMENTATIONS = {`
`   'activities': ActivitiesButton,`
`   'appMenu': AppMenuButton,`
`   'dateMenu': imports.ui.dateMenu.DateMenuButton,`
`   //'a11y': imports.ui.status.accessibility.ATIndicator,`
`   'volume': imports.ui.status.volume.Indicator,`
`   'battery': imports.ui.status.power.Indicator,`
`   'lockScreen': imports.ui.status.lockScreenMenu.Indicator,`
`   'keyboard': imports.ui.status.keyboard.InputSourceIndicator,`
`   'powerMenu': imports.gdm.powerMenu.PowerMenuButton,`
`   'userMenu': imports.ui.userMenu.UserMenuButton`
`};`

### Cambiare tema delle finestre

A proposito di tema visto poco fa: la barra superiore delle finestre nello stesso colore (bianco/grigio) può non piacere, per cui si può anche colorarla. Inanzitutto è importante sapere che per la gestione di queste impostazioni è responsabile metacity; di conseguenza le modifiche applicate saranno mantenute anche se si cambia tema, proprio perchè il file è il seguente e vale per tutti i temi:
:
*/usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml*

Aprire il file e, dopo aver salvato una copia, andare alla sezione che si occupa dei colori della barra:

`# cp /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml.old`
`# nano /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml`

Nella prima parte si trovano le indicazioni per ''-- meaningfull constants --''

<constant name="C_border_focused" value="blend/#000000/gtk:bg[NORMAL]/0.6" />
<constant name="C_border_unfocused" value="blend/#000000/gtk:bg[NORMAL]/0.8" />
<constant name="C_border_attached_focused" value="blend/#000000/gtk:bg[NORMAL]/0.4" />
<constant name="C_titlebar_focused_hilight" value="gtk:base[NORMAL]" />
<constant name="C_titlebar_unfocused" value="blend/gtk:base[NORMAL]/gtk:bg[NORMAL]/0.4" />
<constant name="C_title_focused" value="blend/gtk:fg[NORMAL]/gtk:bg[NORMAL]/0.1" />
<constant name="C_title_focused_hilight" value="gtk:base[NORMAL]" />
<constant name="C_title_unfocused" value="blend/gtk:text[NORMAL]/gtk:bg[NORMAL]/0.9" />

Si possono identificare facilmente i valori per il bordo, la barra del titolo e del titolo stesso delle finestre. Si può impostare quello che più piace, come esempio è stato scelto un colore blu, che, se non è attiva la finestra diventi grigio con delle righe orizzontali.
La sezione d'esempio diventerebbe così:

<constant name="C_border_focused" value="#000064" />
<constant name="C_border_unfocused" value="#0052FF" />
<constant name="C_border_attached_focused" value="#000064" />
<constant name="C_titlebar_focused_hilight" value="#000064" />
<constant name="C_titlebar_unfocused" value="#0052FF" />
<draw_ops name="titlebar_fill_focused_alt">
`       `<gradient type="vertical" x="0" y="0" width="width" height="height">
`               `<color value="#6B6EAC"/>
`               `<color value="#000064"/>
`       `</gradient>
</draw_ops>
<constant name="C_title_focused_hilight" value="gtk:base[NORMAL]" />
<draw_ops name="titlebar_fill_unfocused">
`       `<gradient type="vertical" x="0" y="0" width="width" height="height">
`               `<color value="#7096E3"/>
`               `<color value="#0052FF"/>
`       `</gradient>
</draw_ops>

Riavviando Gnome-Shell (ALT+F2 &gt; r &gt; Invio) si avranno le finestre come indicato nell'immagine. <img src="Gnome-barra.jpg" title="fig:L&#39;esempio descritto farebbe apparire le finestre così." alt="L&#39;esempio descritto farebbe apparire le finestre così." width="350" />

Utile per comprendere Gnome-Shell è sicuramente una letta alla [documentazione del fedoraproject](https://fedoraproject.org/wiki/Features/Gnome3/it), che contiene anche vari link, tra cui quello alla documentazione ufficiale del progetto GNOME.

Riferimenti
-----------

-   [Blog di Murphy](http://blog.fpmurphy.com/)
-   [Timlau](http://fedora.rasmil.dk/blog/?p=238)
-   [Estensioni per Gnome Shell Frippery](http://intgat.tigress.co.uk/rmy/extensions/index.html)

[Categoria:Ambiente Desktop](Categoria:Ambiente_Desktop "wikilink")
