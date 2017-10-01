Introduzione
------------

![](Artwork_DesignService_fedora-iso-usb.png "Artwork_DesignService_fedora-iso-usb.png")

Una Live USB, consente di avviare Fedora su un computer senza obbligatoriamente installare la distribuzione sull'hard disk dello stesso. L'intento della presente guida, non è quello di elencare tutti i metodi ufficialmente supportati, bensì di riassumere brevemente quelli più raccomandati. In caso di problemi con i passaggi qui delineati e, per una lista più completa, si raccomanda quindi di consultare la [guida ufficiale del Fedora Project](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB). I file ISO necessari invece, sono facilmente reperibili dal sito [getfedora](https://www.getfedora.org/it/) tramite browser, da qualsiasi sistema operativo.

Identificare la propria chiavetta
---------------------------------

Per evitare di agire su un dispositivo diverso da quello scelto, occorre assicurarsi di identificare correttamente il supporto che andrà utilizzato.

### Fedora e altre distribuzioni GNU/Linux

Dopo aver montato la chiavetta, può risultare utile l'utilizzo del comando *`$` `df` `-h`*. Come mostrato dall'immagine d'esempio, la dimensione della partizione **/dev/sdb1** - e la directory in cui essa è montata – sono inequivocabili.

<img src="liveusb_fedora_1.png" title="GNU/Linux: df -h." alt="GNU/Linux: df -h." width="500" />

Un altro comodo output, è quello derivante da *`$` `blkid`*. Indicando la tipologia del file system di /dev/sdb1 come “**vfat**”, esso conferma e rafforza l'ipotesi precedente. Se è stata applicata un'etichetta, essa viene visualizzata in questo modo: *`LABEL=Etichetta`*. <img src="liveusb_fedora_2.png" title="fig:GNU/Linux: blkid." alt="GNU/Linux: blkid." width="500" />

### Windows

I sistemi Microsoft, utilizzano le lettere – **esempio: “E:”** - per identificare le memorie di massa. Visionabili da *Computer*, le partizioni delle pendrive vengono solitamente elencate all'interno del raggruppamento *Dispositivi con archivi rimovibili*.

<img src="liveusb_windows_1.png" title="Supporti rimovibili in Windows 7." alt="Supporti rimovibili in Windows 7." width="500" />

### Mac Os

All'interno dei sistemi operativi Apple, è possibile – in alternativa a *df -h* - ricorrere all'utility **diskutil** per la lista delle memorie di massa connesse. L'output da interpretare è il seguente:

`$ diskutil list`

<img src="liveusb_mac_1.png" title="Mac Os: diskutil list." alt="Mac Os: diskutil list." width="500" />

<img src="liveusb_mac_2.png" title="Mac Os: df -h." alt="Mac Os: df -h." width="500" />

Creazione della LiveUSB
-----------------------

Di seguito si delineano i passaggi consigliati, suddivisi per sistema operativo. Si presuppone che l'utente abbia già scaricato il file ISO relativo alla versione e al prodotto Fedora scelto.

### Fedora: Metodo livecd-iso-to-disk

Se si dispone di un computer che presenta già una versione recente di Fedora, uno dei metodi più indicati è quello proposto dal programma ''livecd-iso-to-disk.

Per prima cosa, occorre installare il pacchetto che ne fornisce le funzionalità:

`# dnf install livecd-tools`

Successivamente, conviene posizionarsi nella directory che contiene il file ISO per la creazione della Live (per esempio, **/home/giulio/Scaricati**).

`# cd /home/giulio/Scaricati`

Di seguito, il comando per applicare il file **Fedora-Live-Workstation-x86\_64-23-10.iso** alla pendrive **/dev/sdX**. Sostituire i valori indicati con quelli la ISO scelta e l'identificativo associato alla propria chiavetta (per esempio, /dev/sdc). Il primo esempio riguarda sistemi BIOS classici:

`# livecd-iso-to-disk --format --reset-mbr Fedora-Live-Workstation-x86_64-23-10.iso /dev/sdX`

Se si desidera creare una live da avviare su computer con firmware UEFI, è necessario in aggiunta anche il parametro **--efi**, come mostrato dal seguente listato:

`# livecd-iso-to-disk --format --reset-mbr --efi Fedora-Live-Workstation-x86_64-23-10.iso /dev/sdX`

Inizialmente, il programma ci avverte che tutti i dati del dispositivo scelto verranno persi. Premere il tasto “**Invio**” per procedere.

<img src="liveusb_fedora_3.png" title="Fedora: livecd-iso-to-disk." alt="Fedora: livecd-iso-to-disk." width="500" />

Se – come nella maggior parte dei casi – un filesystem è già presente, è necessaria un'ulteriore conferma. Digitare “**s**” e convalidare con un “**Invio**” da tastiera.

<img src="liveusb_fedora_5.png" title="fig:livecd-iso-to-disk: processo avviato." alt="livecd-iso-to-disk: processo avviato." width="200" /> <img src="liveusb_fedora_6.png" title="fig:livecd-iso-to-disk: avanzamento." alt="livecd-iso-to-disk: avanzamento." width="200" /> <img src="liveusb_fedora_4.png" title="fig:livecd-iso-to-disk: ulteriore conferma." alt="livecd-iso-to-disk: ulteriore conferma." width="500" />

Dopo qualche minuto di elaborazione, un messaggio di conferma finale, certificherà il successo dell'operazione. *Target device is now setup with a Live image*, indica infatti che il processo si è concluso ed è possibile ora smontare ed utilizzare la nuova Live Usb.

<img src="liveusb_fedora_7.png" title="Fedora: livecd-iso-to-disk." alt="Fedora: livecd-iso-to-disk." width="500" />

### Windows: Metodo Rawrite32

Nato per processare di immagini di sistema NetBSD all'interno di Windows, Rawrite32 può essere utilizzato anche per la creazione di dispositivi Live di Fedora. Soggetto a licenza BSD, è gratuitamente ottenibile dalla [http://www.netbsd.org/~martin/rawrite32/ Home page](http://www.netbsd.org/~martin/rawrite32/_Home_page "wikilink") del progetto. Una volta installato ed avviato, occorre selezionare la ISO desiderata, mediante il bottone **Open**. Per trovare tale tipologia di file, è necessario impostare il filtro **All files (\*.\*)** all'interno della finestra dialogica che viene aperta.

<img src="liveusb_windows_2.png" title="Rawrite 32: selezione ISO effettuata" alt="Rawrite 32: selezione ISO effettuata" width="500" />

In seguito al calcolo automatizzato dell'MD5 Checksum, il programma è pronto ad operare. All'interno del campo **Target**, va ora attentamente selezionata la chiavetta desiderata. Il bottone **Write to disk…** consente di iniziare il processo, previa ulteriore conferma dell'utente.

<img src="liveusb_windows_3.png" title="Rawrite 32 pronto per la scrittura" alt="Rawrite 32 pronto per la scrittura" width="500" />

<img src="liveusb_windows_4.png" title="Rawrite 32: conferma" alt="Rawrite 32: conferma" width="500" />

### GNU/Linux e MacOs: Metodo dd

**dd** è un semplice tool a riga di comando che consente di applicare, all'interno di sistemi operativi derivanti da Unix, un file ISO ad un dispositivo rimovibile. La sua natura minimale e la stabilità raggiunta in svariati anni di esecuzione, lo elegge a metodo praticamente infallibile per la creazione di Live Usb.

Come primo passaggio, per comodità, conviene posizionarsi nella directory che contiene il file ISO per la creazione della Live (per esempio, **/home/giulio/Scaricati**) ed effettuare il login come root.

`$ cd /home/giulio/Scaricati`
`# su`

Di seguito, il comando per applicare il file **Fedora-Live-Workstation-x86\_64-23-10.iso** alla pendrive **/dev/sdX**. Sostituire i valori indicati con quelli della versione di Fedora scelta e l'identificativo associato alla propria chiavetta (per esempio, /dev/sdb o /dev/disk1). Il primo esempio riguarda una distro GNU/Linux:

`# dd if=Fedora-Live-Workstation-x86_64-23-10.iso of=/dev/sdX bs=1M`

Per Mac Os, il passaggio è il medesimo, ma occorre seguire la differente nomenclatura dei sistemi operativi Apple.

`# dd if=Fedora-Live-Workstation-x86_64-23-10.iso of=/dev/diskX bs=1M`

<img src="liveusb_linux_2.png" title="Esempio d&#39;esecuzione di &#39;dd&#39; all&#39;interno di un sistema Fedora 22 Xfce" alt="Esempio d&#39;esecuzione di &#39;dd&#39; all&#39;interno di un sistema Fedora 22 Xfce" width="500" />

Fonti
-----

[Guida ufficiale Fedora Project](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB)

[:Categoria:Installazione](:Categoria:Installazione "wikilink") [Categoria:Scrittura in corso](Categoria:Scrittura_in_corso "wikilink")
