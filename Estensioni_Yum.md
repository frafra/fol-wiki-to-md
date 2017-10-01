Introduzione
------------

Esistono una serie di estensioni utili per Yum (**Y**ellowdog **U**pdater **M**odified) se si utilizza la linea di comando.
Ovviamente non si vuole elencare tutte le possibilità, aspetto per il quale si rimanda alle pagina *man*, ma si elencheranno quelle più significative. Per avere l'elenco dei plugin presenti sul sistema basta digitare:

`$ ls /etc/yum/pluginconf.d/`

Inoltre, per utilizzare i plugin, è necessario verificare che siano attivati. Per questo è necessario che nel file *'*/etc/yum.conf *'* ci sia l'impostazione dei plugin a 1, ovvero ci sia ***plugins=1***.
Per vedere tutti i plugin disponibili si può interrogare direttamente Yum:

`# yum provides yum-plugin-*`

L'output riporterà, oltre ai singoli pacchetti, anche una breve descrizione.

Yum-fastestmirror
-----------------

Siccome i pacchetti RPM per Fedora sono presenti su più di un server, quindi anche nei cosiddetti mirror, questo plugin verifica quale sia in quel preciso momento il server più veloce. Un'estensione che si rivela utile per minimizzare i tempi di installazione o disinstallazione dei singoli pacchetti.
Lo si installa così:

`# yum install yum-plugin-fastestmirror`

Yum-presto
----------

Un'altra estensione che velocizza il download, in questo caso gli aggiornamenti dei pacchetti presenti sul sistema è yum-presto. Installato di default sulle ultime versioni di Fedora, ha il compito di scaricare soltanto le differenze da un pacchetto all'altro, senza fare il download dell'intero RPM.
Per le versioni più vecchie va installato così:

`# yum install yum-plugin-presto`

Prima di utilizzare questo plugin, se non fosse installato di default, è necessario pulire la cache:

`# yum clean all`

Yum-downloadonly
----------------

E' possibile installare un plugin per scaricare i pacchetti RPM dai repository senza dover installare necessariamente il pacchetto. Questo plugin diventa utile per recepire dei pacchetti RPM da trasferire successivamente su altri sistemi.

`# yum install yum-plugin-downloadonly`

Dopo aver installato il pacchetto si dovrà lanciare Yum specificando le opzioni "--downloadonly" e "--downloaddir", identificando la directory dove salvare il pacchetto rpm. Per esempio:

`# yum install --downloadonly --downloaddir=/tmp/ unrar`

L'installazione verrà bloccata, perchè con queste opzioni verrà solo scaricato il pacchetto nella directory indicata nel opzione "--downloaddir". Se il pacchetto è già installato sul sistema e si è caricata l'ultima versione disponibile, il pacchetto non verrà scaricato.
Conviene dunque sfruttare il comando "yumdownload". Installare via yum il pacchetto yum-utils.

`# yum install yum-utils`

Dopodiché si richiama il comando yumdownloader seguito dal nome del pacchetto da scaricare.

`$ yumdownloader unrar`

<Categoria:Yum>
