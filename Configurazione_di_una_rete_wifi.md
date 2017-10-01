Introduzione
------------

Come installare e configurare utilizzando ndiswrapper o madwifi per far funzionare la scheda wireless in una connessione wifi.
Nei portatili sono sempre "onboard" ormai, ma anche al lavoro o a casa se ne trovano sempre di più. Parliamo delle reti wireless, Questa guida vuole essere utile per far funzionare la propria scheda PCI oppure USB utilizzando il driver appropriato, configurando la connessione in base alla sicurezza scelta.

Identificazione del chip
------------------------

Prima di cominciare è necessario capire che chip monta la propria scheda, mentre il nome e modello probabilmente sarà conosciuto. Quindi, per una scheda PCI:

`# lspci`

Oppure, nel caso si tratti di una scheda USB:

`# lsusb`

Si avrà un output simile a questo:

    00:00.0 Host bridge: VIA Technologies, Inc. VT8377 [KT400/KT600 AGP] Host Bridge (rev 80)
    00:01.0 PCI bridge: VIA Technologies, Inc. VT8237 PCI Bridge
    00:0a.0 Ethernet controller: Atheros Communications, Inc. AR5212 802.11abg NIC (rev 01)
    00:0f.0 IDE interface: VIA Technologies, Inc. VT82C586A/B/VT82C686/A/B/VT823x/A/C PIPC Bus Master IDE (rev 06)
    00:10.0 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1.1 Controller (rev 81)
    00:10.1 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1.1 Controller (rev 81)
    00:10.2 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1.1 Controller (rev 81)
    00:10.4 USB Controller: VIA Technologies, Inc. USB 2.0 (rev 86)
    00:11.0 ISA bridge: VIA Technologies, Inc. VT8237 ISA bridge [KT600/K8T800/K8T890 South]
    00:11.5 Multimedia audio controller: VIA Technologies, Inc. VT8233/A/8235/8237 AC97 Audio Controller (rev 60)
    00:13.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8139/8139C/8139C+ (rev 10)
    01:00.0 VGA compatible controller: ATI Technologies Inc RV280 [Radeon 9200 SE] (rev 01)

Ora si sa che il chip è Atheros, ma è utile memorizzare la prima colonna, perché da questa si ricaverà l'ID PCI oppure USB.

    # lspci -n
    00:00.0 0600: 1106:3189 (rev 80)
    00:01.0 0604: 1106:b198
    00:0a.0 0200: 168c:0013 (rev 01)
    00:0f.0 0101: 1106:0571 (rev 06)
    00:10.0 0c03: 1106:3038 (rev 81)
    00:10.1 0c03: 1106:3038 (rev 81)
    00:10.2 0c03: 1106:3038 (rev 81)
    00:10.4 0c03: 1106:3104 (rev 86)
    00:11.0 0601: 1106:3227
    00:11.5 0401: 1106:3059 (rev 60)
    00:13.0 0200: 10ec:8139 (rev 10)
    01:00.0 0300: 1002:5964 (rev 01)

Ora collegarsi alla lista delle schede supportate da [ndiswrapper](http://ndiswrapper.sourceforge.net/mediawiki/index.php/List) e cercare la propria in base al modello e l'ID PCI o USB. Per l'esempio concreto si trova l'ID, ma non in corrispondenza della scheda giusta, invece si trova un link presso un'altra scheda che conferma che si dovrà capire se è supportata in [madwifi](http://madwifi.org/wiki/Compatibility)...ed eccola, completamente supportata, viene indicato anche il chipset, come da output "lspci", ovvero Atheros 5212.

Si proseguirà direttamente con l'installazione di madwifi, per chi ha una scheda supportata da ndiswrapper deve continuare a leggere [qui](Configurazione_di_una_rete_wifi#Installazione_di_ndiswrapper "wikilink"), dove si parla dell'installazione di ndiswrapper e poi delle configurazioni delle schede con i driver madwifi e ndiswrapper.

Installazione di madwifi
------------------------

Per installare madwifi si può scaricare il file sorgente dal sito ufficiale e compilarlo oppure installare il pacchetto madwifi e il pacchetto per il kernel da livna. Per fare la seconda (e la più semplice) si deve configurare i [repository](:Categoria:Repository "wikilink") e poi digitare nel terminale:

`# dnf --enablerepo=livna install kmod-madwifi madwifi `

L'ultima versione di madwifi verrà installata insieme al modulo del kernel e probabilmente alla propria scheda verrà dato il nome del dispositivo *wifi0*. Per l'uso serve però una piccola modifica, perchè *wifi0* la si dovrà configurare come la scheda *eth0*, invece per il wireless si ha bisogno di un dispositivo *ath0*.
Per verificarlo si può andare nella sezione "rete" del menu di amministrazione per poi vedere se si riesce a caricare il modulo per *ath0*. Tradotto in parole povere (visto che nell'esempio c'è solo una scheda wifi0 e nient'altro), verificare inanzitutto se il modulo che si vuole caricare (è il *ath\_pci*) è presente e poi modificare il *modprobe.conf*: Ora aprire il file */etc/modprobe.conf* con l'editor preferito e fare sì che ci siano queste tre righe all'interno:

`alias ath0 ath_pci`
`options ath_pci autocreate=sta  `
`alias wifi0 ath_pci`

Salvare e chiudere tornando nel terminale e caricare il driver (per la scheda PCI) verificando il nome del dispositivo:

`# modprobe ath_pci`

E' giunto il momento di configurazione della scheda, andare quindi in *amministrazione &gt; rete* e aggiungere un nuovo dispositivo wireless che si nominerà, selezionandolo dal menu dei dispositivi, come da output di iwconfig, nel caso specifico ath0.
Scegliere se usare un IP fisso o il DHCP (consigliato), salvare e uscire. Non preoccuparsi se prima del salvataggio verrà detto che non è possibile attivare la scheda o prendere un IP dal Router o Access Point, lo si risolverà successivamente.
Tornando nel terminale si tenterà di tirare su la propria scheda, dopodichè si può fare uno scan della propria rete:

`# ifconfig ath0 up`
`# iwlist ath0 scan`

La scheda è installata, almeno per quanto riguarda il driver, il modulo del kernel e la rete. A questo punto si vorrà anche navigare in Internet immagino, ma non funziona ancora, manca ancora il collegamento al Router o al Access Point che si vedrà dopo, diversificando la configurazione per una rete aperta, con chiave Wep o attraverso WPA-Psk.
Andare avanti fino a trovare la configurazione e gli strumenti necessari per andare finalmente online.

Installazione di ndiswrapper
----------------------------

### Prerequisiti

Per installare ndiswrapper è necessario, a differenza del driver madwifi, soddisfare alcuni prerequisiti:

1.  Aver compilato il proprio kernel o almeno installato gli header del kernel, per farlo basterà digitare, dopo aver configurato i repository:
        # dnf install kernel-devel

    e poi, per avere il link ai propri header nella posizione giusta, creare un link simbolico:

        # ln -s  /usr/src/kernels/<versione-del-kernel> /lib/modules/<versione-del-kernel>/build

2.  Avere i driver per la propria scheda di winXP, ovvero il file \*.inf, \*.sys e \*.cab.

### Installazione

Per prima cosa scaricare il pacchetto dal [sito ufficiale](http://sourceforge.net/projects/ndiswrapper) e scompattarlo da terminale, digitando:

`# tar -zxvf versione-ndiswrapper.tar.gz`
`# cd versione-ndiswrapper`

Ora serve compilarlo, per farlo si scrive nel terminale:

`# make distclean`
`# make`
`# make install`

Ci metterà un pochino, si può seguire le operazioni e aspettare che la compilazione termini. Dopodichè si deve installare il driverXP, è importante che sia un driver perfettamente funzionante!

`# ndiswrapper -i filename.inf`

Ora il driver è installato, si può verificare il tutto con:

`# ndiswrapper -l`

Ora si carica il modulo, prima è meglio verificare se ci sono errori e quindi si digita:

`# depmod -a`
`# modprobe ndiswrapper`

E per vedere la propria scheda attiva con il suo dispositivo si può digitare:

`# iwconfig`

Configurazione della connessione wifi in un sistema aperto
----------------------------------------------------------

Dopo aver visto le installazioni con i due driver per le schede wireless ora si vuole descrivere come configurare correttamente la connessione al router o access point. Per primo la soluzione più semplice ma anche meno sicura, ovvero quella in un sistema aperto.
Esiste uno strumento in modalità grafica che potrà dare una mano nella configurazione, senza dover specificare tutto su linea di comando. Si installa con:

`# dnf install wlassistant`

Il programma è molto piccolo e lo si troverà nel menu di amministrazione del sistema, la configurazione è semplice ed intuitiva: ![](Wlass1.jpg "fig:Wlass1.jpg")

![](Wlass2.jpg "fig:Wlass2.jpg") Si aprirà una schermata di configurazione della propria rete, nella quale bisogna digitare il nome della rete (ESSID) e la configurazione IP o DHCP. Nella scheda di sicurezza si sceglierà una rete aperta e si confermano le impostazioni cliccando su OK.
Ora si sceglie la rete con il tasto destro e ci si connette al router o all'access point.
Per connettere la scheda wifi al boot è necessario che in *amministrazione &gt; reti* sia attivato il flag su "connetti all'avvio del sistema". ![](Wlass3.jpg "fig:Wlass3.jpg")

Configurazione della connessione wifi in un sistema protetto con chiave WEP
---------------------------------------------------------------------------

Anche se si dovesse scegliere una cifratura WEP il consiglio è di installare wlassistant (come per il sistema aperto), che per semplicità ed efficacia è un ottimo strumento ad interfaccia grafica.
Eseguire quindi i passi della configurazione aperta, ma invece di scegliere un sistema "open", e quindi aperto, si sceglierà quello "restricted" inserendo la chiave WEP nel campo sottostante.
A questo punto è possibile connettersi alla rete, che verrà identificata in grassetto una volta connessi. ![](Wlass4.jpg "fig:Wlass4.jpg") Per avviare la scheda all'avvio scegliere sempre la scheda di configurazione in *amministrazione &gt; reti* e flaggare la connessione all'avvio; unica cosa in più che si deve fare è inserire la chiave WEP che viene richiesta nel campo successivo, ma sempre all'interno della configurazione.

Configurazione della connessione wifi in un sistema protetto con chiave WPA-PSK
-------------------------------------------------------------------------------

La configurazione con cifratura WPA-PSK è un pochino più difficile ma anche la più sicura. Ci sono vari strumenti, come d'altronde per le altre cifrature, che si possono utilizzare, ma nessuno in modalità grafica da un supporto al 100% per il WPA-PSK.
Si userà quindi il metodo testuale, installando prima di tutto *wpa\_supplicant*:

`# dnf install wpa_supplicant`

Si può procedere subito con il file di configurazione aprendo con il proprio editor di testo preferito il file */etc/wpa\_supplicant/wpa\_supplicant.conf*.
 Di seguito un esempio (con \# viene indicato qualche commento utile).

    ctrl_interface=/var/run/wpa_supplicant
    ctrl_interface_group=0
    eapol_version=1
    # ap_scan=0,1,2 di solito funziona 1
    ap_scan=1
    fast_reauth=1

    network={
            # nome della nostra rete
            ssid="nome-rete"
            proto=WPA
            key_mgmt=WPA-PSK
            pairwise=TKIP
            group=TKIP
            # psk=chiave segreta
            psk="password"
    }

Salvare e uscire. Digitare nel terminale:

`# wpa_passphrase nome-rete password`

si avrà come output la parte della rete del file di configurazione:

    network={
            ssid="nome-rete"
            key_mgmt=WPA-PSK
            # psk=password
            psk="chiaveHEX123ABC"
    }

Fatto questo bisogna connettersi al router, per verificare che sia tutto ok, quindi digitare nel terminale per identificare la rete alla quale ci si vuole connettere:

`# iwconfig ath0 essid nome-rete`

Sostituire *ath0* se necessario con il dispositivo che usa la scheda wireless.
Ora tirare su la scheda e lanciare il demone di *wpa\_supplicant* indicando il driver usato, ovvero:

`# ifconfig ath0 up`
`# wpa_supplicant -Bw -Dwext -iath0 -c/etc/wpa_supplicant/wpa_supplicant.conf -qq`

Anche qui, se necessario sostituire *ath0* con il dispositivo che usa la propria scheda, se si utilizza il driver ndiswrapper invece di *-Dwext* usare *-Dndiswrapper*.
Infine connettersi facendosi assegnare un indirizzo dal router in automatico:

`dhclient ath0`

Se tutto funziona per il verso giusto si dovrebbe essere online, e lo si può verificare anche attraverso gli strumenti ad interfaccia grafica come wlassistant.
Se la connessione dovrà avvenire direttamente all'avvio è utile uno script da far eseguire durante il boot. Quindi, prima di tutto, in *amministrazione &gt; servizi* attivare il demone wpa\_supplicant. Salvare e uscire.
Lo script da far eseguire lo si inserirà in */etc/rc.local* (l'ultimo che viene eseguito durante la fase di boot), nel quale si aggiungeràla seguente riga:

`/usr/local/sbin/wifi-script`

Lo script */usr/local/sbin/wifi-script* invece è il seguente, è un file che contiene niente meno che i comandi visti prima:

    #!/bin/bash

    # specifica il nome della rete cui connettersi
    iwconfig ath0 essid nome-rete

    # Attiva la scheda di rete
    ifconfig ath0 up

    # Lancia il demone che gestisce la protezione WPA
    wpa_supplicant -Bw -Dwext -iath0 -c/etc/wpa_supplicant/wpa_supplicant.conf -qq

    # Chiede al dhcp server del router un indirizzo ip
    dhclient ath0

Ora non solo si potrà navigare ma ogni volta che si avvia il PC esso si connetterà automaticamente al proprio router o all'access point.

<Categoria:Wi-Fi>
