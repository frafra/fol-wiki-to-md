Introduzione
------------

L'utilizzo delle macchine virtuali è sempre più diffuso per gli innumerevoli vantaggi che questo comporta. Innanzitutto l'elevata compatibilità hardware consente l'installazione di una macchina virtuale su qualsiasi sistema x86. Inoltre è possibile compiere test su differenti sistemi operativi senza dover dedicare un computer per ciascun sistema operativo o senza dover riavviare il sistema operativo in caso di dual boot. Infatti è possibile installare più macchine virtuali all'interno di un unico sistema operativo host, grazie alle elevate prestazioni dei componenti hardware più recenti con costi relativamente contenuti. Può a volte anche essere inevitabile utilizzare sistemi proprietari per lo svolgimento di alcune operazioni e l'installazione di questi sistemi in una macchina virtuale costituisce una valida soluzione.

In questa guida si indicheranno i passaggi necessari ad installare un sistema operativo guest XP nel sistema operativo host Fedora 17 attraverso l'utilizzo di *qemu-kvm* e l'interfaccia grafica *virt-manager*.

La virtualizzazione attraverso *qemu-kvm* è una scelta interessante perchè nasce da un progetto legato al kernel linux e questo lo rende una piattaforma economica, flessibile e performante. *Qemu-kvm* può essere considerato una "base" che se associata con i driver *virtio* e *spice* può offrire prestazioni notevoli. Il suo utilizzo non è ancora diffuso come quello di altre soluzioni, ma in futuro si rivelerà certamente uno strumento sempre più apprezzato.

Preparazione del sistema
------------------------

Il primo passo è verificare che il proprio processore supporti la virtualizzazione dell'hardware:

`$ grep -E 'svm|vmx' /proc/cpuinfo`

Se l'output di questo comando non presenta nulla allora il processore non supporta la virtualizzazione dell'hardware oppure tale virtualizzazione non è stata abilitata. In questo secondo caso è possibile accedere al bios all'avvio del pc e attivare l'opzione.

Qualora invece il processore supporti la virtualizzazione si visualizzeranno vari flags, e a seconda dei casi si troverà *vmx* se il nostro processore è intel, oppure *svm* se il nostro processore è un amd.

Se il processore è intel sarà necessario caricare i reltivi moduli con i comandi:

`# modprobe kvm`
`# modprobe kvm_intel`

Se invece è un processore amd:

`# modprobe kvm`
`# modprobe kvm_amd`

Se tutto è andato a buon fine si verificherà una situazione di questo tipo:

`$ lsmod | grep kvm `
`kvm_intel             126707  0 `
`kvm                   363507  1 kvm_intel`

Installazione
-------------

Si installino i pacchetti necessari per la virtualizzazione:

`# yum groupinstall @virtualization`

Si installi ora la macchina virtuale con l'interfaccia grafica Virt-manager. A questo punto infatti nel menu *Applicazioni =&gt; Strumenti di sistema* dovrebbe essere comparsa l'icona di Virtual Machine Manager. All'avvio sarà richiesta la password di root.

<img src="vm1.png" title="vm1.png" alt="vm1.png" width="310" />

Cliccando sul primo pulsante a sinistra si apre la seguente finestra.

<img src="vm2.png" title="vm2.png" alt="vm2.png" width="310" />

Inserire il nome da attribuire alla nuova macchina virtuale. Qualora per l'installazione si utilizzi una immagine iso o un cd di installazione si lasci invariata la modalità di installazione. Cliccando su avanti comparirà la seguente finestra.

<img src="vm3.png" title="vm3.png" alt="vm3.png" width="310" />

Scegliere il supporto di installazione con il percorso corretto. In *Tipo OS* si scelga 'Windows' e in *Versione* 'Microsoft Windows XP'. La schermata successiva chiede di indicare al sistema quanta RAM dedicare alla macchina virtuale e quante cpu. La RAM massima gestibile da qemu-kvm è di 2048 MB, mentre per le cpu è consigliabile inserire tutte quelle disponibili.

<img src="vm4.png" title="vm4.png" alt="vm4.png" width="310" />

Nel passo successivo si creerà lo spazio sul disco che sarà utilizzato dalla macchina virtuale. Si indichi la quantità di spazio opportuna: lasciando invariate le impostazioni predefinite lo spazio verrà creato nella partizione di sistema dell'host.

È consigliabile marcare l'opzione *Alloca l'intero disco ora*. Questo significa che verrà creato immediatamente tutto lo spazio indicato. In caso contrario verrà creato solo lo spazio necessario all'installazione e il restante verrà allocato dinamicamente al bisogno. Questa possibilità rallenterà però il funzionamento della macchina virtuale.

Potrebbe essere presente già uno spazio dedicato ad una macchina virtuale, oppure si potrebbe ricavare lo spazio per la macchina virtuale in una posizione diversa da quella del file system dell'host. In questi casi sarà sufficiente cliccare su *Selezionare managed o altro storage esistente* e indicare il percorso.

Nella creazione di un nuovo storage la dimensione sarà sempre quella indicata nel campo della dimensione, nell'esempio “13 GB”.

<img src="vm5.png" title="vm5.png" alt="vm5.png" width="310" />

Nell'ultimo passo sarà visualizzato un riepilogo dei dati inseriti (i nomi attribuiti e evidenziati nella finestra sono puramente indicativi) e si presenteranno alcune opzioni:

- *Customize configuration before install*: offre la possibilità di effettuare delle configurazioni aggiuntive prima dell'avvio della MV;

- nelle *Opzioni avanzate* si lasci tutto come di default, facendo attenzione a non modificare il campo *Tipo virt*. Questo campo deve rimanere con l'indicazione 'kvm', perchè in caso contrario sarà impossibile ottimizzare successivamente il disco configurandolo come Virtio.

<img src="vm6.png" title="vm6.png" alt="vm6.png" width="310" />

Nella configurazione generale della macchina si è rivelato opportuno scegliere nella opzione *Sound* la scheda virtuale 'ac97', nella opzione *Schermo Spice* -&gt; 'Tipo Spice' e nella opzione *Schermo* -&gt; 'Modello qxl'. Tali impostazioni possono essere modificate subito (selezionando *Customize configuration before install* e cliccando su *Fine*) o dopo il primo avvio della MV.

Cliccando sul tasto *Fine* si avvierà l'installazione del sistema operativo attraverso il supporto (cd o iso) scelto inizialmente.

Configurazione driver virtio e spice
------------------------------------

Una volta terminata l'installazione del sistema operativo guest, si proceda con l'installazione dei driver per rendere il sistema più veloce ed efficiente nella gestione delle risorse hardware disponibili.

Dalla finestra principale di virt-manager si clicchi sui menu *Modifica* -&gt; *Dettagli* virtual machine e nella finestra che si apre si vada su *Visualizza* -&gt; *Dettagli*. La schermata seguente permette di configurare molti aspetti riguardo al modo in cui la MV si interfaccia con il sistema host.

<img src="vm7.png" title="vm7.png" alt="vm7.png" width="310" />

### Installazione driver VirtIO

I driver virtio offrono un controller per il disco virtuale che incrementa la velocità di accesso ai dati contenuti nel disco stesso. Nella schermata precedente compare una voce, indicata con 'IDE Disk 1' che è il disco dove è installato il sistema operativo guest. Selezionando questa opzione si visualizza la seguente finestra.

<img src="vm8.png" title="vm8.png" alt="vm8.png" width="310" />

In *Opzioni avanzate* nel campo 'Disk bus' è possibile scegliere il tipo di disco con cui operare: ide, sata, scsi, usb o virtio. Scegliendo subito Virtio al riavvio della nostra MV il sistema operativo non partirà, perché non ha i driver per riconoscere tale tipo di disco. Quindi, fino a che non verrà resa disponibile qualche altra soluzione dovremo utilizzare un *workaround*.

Si proceda scaricando da [qui](http://alt.fedoraproject.org/pub/alt/virtio-win/latest/images/bin/virtio-win-0.1-30.iso) l'immagine iso che contiene i driver virtio per windows e si aggiunga tale disco alla MV come segue. Cliccando su *Aggiungi hardware* e si aprirà la seguente finestra:

<img src="vm9.png" title="vm9.png" alt="vm9.png" width="310" />

Si scelga *Selezionare managed o altro storage esistente*, poi *Sfoglia*, *Sfoglia in locale* e si cerchi la iso nella posizione in cui è stata salvata e si clicchi su *Apri*. Il campo *Alloca l'intero disco ora* conviene che sia sempre selezionato. In *Tipo dispositivo* si selezioni 'IDE cdrom' e poi *Fine*.

Nei dettagli della MV comparirà il nuovo disco 'IDE CDROM 1'.

Nuovamente si clicchi sul pulsante *Aggiungi hardware*, poi su *Selezionare managed o altro storage esistente* -&gt; *Sfoglia* -&gt; *Sfoglia in locale* e si scelga la cartella in cui creare un piccolo disco virtio, chiamato in questo esempio VirtDisk. Cliccando su *Apri* si torni alla precedente finestra.

Nel campo delle dimensioni del disco *GB* si scriva 1,0 o una qualsiasi dimensione, ma non serve che sia molto grande. In *Tipo dispositivo* si selezioni 'Virtio Disk' e in *Storage format* si scelga 'raw' oppure 'qcow2' che a parità di prestazioni permette un risparmio di spazio occupato sul disco. Cliccando su *Fine* si dovrà attendere qualche istante per la creazione del piccolo disco virtio. Il nuovo disco si aggiungerà alla MV con il nome 'VirtIO Disk 1'.

Dopo queste operazioni la finestra dei dettagli della MV si presenterà più o meno come segue:

<img src="vm11.png" title="vm11.png" alt="vm11.png" width="310" />

Avviamo la MV sul pulsante con il triangolo *Play*.

Al termine del boot il sistema guest chiederà i driver di installazione del nuovo disco aprendo automaticamente la consueta finestra guida. Si scelga di installare i driver manualmente e si indichi il percorso dove trovarli, cioè nella iso che aggiunta poc'anzi, rilevata come un cdrom.

Si trovino i driver nella cartella WXP &gt; X86 e si clicchi su *Avanti* e al termine della procedura su *Fine*.

A questo punto si spenga il sistema guest. Il piccolo disco virtio non è più necessario, per cui nel menu *Visualizza* -&gt; *Dettagli* si clicchi con il tasto destro su *VirtIO Disk 1* e *Remove hardware*.

Si selezioni ora 'IDE Disk 1' e si modifichi il tipo di disco selezionando in *Disk bus* il tipo 'Virtio'. Al prossimo avvio il disco sarà configuato come disco VirtIO e riconosciuto dai driver già installati.

La finestra dei dettagli della MV dovrebbe presentarsi in questo modo:

<img src="vm12.png" title="vm12.png" alt="vm12.png" width="310" />

### Installazione driver Spice

La gestione delle periferiche video risulta abbastanza pesante per l'emulatore qemu-kvm, i filmati vengono a volte visualizzati a scatti, sia in locale che in streaming, quindi è necessario installare i driver spice per ovviare a questa difficoltà. In questo caso la procedura è molto più semplice.

Con la MV spenta si vada in *Visualizza* -&gt; *Dettagli* e nell'opzione *Schermo Spice* si controlli che nel campo *Tipo* sia impostato 'Spice'. Si avvii la MV e si faccia il download dei driver spice per windows da [qui](http://spice-space.org/download/binaries/spice-guest-tools-0.1.exe). La rete dovrebbe già essere configurata automaticamente e dovrebbe essere funzionante. Si installino i driver con l'eseguibile scaricato e si riavvii la MV. La gestione delle periferiche video non dovrebbe più rappresentare un problema.

<Categoria:Virtualizzazione>
