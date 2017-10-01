\_\_TOC\_\_

Introduzione
------------

Quando si avvia un computer sul quale Fedora è il sistema operativo prescelto, dopo il boot compare *GRUB2*, nel quale c'è almeno una riga che indica il kernel che sta per essere lanciato (di solito parte in automatico dopo pochi secondi).
In seguito le righe aumenteranno man mano che si installeranno nuovi kernel.

Verifica
--------

Dalla versione 8 "Werewolf" di Fedora il file da modificare è:

`/etc/yum.conf`

e va modificato con un editor di testo per aumentare (o diminuire) il numero di pacchetti da mantenere contemporaneamente.
Subito dopo l'installazione in genere sono presenti le seguenti righe:

`[main]`
`cachedir=/var/cache/yum/$basearch/$releasever`
`keepcache=0`
`debuglevel=2`
`logfile=/var/log/yum.log`
`exactarch=1`
`obsoletes=1`
`gpgcheck=1`
`plugins=1`
`installonly_limit=3`

Il valore da modificare è l'ultima riga, **installonly\_limit=3**, e va modificato con il numero di pacchetti, e quindi anche di kernel, che si vuole avere contemporaneamente. Questo ovviamente influisce su quei pacchetti che permettono di averne più versioni contemporaneamente, come appunto il kernel.
Nel conteggio **NON** sono ovviamente compresi i vari kernel-devel, kernel-headers ecc. che servono per svolgere compiti particolari ma non possono esistere 'da soli', cioè senza il kernel di base.

Modifica del file
-----------------

Naturalmente è sempre buona norma salvare la versione iniziale prima di cambiarla:

`# cp /etc/yum.conf /etc/yum.conf_backup`

(o qualsiasi altro nome che faccia ricordare cosa sia).
Procedere poi alla modifica vera e propria:

`# vim /etc/yum.conf`

e modificare la riga come detto precedentemente.

Sezione da non modificare
-------------------------

Tenere conto che se si utilizza qualche plugin (per esempio fastestmirror o presto), nel file ci sarà anche la riga:

`plugins=1`

dove il numero **non** indica la quantità di plugin attivi nella propria installazione, ma va inteso in senso binario: 1 significa che questa opzione è attivata e funzionante, 0 che è disattivata.
Per maggiori delucidazioni e approfondimenti, in ogni caso, è opportuno prendere visione direttamente della pagina di manuale specifica:

`$ man yum.conf`

che è molto chiara, assai dettagliata e permette di specificare moltissime altre opzioni, oltre a queste di "base".

<Categoria:Grub>
