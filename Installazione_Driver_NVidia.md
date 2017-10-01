\_\_TOC\_\_

Introduzione
------------

Fedora utilizza per le schede video NVidia (tra cui le GeForce) di default, senza necessità di configurazioni aggiuntive, il driver libero "[nouveau](http://nouveau.freedesktop.org/wiki/). Si possono tuttavia utilizzare, al suo posto, il driver proprietario (non libero) ufficialmente fornito da Nvidia stessa. Questa guida spiega come installare quest'ultimo.

Per installare i driver nVidia sono possibili, sostanzialmente, due metodi: tramite pacchetto rpm fornito da RPMFusion o tramite installer ufficiale. Di seguito verranno descritti entrambi.

### Serie di schede video NVidia supportate

Come primo passo, bisogna sapere a quale [serie](http://en.wikipedia.org/wiki/GeForce#Generations) appartiene la nostra scheda video. Per far ciò si può per esempio confrontare l'output del comando:

`# lspci|grep -i vga`

con [questa pagina di wikipedia](http://en.wikipedia.org/wiki/Comparison_of_Nvidia_graphics_processing_units), che elenca le gpu suddivise per serie.

Esistono infatti quattro driver diversi, a seconda della serie della scheda video:

-   **Serie 400 o superiori**, cioè schede video prodotte indicativamente a partire dal 2010 (GeForce 4xx, 5xx, 6xx, 7xx, 8xx, 9xx): **ultima versione del driver**;
-   **Serie da 8 e 300**, cioè schede video prodotte indicativamente dal 2006 al 2009 (GeForce 8xxx, 9xxx, 1xx, 2xx, 3xx): **driver versione 340**;
-   **Serie da 6 e 7**, cioè schede video prodotte indicativamente dal 2004 al 2006 (GeForce 6xxx, 7xxx): **driver versione 304**;
-   **Serie 5**, cioè schede video prodotte indicativamente nel 2003 (GeForce FX 5xxx): **driver versione 173**;
-   **Serie da 2 a 4**, cioè schede video prodotte indicativamente dal 2000 al 2002: **driver versione 96**.

NOTA: per fedora 20 attualmente non esistono driver aggiornati compatibili per schede serie 4 e precedenti, mentre per fedora 21 quelli per schede serie 5 e precedenti

Installazione dei drivers usando RPMFusion
------------------------------------------

### Installazione del driver

Occorre installare il pacchetto sviluppo del kernel:

`# dnf install kernel-devel`

Si può quindi installare il driver NVidia, facendo attenzione alla giusta versione del driver a seconda della scheda video utilizzata:

-   serie 400 o superiore

`# dnf install akmod-nvidia kmod-nvidia xorg-x11-drv-nvidia-cuda`

-   serie da 8 a 300

`# dnf install akmod-nvidia-340xx kmod-nvidia-340xx xorg-x11-drv-nvidia-340xx-cuda`

-   serie da 6 a 7

`# dnf install akmod-nvidia-304xx kmod-nvidia-304xx`

-   serie 5

`# dnf install akmod-nvidia-173xx kmod-nvidia-173xx`

-   serie da 2 a 4

`# dnf install akmod-nvidia-96xx kmod-nvidia-96xx`

L'installazione essenziale del driver Nvidia è terminata. Riavviare la macchina e controllare eventuali errori.

### Ulteriori configurazioni

In alcuni casi, può essere utile effettuare ulteriori operazioni, che vengono spiegate in questo paragrafo.

#### Accelarazione video per applicazioni a 32 bit in Fedora 64 bit

Se si sta utilizzando una fedora a 64 bit, e si vuole che l'accelerazione video sia disponibile anche per le applicazioni a 32 bit, bisogna inoltre installare un ulteriore pacchetto:

-   Per una serie 400 o superiore

`# dnf install xorg-x11-drv-nvidia-libs.i686`

-   Per una serie da 8 a 300

`# dnf install xorg-x11-drv-nvidia-340xx-libs.i686`

-   Per una serie 6 o 7

`# dnf install xorg-x11-drv-nvidia-304xx-libs.i686`

-   Per una serie 5

`# dnf install xorg-x11-drv-nvidia-173xx-libs.i686`

-   Per una serie da 2 a 4

`# dnf install xorg-x11-drv-nvidia-96xx-libs.i686`

#### In caso di mancanza della libreria OpenCL

Se programmi che utilizzano OpenCL affermano la mancanza di tale libreria, eseguire il comando

`# dnf install mesa-libOpenCL`

#### Decodifica filmati su gpu

Se si possiede una serie 8 o superiore, per poter usufruire della decodifica video offerta da VDPAU, bisogna aggiungere il pacchetto:

`# dnf install libva-vdpau-driver`

#### Risoluzione problemi monitor

Qualora il monitor non venga riconosciuto e la frequenza non sia quella indicata dal produttore, per una regolazione più "fine" del display e si vuole impostare i valori corretti, ci si deve servire di questo tool di nvidia per farlo. Occorrono i permessi di root, quindi:

`$ su`
`password`
`# nvidia-settings`

Da "X Server Display configuration" impostare la risoluzione e la frequenza a 60hz e salvare il file nel xorg.conf con il bottone che è visualizzato nella GUI. Dopodichè aprire il file xorg.conf ed inserire le modifiche:

`# gedit /etc/X11/xorg.conf `
`Section "Monitor"`
`   # HorizSync source: edid, VertRefresh source: edid`
`   Identifier     "Monitor0"`
`   VendorName     "Unknown"`
`   ModelName      "Samsung SyncMaster 950B"`
`   HorizSync       30.0 - 81.0`
`   VertRefresh     56.0 - 75.0`
`   Option         "DPMS"`
`EndSection`

Da notare che la sovrascrittura da parte di nvidia-settings ha tolto il path per il driver stesso, per cui non si avrà più il direct rendering attivo. Inserite, quindi, nel "file section" quanto necessario:

`Section "Files"`
`    FontPath        "/usr/share/fonts/default/Type1"`
`    `**`ModulePath` `"/usr/lib/xorg/modules/extensions/nvidia"`**
`    `**`ModulePath` `"/usr/lib/xorg/modules"`**
`EndSection`

Da Fedora 16 questa modifica non dovrebbe essere necessaria.
Salvare il proprio xorg.conf e riavviare il server X con `Ctrl+Alt+Backspace`.
Verificare ora se tutto è andato come desiderato:

`$ glxgears`
`37026 frames in 5.0 seconds = 7405.197 FPS`
`29492 frames in 5.0 seconds = 5898.224 FPS`
`29925 frames in 5.0 seconds = 5984.936 FPS`
`29787 frames in 5.0 seconds = 5957.285 FPS`
`29894 frames in 5.0 seconds = 5978.601 FPS`

Volendo si può anche abilitare gli effetti Desktop, ora tutto il necessario è stato attivato.

Dopo l'uso di:

`# nvidia-settings`

con versioni di Fedora precedenti alla 16 di controllare che in /etc/X11/xorg.conf sia presente la Section "Files"

#### Ripristinare Plymouth all'avvio del pc

Il driver proprietario NVidia non ha il KernelModeSetting, quindi la sua installazione disattiva il boot grafico Plymouth. Il problema è esclusivamente estetico, e solo per quei pochi secondi di avvio di Fedora (tra la schermata di grub e quella del login utente). Tuttavia è possibile ripristinare l'avvio di Plymouth [impostando manualmente la risoluzione video desiderata](http://doc.fedoraonline.it/Plymouth#Risoluzioni)

### Verifica della corretta installazione del driver

E' possibile verificare che il driver nvidia sia stato correttamente installato e sia in funzione.

-   Primo test:

`$ lspci -nnk | grep -i vga -A3`

deve restituire "Kernel driver in use: nvidia".

-   Secondo test:

`$ glxinfo | grep direct`

deve restiture come prima riga "direct rendering: Yes"

-   Terzo test (valido solo per la verifica della corretta decodifica filmanti sulla gpu per geforce serie 8 o superiore). Bisogna prima installare:

`# dnf install vdpauinfo libva-utils`

e poi verificare che non generino errori i seguenti comandi, che dovrebbero elencare le capacità di decodifica:

`$ vdpauinfo`
`$ vainfo`

### Disinstallazione del driver NVidia

Nel caso si voglia disinstallare i driver NVidia, è possibile farlo anche nel caso Fedora non possa avviarsi in modalità grafica.

`# dnf remove *nvidia*`

e poi riavviare

Installazione dei drivers usando l'installer scaricabile dal sito di nvidia
---------------------------------------------------------------------------

Questa procedura non è consigliata agli utenti meno esperti.

Una volta scaricato il package per la propria videocard [dal sito di NVidia](http://www.nvidia.it/Download/indexsg.aspx?lang=it), occorrerà procedere in runlevel 3, avviando Fedora in tale stato oppure dando:

`# init 3`

Quindi far partire l'installer con

`# sh NVIDIA-Linux-`<arch>`-`<version>`-pkgX.run`

Usando questo metodo, saranno necessarie alcune librerie; l'installer man mano dirà cosa è necessario. Personalmente nel sistema ho installato i gruppi "Strumenti di sviluppo" e "Librerie di sviluppo". Per installarli:

`# dnf groupinstall "Strumenti di sviluppo" "Librerie di sviluppo"`

(Se avete voglia di battere meno tasti potete dare:

`# dnf install @development-tools @development-libs`

Se si possiede un sistema a 64 bit, e si vuole che funzionino le "OpenGL 32 bit compatibility mode", si può installare:

`# dnf install glibc*686`

Non credo che si avrà bisogno di altro. Se si ha necessità di disinstallare i drivers nvidia usando questo II metodo occorrerà dare un:

`# nvidia-uninstall`

Se si avrà la necessità, l'utility

`# nvidia-xconfig `

genererà un nuovo xorg.conf creando automaticamente anche una copia di backup

Nel secondo metodo descritto, si avrà lo svantaggio di dover ad ogni aggiornamento dei drivers, procurarsi l'ultima versione e reinstallarli. Si dovrà fare lo stesso ad ogni nuova versione di kernel che si installerà.

Riferimenti
-----------

-   <http://rpmfusion.org/Howto/nVidia>
-   <http://www.nvidia.it/Download/index.aspx?lang=it>
-   <http://www.nvidia.com/object/unix.html>

[Categoria:Schede grafiche](Categoria:Schede_grafiche "wikilink")
