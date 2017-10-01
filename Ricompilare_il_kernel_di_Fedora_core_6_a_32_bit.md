Come ricompilare il kernel in Fedora Core 6

Si farà tutto da utente normale, non da root e con pochi e semplici passaggi.
La compilazione richiede fino ad un massimo di quasi 3 GB, quindi accertarsi che tale spazio sia disponibile nella propria */home*.
Iniziare con lo spostasi nella nostra home con:

`$ cd ~/`

Installare gli strumenti necessari:

`$ su -c yum 'install rpmdevtools yum-utils' `

Inserire la password di root quando richiesto. Poi creare la dir *rpmbuild* con:

`# rpmdev-setuptree `

Ora installare i sorgenti del kernel con:

`# yumdownloader -e updates-source --source kernel `

Adesso i sorgenti del kernel si trovano nella propria home. Si installano sempre da utente non root con:

`# rpm -Uvh kernel-versione-scaricata.src.rpm `

Saranno notificati degli errori, ma vanno ignorati, nulla di preoccupante.
Quello che si sta per fare ora abbrevia i tempi di compilazione:

`# kate ~/rpmbuild/SPECS/kernel-2.6.spec `

Nuova sessione-&gt;visualizza-&gt;mostra i numeri di riga (se si usa gnome si saprà quale editor usare e come usarlo)

`Riga 13 %define buildxen 1 -mettere 0 al posto di 1-`
`Riga 15 %define buildkdump 1 -mettere 0 al posto di 1-`

Per dare un nome personalizzato al nuovo kernel,

`Riga 35 %define release %(R="$Revision: 1.2868 $"; RR="${R##: }"; echo ${RR%%?})%{?dist}`

sostituire 1.2868 in un nome a piacere, tipo nuovo, ricompilato ecc..

`Riga 97 %define buildpae 1 -mettere 0 al posto di 1-`

Salvare ed uscire.

Ora si può passare alla compilazione con:

`# rpmbuild -bb --target $(uname -m) kernel-2.6.spec`

Si consiglia di andare a fare una passeggiata, il mio Notebook con Athlon64 3000+ 512 di ram ha impiegato poco più di 2 ore.

Quando ha finito si può installare il nuovo kernel. Spostarsi in:

`# cd /home/mia_home/rpmbuild/RPMS/i386 `

Installare con:

`# rpm -Uvh --force --oldpackage kernel-2.6.18-nome_che_si_è_dato.i686.rpm `

Al riavvio partirà il proprio kernel. Per crearsi un kernel personalizzato per il proprio PC, alleggerito ecc. Diventare root con <su -> poi:

`# cd /home/mia_home/rpmbuild/BUILD/kernel-2.6.18/linux-2.6.18.i686 `

Per chi vuole usare una GUI:

`# yum install qt-devel `
`# make xconfig `

Si apre l'interfaccia grafica che permette di apportare le modifiche volute.
Ci si trova nel cuore di Linux: il kernel. Un'operazione sbagliata può compromettere il funzionamento di tutto il sistema e magari non avviarsi più. Come detto all'inizio la responsabilità è vostra.

Volendo continuare, una volta effettuate le modifiche, per renderle operative occorre dare nell'ordine i seguenti comandi:

`# make all`
`# make modules_install`
`# make install`

Per fare pulizia e recuperare spazio:

`# make clean `

Riferimenti
-----------

-   <http://www.pcarea.it/linux/linux.html>

<Categoria:Sistema> [Categoria:Programmazione e Sviluppo](Categoria:Programmazione_e_Sviluppo "wikilink")
