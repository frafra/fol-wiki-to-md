Nei sistemi Unix i file descriptors sono utilizzati dai programmi per puntare ai file che vengono aperti, come una sorta di chiave astratta. Ogni utente ha dei limiti di file descriptors che può utilizzare.

Lanciando un *ulimit -n* è possibile verificare il numero di file descriptors massimi settati.

`# ulimit -n`
`1024`

E' possibile verificare il numero totale di file descriptors usati e liberi per tutti gli utenti. Aprendo il file */proc/sys/fs/file-nr* si troverà nella prima colonna il numero di fd utilizzati, nella seconda quelli liberi e nell'ultima i massimi utilizzabili.
Se si utilizza un kernel 2.4 o superiore si avrà il valore dei file descriptors liberi a 0, perchè il kernel utilizza in modo dinamico i fd e li crea quando necessario (quindi il valore sarà a 0).

`# cat /proc/sys/fs/file-nr`
`6656   0   203692`

Ora bisognerà risalire al pid del processo che si vuole analizzare dal punto di vista dei file descriptors usati. Tramite il comando *ps* si può risalire al *pid*. Nel caso specifico con *awk* si estrae il pid del processo pidgin.

`# ps -ef | grep -i pidgin | grep -v grep | awk '{print $2}'`
`3516`

Ora tramite il comando *lsof* è possibile avere la lista di tutti i files aperti da un determinato processo. Con il pid in precedenza ricavato, si potrà contare il numero di file aperti dal processo interessato.

`# lsof -p 3516 | wc -l`
`254`

oppure

`` # lsof -p `ps -ef | grep -i pidgin | grep -v grep | awk '{print $2}'` ``
`254`

Ora per determinare il numero di file descriptors utilizzati bisognerà spostarsi sotto il *procfs* (direttorio /proc) e cercare una directory con il numero del pid che è stato rintracciato in precedenza.
Linux per ogni processo crea un direttorio sotto il *procfs* e vi salva alcune informazioni relative al processo. Nella subdirectory fd sono contenuti tutti i files descriptors usati. Basterà contare il numero di file contenuti.

`# ls -l /proc/3516/fd | wc -l`
`21`

oppure

`` # ls -l /proc/`ps -ef | grep -i pidgin | grep -v grep | awk '{print $2}'`/fd | wc -l ``
`21`

Il numero di fd e file aperti non è uguale perchè molti file aperti vengono inizializzati senza dover creare un puntamento tramite fd, quindi il numero sarà diverso.

[Categoria:Programmazione e Sviluppo](Categoria:Programmazione_e_Sviluppo "wikilink")
