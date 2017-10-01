\_\_TOC\_\_

Questa guida tratta l'installazione di Fedora su personal computer utilizzando la modalità *Net-Install*. Questa modalità è indicata per utenti più smaliziati che vogliono provare una nuova strada per installare Fedora.
Le raccomandazioni sono le stesse di una normale installazione. È perciò sempre consigliato creare un dischetto di ripristino, qualora fosse presente, del sistema operativo Windows a scanso di eventuali problemi futuri e, comunque, di eseguire sempre un backup dei propri dati importanti su dispositivi "esterni".

Introduzione
------------

La modalità di installazione Net-Install permette di scaricare una quantità di dati inferiore ad un live-cd o dvd (intorno ai 400MB contro i più di 800 di un live-cd o i 4GB di un dvd).
Questa procedura è utile se si ha disponibilità di una connessione a internet con ampia larghezza di banda, in quanto tutti i pacchetti che si scelgono di installare vengono scaricati completamente dai server "mirror" del fedoraproject; pertanto, più la connessione è veloce, meno tempo impiegherà il processo di installazione.

Download delle Immagini Iso
---------------------------

Tutte le versioni di Fedora sono liberamente scaricabili e vengono messe a disposizione dal FedoraProject. Recarsi nella [pagina di download del FedoraProject](http://fedoraproject.org/it/get-fedora-options#formats), scorrere verso il basso ed assicurarsi di scaricare la versione targata **CD di installazione da rete Fedora 20** nell'architettura specifica del sistema su cui si andrà a installare.
Per comprendere quale architettura supporta il sistema su cui si installerà, seguire i consigli della [documentazione ufficiale](http://docs.fedoraproject.org/en-US/Fedora/20/html/Installation_Guide/ch-new-users.html#sn-which-arch).
Si può ottenere la stessa iso per la modalità net-install anche scaricandola dai numerosi server mirror, cercandola sotto il nome di *boot.iso*. Notare che i file possono essere chiamati con nomi diversi (boot.iso, Fedora-*RELEASE*-*ARCHITETTURA*-netinst.iso) ma strutturalmente sono lo stesso file, solamente chiamato in modo diverso.

Preparazione all'installazione
==============================

L'immagine scaricata va quindi masterizzata su cd o copiata su una chiavetta usb.
Per maggiori informazioni su come creare un CD/DVD bootabile, consultare la [documentazione ufficiale del FedoraProject](http://docs.fedoraproject.org/en-US/Fedora/20/html/Burning_ISO_images_to_disc/index.html).

Per creare una penna usb bootabile seguire invece [queste istruzioni](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB/it).
Seguire ora le indicazioni della guida all'installazione di fedora, alla sezione [Avvio dell'installazione](Installazione_Fedora#Avvio_dell.27installazione "wikilink").

Riepilogo Installazione
-----------------------

La schermata principale presenta il *Riepilogo Installazione*, formato da tre categorie principali: **Localizzazione**, **Software** e **Sistema**, con le relative sottocategorie.
Si nota subito che in alcune sottocategorie ci possono essere dei triangoli gialli; questi simboli avvisano di dover completare i vari passaggi prima di procedere con l'installazione. Normalmente, se la connessione a internet è già stata stabilita, l'unico segnale di avvertenza rimane quello della *Destinazione di installazione*.
<img src="Netinstall_f20_main.png" title="fig:Riepilogo installazione con avvertenze sui passaggi da completare." alt="Riepilogo installazione con avvertenze sui passaggi da completare." width="800" />

Localizzazione
--------------

Per la categoria "Localizzazione" fare riferimento alla sezione [localizzazione](Installazione_Fedora#Localizzazione "wikilink") della guida principale.

Software
--------

Nella categoria Software sono presenti due voci: *Sorgente di Installazione* e *Selezione del Software*.
Se è già attiva una connessione a internet, l'installer "Anaconda" (il nome del programma che gestisce l'installazione) procede in automatico a scaricare i dati per proseguire e, una volta terminato, le due sotto-sezioni saranno selezionabili.
Se bisogna impostare parametri o protocolli specifici per attivare la connessione alla rete, questi si possono configurare nella sotto-categoria [Configurazione di rete](#Configurazione_di_Rete "wikilink"). Una volta che la connessione è stabilita e i dati necessari scaricati, si potrà finalmente accedere alle due sotto-categorie.

### Sorgente di Installazione

Una volta scaricati i sorgenti di installazione, cliccando sulla voce "Sorgente di Installazione" si possono definire dei parametri avanzati: <img src="Netinstall_f20_sorgenti.png" title="fig:Schermata &quot;Sorgenti di Installazione&quot;, contenente varie opzioni." alt="Schermata &quot;Sorgenti di Installazione&quot;, contenente varie opzioni." width="450" />

-   In questa sezione si ha la possibilità di specificare il protocollo di trasmissione dei dati (http, https, ftp, nfs) o "**Mirror più vicino**": quest'ultima è la scelta migliore, poiché si userà sempre il server più vicino, e quindi più rapido, in base alla propria locazione.
    In caso si voglia specificare un indirizzo server particolare da usare per installazione, come ad esempio *nfs* (guide ufficiali [in inglese](http://docs.fedoraproject.org/en-US/Fedora/20/html/Installation_Guide/ch-Installation_Phase_2-x86.html#s1-begininstall-nfs-x86) e [in italiano](http://docs.fedoraproject.org/it-IT/Fedora/11/html/Installation_Guide/ch03s05s02.html), quest'ultima parzialmente obsoleta), lo si può specificare nel campo seguente.
-   Nella casella "Aggiornamenti" si chiede se scaricare dal server i pacchetti predefiniti al momento del rilascio o se scaricare i pacchetti più aggiornati possibile.
    Normalmente dovrebbe essere disabilitata e il consiglio è di mantenerla così, in modo da scaricare tutti i pacchetti già aggiornati ed evitare un ulteriore aggiornamento una volta acceso il computer.
-   L'ultima sezione riguarda eventuali repository aggiuntivi da poter aggiungere oltre a quelli base, impostandone i parametri necessari. Una lista di alcuni repository dedicati a Fedora è contenuta nell'apposità categoria [Repository](:Categoria:Repository "wikilink").

### Selezione del Software

Una volta definiti i sorgenti di installazione si arriva alla parte cruciale e più importante del processo: la "Selezione del Software". In questa sezione è possibile scegliere quale ambiente Desktop installare (Gnome, Kde, XFCE, LXDE, ecc.) e, opzionalmente, quali componenti aggiuntivi o altre applicazioni installare (per es. "Libreoffice", "Strumenti di Amministrazione" e molti altri).
Fare riferimento alla guida principale nella sezione [Selezione Software](Installazione_Fedora#Selezione_Software "wikilink") per altre informazioni.
Cliccare quindi sul tasto *Fatto* in alto a sinistra per tornare al *Sommario di Installazione* e proseguire nella configurazione del processo di installazione.

Sistema e Installazione
-----------------------

Nella sezione "Sistema" trovano posto le sotto-categorie *Configurazione Rete* e *Destinazione di Installazione*.

### Configurazione di Rete

Se si è connessi a internet via cavo il riquadro Configurazione di Rete dovrebbe normalmente segnalare **"Cavo (p2p1) connesso"**; se si desidera invece usare altre impostazioni di rete, come ad esempio una connessione Wi-Fi o un proxy, si possono configurare ora.
Una volta che la connessione via rete è attiva, i due riquadri "Sorgente di Installazione" e "Selezione del Software" dovrebbero diventare grigi con un triangolino arancione in alto a destra, segno che "Anaconda" sta scaricando le informazioni e i dati necessari per procedere all'installazione. Procedere dalla relativa sezione.

### Destinazione di Installazione

Per quanto riguarda il partizionamento e l'installazione si rimanda alla sezione apposita nella [guida all'installazione](Installazione_Fedora#Sistema "wikilink") da DVD, poiché i passaggi sono identici.

Per eventuali dubbi o domande non contemplate in questa guida, cercare prima se è già stato discusso un problema simile all'interno del forum ed eventualmente chiedere.

That's all folks, enjoy! ;-)

<Categoria:Installazione>
