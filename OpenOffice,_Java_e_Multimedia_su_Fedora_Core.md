Introduzione
------------

Come dare alla nostra preferita suite di programmi per ufficio il pieno supporto ai contenuti multimediali che Java di Sun ci può offrire. Guida testata con FC5 e FC6. Questa guida è stata scritta da Nico Timeo, sistemista presso la Società [Techpoint](http://www.techpoint.catania.it/) di Catania.

Molti utenti che passano da Windows a Linux trovano in Openoffice.org una suite all'altezza del suo “concorrente” Microsoft Office.In effetti, con *Ooo* abbiamo la possibilità di lavorare praticamente con gli stessi strumenti avendo però a disposizione la collaudatissima stabilità dei sistemi Linux.
Il problema però è che con un'installazione di default su Fedora Core 5 OpenOffice.org non dispone di funzionalità multimediali, in quanto queste ultime sono utilizzabili solo tramite il supporto del Java Media Framework (non incluso per motivi di licenza) e non con i trucchi della sua controparte open source GCJ.
In questo tutorial spiegheremo come sostituire GCJ con il runtime Java di Sun, installare il JMF ed abilitare le funzioni multimediali di OpenOffice.org.

Rimozione di GCJ E OpenOffice
-----------------------------

Per rimuovere GCJ da un'installazione standard di FC5, utilizzeremo pirut. Dal menu *Applicazioni* selezioniamo ***Add/Remove Software***, diamo la password di root e attendiamo la verifica dei pacchetti.
A questo punto possiamo rimuovere l'intero componente JAVA dalla sezione BASE SYSTEM e tutti i pacchetti OPENOFFICE-\* dal componente UFFICIO/PRODUTTIVITA' nella sezione APPLICAZIONI.
Altrimenti, molto semplicemente da riga di comando:

`# yum remove libgcj`
`# yum remove openoffice*`

Prepariamo l'ambiente
---------------------

Installiamo ***fedora-rpmdevtools***, che ci consentirà di “pacchettizzare” tutto il nostro lavoro in comodi file rpm, DA NON DISTRIBUIRE, ma liberamente utilizzabili per l'installazione su tutte le macchine della nostra LAN.

`# yum install fedora-rpmdevtools`
`=============================================================================`
` Package                 Arch       Version          Repository        Size`
`=============================================================================`
`Installing:`
` fedora-rpmdevtools      noarch     1.6-1.fc5        extras             61 k`
`Installing for dependencies:`
` gcc                     i386       4.1.1-1.fc5      updates           4.6 M`
` gcc-c++                 i386       4.1.1-1.fc5      updates           3.3 M`
` libgomp                 i386       4.1.1-1.fc5      updates            48 k`
` libstdc++-devel         i386       4.1.1-1.fc5      updates           9.5 M`
` redhat-rpm-config       noarch     8.0.40-1         core               44 k`
` rpm-build               i386       4.4.2-15.2       core              534 k`

Fatto ciò, possiamo creare il nostro “tree” per rpmbuild (da utente comune):

`$ fedora-buildrpmtree`

e verifichiamo con:

`$ ls`

la presenza nella nostra Home della cartella rpmbuild, al cui interno troveremo:

`BUILD`
`RPMS`
`SOURCES`
`SPECS`
`SRPMS`

Ora dobbiamo inserire nella lista dei nostri repository anche quello del [*Jpackage Project*](http://www.jpackage.org/). Da root:

`# cd /etc/yum.repos.d/`
`# wget `[`http://www.jpackage.org/jpackage.repo`](http://www.jpackage.org/jpackage.repo)

Installiamo il Java Development Kit
-----------------------------------

Per scaricare il JDK Sun andiamo sul sito di [Sun](http://java.sun.com/j2se/1.5.0/download.jsp), clicchiamo su Download JDK 5.0 Update 10 (la più recente al momento in cui scrivo).
Accettiamo la licenza e scarichiamo il file jdk-1\_5\_0\_10-linux-i586.bin scegliendo il formato Linux self-extracting, che deve essere copiato nella cartella SOURCES del nostro build tree:

`$ cp jdk-1_5_0_10-linux-i586.bin ~/rpmbuild/SOURCES/`

Dobbiamo scaricare [da questo sito](http://mirrors.dotsrc.org/jpackage/1.6/generic/non-free/SRPMS/) il file java-1.5.0-sun-1.5.0.10-2jpp.nosrc.rpm ([questo](http://mirrors.dotsrc.org/jpackage/1.6/generic/non-free/SRPMS/java-1.5.0-sun-1.5.0.10-2jpp.nosrc.rpm) è il link diretto).
Ora, posizionandoci nella cartella dove abbiamo scaricato quest'ultimo file, possiamo lanciare il comando di “pacchettizzazione”:

`$ rpmbuild --rebuild java-1.5.0-sun-1.5.0.10-2jpp.nosrc.rpm`

Al termine dell'operazione, troveremo nella cartella /rpmbuild/RPMS/i586/ i pacchetti rpm del nostro Java Development Kit. I pacchetti vanno poi installati in questo modo:

`# cd ~/rpmbuild/RPMS/i586/`
`# yum localinstall *.rpm`
`=============================================================================`
` Package                 Arch       Version          Repository        Size`
`=============================================================================`
`Installing:`
` java-1.5.0-sun          i586       1.5.0.07-1jpp    java-1.5.0-sun-1.5.0.07-1jpp.i586.rpm   85 M`
` java-1.5.0-sun-alsa     i586       1.5.0.07-1jpp    java-1.5.0-sun-alsa-1.5.0.07-1jpp.i586.rpm   64 k`
` java-1.5.0-sun-demo     i586       1.5.0.07-1jpp    java-1.5.0-sun-demo-1.5.0.07-1jpp.i586.rpm   14 M`
` java-1.5.0-sun-devel    i586       1.5.0.07-1jpp    java-1.5.0-sun-devel-1.5.0.07-1jpp.i586.rpm   12 M`
` java-1.5.0-sun-fonts    i586       1.5.0.07-1jpp    java-1.5.0-sun-fonts-1.5.0.07-1jpp.i586.rpm  2.0 M`
` java-1.5.0-sun-jdbc     i586       1.5.0.07-1jpp    java-1.5.0-sun-jdbc-1.5.0.07-1jpp.i586.rpm   66 k`
` java-1.5.0-sun-plugin   i586       1.5.0.07-1jpp    java-1.5.0-sun-plugin-1.5.0.07-1jpp.i586.rpm  1.9 M`
` java-1.5.0-sun-src      i586       1.5.0.07-1jpp    java-1.5.0-sun-src-1.5.0.07-1jpp.i586.rpm   17 M`
`Installing for dependencies:`
` jpackage-utils          noarch     1.6.6-1jpp_2rh   core               50 k`
` unixODBC                i386       2.2.11-6.2.1     core              905 k`
` unixODBC-devel          i386       2.2.11-6.2.1     core              850 k`

Se durante l'installazione riceviamo un errore riguardante la “firma” dei pacchetti, dobbiamo momentaneamente disabilitarne la verifica. Per far ciò basterà modificare il parametro gpgcheck in *gpgcheck=0* nel file /etc/yum.conf.
Ora dobbiamo indicare al sistema, ma soprattuto alle applicazioni che utilizzano Java, dove si trova il nuovo ambiente di runtime modificando il file /etc/profile:

`# gedit /etc/profile`

Nella sezione \# Path manipulation (rigo 23 circa, in un file standard) dobbiamo inserire:

`JAVA_HOME=/usr/lib/jvm/java-1.5.0-sun-1.5.0.10/jre`
`pathmunge $JAVA_HOME/bin before`
`export JAVA_HOME`

Visto che siamo in ballo, ne approfittiamo per configurare anche il plugin per il browser Firefox, in modo da utilizzare le funzionalità Java anche nei siti abilitati:

`# cd /usr/lib/mozilla/plugins`
`# rm -f libjavaplugin_oji.so`
`# ln -s  ../../../lib/jvm/java/jre/plugin/i386/ns7/libjavaplugin_oji.so`

Ora possiamo riavviare il sistema per rendere effettive le modifiche.

Installiamo il Java Multimedia Framework
----------------------------------------

Andiamo sul [sito](http://java.sun.com/products/java-media/jmf/2.1.1/download.html), clicchiamo su Download, accettiamo la licenza e scarichiamo il file jmf-2\_1\_1e-alljava.zip selezionando Cross-platform Java.
Con lo stesso procedimento andiamo [qui](http://java.sun.com/javase/technologies/desktop/media/jmf/2.1.1/specdownload.html) per sacricare il file jmf-2\_0-spec.zip (JMF 2.0 API Specification).
Inoltre da [questo sito](http://javashoplm.sun.com/ECom/docs/Welcome.jsp?StoreId=22&PartDetailId=7276-jmf-2.0-fr-doc-oth-JSpec&SiteId=JSC&TransactionId=noreg) preleviamo il file jmf2\_0-guide-html.zip (JMF 2.0 API Guide).
Questi tre file, vanno copiati nella cartella ~/rpmbuild/SOURCES.
Infine, dal sito &lt;="" a=""&gt; dobbiamo scaricare il file jmf-2.1.1e-1jpp.nosrc.rpm.
Ci posizioniamo nella cartella dove abbiamo salvato quest'ultimo file e, come per il JDK, procediamo con la pacchettizzazione (da utente normale, non root!). Al termine di questa procedura, avremo i pacchetti nella cartella ~/rpmbuild/RPMS/noarch.

L'installazione è semplice:

`$ cd ~/rpmbuild/RPMS/noarch`
`# rpm -ivh *.rpm`

Installiamo OpenOffice.org
--------------------------

Utilizzeremo, per l'installazione, i binari ufficiali disponibili a [questo indirizzo](http://it.openoffice.org/).
Scarichiamo la versione 2.1.0 (la più aggiornata al momento in cui scrivo), ovviamente quella senza JRE. Otterremo il file Ooo\_2.1.0\_LinuxIntel\_install\_it.tar.gz, da scompattare. Nella cartella estratta troviamo una sottocartella RPMS, con tutti i file rpm da installare. Ci posizioniamo in questa cartella e digitiamo:

`# rpm -ivh *.rpm`

poi passiamo alla sottocartella *desktop-integration*:

`# cd desktop-integration`
`# rpm -ivh openoffice.org-redhat*`

Abbiamo completato l'installazione di OpenOffice.org!

Configurazione JMF in OpenOffice
--------------------------------

Dal menu *Strumenti* selezioniamo *Opzioni*. Nella sezione *OpenOffice.org*, sotto *Java*, premiamo il pulsante *Classpath*. Nella scheda seguente clicchiamo su *Aggiungi Archivio* e selezioniamo il file *jmf.jar* dalla cartella */usr/share/jmf/lib*. Riavviamo OpenOffice per rendere effettive le modifiche.

Verifica
--------

Per verificare che effettivamente OpenOffice sia in grado di supportare le nuove funzionalità multimediali di JMF, basta aprire un documento vuoto, selezionare dal menu *Strumenti* la voce *Gallery*, e selezionare la voce *Suoni* dal menu a sinistra. Se facendo doppio click su un evento sonoro siamo in grado di ascoltare il suono in questione, tutto è andato a buon fine.

Note finali
-----------

In questo modo non abbiamo più motivo di rimpiangere Microsoft Office.
Se soltanto la scelta di Sun in merito alle licenze non fosse così infelice, potremmo aggiungere il supporto multimediale ad OpenOffice in modo sicuramente meno macchinoso! In ogni caso, una volta generati i pacchetti rpm, possiamo utilizzarli per tutte le nostre installazioni. L'importante è non “redistribuirli”.
Ricordiamoci, durante gli aggiornamenti con YUM, di disabilitare la ricerca di nuove versioni di OpenOffice, altrimenti il nostro lavoro sarà stato inutile! Il comando da eseguire è quindi:

`# yum --exclude openoffice* update`

Infine, se abbiamo modificato il file */etc/yum.conf* per installare pacchetti non firmati, questo è il momento opportuno per ripristinare il valore *gpgcheck=1*. Quando si parla di sicurezza, è bene essere previdenti!

Copyright
---------

Questo articolo viene rilasciato sotto [Licenza Creative Commons](http://creativecommons.org/licenses/by-nc-sa/2.0/it/).

<Categoria:Fedoraserver>
