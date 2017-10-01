Le modalità per l'installazione di una stampante multifunzione sono diverse. In questo caso si parla di una stampante e scanner con la funzionalità wireless. Nel caso di un collegamento tramite usb, non si sono riscontrati particolari problemi, per cui i passi sono semplicissimi:

`# yum install hplip hplip-gui libsane-hpaio xsane libusb sane net-snmp-devel libusb-devel sane-backends-devel`

Dopodichè, da utente normale, si lancia il comando:

`$ hp-setup`

che permette l'installazione e la configurazione della stampante selezionando l'opzione Wireless/802.11.
La configurazione iniziale è da fare con l'usb inserita mentre il prosieguio è del tutto intuitivo. Il programma installerà la stampante e lo scanner.
Con il tool:

`$ hp-toolbox`

si potranno gestire tutte le impostazioni e le opzioni di stampa.

<Categoria:Stampanti>
