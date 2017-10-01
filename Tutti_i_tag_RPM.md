Introduzione
------------

In questa guida si vuole illustrare come scaricare i file e come usarli per avere tutte le informazioni sui vari pacchetti RPM sempre a disposizione in qualsiasi momento.

Procedura
---------

### Download del file

Per prima cosa è necessario scaricare il file compresso [RpmTag\_Fedora14.tgz](http://depositfiles.com/en/files/035hb0xq8) da <http://depositfiles.com/en/> seguendo la semplice procedura di download e salvandolo dove preferisci.
Il file tgz è di 22MB e contiene il file di testo RpmTag Fedora14.Txt, che una volta scompattato, occupa circa 218MB.

### Decompressione del file

Ci sono tantissimi programmi di decompressione dei file tgz in modalità grafica, da terminale la procedura è:

`$ tar xzvf RpmTag_Fedora14.tgz`

### Apertura del file

Qui vengono le note dolenti, perchè Linux ha ben pochi programmi che riescano a gestire file ASCII di grosse dimensioni in modo decente.
Gli unici programmi in grado di gestire decentemente questo tipo di file sono emacs e nedit, tutti gli altri programmi per una ragione o per l'altra si incagliano miseramente o sono molto lenti.

Contenuto del file
------------------

Come detto il file non è altro che un enorme file di testo contenente una sezione per ogni pacchetto presente nella cartella **releases\\14\\Everything\\i386\\os\\Packages\\**, ordinati alfabeticamente.
Ogni sezione contiene una sottosezione per ciascun TAG RPM, di una qualche utilità, presente nel pacchetto. L'elenco di questi TAG li trovate [qui](http://rpm.org/api/4.6.0/rpmtag_8h-source.html), mentre [qui](http://www.rpm.org/max-rpm/s1-rpm-inside-tags.html) trovate una breve descrizione di quelli più importanti.
Vedendo la struttura meglio nel dettaglio si nota che ogni riga comincia con la riga:
**-------------------------- START PACKAGE ----------------------------**

-   Il primo TAG è privato ed è **LOC\_INDEX**, che non è altro che il numero del pacchetto nell'elenco;
-   I TAG **RPMTAG\_NAME, RPMTAG\_VERSION** e **RPMTAG\_RELEASE** indicano il nome del programma, la sua versione e la sua release;

Per facilitarne la ricerca tutti i nomi dei pacchetti cominciano con ~.

-   Il TAG **RPMTAG\_SUMMARY** contiene una breve descrizione del pacchetto;
-   Il TAG **RPMTAG\_DESCRIPTION** contiene una descrizione più dettagliata del pacchetto;
-   Il TAG **RPMTAG\_BUILDTIME** contiene la data ed ora di compilazione del pacchetto;
-   Il TAG **RPMTAG\_LICENSE** contiene il tipo di licenza con cui è rilasciato il pacchetto;
-   Il TAG **RPMTAG\_GROUP** contiene il gruppo di appartenenza del pacchetto;
-   Il TAG **RPMTAG\_URL** è uno dei più importanti e contiene l'indirizzo URL del progetto da cui si è ricavato il pacchetto;
-   Il TAG **RPMTAG\_ARCH** contiene l'architettura per cui si è compilato il pacchetto;
-   Il TAG **RPMTAG\_SOURCERPM** contiene il nome del pacchetto sorgente con cui si è generato il pacchetto;
-   Il TAG **RPMTAG\_PROVIDENAME** contiene l'elenco degli oggetti forniti dal pacchetto;
-   Il TAG **RPMTAG\_REQUIRENAME** contiene l'elenco degli oggetti necessari al pacchetto per poter essere installato;
-   I TAG **RPMTAG\_CHANGELOGTIME, RPMTAG\_CHANGELOGNAME** e **RPMTAG\_CHANGELOGTEXT** contengono gli elenchi della data/ora, nome dell'autore e descrizione dei cambiamenti apportati nel tempo al pacchetto;
-   Il TAG **RPMTAG\_BASENAMES** è importantissimo e contiene l'elenco completo dei file e/o directory contenuti nel pacchetto;
-   Il TAG **RPMTAG\_OPTFLAGS** contiene le opzioni di compilazione del pacchetto;
-   I TAG **RPMTAG\_PREIN, RPMTAG\_POSTIN, RPMTAG\_PREUN** e **RPMTAG\_POSTUN** contengono gli script eseguiti nei vari momenti dell'installazione o rimozione del pacchetto;
-   I TAG **RPMTAG\_MOREFILE, RPMTAG\_MORESIZE** e **RPMTAG\_MORETIME** sono privati e contengono il nome completo, la dimensione in byte e la data/ora del pacchetto.

Come già detto ci sono moltissimi altri tag di importanza "minore". I tag appena elencati, a parte gli ultimi, sono presenti in tutti i pacchetti, gli altri sono presenti solo quando necessario.
Ogni sezione si conclude con la riga:

**------------------------------ END PACKAGE ------------------------------------**

Utilizzo
--------

E' difficile dire in due parole come usare questo file. In genere si possono fare ricerche a parola chiave, come il nome di un file, del pacchetto o qualsiasi altro elemento che conosci e che può tornarti utile per identificare quello che cerchi.
Altre volte invece può capitare di scorrere il file alla ricerca di qualche pepita relativa a programmi che non si conoscono.

Insomma, gli utilizzi sono tantissimi, basta solo scovarli.

[Categoria: Programmazione e Sviluppo](Categoria:_Programmazione_e_Sviluppo "wikilink")
