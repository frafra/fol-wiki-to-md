Una mini guida per le operazioni più comuni che possono essere utili quando si inizia per la prima volta a usare Linux

Il filesystem: come muoversi fra le directory, creare, copiare e spostare file e cartelle
-----------------------------------------------------------------------------------------

Il filesystem è organizzato in directory, ogni directory ha un proprio percorso (path).
La directory principale da cui tutte partono è detta **radice** e viene indicata da **/** (slash).
Per muoversi all'interno del filesystem e per copiare file bisogna indicare il percorso della directory in cui ci si vuole spostare o il percorso, ad esempio, del file da copiare.
Il percorso viene detto assoluto se inizia con / e include tutte le directory intermedie fino ad arrivare a quella che interessa, viene invece detto relativo se non parte da / , in questo caso il sistema 'assume' che il percorso indicato sia all'interno della directory in cui ci si trova quando viene dato il comando.

**`pwd`**` indica la directory in cui ci si trova`
**`ls`**` mostra un elenco del contenuto della directory in cui ci si trova`
**`ls` `-l`**` mostra l'elenco con i dettagli su dimensioni dei file e i loro permessi`
**`ls` `-la`**` come ls -l ma mostra anche i file e directory 'nascosti', hanno un punto davanti al nome`
**`cd` `/percorso`**` ci si sposta nella directory corrispondente al percorso indicato`
**`cd` `..`**` (cd spazio punto punto) ci si sposta nella directory di livello superiore a quella in cui ci si trova`
**`cd`**` ci si sposta nella directory home dell'utente corrente`

**`cp` `/percorso/nomefile` `/percorso/nomefile.old`**` fa una copia del file del file chiamato 'nomefile' e la chiama 'nomefile.old'`

se si vuole copiare un file nella stessa directory in cui ci si trova, si può evitare di scrivere il percorso assoluto, basta scrivere

**`cp` `nomefile` `nomefile.old`**
**`mv` `/path/origine/nomefile` `/path/destinazione/nomefile`**` sposta un file da una directory ad un'altra,`

oppure, se non viene indicato il percorso rinomina il file

**`rm` `nomefile`**` elimina il file`
**`rm` `-rf` `nomedirectory`**` elimina una directory e tutto cio' che contiene senza chiedere conferme`
**`mkdir` `nomedirectory`**` crea una directory`
**`rmdir` `nomedirectory`**` elimina una directory vuota`

Per evitare di dover scrivere per intero tutto il percorso come argomento del comando che si sta usando, si può usare una scorciatoia: iniziare a scrivere parte del nome del file o della directory e poi premere il tasto TAB per farlo completare al sistema.
Se sono possibili più alternative per completare il nome continuando a premere TAB viene proposto un elenco.
Una guida sull'uso di TAB è qui: <http://www.fedoraonline.it/modules/wfsection/article.php?articleid=13>
(Per una guida sui permessi dei file vedere qui: <http://www.fedoraonline.it/modules/wfsection/article.php?page=1&articleid=18>)

L'utente root e le operazioni che richiedono password
-----------------------------------------------------

Per eseguire alcuni comandi è necessario 'essere root', l'utente root è quello che ha il controllo totale del sistema, è in grado anche di fare danni, quindi conviene usare i privilegi di root solo quando è effettivamente necessario.
Per diventare root si usa il comando **su** e poi bisogna inserire la password di root, appunto.
Il comando 'su' dà all'utente normale i privilegi di root, ma per comodità può servire 'loggarsi come root' con il comando **su -** (su spazio meno), in questo modo è più comodo dare alcuni comandi.
Per uscire da root e tornare utente semplice si scrive exit.

Concatenare i comandi
---------------------

Di norma il risultato di un comando viene riportato a video (lo standard output), ma spesso è utile riutilizzare ciò che uscirebbe solo a video e usarlo come 'materiale' da trattare con un altro comando.
Per fare ciò si usa il carattere **|**, che sulla tastiera italiana il carattere pipe, cioè | , si ottiene premendo MAIUSCOLO e contemporaneamente "backslash" (è il tasto in alto a sinistra, subito prima del numero 1).
Può capitare che volendo leggere l'elenco dei file di una directory col comando ls, questo sia molto lungo e che scorra sullo schermo troppo velocemente per essere letto. In questo caso si può passare l'elenco al comando less, che lo tratta per proporlo sul video una pagina per volta.

`ls | less`

### less e grep

I comandi less e grep sono utili per leggere a video (less) e per cercare parole (grep) all'interno di un testo.

-   **less** fa apparire un testo lungo una pagina per volta sul video, premendo spazio si passa alla pagina successiva, con invio si va alla riga successiva, premendo q si può uscire dalla visualizzazione di less.
-   **grep** permette di cercare sequenze di caratteri, è utile per filtrare ad esempio una lunga pagina di manuale alla ricerca di una certa parola.

Esempio: cercare la parola 'nome' in un elenco di file e directory

`ls | grep nome`

restituisce sullo schermo tutte le righe dell'elenco che contengono 'nome', se le righe fossero molte si può ripassare di nuovo l'output di grep a less per leggerlo una pagina alla volta

`ls | grep nome | less`

A volte vedere solo la riga in cui compare il nome cercato può non dare l'idea del contesto in cui quel nome si trova, in questo caso un'opzione di grep permette di riportare anche le n righe che precedono e seguono la riga che contiene il nome.

`ls | grep -3 nome | less `

riporta le 3 righe prima e dopo quella cercata.

Ricerca di file sull'hard disk
------------------------------

Il comando **locate** permette di cercare nomi di file o directory. Per funzionare si basa su un database che va aggiornato periodicamente. Per aggiornare il database si usa il comando **updatedb** (bisogna essere root) e bisogna attendere che ritorni la riga del prompt, che durante l'aggiornamento non è visibile.
Anche l'output di locate può essere passato a less.

Modificare un file di testo
---------------------------

Praticamente tutte le impostazioni di Linux sono contenute in file di testo, ad esempio la risoluzione dello schermo o il tipo di layout della tastiera.
Per modificare un file di testo, un programma molto usato è **vi**, ha moltissime funzioni.
Esiste già un tutorial che ne spiega [l'uso di base](Guida_base_ai_comandi_vi "wikilink")

Interrompere un comando
-----------------------

Per interrompere l'esecuzione di un comando si usa la combinazione di tasti *CTRL+C*.

Le pagine di manuale
--------------------

Tutti i comandi hanno un manuale in linea su Linux, per richiamare le istruzioni su come usare un comando si usa il comando **man nomecomando**.
All'interno delle pagine di manuale ci si sposta in su e in giù tra le varie pagine con i tasti PGSU e PGGIU della tastiera. Si esce dal manuale premendo **q**.
Naturalmente ciò che apparirebbe sullo schermo può essere passato ai comandi grep e less per filtrare i le pagine.

<Categoria:Sistema>
