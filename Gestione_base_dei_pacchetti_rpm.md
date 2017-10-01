In questo piccolo articolo sono raccolti i comandi base per l'installazione dei pacchetti rpm e l'uso di yum.

Installazione software con RPM su Fedora
----------------------------------------

Uno degli ostacoli più duri da superare quando si inizia ad usare un nuovo sistema operativo è quello di sapere come installare i software desiderati o usati spesso e che non vengono installati di default. In ambienti Linux, di certo non troveremo dei file .exe che fanno tutto il lavoro di installazione (e spesso qualcos'altro); invece si scoprirà che ci sono modi per installare un software, inizialmente difficili da interpretare, ma che con un po' di pazienza e di studio risulteranno piuttosto semplici.

Sicuramente la strada più semplice è quella di utilizzare yum (Yellowdog Updater Modified) che è un package manager (manager di pacchetti basato sugli rpm), non prima di aver configurato i repository giusti per la propria versione di Fedora, ma per questo si rimanda alle ottime guide che si possono trovare su Fedoraonline. Un esempio: si ha la necessità di installare un software per Fedora che gestisca la contabilità personale; bene allora andare in programmi-&gt;sistema-&gt;terminale:

`$ yum search personal finance manager`

le parole chiave sono molto importanti per una buona ricerca; yum cercherà le tre parole chiave (personal, finance, manager) tra le descrizioni dei pacchetti a disposizione nei repository on line e darà una lista degli rpm trovati. Tra i primi pacchetti, dando quel comando, yum ha trovato:

`grisbi.i386 : Personal finances manager `

allora:

`$ su -`
`password: password di root             `
`# yum install grisbi`

yum installerà il software “grisbi.i386”, non prima di aver chiesto una conferma. Se il software non convince, lo si può rimuovere:

`# yum remove grisbi`

Può succedere però che yum non trovi il software che si cerca o che abbia a disposizione dei software che all'utente non vadano bene.
Si può fare una ricerca più ampia del pacchetto software .rpm, ma bisogna tener presente delle indicazioni:

1.  Su Internet esistono vari siti con hanno a disposizione dei database di pacchetti rpm, dedicati ad una o più distribuzioni Linux, come “RPMfind” o “RPMseek”;
2.  E' fondamentale fare attenzione al tipo di rpm:

`pacchetto.i386.rpm                  pacchetto per architetture di processori a 32 bit`
`pacchetto.src.rpm                   contiene codice sorgente`
`pacchetto-devel.i386.rpm            dedicato solo allo sviluppo (development)`
`pacchetto.noarch.rpm                pacchetto che non dipende dal tipo di architettura `
`pacchetto-doc.rpm                   pacchetto che contiene anche documentazione`

Una volta ottenuto il pacchetto si può installarlo usando RPM.

Rpm (RedHat Package Manager) è un potente gestore di pacchetti rpm che permette di creare, installare, interrogare, verificare, aggiornare o rimuovere singoli pacchetti software. Per pacchetto s'intende un archivio di file che sono le “fonti” di installazione o rimozione di un dato software; essi si possono presentare di due tipi: binary packages (pacchetti binari) usati per incapsulare i software da installare o source packages (pacchetti sorgente) che contengono il codice sorgente e le istruzioni per compilarlo per avere un binary package.

Per prima cosa spostarsi da terminale nella cartella contenente il file .rpm, ammettendo che la cartella sia Download:

`$ cd home/utente/Download`
`$ su`
`password: password di root`

Comandi di installazione/aggiornamento
--------------------------------------

Per installare ad esempio il file package-1.0.rpm bisogna digitare

`# rpm -i package-1.0.rpm`

Per aggiornare ad un pacchetto più recente ad es. package-2.0.rpm bisogna digitare

`# rpm -U package-2.0.rpm`

quest'ultimo comando aggiorna il pacchetto alla versione più recente, dopodiché rimuove le versioni più datate.

Se invece si volesse tornare ad una versione precedente perché l'ultima ha ancora qualche problemino, allora bisogna procurarsi il pacchetto precedente ed es. package-0.9.rpm del software e da terminale digitare

`# rpm -U --oldpackage package-0.9.rpm`

Il postfisso --oldpackage è una delle numerose opzioni dei comandi generali; un'altra interessante opzione è --test che permette di effettuare un test prima di installare o aggiornare un pacchetto

`# rpm -i --test package.rpm  [/code]`

Comandi di rimozione
--------------------

Il comando generale per rimuovere un pacchetto è

`# rpm -e nomepackage`

se ad esempio è installato il pacchetto grisbi-0.5.9-8.fc10.i386.rpm allora da terminale digitare

`$ su -`
`password: password di root`
`# rpm -e grisbi`

Anche per il comando di rimozione *-e|--erase*' vale l'opzione *--test*

`# rpm -e --test grisbi`

mentre se vogliamo rimuovere più versioni installate dello stesso software, allora digitare

`# rpm -e --allmatches grisbi`

Comando di verifica
-------------------

Il comando *-V|--verify* confronta le informazioni del pacchetto appena installato con le informazioni dello stesso nei metadati del database che lo conteneva: confronta le dimensioni, i permessi, il tipo, il proprietario di ogni file; mentre i file non installati, come ad esempio la documentazione, saranno ignorati.
Installazione e verifica del pacchetto software-1.2.noarch.rpm

`# rpm -iV  software-1.2.noarch.rpm`

<Categoria:Sistema>
