Introduzione
------------

**Nautilus** è il file manager (gestore dei file) ufficiale del desktop di Gnome, rilasciato nel 2001 e da allora in continuo sviluppo con nuove versioni, ultima delle quali la **3.6**, che vede un rimodernamento nel design, nuove modalità di ricerca (con l'introduzione di una visualizzazione filtrata di quanto digitato nella casella di ricerca all'interno di una cartella), e diverse altre caratteristiche. Tra le novità c'è anche la rimozione della possibilità di effettuare configurazioni quali la scelta di un *pattern* come sfondo per le cartelle in alternativa al bianco, o la possibilità di aprire una data estensione di file con un comando personalizzato, ed altre, che, se per certi versi possono risultare superflue (come la citata scelta di un *background* per le cartelle), per altri la novità può essere sinonimo di scomodità e forse anche problematicità.

Questa guida nasce dalla [discussione](http://forum.fedoraonline.it/viewtopic.php?pid=202930) aperta sul Forum di [*Fedora online*](http://www.fedoraonline.it/) e dedicata a Fedora 18, proponendosi di dettagliare meglio l'argomento, indicando quindi un metodo per [reintrodurre](#Implementazioni_per_la_versione_3.6_di_Nautilus "wikilink") funzionalità perse nella versione 3.6 di Nautilus, e in particolare il ripristino della voce [*Crea nuovo documento*](#Reintegrazione_della_voce_.22Nuovo_documento.22 "wikilink") nel menu che compare alla pressione del tasto destro del mouse all'interno di una cartella, ma anche la possibilità di inserire nello stesso menu l'accesso a [scripts personalizzati](#nautilus-action "wikilink"). Per una maggior completezza, andremo anche ad indagare alcune delle voci presenti nelle [preferenze](#Configurazione "wikilink") di Nautilus, e verrà proposta l'installazione di [programmi](#Programmi "wikilink") ed [estensioni](#Estensioni "wikilink") utili che aumentano l'usabilità della versione 3.6.

Configurazione
--------------

Partiamo quindi col dare un'occhiata alle preferenze di Nautilus, a cui è possibile accedere dal pannello superiore di *gnome-shell*, facendo click col tasto dx sulla voce *File* che compare quando la finestra di Nautilus è attiva, come mostrato in [*figura 1*](media:nautilus_3.6-fig_1.png "wikilink").

<img src="nautilus_3.6-fig_1.png" title="Figura 1. Preferenze di Nautilus 3.6" alt="Figura 1. Preferenze di Nautilus 3.6" width="420" />

Le impostazioni mostrate nelle successive *figure 2-6* sono personalizzabili, e non richiedono grossi commenti:

<img src="nautilus_3.6-fig_2.png" title="fig:Figura 2. Preferenze di Nautilus 3.6 - Scheda Viste" alt="Figura 2. Preferenze di Nautilus 3.6 - Scheda Viste" width="350" /> <img src="nautilus_3.6-fig_3.png" title="fig:Figura 3. Preferenze di Nautilus 3.6 - Scheda Comportamento" alt="Figura 3. Preferenze di Nautilus 3.6 - Scheda Comportamento" width="350" />
<img src="nautilus_3.6-fig_4.png" title="fig:Figura 4. Preferenze di Nautilus 3.6 - Scheda Visualizzazione" alt="Figura 4. Preferenze di Nautilus 3.6 - Scheda Visualizzazione" width="350" /> <img src="nautilus_3.6-fig_5.png" title="fig:Figura 5. Preferenze di Nautilus 3.6 - Scheda Colonne dell&#39;elenco" alt="Figura 5. Preferenze di Nautilus 3.6 - Scheda Colonne dell&#39;elenco" width="350" /> ![](grv_image_spacer_5px.png "fig:grv_image_spacer_5px.png")

Da notare solamente, nella scheda *Comportamento* ([*figura 3*](media:nautilus_3.6-fig_3.png "wikilink")), la scelta dell'azione da eseguire al click doppio (o singolo, a seconda di quanto scelto alla voce *Comportamento*, nella stessa scheda) di un file reso eseguibile: la scelta è stata impostata sulla diretta esecuzione; se fosse indicato di mostrare il file, esso verrebbe invece aperto con l'applicazione di *default* (predefinita) per la lettura dei files di testo, mentre, se si scegliesse di *Chiedere ogni volta*, si avrebbe un pop-up che interrogherebbe ogni volta sull'azione da eseguire, quale appunto l'esecuzione in un terminale o l'apertura come semplice file di testo o l'esecuzione normale. <img src="nautilus_3.6-fig_6.png" title="fig:Figura 6. Preferenze di Nautilus 3.6 - Scheda Anteprima" alt="Figura 6. Preferenze di Nautilus 3.6 - Scheda Anteprima" width="350" />

Per rendere eseguibile un file si può operare in due modalità:

1.  per via grafica, scegliendo la voce *Proprietà* nel menu del *click dx* sul file e andando nella scheda *Permessi* per selezionare la casella *Consentire l'esecuzione del file come programma*, in corrispondenza della voce *Esecuzione*;
2.  via terminale, con in comandi:

`$ cd /percorso_cartella_contenente_il_file_da_rendere_eseguibile`
`$ chmod +x ./file_da_rendere_eseguibile`

Programmi ed estensioni utili
-----------------------------

Di seguito si vogliono citare alcuni *programmi* che permettono di configurare ulteriormente Nautilus, oltre che alcune utili *estensioni* che ne aumentano la funzionalità, insieme anche a quella parte discussa nel citato [*topic*](http://forum.fedoraonline.it/viewtopic.php?pid=202930) che permette di superare alcune delle mancanze presenti nella versione 3.6, togliendo spazio ai rimpianti della precedente 3.4:

### Programmi

#### ***dconf-editor***

  
Le impostazioni indicate nella precedente sezione possono essere addizionate di ulteriori configurazioni tramite l'applicazione *dconf-editor*, che si installa con il comando:

`# yum install dconf-editor`

  
Avviando rapidamente il programma tramite la combinazione di tasti *Alt+F2* e successiva digitazione di *dconf-editor* e pressione del tasto *invio*, ci si trova davanti una finestra con un menu sulla sinistra. Andando a questo punto nel percorso *org--&gt;gnome--&gt;nautilus--&gt;preferences*, come indicato nella [*figura 7*](media:dconf-editor_Nautilus_preferences-fig_7.png "wikilink"), sarà qui possibile controllare ulteriori voci o ritrovare quelle che si sono settate precedentemente. La [*figura 7*](media:dconf-editor_Nautilus_preferences-fig_7.png "wikilink"), ad esempio, evidenzia la possibilità di scegliere dove aprire le nuove schede create all'interno di Nautilus, se dopo quella correntemente aperta (opzione predefinita) o alla fine di tutte le altre.

<!-- -->

  
<img src="dconf-editor_Nautilus_preferences-fig_7.png" title="fig:Figura 7. Preferenze di Nautilus tramite dconf-editor" alt="Figura 7. Preferenze di Nautilus tramite dconf-editor" width="420" />

<!-- -->

  
Il programma *dconf-editor* è utile anche per molteplici altre personalizzazioni del nostro desktop, come ad esempio la scelta di quali pulsanti mostrare nella barra del titolo delle finestre, e con quale ordine e posizione: la [*figura 8*](media:dconf-editor_gnome-shell_title_buttons-fig_8.png "wikilink"), mostra infatti come sia possibile, andando nel percorso *org--&gt;gnome--&gt;shell--&gt;overrides*, scegliere se mostrare il solo pulsante di chiusura o se mostrare anche quelli per il menu e/o la minimizzazione e/o la massimizzazione di una finestra aperta, oltre che decidere se posizionarli a destra o a sinistra. Nel caso specifico, riportato in [*figura 8*](media:dconf-editor_gnome-shell_title_buttons-fig_8.png "wikilink"), si vuole mostrare il solo pulsante di chiusura (*close*), posizionandolo a sinistra (i : posti alla destra di *close* danno questo effetto). Il percorso anzidetto (*org--&gt;gnome--&gt;shell--&gt;overrides*) vale quando è in uso [gnome-shell](http://doc.fedoraonline.it/Estensioni_di_Gnome-Shell), per cui questa impostazione sostituirà la preferenza settata invece nel percorso *org--&gt;gnome--&gt;desktop--&gt;wm--&gt;preferences*, mostrata in [*figura 9*](media:dconf-editor_title_buttons-fig_9.png "wikilink"):

<!-- -->

  
<img src="dconf-editor_gnome-shell_title_buttons-fig_8.png" title="fig:Figura 8. Configurazione dei pulsanti della barra del titolo delle finestre di gnome-shell tramite dconf-editor" alt="Figura 8. Configurazione dei pulsanti della barra del titolo delle finestre di gnome-shell tramite dconf-editor" width="420" />

<img src="dconf-editor_title_buttons-fig_9.png" title="fig:Figura 9. Configurazione dei pulsanti della barra del titolo delle finestre tramite dconf-editor" alt="Figura 9. Configurazione dei pulsanti della barra del titolo delle finestre tramite dconf-editor" width="420" /> ![](grv_image_spacer_5px.png "fig:grv_image_spacer_5px.png")

#### ***beesu***

  
Qualora si avesse l'esigenza, per qualche motivo, di eseguire un programma in modalità grafica con i diritti amministrativi, viene incontro il programma *beesu*, il quale fornisce un comando (*beesu*, appunto) che, anteposto ad un altro comando, esegue quest'ultimo da utente *root*, previa immissione della sua password. In questa maniera è possibile ad esempio aprire una finestra di Nautilus da *root* con il comando:

`$ beesu "nautilus /home"`

  
il che dà vantaggi se si sa cosa si sta facendo, ma in caso contrario può anche mettere a rischio l'integrità e la stabilità del sistema.

### Estensioni

#### ***nautilus-open-terminal***

  
Installabile per via grafica tramite il gestore di pacchetti, oppure tramite terminale attraverso il comando:

`# yum install nautilus-open-terminal`

  
Questa estensione fornisce l'opzione di apertura del percorso corrente di Nautilus in un terminale, al *click dx* del mouse ([*figura 10*](media:nautilus-open-terminal-fig_10.png "wikilink")), una possibilità molto utile, da integrare volendo con quella che segue.

<!-- -->

  
<img src="nautilus-open-terminal-fig_10.png" title="fig:Figura 10. Estensione nautilus-open-terminal" alt="Figura 10. Estensione nautilus-open-terminal" width="420" />

#### ***nautilus-terminal***

  
Dopo la sua installazione e il riavvio di Nautilus con *Alt+F2* seguito dall'immissione del comando *nautilus -q* (*invio*), aprendo Nautilus si vedrà un terminale integrato in maniera permanente che segue il percorso di navigazione tra le cartelle ([*figura 11*](media:nautilus-terminal-fig_11.png "wikilink")). Versioni precedenti di questa estensione prevedevano la presenza di un pulsante per chiudere ed aprire il *terminale integrato* al click, ma da diverso tempo questa, che era un'opzione tra le configurazioni dell'estensione è stata sostituita dalla pressione del *tasto F4*, come si può leggere sulla sua [*home page*](http://projects.flogisoft.com/nautilus-terminal/).

<!-- -->

  
<img src="nautilus-terminal-fig_11.png" title="fig:Figura 11. Estensione nautilus-terminal" alt="Figura 11. Estensione nautilus-terminal" width="420" />

#### ***nautilus-image-converter***

  
Utile per ruotare e ridimensionare al volo files immagine col semplice *click dx* sull'immagine selezionata e scelta della voce relativa nel menu contestuale.

<!-- -->

  
Si potrà installare questa estensione da terminale con il comando:

`# yum install nautilus-image-converter`

#### ***nautilus-cd-burner***

  
Permette di masterizzare su CD o DVD dei files trascinati e rilasciati (*drag-&-dropped*) nella cartella *burn:///* aperta in Nautilus, con successiva pressione del pulsante *Scrivi su disco*.

<!-- -->

  
Si installa da terminale con il comando:

`# yum install nautilus-cd-burner`

  
Sembra che ci siano però alcune funzionalità mancanti quali:

:\* impossibilità di chiudere il disco;

:\* impossibilità di aggiungere una sessione ad un disco aperto;

:\* impossibilità di masterizzare un CD audio;

:\* impossibilità di ordinare le tracce.

  
Tutto ciò non è stato testato, in quanto per la masterizzazione si possono usare programmi appositi, come per esempio \[<http://it.wikipedia.org/wiki/Brasero>| Brasero\].

#### ***nautilus-sendto***

  
Questa estensione fa comparire, nel menu contestuale di Nautilus, una voce per l'invio rapido di files attraverso gli accounts e-mail di \[<http://it.wikipedia.org/wiki/Evolution_(software)>| Evolution\] o \[<http://it.wikipedia.org/wiki/Mozilla_Thunderbird>| Thunderbird\], oppure ai contatti dei programmi di messaggistica istantanea come \[<http://it.wikipedia.org/wiki/Pidgin_(software)>| Pidgin\], \[<http://it.wikipedia.org/wiki/Gajim>| Gajim\], ecc.

<!-- -->

  
Si installa da terminale con il comando:

`# yum install nautilus-sendto`

#### ***nautilus-action***

  
Questa estensione offre invece la possibilità di aggiungere nuove azioni al menu del *click dx* del mouse in Nautilus, attraverso comandi o scripts da lanciare da un apposito sottomenu che è possibile anche personalizzare filtrandone la sua visualizzazione, rendendola permanente (come nel *primo esempio* che segue) o visibile alla sola selezione di una data estensione di file (come nel *secondo esempio* che segue). Prima di passare agli esempi pratici, si deve ovviamente installare la presente estensione attraverso il pacchetto *nautilus-action* a cui si può aggiungere, volendo, anche la relativa documentazione con il pacchetto *nautilus-action-docs*; si può aggiungere anche *nautilus-extensions*, un pacchetto che provvede alle librerie usate dalle estensioni di Nautilus. Tutto ciò può essere fatto come al solito per via grafica (tramite il gestore dei pacchetti) o via terminale, attraverso il comando:

`# yum install nautilus-action nautilus-action-docs nautilus-extensions`

  
Fatto ciò, il programma viene lanciato con il comando:

`$ nautilus-actions-config-tool`

  
Di seguito si elencano due esempi pratici:

##### ***Esempio - Reintegrazione della voce "Nuovo lanciatore"***

  
Da un po' di tempo è scomparsa la possibilità che veniva offerta di creare *nuovi lanciatori* di eseguibili sul *Desktop* (o *Scrivania*), ma questo non significa che non fosse sempre possibile farlo tramite *terminale*. Anche in questo caso, *nautilus-action* offre la possibilità di creare una scorciatoia nel menu del *click dx* del mouse all'interno di Nautilus, con la possibilità di creare un *nuovo lanciatore* non soltanto sul *Desktop* ma in qualunque cartella in cui si abbiano i permessi di scrittura o, facendo uso del citato comando [ *beesu*](#beesu "wikilink"), direttamente in qualunque cartella di sistema, come ad esempio */usr/share/applications*, cui fa riferimento la *Dash* di *gnome-shell*. Si veda quindi come procedere, con l'aiuto degli *screenshots*:

<!-- -->

  
<img src="fig_12-nautilus-action_azione.png" title="fig:Figura 12. nautilus-action - Nuovo lanciatore - Azione" alt="Figura 12. nautilus-action - Nuovo lanciatore - Azione" width="350" />

<img src="fig_13-nautilus-action_comando_beesu.png" title="Figura 13. nautilus-action - Nuovo lanciatore - Comando con beesu" alt="Figura 13. nautilus-action - Nuovo lanciatore - Comando con beesu" width="350" />

  
<img src="fig_14-nautilus-action_comando_nobeesu.png" title="fig:Figura 14. nautilus-action - Nuovo lanciatore - Comando senza beesu" alt="Figura 14. nautilus-action - Nuovo lanciatore - Comando senza beesu" width="350" />

<img src="fig_15-nautilus-action_esecuzione.png" title="Figura 15. nautilus-action - Nuovo lanciatore - Esecuzione" alt="Figura 15. nautilus-action - Nuovo lanciatore - Esecuzione" width="350" />

  
<img src="fig_16-nautilus-action_nomi_di_base.png" title="fig:Figura 16. nautilus-action - Nuovo lanciatore - Nomi di base" alt="Figura 16. nautilus-action - Nuovo lanciatore - Nomi di base" width="350" />

<img src="fig_17-nautilus-action_tipi_mime.png" title="Figura 17. nautilus-action - Nuovo lanciatore - Tipi MIME" alt="Figura 17. nautilus-action - Nuovo lanciatore - Tipi MIME" width="350" />

  
<img src="fig_18-nautilus-action_cartelle.png" title="fig:Figura 18. nautilus-action - Nuovo lanciatore - Cartelle" alt="Figura 18. nautilus-action - Nuovo lanciatore - Cartelle" width="350" />

<img src="fig_19-nautilus-action_schemi.png" title="Figura 19. nautilus-action - Nuovo lanciatore - Schemi" alt="Figura 19. nautilus-action - Nuovo lanciatore - Schemi" width="350" />

  
<img src="fig_20-nautilus-action_capacità.png" title="fig:Figura 20. nautilus-action - Nuovo lanciatore - Capacità" alt="Figura 20. nautilus-action - Nuovo lanciatore - Capacità" width="350" />

<img src="fig_21-nautilus-action_ambiente.png" title="Figura 21. nautilus-action - Nuovo lanciatore - Ambiente" alt="Figura 21. nautilus-action - Nuovo lanciatore - Ambiente" width="350" />

  
<img src="fig_22-nautilus-action_proprietà.png" title="fig:Figura 22. nautilus-action - Nuovo lanciatore - Proprietà" alt="Figura 22. nautilus-action - Nuovo lanciatore - Proprietà" width="350" />

<img src="fig_23-nautilus-action_nuovo_lanciatore.png" title="fig:Figura 23. nautilus-action - Nuovo lanciatore" alt="Figura 23. nautilus-action - Nuovo lanciatore" width="350" /> ![](grv_image_spacer_5px.png "fig:grv_image_spacer_5px.png")

  
Lanciato il programma con l'anzidetto comando *nautilus-actions-config-tool*, si aggiunge una nuova voce cliccando sul + inscritto nel rettangolo in alto a sinistra, che attiverà la scheda *Azione* ([figura 12](media:fig_12-nautilus-action_azione.png "wikilink")), dove sarà possibile:

-   impostare il nome della voce da far comparire nel menu;
-   scegliere se visualizzare la voce alla selezione di un file e/o al *click dx* in uno spazio vuoto della cartella di Nautilus, nel solo menu contestuale e/o nel menu che compare alla pressione del pulsante in alto a dx di Nautilus (dove compaiono ad esempio anche le voci per l'apertura di una nuova scheda);
-   scegliere un'icona da associare al comando da mostrare nel menu.

<!-- -->

  
Nella [figura 13](media:fig_13-nautilus-action_comando_beesu.png "wikilink") è mostrata la scheda *Comando*, dov'è possibile indicare il comando che, in questo caso specifico, permetterà di creare un nuovo lanciatore in una qualunque cartella di sistema, grazie ai diritti amministrativi forniti dal comando *beesu*; in alternativa, la [figura 14](media:fig_14-nautilus-action_comando_nobeesu.png "wikilink") mostra lo stesso comando ma senza *beesu*, con la possibilità quindi di creare il lanciatore solo nell'ambito della *home* dell'utente in uso.

<!-- -->

  
Nella [figura 15](media:fig_15-nautilus-action_esecuzione.png "wikilink") è rappresentata la scheda *Esecuzione*, dove andrà indicato il tipo di esecuzione del comando scelto nella scheda *Comando* precedente.

<!-- -->

  
Le *figure 16-22*, in questo caso, lasciano i valori predefiniti; l'[esempio che segue](#Esempio_-_Aprire_un_pdf_con_Adobe_Reader "wikilink"), diversamente, vedrà una specifica per la scheda *Nomi di base*.

<!-- -->

  
Salvato quindi il tutto con l'apposito pulsante in alto a sx, si può chiudere *nautilus-action*. Si può riavviare Nautilus con il comando *Alt+F2* seguito dalla digitazione del comando *nautilus -q* (*invio*), e riaprendo Nautilus si avrà la comparsa della voce *Nuovo lanciatore* nel sottomenu *Nautilus-Actions actions*, come mostrato in [figura 23](media:fig_23-nautilus-action_nuovo_lanciatore.png "wikilink").

##### ***Esempio - Aprire un pdf con Adobe Reader***

  
Nonostante Linux offra lettori di *pdf* leggeri e veloci come [*Evince*](http://it.wikipedia.org/wiki/Evince), è molto utile l'installazione di *Adobe Reader* per la visualizzazione di oggetti *3D* nel formato *U3D*, inseriti nel *pdf* per esempio tramite [*LaTeX*](http://it.wikipedia.org/wiki/LaTeX), mediante i pacchetti [*movie15*](http://www.ctan.org/tex-archive/macros/latex/contrib/movie15) o [*media9*](http://www.ctan.org/pkg/media9). Dopo l'installazione, *Adobe Reader* non compare nell'elenco dei programmi proposti per l'apertura di un determinato file (in questo caso il *pdf*) per renderlo ad esempio anche *predefinito*, ma si può risolvere aggiungendo una voce apposita al menu del *click dx* di Nautilus attraverso *nautilus-action*, voce che, in questo caso, diversamente dal [precedente esempio](#Esempio_-_Reintegrazione_della_voce_.22Nuovo_lanciatore.22 "wikilink"), non si vuole rendere permanente, ma visibile solo quando si esegue il *click dx* su un file con estensione *pdf*; di seguito si vedrà come, evidenziando solo le differenze rispetto all'esempio precedente:

<!-- -->

  
<img src="fig_24-nautilus-action_acroreader_azione.png" title="fig:Figura 24. nautilus-action - Apri con Adobe Reader - Azione" alt="Figura 24. nautilus-action - Apri con Adobe Reader - Azione" width="350" />

<img src="fig_25-nautilus-action_acroreader_comando.png" title="Figura 25. nautilus-action - Apri con Adobe Reader - Comando" alt="Figura 25. nautilus-action - Apri con Adobe Reader - Comando" width="350" />

  
<img src="fig_26-nautilus-action_acroreader_nomi_di_base.png" title="fig:Figura 26. nautilus-action - Apri con Adobe Reader - Nomi di base" alt="Figura 26. nautilus-action - Apri con Adobe Reader - Nomi di base" width="350" />

<img src="fig_27-nautilus-action_acroreader.png" title="fig:Figura 27. nautilus-action - Apri con Adobe Reader" alt="Figura 27. nautilus-action - Apri con Adobe Reader" width="350" /> ![](grv_image_spacer_5px.png "fig:grv_image_spacer_5px.png")

  
Nella scheda *Azione* ([figura 24](media:fig_24-nautilus-action_acroreader_azione.png "wikilink")), le impostazioni sono tali da permettere di mostrare la voce alla sola selezione di un file; in particolare, andando nella scheda *Nomi di base* ([figura 26](media:fig_26-nautilus-action_acroreader_nomi_di_base.png "wikilink")), si può applicare un filtro per il tipo di file selezionato, specificando che non debba essere un generico file, ma avere l'estensione *pdf*, in modo tale che solo al *click dx* del mouse sopra un *pdf* possa comparire nel menu la voce *Apri con Adobe Reader* al livello del sottomenu *Nautilus-Actions actions*. La [figura 25](media:fig_25-nautilus-action_acroreader_comando.png "wikilink") mostra invece il comando da eseguire, e nella [figura 27](media:fig_27-nautilus-action_acroreader.png "wikilink") il risultato finale, notando come, nella [figura 23](media:fig_23-nautilus-action_nuovo_lanciatore.png "wikilink") del precedente esempio, la voce era assente nell'elenco del menu, mentre ora compare perché appunto selezionato un *pdf*.

### Implementazioni per la versione 3.6 di Nautilus

  
Si è così arrivati alla parte conclusiva di questa guida, nata come si è detto dalla problematica [discussa](http://forum.fedoraonline.it/viewtopic.php?pid=202930) nel forum, che viene qui ripresa ed inserita per completare questa panoramica con tema la versione 3.6 di Nautilus. Si è parlato nell'[introduzione](#Introduzione "wikilink") delle novità di questa versione, ma anche di alcune mancanze che qui si è cercato di colmare. Rimane quindi da reintrodurre la possibilità di creare semplicemente un *Nuovo documento* dal menu contestuale del tasto destro del mouse all'interno di Nautilus.

#### ***Reintegrazione della voce "Nuovo documento"***

  
Esistono fondamentalmente due approcci, di cui uno estremamente semplice, efficace e versatile, e l'altro un po' più macchinoso ma comunque utile per lo scopo. Partendo dal primo:

##### ***Utilizzo della cartella Modelli (o Templates)***

  
Si tratta di sfruttare il fatto che, inserendo almeno un file nella cartella *Modelli* (o *Templates*, a seconda della lingua di sistema) della *home* dell'utente in uso, si abilita la comparsa di un sottomenu *Nuovo documento* nel menu contestuale di Nautilus, con in elenco la voce *Documento vuoto*, insieme al file inserito. Come ben proposto nella [discussione](http://forum.fedoraonline.it/viewtopic.php?pid=202930), un esempio di file da poter inserire nella cartella *Modelli* è la base per un *nuovo script*, da avere così a portata di mano, insieme alla voce *Documento vuoto*. In pratica, si tratta di aprire un *terminale* e dare i seguenti comandi:

:\* Nel caso si abbiano le cartelle in italiano:

`$ cd ~/Modelli`
`$ touch "Bash script"`

:\* Nel caso si abbiano le cartelle in inglese:

`$ cd ~/Templates`
`$ touch "Bash script"`

  
Il comando *touch* crea un file vuoto dal nome *Bash Script* nella cartella *Modelli* (o *Templates*) della *home* dell'utente in uso; le virgolette servono a permettere lo spazio nel nome attribuito al file; in alternativa si potrebbe scrivere:

:\* Nel caso si abbiano le cartelle in italiano:

`$ cd ~/Modelli`
`$ touch Bash\ script`

:\* Nel caso si abbiano le cartelle in inglese:

`$ cd ~/Templates`
`$ touch Bash\ script`

  
A questo punto si può come al solito procedere per via grafica o via terminale, per editare il file appena creato; da terminale ad esempio:

`$ gedit Bash\ script`

  
verrà quindi aperto il file con *gedit* e in esso, a questo punto, si può scrivere un semplice [Shabang](http://it.wikipedia.org/wiki/Shabang):

`#!/bin/sh`

  
Salvare il file, che si può successivamente anche rendere eseguibile con il comando:

`$ chmod +x Bash\ script`

  
In questa maniera, nel sottomenu *Nuovo documento* si avrà a disposizione la possibilità di creare sia un *Documento vuoto* sia la base per un *nuovo script* ([figura 28](media:fig_28-cartella_Modelli-Nuovo_documento.png "wikilink")).

<img src="fig_28-cartella_Modelli-Nuovo_documento.png" title="Figura 28. Cartella Modelli (o Templates) - Nuovo Documento vuoto" alt="Figura 28. Cartella Modelli (o Templates) - Nuovo Documento vuoto" width="420" />

##### ***Utilizzo di nautilus-python e python3-gi***

  
Come anticipa il titolo, in questo caso (alterativo al precedente) sarà necessario installare *nautilus-python* e *python3-gi*, insieme alle relative dipendenze per lo scopo. Procedere quindi da terminale con i seguenti passi:

<!-- -->

  
**a**.

`# yum install nautilus-python`

  
**b**.

<!-- -->

  
*python3-gi*, diversamente dal precedente, non è installabile come pacchetto, ma è reperibile sul web a [questo](http://repo.fedoramd.org/mirrors/cygwin/release/GNOME/python-gi/python3-gi/) indirizzo. Scelta la versione più recente, la si scarica come archivio *tar.bz2* e si estrae per via grafica (col doppio click sul file o dal menu contestuale sul file selezionato col *click dx*) o via terminale con il comando:

`$ tar xvjf python3-gi-3.4.2-2.tar.bz2`

  
Si otterrà una cartella *usr* con all'interno le sottocartelle *bin* e *lib*, per cui si può procedere dando il comando per copiare la cartella estratta (*usr*) nella cartella radice (/):

`# cp -r ./usr /`

  
**c**.

<!-- -->

  
Sul [sito](http://repo.fedoramd.org/mirrors/cygwin/release/GNOME/python-gi/python3-gi/) è riportato quel file [setup.hint](http://repo.fedoramd.org/mirrors/cygwin/release/GNOME/python-gi/python3-gi/setup.hint) che indica come requisiti:

<!-- -->

  
*requires: libcairo2 libgirepository1.0\_1 libglib2.0\_0 python3 python-gi-common python3-cairo girepository-GLib2.0*

<!-- -->

  
Per conoscere i pacchetti che forniscono quelle dipendenze, si può dare il comando:

`# yum provides libcairo2 libgirepository1.0_1 libglib2.0_0 python3 python-gi-common python3-cairo girepository-GLib2.0`

  
L'output del comando fornirà i pacchetti *python3-3.3.0-1.fc18.i686*, *python3-cairo-1.10.0-4.fc18.i686* e *python3-3.3.0-1.fc18.i686*, che si dovranno installare con i comandi:

`# yum install python3-3.3.0-1.fc18.i686`
`# yum install python3-cairo-1.10.0-4.fc18.i686`
`# yum install python3-3.3.0-1.fc18.i686`

  
**d**.

<!-- -->

  
Sempre da terminale, si crea una cartella con al suo interno un file nel seguente percorso:

`$ mkdir -p ~/.local/share/nautilus-python/extensions`
`$ gedit ~/.local/share/nautilus-python/extensions/nautilus-acme.py`

  
Apertosi il file *nautilus-acme.py* con *gedit*, copiare ed incollare in esso il seguente codice scritto in python:

`from os.path import join`
`from gi.repository import GObject, Nautilus`
`class Acme(GObject.GObject, Nautilus.MenuProvider):`
`   def __init__(self):`
`       pass`
`   def new_empty_file(self, menu, folder):`
`       with open(join(folder.get_uri().replace("`[`file://`](file://)`", ""), "Nuovo documento"), 'w') as f:`
`           f.write('')`
`       return`
`   def get_background_items(self, window, current_folder):`
`       AcmeMenuItem = Nautilus.MenuItem(`
`           name="Acme::NewEmptyFile",`
`           label="Crea file vuoto",`
`           tip="Crea un nuovo file vuoto"`
`       )`
`       AcmeMenuItem.connect('activate', self.new_empty_file, current_folder)`
`       return [AcmeMenuItem]`

  
**e**.

<!-- -->

  
Salvare e chiudere il file *nautilus-acme.py*, riavviando poi Nautilus sempre da *terminale* col comando:

`$ nautilus -q`

  
In questa maniera si vedrà comparire, nel menu contestuale del *tasto dx* del mouse all'interno di Nautilus, la voce *Crea file vuoto*, che genererà un file vuoto *Nuovo documento* nel percorso in cui si è ([figura 29](media:fig_29-nautilus-python-Nuovo_documento.png "wikilink")).

<img src="fig_29-nautilus-python-Nuovo_documento.png" title="Figura 29. nautilus-python &amp; python3-gi - Nuovo Documento vuoto" alt="Figura 29. nautilus-python &amp; python3-gi - Nuovo Documento vuoto" width="420" />

  
**f**.

<!-- -->

  
Se si volesse eliminare questa voce, basta semplicemente cestinare il file *nautilus-acme.py* e riavviare Nautilus, ovvero dare i comandi:

`$ rm ~/.local/share/nautilus-python/extensions/nautilus-acme.py`
`$ nautilus -q`

Riferimenti
-----------

-   [Nautilus su Wikipedia](http://en.wikipedia.org/wiki/Nautilus_(file_manager))
-   [Discussione sul Forum di Fedora OnLine](http://forum.fedoraonline.it/viewtopic.php?pid=202930)

<Categoria:Ambiente_Desktop>
