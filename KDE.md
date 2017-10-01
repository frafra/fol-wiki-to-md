Panoramica su KDE
-----------------

La versione 4 del Desktop Environment KDE (per chi già non lo conoscesse), apporta diverse novità e migliorie sia sul piano tradizionale che su un piano innovativo.
Non si vuole contrapporre i due DE di riferimento dei sistemi Linux (Gnome e KDE), e non si vuole convincere nessuno ad usare l'uno o l'altro.
La scelta del Fedora Project è quella di utilizzare Gnome come DE predefinito ma per chi volesse avere anche KDE installato sul sistema questa guida si prefigge di aiutarlo all'installazione.

Innanzitutto KDE basa la propria architettura sulle librerie Qt4, altamente programmabili e per chi volesse saperne di più, possiamo riferirci a [questa sezione](http://techbase.kde.org/Development/Tutorials) dei tutorials KDE

Il look di KDE4 è decisamente innovativo, costituito da molti punti fondamentali:

1.  solid è la struttura che colloquia con l'hardware, avente API che offrono l'accesso all'hardware di sistema;
2.  kross è il punto di incontro tra KDE e vari linguaggi di programmazione;
3.  plasma è l'ambiente desktop, che offre la possibilità di utilizzare widgets aggiuntivi altamente configurabili per l'utilizzo di software o utilità direttamente dal desktop;
4.  oxigen è la parte grafica del sistema;
5.  phonon fornisce le api per interagire con qualsiasi riproduttore multimediale;
6.  dolphin è il nuovo file manager che,rispetto a konqueror, offre una migliorata usabilità;
7.  gwenview è il visualizzatore di immagini;
8.  kwin è il gestore degli effetti del desktop (simil-compiz).

Installazione di KDE
--------------------

Per installare KDE, basta yum:

`$ su -c 'yum groupinstall KDE'`

Al successivo riavvio, alla schermata di login, sarà possibile effettuare la scelta (casella in basso) tra Gnome e, appunto, KDE.

Configurazione di KDM
---------------------

Installando KDE, come dipendenza viene anche installato il proprio login manager, solo che non è attivato di default.
Per attivarlo, aprire un terminale e digitare:

`$ su -c 'nano /etc/sysconfig/desktop'`

Si aprirà un file vuoto, all'interno del quale si dovrà scrivere questa riga:

`DISPLAYMANAGER="KDE"`

ed al successivo riavvio, comparirà il display manager di KDE.

Per modificarne le impostazioni ed i temi, sarà sufficiente andare nel menù K --&gt; impostazioni di sistema e selezionare quelle "avanzate", poi "gestione degli accessi" ed infine il tab "tema".
Dalla stessa finestra, è possibile installare nuovi temi salvati in locale, oppure scaricandoli direttamente da [kde/look.org](http://www.kde-look.org/) ed installandoli automaticamente.
La gestione degli accessi consente di poter configurare KDM soddisfando al meglio le proprie esigenze.
Ad esempio voglio fare comparire una immagine utente (ove previsto) di mia scelta nella schermata del login, per cui scelgo il tab "utenti" e cerco la parte relativa all'immagine, seleziono il mio utente e premo il pulsante raffigurante l'immagine.
Mi verranno proposte alcune immagini che se non sono di mio gradimento, posso sostituire con una a piacere semplicemente premendo "sfoglia" e ricercandola nel filesystem.

Installazione lingua italiana
-----------------------------

Sovente capita di vedere utenti in difficoltà per la mancanza della lingua italiana, per porre fine al problema:

`$ su -c 'yum install kde-l10n-Italian'`

Installato il pacchetto, andare nella gestione degli accessi, come sopra descritto, e selezionare il tab "generale" impostando la lingua italiana.

Personalizzazione di KDE
------------------------

Lo strumento "principe" per la personalizzazione del DE è sicuramente "impostazioni di sistema", il quale può essere richiamato da terminale:

`$ systemsettings`

oppure da menù:

`menù K --> Impostazione di sistema`

Da questo pannello si ha accesso a tutte le più importanti e specifiche impostazioni di KDE.
Altra cosa importante è data dal fatto che alcune applicazioni per gnome non riportano un buon font se aperte in kde, per ovviare:

`su -c 'yum install kcm-gtk'`

Attivazione effetti desktop
---------------------------

Esistono due gestori degli effetti, per ciò che riguarda KDE:
Kwin e Compiz-fusion.
Per attivare kwin e gli effetti da esso supportati **bisogna avere attivato l'accelerazione video ed il 3D** mediante l'installazione dei drivers proprietari della propria scheda video in quanto le versioni free non sono ancora abbastanza "performanti".
Relativamente agli effetti predisposti dal tema KDE, per attivarli occorre digitare:

`$ systemsettings`

oppure da

`menù K --> Impostazione di sistema.`

Nel tab "Generale" selezionare la voce Desktop. Apparirà la maschera di configurazione specifica per il desktop, e la prima voce a sinistra è quella relativa agli effetti. Basta abilitarli per poi passare alle varie voci di configurazione (che vi lascio scoprire).
Se invece si vuole attivare gli effetti Compiz, bisogna tenere a mente che se si vuole utilizzare quelli del [repositorio compiz-fusion](Compiz-Fusion "wikilink"), **bisogna assolutamente disinstallare i pacchetti compiz provenienti da altre parti**, compresi i nativi Fedora. In questo paragrafo parliamo, invece, dei soli pacchetti provenienti dal Fedora Project e, per non dimenticarsi niente:

`$ su -c 'yum install ccsm emerald-themes compizconfig-backend-kconfig fusion-icon-qt  \`
`emerald compiz-fusion  libcompizconfig compiz-bcop compiz compizconfig-python \`
`compiz-fusion-extras  compiz-kde compiz-manager'`

A questo punto si è installato compiz (ricordarsi che è specifica per kde) e lo si può avviare o digitando:

`$ fusion-icon`

sul terminale, oppure selezionando fusion-icon dal menùK --&gt; Applicazioni --&gt; Sistema --&gt; Compiz Fusion Icon.
Comparirà una icona nel system tray che indica l'avvio di compiz.
Per attivare gli effetti anche al prossimo riavvio, bisogna andare in systemsettings (come detto in precedenza), selezionare il tab "avanzate" e, successivamente, "Avvio automatico", premere "aggiungi programma" e selezionare espandendo il gruppo "sistema", il programma "Compiz fusion-icon". Più facile a farsi che a dirsi.....
In alternativa, da linea di comando:

`$ ln -s /usr/bin/fusion-icon ~/.kde/Autostart/`

Usando i tasti del mouse sull'icona, si ha accesso alle impostazioni degli effetti.

Installazione widgets e google gadgets
--------------------------------------

I widgets sono quei programmi, generalmente di utilità, informazione o per il tempo libero, che si insediano sul desktop (si ricorda superkaramba, anche se il concetto è diverso), e possono essere realizzate da chiunque. Io mi occuperò solo di quelle di provenienza google e [kde-look.org](http://www.kde-look.org/).
Innanzitutto installare il supporto google-gadgets dai repo:

`$ su -c 'yum install kdebase-workspace-googlegadgets'`

Si è ora pronti per l'installazione di widgets provenienti sia da [kde-look](http://www.kde-look.org/) che da google:

1.  selezionare col tasto sinistro del mouse l'icona dei widgets in alto a destra sul desktop;
2.  selezionare "Aggiungi oggetti";
3.  selezionare "Installa nuovi oggetti";
4.  scaricare nuovi oggetti plasma (o google gadgets);

Nella maschera che appare, selezionare gli oggetti e installarli.
Infine l'attivazione avviene nella maschera principale selezionando il gadget e premendo "Aggiungi oggetto".

Installazione temi-icone-sfondi
-------------------------------

Per l'installazione di nuovi temi di icone (sempre da [kde-look](http://www.kde-look.org/)), occorre entrare in:

`$ systemsettings`

oppure da

`menùK--> Impostazioni di sistema.`

Nel tab "Generale" selezionare "Aspetto" e nel menù a sinistra "Icone".
Si vede in basso la voce "Scarica nuovi temi", si preme e si selezionano i temi di interesse. Al termine dell'installazione si troveranno le relative voci in elenco, pronte per essere applicate.
Parimenti, per l'installazione di schemi di colori, sempre da systemsettings --&gt; aspetto, selezionare l'icona dei colori, dopo di che digitare "Scarica nuovi schemi". Una volta installati, come in precedenza, sono pronti per la selezione.
Differentemente da quanto detto in precedenza, per poter installare nuovi sfondi, oltre ai metodi tradizionali, basta posizionarsi su un'area vuota del desktop e premere il tasto destro del mouse e nella finestra che appare premere "Ottieni nuovi sfondi", dopodichè la procedura è la medesima vista in precedenza.

[Categoria:Ambiente Desktop](Categoria:Ambiente_Desktop "wikilink")
