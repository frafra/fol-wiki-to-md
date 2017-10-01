Per chi è appena passato ad un nuovo sistema operativo libero, come Fedora, spesso si trova spiazzato dall'enorme quantità di pacchetti e programmi disponibili per l'archiviazione e la compressione dei file.
Un **utente proveniente dal sistema operativo MS Windows** sicuramente conoscerà il [formato Zip](http://www.info-zip.org/) e quasi sicuramente sarà venuto in contatto anche col [formato Rar](http://www.rarlab.com/). Inoltre, se è un utente un po' più smaliziato e già orientato al software libero, avrà anche conosciuto [7zip](http://www.7-zip.org/) ed il formato di archiviazione compressione di questo.
Proverò a fare un po' di chiarezza e a fornire delle informazioni basilari all'approccio di questi file.
Innanzitutto bisogna fare una netta distinzione tra: **archiviazione** e **compressione**:

-   **il primo è un procedimento di raccolta** di file o directory in un unico file facilmente trasportabile e trasferibile. Esattamente come avviene nella realtà: prendo dei fogli, ad esempio i miei appunti universitari, e li infilo in una cartellina per raccoglierli e portarmeli in giro. Di per se non vi è alcun guadagno di spazio, le dimensioni rimangono tali e quali, anzi lo spessore della mia cartellina può far risultare il tutto di un volume più grande;
-   **il secondo**, invece, **è un processo di compattamento** che permette di risparmiare spazio e peso tramite l'uso di vari algoritmi. Dall'esempio precedente: schiaccio la mia cartellina per eliminare l'aria presente tra i fogli e/o elimino i fogli doppi per ridurre il più possibile il peso ed il volume della mia cartella, in modo da portarla in giro più facilmente assieme ai miei libri.

Questi due concetti spesso si perdono di fronte alla presenza dei formati come Zip o Rar, in quanto sono formati sia di archiviazione sia di compressione. Perso questo concetto diventa facile confondersi e non capire la denominazione di alcuni file.
Fatta questa premessa, cercherò di presentare i più comuni formati di archiviazione e compressione che si possono trovare nel mondo del software libero e come utilizzarli in modo semplice e veloce da terminale.
In realtà, gli ambienti desktop più moderni come Gnome o KDE, tramite anche i rispettivi programmi *File Roller* o *Ark*, danno la possibilità di archiviare, comprimere, visionare, estrarre, aggiungere, togliere ecc. file o directory dai vari archivi in modo molto, molto, semplice con una comoda interfaccia grafica. Risulta però, a volte, utile avere uno specchietto ai principali comandi da impartire al terminale, per estrarre o archiviare file o directory.
Di seguito l'indice ordinato per "estensione", ricordo che in *bash* l'estensione di un file non indica il tipo di file, che è un carattere intrinseco del file stesso e che si può vedere con il comando `file`, ne è solo una indicazione.

Installazione dei pacchetti necessari:
--------------------------------------

Fedora, come la maggior parte delle distro linux, fornisce già i pacchetti necessari per lavorare con i tipo di file citati, i programmi spesso sono già installati.
Se non presenti sul sistema si possono installare con yum. Eccezion fatta per unrar, sono tutti presenti nei repo ufficiali di Fedora:

`# yum install tar gzip bzip2 p7zip`

Per unrar è necessario avere installato ed abilitato i [repo rpmfusion non free](http://rpmfusion.org/), poi si può utilizzare yum:

`# yum install unrar`

Semplici archivi di file o directory ( .tar )
---------------------------------------------

I file con estensione `.tar` normalmente indicano semplici archivi di file o directory create con il [programma tar](http://www.gnu.org/software/tar/) e sono chiamati archivi tarball.

### Per creare un archivio tar

`$ tar cvf nome_archivio.tar directory/ # o si indica il nome di un file o di più file o di più directory`
`# oppure`
`$ tar cv directory/ > nome_archivio.tar # anche qui al posto di directory/ può essere come sopra`

Le due forme si equivalgono, la seconda utilizza semplicemente la re-direzione dello standard output di bash invece che utilizzare l'opzione interna di tar (`f`).

### Per estrarre un archivio tar

`$ tar xvf nome_archivio.tar`

### Per vedere solo il contenuto di un archivio tar

`$ tar tvf nome_archivio.tar`

Di seguito la spiegazione delle opzioni usate precedentemente:

-   **c**: crea;
-   **x**: estrai;
-   **v**: verbose, fa vedere i file che sono processati, può essere omessa;
-   **f**: indica il nome dell'archivio.

Il manpage del comando tar spiega in modo più completo tutti gli altri comandi e opzioni disponibili.
Gli archivi tar, poi, vengono spesso compressi utilizzando altri comandi che tratterò di seguito.

Archivi o file compressi tipo .tar.gz, .tgz, .gz
------------------------------------------------

I file con estensione `.tar.gz` o `.tgz`, forma abbreviata, sono archivi tarball compressi utilizzando il [programma gzip](http://www.gzip.org/). I file con estensione `.gz` sono, invece, dei semplici file compressi, non sono degli archivi.
Da notare che la distribuzione [Slackware](http://slackware.it/) ha utilizzato il formato `.tgz` per distribuire i software da installare tramite `pkgtool`.

### Creare un archivio .tar.gz o .tgz o un file .gz

La creazione di un file .tar.gz o di un file .gz è identica, semplicemente il .tar.gz ha come partenza un archivio tar:

`$ ls`
`nome_archivio.tar`
`$ gzip nome_archivio.tar # se non è un archivio tar allora si fa la compressione di un semplice file`
`$ ls`
`nome_archivio.tar.gz`

In realtà si può **utilizzare** direttamente il comando **tar per creare un archivio compresso tar.gz**:

`$ tar cvfz nome_archivio.tar.gz directory/ # al posto di directory può esserci uno o più file`

L'opzione **z** specifica a tar di comprimere l'archivio usando gzip.

### Decomprimere un file .gz o un archivio .tar.gz

`$ ls`
`nome_archivio.tar.gz`
`$ gunzip nome_archivio.tar.gz`
`# oppure`
`$ gzip -d nome_archivio.tar.gz`
`$ ls`
`nome_archivio.tar`

Se si tratta di un semplice file con estensione .gz si avrà il file decompresso. Si può **decomprimere** ed estrarre l'archivio direttamente anche **con il comando tar**:

`$ tar xvfz nome_archivio.tar.gz`
`$ ls`
`directory`

### Vedere il contenuto dei un archivio .tar.gz

`$ tar tvfz nome_archivio.tar.gz`

Archivi o file compressi tipo .tar.bz2, .bz2
--------------------------------------------

I file con estensione `.tar.bz2` sono archivi tarball compressi utilizzando il [programma bzip2](http://www.bzip.org/). I file con estensione `.bz2` sono invece dei semplici file compressi.
L'uso base di bzip2 è praticamente uguale a gzip, cambia solamente il nome del programma da usare e, per quanto riguarda l'uso di tar, l'opzione da usare (si usa "j" invece di "z").

### Creare un archivio .tar.bz2 o un file .bz2

`$ ls`
`nome_archivio.tar`
`$ bzip2 nome_archivio.tar # se non è un archivio tar allora si fa la compressione di un semplice file`
`$ ls`
`nome_archivio.tar.bz2`

Con tar:

`$ tar cvfj nome_archivio.tar.bz2 directory/ # al posto di directory può esserci uno o più file`

L'opzione **j** specifica a tar di comprimere l'archivio usando bzip2.

### Decomprimere un file .bz2 o un archivio .tar.bz2

`$ ls`
`nome_archivio.tar.bz2`
`$ bzip2 -d nome_archivio.tar.bz2`
`$ ls`
`nome_archivio.tar`

Decomprimere con tar:

`$ tar xvfj nome_archivio.tar.bz2`
`$ ls`
`directory`

### Vedere il contenuto dei un archivio .tar.gz

`$ tar tvfj nome_archivio.tar.bz2`

Archivi compressi tipo .zip
---------------------------

I file con estensione `.zip` sono in genere archivi compressi zip, che è forse il formato più conosciuto tra gli utenti medi. Nei vari sistemi operativi liberi, come Fedora, il programma di riferimento è [zip](http://www.info-zip.org/).

### Creare archivi compressi con zip

`$ zip nome_archivio.zip file1 file2 # ecc. si può indicare anche un solo file`
`# oppure in caso di directory, usare il modo ricorsivo, aggiungere -r`
`$ zip -r nome_archivio.zip directory/ # si possono aggiungere altre directory o file`

### Decomprimere un file .zip

`$ unzip nome_archivio.zip`

### Vedere il contenuto di uno zip

`$ unzip -l nome_archivio.zip`

Archivi compressi tipo .rar
---------------------------

Il formato di compressione e archiviazione [rar](http://www.rarlab.com/) è proprietario. Se ne sconsiglia dunque l'uso per motivi, fondamentalmente, di carattere etico.
Come già detto, nelle distro Linux ed in particolar modo in Fedora, si può installare il comando unrar tramite l'installazione e l'abilitazione dei repository `rpmfusion-nonfree`.

### Creare un archivio compresso rar

Il comando unrar, principalmente, permette di decomprimere un archivio rar e/o di visionarne il contenuto. Se si vuole poter creare un archivio rar bisogna comprare il software o scaricare la versione con la licenza di prova a [questo indirizzo](http://www.rarlab.com/download.htm).

### Decomprimere un archivio rar

`$ unrar x nome_archivio.rar`

Estrae l'archivio nella directory corrente.

### Vedere il contenuto di un file rar

`$ unrar l nome_archivio.rar`

Archivi compressi tipo .7z
--------------------------

Il formato di compressione di [7zip](http://www.7-zip.org/) non è in realtà molto utilizzato, si preferisce, in genere, utilizzare il tar.gz o il tar.bz2.

### Creare un archivio compresso .7z

`$ 7z a -t7z nome_archivio.7z directory/ # si possono aggiungere file o directory`

### Decomprimere un archivio compresso .7z

`$ 7z x nome_archivio.7z`

Nel caso la directory corrente contenesse gli stessi nomi dei file che si stanno estraendo, 7z chiederà come si vuole procedere.

### Vedere il contenuto di un archivio compresso .7z

`$ 7z l nome_archivio.7z`

Conclusione
-----------

Tutti i programmi/comandi citati contengono altre opzioni utili per lavorare con i vari formati di compressione e archiviazione.
Sul web si possono trovare decine e decine di guide sul loro uso e di seguito elencherò solo alcuni articoli che credo possano essere utili ad avvicinarsi a questi formati di archivio.
Come si può vedere, forse il comando che fa davvero da padrone su tutti è `tar` con il quale si possono creare archivi e comprimerli come si preferisce. Volendo anche `7z` può essere utilizzato per estrarre, creare e comprimere directory o file in formato sia 7zip che zip, bzip, bzip2 o tar.
Ognuno poi prenderà famigliarità con il comando ed il formato di compressione che preferisce.

Riferimenti e documentazione utile
----------------------------------

-   Articolo pubblicato precedentemente su: [marionline.it](http://blog.marionline.it/linux/formati-di-compressione-e-decompressione-base/)
-   [Esempi del comando bzip](http://www.thegeekstuff.com/2010/10/bzcommand-examples/) (inglese)
-   [Esempi uso del comando tar](http://www.thegeekstuff.com/2010/04/unix-tar-command-examples/) (inglese)
-   [Linux formati di compressione e decompressione su terminale](http://antoniodeluci.wordpress.com/2006/12/21/linux-formati-di-compressione-e-decompressione-su-terminale/)
-   [Appunti di informatica libera - Archiviazione](http://appuntilinux.mirror.garr.it/mirrors/appuntilinux/a2/a231.htm#almltitle1175)

<Categoria:Sistema>
