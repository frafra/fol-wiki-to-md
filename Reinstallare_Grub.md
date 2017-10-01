\_\_TOC\_\_

Introduzione
------------

**GRUB** (GRand Unified Bootloader) è un *boot loader* usato da molte distribuzioni Linux, tra cui Fedora. Lo scopo di un boot loader è caricare il kernel di un sistema operativo e permetterne l'avvio. Dalla versione **15** di fedora si è passati alla versione 1.99 di grub, gergalmente definita Grub2; per questo motivo chi volesse reinstallare Grub per fedora 15 o superiore dovrà attenersi alla [seconda parte](Reinstallare_Grub#Grub2 "wikilink") di questa guida.

Ricavare le informazioni necessarie
-----------------------------------

Prima di procedere alla reinstallazione vera e propria di Grub bisognerà accedere da una live o da un DVD per recuperare le informazioni necessarie ai passaggi seguenti. Una volta avuto accesso ad un terminale con permessi root, si cerca la partizione sulla quale reinstallare Grub con:

`# fdisk -l`

e bisogna riconoscere il device in cui sovrascrivere il MBR (Master Boot Record). In questo caso si possono utilizzare anche tool grafici, come può essere GParted, per trovare la partizione esatta.

### Grub Legacy

In questa parte della guida si andrà a resettare Grub, versione *Legacy*, per **Fedora 14** o precedenti.

Procurarsi il DVD di Fedora e impostare dal bios (se già non è settato) il boot dal lettore DVD.
Alla prima opportunità di scelta, premere il tasto "F5" ed al successivo prompt digitare:

`# linux rescue`

seguito dal tasto enter. A questo punto digitare:

`# chroot /mnt/sysimage  `

e premere enter.

Dare quindi un'occhiata al contenuto del file device.map:

`# cat /boot/grub/device.map `

Verificare siano presenti i dischi necessari e annotare la loro posizione. Nel caso ne manchi uno, lo si aggiunge con un editor di testo.
A questo punto digitare:

`# grub-install /dev/hda`

e premere nuovamente enter.
Scegliendo **hda** Grub andrà a installarsi nel MBR del primo disco ata, in caso di differenti esigenze, specificare il device appropriato.
Digitare quindi:

`# exit`

e riavviare il sistema, togliendo ovviamente il DVD dal drive.

### Grub2

<img src="Fedora16_Troubleshootings.png" title="fig:All&#39;avvio scegliere &quot;Troubleshootings&quot;" alt="All&#39;avvio scegliere &quot;Troubleshootings&quot;" width="200" /> <img src="Fedora16_Rescue.png" title="fig:Scegliere poi &quot;Rescue a fedora system&quot;" alt="Scegliere poi &quot;Rescue a fedora system&quot;" width="200" /> Questa parte della guida invece è riservata ai possessori di **Fedora 15** o superiori, in quanto Grub è aggiornato alla versione 1.99, che ha apportato cambiamenti radicali.

Una volta trovata la partizione esatta su cui andare a reinstallare Grub2, inserire il DVD di fedora nel drive, selezionarne l'avvio dal bios e recarsi nella sezione *Troubleshootings* dal menù di avvio, e poi *Rescue a Fedora system*, come mostrato dalle due immagini a lato.
Dopo aver scelto la lingua di sistema e della tastiera il menù contestuale cercherà eventuali sistemi fedora già presenti e chiederà se montarli direttamente in automatico: acconsentite.
Ora da root si eseguono questi passaggi, digitando nel terminale:

`# chroot /mnt/sysimage`
`# grub2-install /dev/sdX`

Inserire al posto della **X** il disco su cui installare il boot-loader (generalmente è *sda*).
Si passa ora all'aggiornamento dell'elenco dei sistemi operativi e dei kernel presenti che effettivamente verranno presentati all'avvio del computer, riscrivendo il file di configurazione di *Grub2* con il comando seguente, che controlla la presenza o meno di una installazione tramite [EFI](http://it.wikipedia.org/wiki/Extensible_Firmware_Interface) e provvede ad installare grub2 nel percorso specifico:

`# (for f in /boot/{grub2,efi/EFI/fedora}/grub.cfg;do [ -f $f ]&&grub2-mkconfig -o $f;done)`

Fatto anche questo si esce da chroot con un semplice

`# exit`

e si riavvia la macchina, togliendo ovviamente il DVD dal drive.

<Categoria:Grub> <Categoria:Installazione> <Categoria:Sistema>
