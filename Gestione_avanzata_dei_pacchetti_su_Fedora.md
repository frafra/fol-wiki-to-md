Introduzione
------------

Ecco alcune utili tecniche che rendono più facile la gestione dei pacchetti su Fedora.
Per approfondire la propria conoscenza sul formato RPM e imparare a creare i propri pacchetti è utile leggere il manuale Maximum RPM:
<http://www.rpm.org/max-rpm/>
Se si vogliono inviare i propri pacchetti nei repository di Fedora si devono rispettare queste regole durante la creazione del pacchetto:
<http://fedoraproject.org/wiki/Packaging/Guidelines>
Queste sono le istruzioni per chi, dopo essere diventato un esperto di RPM, volesse diventare un manteiner di Fedora:
<http://fedoraproject.org/wiki/PackageMaintainers/Join>

Yumdownloader
-------------

yumdownloader è un programma in grado di fare molte cose. Può essere usato per scaricare un pacchetto RPM dai repository, e se si desidera anche le sue dipendenze. Si possono scaricare sia pacchetti binari che pacchetti sorgenti. Invece di scaricare i pacchetti può essere usato per ottenere la lista degli URL dei pacchetti, e scaricarli da un altro PC con una connessione più veloce per esempio.
Si trova nel pacchetto yum-utils. L'equivalente su Debian di yumdownloader è apt-zip.

Questa è la sintassi:

`yumdownloader [opzioni] Lista-Pacchetti`

Queste sono le opzioni più importanti:

`--urls`

Invece di scaricare gli RPM, visualizza soltanto gli indirizzi dei pacchetti da scaricare.

`--resolve`

Assieme al pacchetto RPM scarica anche le sue dipendenze.

`--source`

Scarica il pacchetto RPM con i sorgenti invece del pacchetto binario.

`--destdir DIR`

Specifica la directory di destinazione. La directory predefinita è quella corrente.

### Esempi

Scarica il pacchetto binario del kernel:

`yumdownloader kernel`

Scarica il pacchetto sorgente del kernel:

`yumdownloader --source kernel`

Scarica il pacchetto binario del kernel e le sue dipendenze:

`yumdownloader --resolve kernel`

E' possibile selezionare più di un pacchetto e anche la relativa versione:

`yumdownloader kernel-2.6.22 openoffice-2.0.3`

Stampa la lista degli indirizzi da cui scaricare il kernel e le sue dipendenze:

`yumdownloader --urls --resolve kernel`

Le opzioni --urls e --resolve usate in combinazione sono utili per generare una lista con gli indirizzi dei pacchetti da scaricare e delle relative dipendenze. Si può usare su una macchina scollegata dalla rete su cui si vuole installare un programma in modo da ottenere la lista dei pacchetti necessari e poi scaricarli su un altro PC collegato in rete.
Il seguente comando:

`yumdownloader --urls --resolve -d 0 kernel > pacchetti_da_scaricare.txt`

crea un file di nome pacchetti\_da\_scaricare.txt con all'interno la lista degli url da scaricare per ottenere il pacchetto contenente il kernel e le sue dipendenze. L'opzione -d 0 serve per impedire che venga stampato anche l'output di Yum.

Mock
----

Mock è un potente programma per la compilazione di pacchetti sorgente. E in grado di creare un chroot, installarci dentro le dipendenze necessarie per compilare il pacchetto sorgente, compilarlo e sfornare l'RPM pronto da installare. Una volta finito, il chroot può essere riutilizzato per la prossima volta, in modo da rendere più veloce l'operazione, oppure può essere cancellato per risparmiare spazio. Mock ha l'enorme vantaggio di permettere di compilare i propri pacchetti sorgente senza sporcare il sistema con le librerie di sviluppo. E possibile creare un profilo personalizzato con i propri flag e le proprie opzioni di compilazione personalizzate, oppure usare uno di quelli standard. I profili si trovano nella cartella /etc/mock. Sono dei file nominati in questo modo:

`fedora-8-i386.cfg`
`fedora-8-ppc64.cfg`
`fedora-8-x86_64.cfg`

Si può creare un link simbolico, chiamato defaults.cfg, al proprio profilo preferito, in modo da non doverlo specificare ogni volta.
All'interno del profilo è possibile aggiungere i repository desiderati, personalizzare il flag e le opzioni di compilazione, e molto altro.

L'utilizzo è molto semplice. Si suppone di voler compilare il source RPM del kernel. Innanzitutto si ottiene il pacchetto sorgente con yumdownloader:

`yumdownloader --source kernel`

poi si costruisce il pacchetto RPM cosi:

`mock kernel.srpm`

Attendere un po', e a lavoro terminato lo si troverà nella cartella /var/lib/mock l'RPM pronto da installare.
Mock ha molte altre opzioni, leggere man mock per approfondire.

rpmbuild
--------

rpmbuild è un programma che permette di creare nuovi paccheti RPM o di convertire pacchetti sorgente in pacchetti binari. Notare che a differenza di Mock non scarica i pacchetti necessari per la compilazione, i quali devono essere già installati.
Ecco gli utilizzi tipici:

Costruisce il pacchetto RPM:

`rpmbuild --rebuild pacchetto.srpm`

-   Crea un RPM partendo dall'archivio in cui sono contenuti i sorgenti del programma.
-   Funziona solo se all'interno dell'archivi è presente il file SPEC.

`rpmbuild -ta sorgenti.tar.bz2`

rpmbuild è uno strumento completo e molto versatile, per imparare a usarlo a dovere si può studiare il capitolo dedicato alla costruzione degli RPM nel manuale Maximum RPM:
<http://www.rpm.org/max-rpm/p5208.html>

Yum presto
----------

I DeltaRPM sono dei pacchetti che contengono solo la differenza tra la vecchia versione del programma e quella nuova. Presto è il plugin per Yum che permette di gestire i DeltaRPM in automatico senza che l’utente se ne accorga.
I vantaggi sono enormi, se su un pacchetto da 50MB vengono modificati solo 100KB, durante l'aggiornamento vangono scaricati solo 100KB invece di 50.
L'utilità si vede tutta quando c’è da aggiornare pacchetti grossi come OpenOffice: invece di 110MB ne scarica solo 2 o 3! Oppure quando si installa Fedora da un DVD vecchio di mesi e invece di scaricare magari 600MB di aggiornamenti ne fa scaricare meno di 100.
Mediamente si risparmia dal 75% al 90%. Su Fedora 9 è già abilitato di default, per cui non è necessario fare nulla per abilitarlo.

Yum provides
------------

Il comando yum provides fornisce il nome del pacchetto in cui si trova il file desiderato.

`# yum provides /path/nomeFile`

è necessario indicare il percorso completo del file. In alternativa, se non lo si conosce, si puo usare il carattere \*, cosi:

`# yum provides *nomeFile`

Una utile applicazione di questo comando è quando si deve cercare il pacchetto che contiene un file header necessario per compilare un programma. Ad esempio se nei sorgenti in C c'è scritto:

`# include "pippo.h"`

eseguendo:

`# yum provides *pippo.h`

si otterrà la lista dei pacchetti che contengono il file pippo.h, e sarà possibile installare quello desiderato.

<Categoria:Yum>
