Introduzione
------------

Di recente si parla tanto di GRUB2, la nuova versione del bootloader più usato nell'ambiente GNU/Linux.
Molti parlano delle sue potenzialità, molti lo criticano ma sono indiscusse le sue qualità, pratiche ed estetiche.
In primo luogo la possibilità di effettuare il boot da immagini ISO, estremamente comodo per distribuzioni di ripristino del sistema, recupero dati e perché no, di prova.

Installazione
-------------

Purtroppo i pacchetti forniti nei repository Fedora sono piuttosto lacunosi ma viste le poche dipendenze è piuttosto facile compilarlo da se includendo le funzionalità necessarie per mostrare le sue vere potenzialità...

Per prima cosa scaricare dall'ftp ufficiale i sorgenti: <ftp://alpha.gnu.org/gnu/grub/> la versione odierna relativamente a questa guida è la 1.97:

da terminale digitare:

`$ wget `[`ftp://alpha.gnu.org/gnu/grub/grub-1.97.tar.gz`](ftp://alpha.gnu.org/gnu/grub/grub-1.97.tar.gz)

e estrarlo:

`$ tar -xzf grub-1.97.tar.gz`
`(-x = estrai)`
`(-z = estrai gzip)`
`(-f = accetta l'argomento del file al posto dello stdin)`

a questo punto entrare nella cartella generata:

`$ cd grub-1.97`

prima di compilare bisogna aggiungere alcune dipendenze:

`$ yum install bison diffutils gawk gcc`

ed eventuali soliti utility per la compilazione che se mancano vi verrà segnalato dallo script di configurazione...

Ora, assicurarsi di avere gli strumenti necessari (mancanti negli rpm di fedora), eseguire:

`$ ./configure --enable-grub-mkfont`

più avanti questo arcano sarà svelato...

Ora, se configure non ha dato errori passare alla compilazione:

`$ make`

se ancora una volta si è stati fortunati (cosa probabile vista la penuria di dipendenze) si può passare all'installazione:

`$ su -c 'make install'`

se tutto è andato a buon fine si avranno finalmente gli strumenti per installare il bootloader...

Ora è il momento di scaricare i fonts preferiti da vedere nella modalità grafica.

I tools che suggeriti a configure di installare (--enable-grub-mkfont) permettono di convertire qualunque font nel formato richiesto da grub, quindi scegliere il font ed eseguire su di esso:

`grub-mkfont --output=`<nomedelfont>`.pf2 `<fontoriginale.{ttf,pcf}>

Il mio consiglio è quello di usare i font Unicode poiché alcuni caratteri speciali (quali ad esempio quelli per fare le cornici) non sono sempre presenti e potrebbe non essere gradevole vedere al posto di una cornice dei quadratini con un punto interrogativo dentro...)

I font unicode sono reperibili qui:
[<http://unifoundry.com/unifont-5.1.20080820.pcf.gz>](http://unifoundry.com/unifont-5.1.20080820.pcf.gz)
a questo punto non resta che copiarli nel hd di boot o ovunque si è in grado di reperirli da grub (è preferibile una partizione senza lvm come anche quello di boot generato automaticamente dall'installazione di fedora)

Ora installare grub sul mbr:
ovviamente con i privilegi di superutente ($ su):

`# grub-install --no-floppy /dev/sdX`

al posto di sdX inserire l'hd impostato al boot dal bios...

Bene, ora è tutto pronto, non resta che configurare...

Il file in questione (a differenza del vecchio grub) è grub.cfg e si trova presumibilmente nella partizione di boot in /boot/grub/grub.cfg probabilmente ci sarà un file pregenerato senza grafica che si può praticamente cancellare del tutto, meglio conservarlo per non dover ricopiare le funzioni menuentry...
Il primo passo è impostare la variabile timeout che dice quanto tempo bisogna aspettare prima che parta automaticamente la funzione menuentry di default:

`set timeout=`<tempoinsecondi>

al posto del tempo in secondi si può anche mettere -1 che non darà una scadenza...
poi impostare:

`set default=`<menuentrydefault>

con al posto di <menuentrydefault> il menuentry preferito nell'ordine in cui si scriverà sul file (partendo da 0 non da 1!!)
E fin qui niente di nuovo...
Ora impostare la partizione di lavoro di grub (quella dove si hanno le immagini di sfondo e fonts)

`set root=(hd0,0)`

al posto di (hd0,0) indicare la partizione di boot (badare che grub0.xx già di suo aveva una tabella particolare:

`hd0 -> /dev/sda - hd0,0 -> /dev/sda1 - hd0,1 -> /dev/sda2`
`hd1 -> /dev/sdb - hd0,0 -> /dev/sdb1 - hd0,1 -> /dev/sdb2`

ora per semplificare le cose (o meglio, complicarle a chi è abituato già alle stranezze di grub0.xx) sono:

`hd0 -> /dev/sda - hd0,1 -> /dev/sda1 - hd0,2 -> /dev/sda2`
`hd1 -> /dev/sdb - hd0,1 -> /dev/sdb1 - hd0,2 -> /dev/sdb2`

per il sommo gaudio degli utenti grub2 ha un'eccellente funzione chiamata search che permette di trovare il disco (hdx,x) tramite il suo uuid, così prevenendo anche problemi di scambio di dischi e la sintassi (per quanto sia impossibile trovarla) è piuttosto semplice:

`search -s root --fs-uuid <UUID dell'HD>`

al posto di set root....
e per rintracciare l'uuid del disco di boot basta fare un bel:

`ls -l /dev/disk/by-uuid/`

Se si hanno dubbi su quale sia, eseguire da root *fdisk -l* e vedere qual'è il disco con l'asterisco che sarà il disco di boot.
Ora per la grafica:

`insmod font`
`insmod gfxterm`
`insmod vbe`
`set gfxmode=1280x1024x32`
`if loadfont /boot/theme/unifont.pf2 ; then`
`        terminal_output.gfxterm`
`fi`
`insmod png`
`if background_image /boot/theme/boot.png; then`
`        set color_normal=black/black`
`        set color_highlight=magenta/black`
`else`
`        set menu_color_normal=cyan/blue`
`        set menu_color_highlight=white/blue`
`fi`

Al posto di *1280x1024x32* impostare la risoluzione che si preferisce nel medesimo formato (es. 800x600x16) e l'ultima parte (quella che indica la profondità di colore è consigliabile ometterla così cercherà da solo quella ottimale e compatibile).

Al posto di /boot/theme/unifont.pf2 bisogna indicare il path completo del font generato precedentemente (attenzione a inserirlo in una partizione raggiungibile, altrimenti funziona lo stesso ma niente grafica...).

Al posto di /boot/theme/boot.png inserire il nome dell'immagine di sfondo (possibilmente proporzionata alla risoluzione che impostata)
(se si preferisce il formato tga basta cambiare anche insmod png in insmod tga)
e dulcis in fundo... le opzioni nel menu (menuentry):
Di seguito si riporta un esempio che si dovrà correggere con le impostazioni del proprio kernel e del proprio *initrd* file...

`menuentry "Fedora (2.6.30.9-96.fc11.x86_64)" {`
`        linux   /boot/f11/vmlinuz-2.6.30.9-96.fc11.x86_64 root=/dev/mapper/vg0-lv0 ro quiet`
`        initrd  /boot/f11/initrd-2.6.30.9-96.fc11.x86_64.img`
`}`
`menuentry "Mictosoft Windows XP" {`
`        search -s root --fs-uuid A8241BF0241BC06C`
`        drivemap (hd0) $root`
`        drivemap $root (hd0)`
`        chainloader +1`

Si nota che lo stesso giochetto di search si può fare anche per trovare la partizione all'interno dei menuentry, la funzione per caricare il kernel è a differenza di grub quella che vede (linux /boot.....)
et voilà, un magnifico avvio grafico e la possibilità di avviare con le funzioni (loop) anche le immagini iso...
<Categoria:Grub>
