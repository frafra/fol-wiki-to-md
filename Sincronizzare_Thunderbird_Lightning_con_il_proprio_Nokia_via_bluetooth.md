Introduzione
------------

Piccolo how-to per sincronizzare il proprio calendario del cellulare con il calendario di Lightning e non solo.
Al linux day in seguito alla presentazione di openoffice 3 ho scoperto Lightning, un’estensione di thunderbird, un vero e proprio PIM(Personal Information Management).
Tornato a casa, ho studiato la situazione e ho scoperto che anche KDE ha dei suoi strumenti PIM molto validi e integrati con l’ambiente desktop, si trovano tutti sotto kde-pim installati di default. Per utilizzarli basta lanciare kontact.
Ero, però, deciso ad utilizzare Lightning. Pertanto l'ho scaricato ed installato.
Per farlo funzionare ho trovato [questa guida](http://www.stefanolaguardia.eu/2008/08/29/linux-desktop-guida-sincronizzare-thunderbird-lightning-sunbird-con-nokia-n-ed-e-series-via-bluetooth/).
E’ scritta per debian/ubuntu. Nell’articolo viene chiarito che c’è la necessità di utilizzare un calendario in formato ICAL ma di default è in SQLite che non funziona con opensync. Il trucco è (cito testualmente): “Il trucco consiste nell’esportare il Calendario di default in un file .ics e, successivamente, cancellare il calendario installato e caricare quello ics esportato (quest’utlima operazione la si fa dal menu “File –&gt; Open –&gt; Calendar File”).”

Installazione
-------------

Parto come presupposto che il bluetooth sia già configurato e già funzionante (per cui che già il telefono si connette al pc e viceversa e che si possono scambiare dei file).
I software di cui abbiamo bisogno per far sincronizzare il telefono via bluetooth sono essenzialmente multisync e opensync al quale deve essere aggiunto i plugin SyncML più altri plugin che possono essere utili per fare la sincronizzazione con altri software(tipo evolution, kde-pim, ecc.).

Come utente root diamo questo bel comando:

`yum install libopensync-devel glib-devel libsyncml-devel wbxml2-devel libopensync-plugin-evolution2 libopensync-plugin-kdepim libopensync-plugin-file multisync-gui libopensync-plugin-gpe libsyncml libopensync-plugin-irmc glib-devel wbxml2-devel`

Ciò installerà multisync e anche la sua finestra grafica, opensync e vari plugin che possono risultare utili.

Ora c’è bisogno anche del plugin “syncml-plugin”, che contiene syncml-obex-client, essenziale per poter far la sincronizzazione tramite bluetooth con il protocollo SyncML.
Per farlo ci sarà bisogno di compilare il pacchetto perchè non si trova l’rpm.
Il pacchetto si scarica da [questa pagina](http://www.opensync.org/attachment/wiki/download) e ha un nome simile a questo: libopensync-plugin-syncml-0.22.tar.bz2 (potrebbero cambiare in funturo i numeri della versione).
Una volta scaricato, scompattarlo dove si preferisce con un *tar xvf*, o con il programma che si preferisce.
Da shell si entra nella cartella scompattata ed eseguire i soliti 3 comandi per la configurazione, compilazione e l’installazione:

`./configure`
`make`
`su - `
`password root`
`make install`

Il *checkinstall* va in errore e non permette la costruzione dell’rpm, per cui ho proceduto con *make install*.

Una volta installati tutti i pacchetti possiamo dare questo comando e vedere il suo output per confermare l’esistenza dei plugin (dovrebbe venire una cosa simile a questa, varia a seconda dei plugin installati, ovviamente):

`$ msynctool --listplugins`
`Available plugins:`
`irmc-sync`
`syncml-http-server`
`syncml-obex-client`
`gpe-sync`
`evo2-sync`
`sunbird-sync`
`file-sync`
`kdepim-sync`

Ora bisogna configurare il file sync e basta seguire queste operazioni:

`#creare un gruppo di nome filenokia`
`$ msynctool --addgroup filenokia`
`#aggiungere il membro sunbird-sync al gruppo filenokia per poi connettersi al database di lightning`
`$ msynctool --addmember filenokia sunbird-sync`
`#aggiunge il membro syncml-obex-client per la connessione via bluetooth`
`$ msynctool --addmember filenokia syncml-obex-client`

Ovviamente potranno essere aggiunti anche gli altri plugin a seconda di cosa si vuole sincronizzare.
Per fare questo si può anche utilizzare l’interfaccia grafica di multisync che è molto intuitiva lanciando il comando “multisync” da shell.

Ora bisogna completare la configurazione di multisync con la configurazione dei vari plugin/membri. Per farlo ci sono più strade la migliore è quella di utilizzare “kitchensync”, programma per fare le sincronizzazioni in kde. E’ molto facile nell’uso ed è molto intuitivo.
Altrimenti si può procedere da shell usando il comando:

`msynctool –configure filenokia 1`

per la configurazione del plugin sunbird-sync, che dovrà contenere una cosa simile a questa:

     <config>
     <file path=”/percorso/file/calendario.ics” />
     </config>
     

e

`msynctool –configure filenokia 2`

per la configurazione del plugin syncml-obex-client, che dovrà contenere una cosa simile a questa:

     <config>
     <bluetooth_address>XX:XX:XX:XX:XX:XX</bluetooth_address>
     <bluetooth_channel>10</bluetooth_channel>
     <interface>0</interface>
     <identifier>PC Suite</identifier>
     <version>1</version>
     <wbxml>1.2</wbxml>
     <username></username>
     <password></password>
     <type>2</type>
     <usestringtable>3</usestringtable>
     <onlyreplace>0</onlyreplace>
     <recvLimit>10000</recvLimit>
     <maxObjSize>50</maxObjSize>
     <contact_db>Contacts</contact_db>
     <calendar_db>Calendar</calendar_db>
     <note_db>Notes</note_db>
     </config>
     

`hcitool scan`

Tramite il comando (ovviamente sostituendo le XX:XX:XX:XX:XX:XX con il mac address del telefono):

`sdptool browse XX:XX:XX:XX:XX:XX`

Cercare la voce “SyncMLClient” e il corrispondente canale su cui è in ascolto il servizio che dovrà essere sostituito nella configurazione poco sopra per il “bluetooth\_channel”.

Per sincronizzare i contatti e l’agenda del telefono basta dare:

`msynctool –sync nokia-sync –filter-objtype contact`

Senza complicarsi la vita kitchensync è molto più intuitivo ed inizierà la sincronizzazione una volta che è stato opportunamente configurato.

Con il mio nokia 6021 sembra funzionare senza problemi. Però devo ancora fare un vero e proprio “testing” massivo di conferma.

Riferimenti
-----------

-   <http://seawolfsanctuary.blogspot.com/2008/03/sync-your-phone-with-fedora-or-when.html>
-   <http://clunixchit.blogspot.com/2007/07/syncing-mobile-phone-and-kontact-via.html>
-   <http://www.harald-hoyer.de/linux_and_syncml_multisync_with_nokia_6280>
-   <http://blog.marionline.it>

Aggiornamenti utili
-------------------

Con l'introduzione di kde4 le cose sono cambiate parecchio e i vari progetti sono evoluti.
sunbird-sync non esiste più, al suo posto si sta facendo strada bluezSync: <http://bluezync.kaarposoft.dk/>

Inoltre ho notato con estremo piacere che SyncML da fedora 10(dalla 9 non so rispondere) è presente nei repo e non necessita di compilazione.

In più in fedora 10 è stato momentaneamente eliminato kitchensync, il bug è qui: <https://bugzilla.redhat.com/show_bug.cgi?id=477193>

Appena avrò del tempo proverò a creare una guida per fedora 10 e/o successive con i software aggiornati.

<Categoria:Ufficio>
