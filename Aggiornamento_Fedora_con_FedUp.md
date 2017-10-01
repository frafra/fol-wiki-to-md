Introduzione
------------

**FedUp** (**FED**ora **UP**grader) è il tool di aggiornamento per le versioni di Fedora dalla 17 in poi. Esso sostituisce in tutto e per tutto [PreUpgrade](Aggiornamento_Fedora_con_preupgrade "wikilink") e l'aggiornamento da DVD, che con il passaggio a Fedora 18 sono divenuti obsoleti.
Per aggiornare Fedora 16 alla versione 18 è necessario prima passare a Fedora 17 con PreUpgrade, e successivamente fare l'aggiornamento con FedUp, in quanto questo tool è in grado di aggiornare soltanto le versioni di Fedora dalla 17 in poi.

Funzionamento
-------------

Il processo che compie FedUp si divide in due parti.
La prima, attraverso il client installato sul sistema da aggiornare, individua e scarica tutti i pacchetti necessari per l'aggiornamento, compreso l'initramfs e il kernel.
Una volta scaricati tutti i pacchetti FedUp riavvia il sistema e passa alla seconda fase: solamente **dopo** il riavvio, infatti, vengono effettivamente installati tutti i pacchetti scaricati precedentemente e verrà visualizzata una barra per segnalare l'avanzamento del processo di aggiornamento.
Nello stato attuale FedUp è disponibile soltanto da riga di comando, una GUI [verrà implementata](https://fedoraproject.org/wiki/FedUp#The_FedUp_Client) (forse) in futuro.

Preparazione del sistema
------------------------

Le operazioni che seguono vanno tutte eseguite con privilegi di root:

`$ su -`
`password_di_root`
`#`

Per poter passare da una versione di Fedora all'altra è necessario portare la vecchia release allo stato più aggiornato possibile. Di conseguenza la prima cosa da fare è un aggiornamento totale del sistema:

`# yum update`

Una volta completato l'update è buona norma cancellare la cache di yum, per essere certi che non influisca nell'operazione di upgrade.

`# yum clean all`

Se c'è quindi stato bisogno di riavviare il computer a causa di aggiornamenti del kernel, bisognerà nuovamente loggarsi nel terminale come utente root per proseguire.

### Installazione pacchetto Fedup

È buona norma utilizzare l'ultima release di fedup disponibile nei repository *stabili* di fedora, installabile tramite:

`# yum install fedup`

Si invitano tutti gli utenti che riscontrano dei bug o problemi simili nell'upgrade con la versione *stabile* di fedup, a fare una ricerca sul [forum](http://forum.fedoraonline.it) per trovare discussioni simili, ed eventualmente segnalarlo aprendo una nuova discussione.
Se vengono rilevati *problemi* di upgrade del sistema utilizzando la versione di fedup proveniente dai *repository stabili*, installata al punto precedente, si può ***tentare*** di proseguire l'upgrade con la versione di fedup proveniente dai *repository di testing* di fedora (solo se all'interno è già presente un nuovo pacchetto), in modo da avere la versione più aggiornata possibile che possa risolvere il problema riscontrato (non si ha la sicurezza però che questa versione sia esente da *altri* bug):

`# yum --enablerepo=updates-testing install fedup`

Opzioni utili da attivare durante il recupero dei file
------------------------------------------------------

### Salvataggio file di log

Può essere utile aggiungere al comando fedup, nelle sue varie tipologie sotto illustrate, l'opzione ***--debuglog***.
Questa opzione permette di salvare l'output che fedup rilascia durante l'esecuzione in un file, consultabile in seguito in caso di problemi. Ad es:

`fedup --debuglog=/home/utente/fedupdebug.log [altre opzioni]`

Finite le operazioni preparative si può controllare il file di log *fedupdebug.log* per eventuali errori.

Recupero effettivo dei nuovi pacchetti
--------------------------------------

A questo [indirizzo](https://fedoraproject.org/wiki/Common_F22_bugs#Upgrade_issues) è reperibile una lista con i problemi più comuni riscontrati nell'upgrade verso Fedora 22.
A quest'altro [indirizzo](https://fedoraproject.org/wiki/Common_F21_bugs#Upgrade_issues) è invece reperibile una lista con i problemi più comuni riscontrati nell'upgrade verso Fedora 21.

### Aggiornamento verso Fedora 22

Per eseguire l'aggiornamento verso Fedora 22, basta utilizzare il seguente comando:

`# fedup --network 22`

### Aggiornamento verso Fedora 21

Fedora 21 è stata rilasciata in 3 categorie di prodotti (**<PRODUCT>**):
\* **Workstation**: pensata per l’utente Desktop, porta con sé molti programmi potenti ed è equipaggiata con il DE Gnome;
\* **Server**: per l'utente Server;
\* **Cloud**: con varie immagini, sia per Cloud privati che pubblici.
Per informazioni più dettagliate, visitare la [pagina dedicata](https://getfedora.org/) sul portale principale del FedoraProject.
Per l'upgrade a F21 è stata quindi aggiunta una nuova opzione a FedUp: "--product=**<PRODUCT>**"
Per aggiornare alla nuova Fedora Workstation, usare: ***"--product=workstation"***. Questo comando installerà tutti i pacchetti dell'installazione di default Fedora 21 Workstation; includendo anche GNOME 3 come Desktop Environment, in aggiunta a tutti i pacchetti già installati.

Se si preferisce rimanere sul generale, semplicemente aggiornando i pacchetti già installati sulla propria macchina, aggiungere: **"--product=nonproduct"**.
La sequenza "minima" corretta quindi per aggiornare il sistema a Fedora 21 è:

`# fedup --network 21 --product=[workstation OPPURE server OPPURE cloud OPPURE nonproduct]`

Altri metodi d'aggiornamento
----------------------------

È possibile effettuare un upgrade del sistema anche con altri metodi oltre al download dei pacchetti dalla rete, come visto finora: questi metodi sono utili soprattutto per macchine senza connessione ad internet.

### Aggiornamento con un file ISO

Per aggiornare Fedora utilizzando un file ISO è necessario che esso risieda sulla macchina da aggiornare. E' possibile attivare il repo *updates* se si possiede una connessione di rete attiva. Il file ISO d'esempio sarà in '' /home/user/fedora-19.iso'', che ovviamente va sotituito con il file e la location del proprio file ISO.

`# fedup --iso /home/user/fedora-19.iso`

### Aggiornamento da un altro device

E' possibile utilizzare drive ottici o altri device in cui è stata installata la versione di Fedora verso cui si desidera fare l'upgrade per procedere con l'aggiornamento. Nell'esempio si assume che la sorgente sia posizionata in */mnt/fedora*.
Dopodiché basta eseguire:

`# fedup --device /mnt/fedora`

Aggiornamento
-------------

Seguire i seguenti passaggi per completare l'aggiornamento:

1.  Se *FedUp* ha completato le operazioni di recupero dei pacchetti senza rilevare errori, riavviare il sistema.
2.  Al riavvio dovrebbe apparire in Grub una nuova voce **System Upgrade**.

<!-- -->

1.  Apparirà uno splashscreen Plymouth in cui appare una barra di avanzamento del processo in corso.
    -   Premendo *ESC* si può visualizzare più dettagliatamente quanto sta succedendo.

2.  Completato l'aggiornamento il sistema si riavvia in automatico e farà il boot con la nuova voce della versione di Fedora aggiornata.

Per aggiornare Grub si può seguire [questa guida](Reinstallare_Grub "wikilink").

Riferimenti
-----------

-   Guida ufficiale del fedoraproject su FedUp: <https://fedoraproject.org/wiki/FedUp>

<Categoria:Installazione>
