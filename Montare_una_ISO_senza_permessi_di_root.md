Rispondere alla domanda: "**come si può vedere il contenuto dei file .iso?**" è molto semplice se si è utenti root o se si può accedere in amministrazione alla macchina che si ha a disposizione. Basta semplicemente montare il file con un comando analogo (da utente root ovviamente):

`# mount -o loop file.iso directory_di_mount/`

e poi navigare in `directory_di_mount/`.
A volte, non serve neppure specificare l'opzione `loop` se il filesystem dell'immagine è conosciuto da [libblkid](http://www.kernel.org/pub/linux/utils/util-linux/libblkid-docs/). La pagina di man del comando mount è abbastanza esaustiva in proposito.
Rispondere alla domanda: "**come si può montare un file immagine da utente normale senza essere root?**" è forse un po' più complicato.
Chi ha installato sul proprio sistema [Midnight Commander](http://www.midnight-commander.org/) dovrebbe riuscire ad aprire il file immagine e visionare il contenuto senza problemi.
Gli utenti Kde, invece, possono fare una cosa simile utilizzando [Krusader](http://www.krusader.org/), dunque in un ambiente grafico.
Ma se non si ha Krusader o Midnight Commander come si fa? Niente paura, si può ottenere questa cosa utilizzando [FuseISO](http://sourceforge.net/projects/fuseiso/). **FuseISO** è un modulo per [FUSE](http://fuse.sourceforge.net/) che supporta file del tipo ISO9660 Level 1 e 2, Rock Ridge, Joliet e zisofs, praticamente i file che circolano con queste estensioni .iso, .nrg, .bin, .mdf e .img.
In Fedora FuseISO è già pacchettizzato e prelevabile dai repository ufficiali. Se non è già installato sulla propria macchina basta installarlo da utente root:

`# yum install fuseiso`

Una volta installato gli utenti potranno montare i file immagine senza necessità di avere i privilegi di utente root. Semplicemente basterà:

`$ fuseiso file.iso directory_di_mount/`

e si potrà vedere il contenuto di `file.iso` in `directory_di_mount/`
Per smontare il dispositivo invece bisognerà dare questo comando:

`$ fusermount -u directory_di_mount/`

Altre informazioni sulle opzioni di fuseiso si possono ottenere lanciandolo con l'opzione -h:

`$ fuseiso -h`

Riferimenti
-----------

-   Articolo pubblicato precedentemente su [marionline.it](http://blog.marionline.it/linux/fedora/montare-alcuni-file-immagine-senza-i-privilegi-di-root/).
-   [How To Mount and View ISO File as Root and Regular User in Linux](http://www.thegeekstuff.com/2009/06/how-to-mount-view-iso-file-as-root-and-non-root-user-in-unix/#more-553) (in Inglese).

<Categoria:Sistema>
