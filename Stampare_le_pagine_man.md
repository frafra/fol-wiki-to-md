Questa articolo spiega come stampare le pagine di manuale di un comando.

Il comando man in Linux permette di leggere a video il 'manuale', la 'guida in linea' di un comando, ossia una spiegazione del suo funzionamento e delle possibili opzioni, spesso anche con degli esempi d'uso.
Per i comandi che prevedono molte opzioni, o che sono più complessi da utilizzare, può essere utile stamparsi il manuale per leggerlo e studiarlo con calma.

Per fare questo si può usare il comando ***a2ps***, che invia alla stampante le pagine di manuale.
 Ad esempio: per avere su carta il manuale d'uso del comando *a2ps*, scrivere in una finestra di terminale:

`$ man a2ps | a2ps`

Per avere il manuale di un qualsiasi altro comando, allo stesso modo, si può scrivere:

`$ man nomecomando | a2ps`

Un altro comando utile per stampare potrebbe essere ***card***, che invece di stampare tutte le pagine man così come apparirebbero sullo schermo, stampa una guida rapida che contiene le sole opzioni del comando desiderato.
Per farlo basta semplicemente scrivere:

`$ card nomecomando`

<Categoria:Sistema>
