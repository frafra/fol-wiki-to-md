\_\_NOTOC\_\_

Introduzione
------------

Adobe Reader è un programma gratuito della Adobe Systems che permette di visualizzare e stampare i documenti in formato PDF. Di seguito verrà esposta la procedura d'installazione di Acrobat Reader su Fedora.

Installazione
-------------

Innanzitutto bisogna provvedere a scaricare l'ultima versione di Adobe Reader disponibile per linux direttamente dal [sito ufficiale](https://get.adobe.com/it/reader/). È inoltre possibile scaricarlo direttamente da [qui](http://get.adobe.com/it/reader/download/?installer=Reader_8.1.7_Italian_for_Linux_%28.rpm%29&standalone=1) per la versione in italiano o [qui](http://get.adobe.com/it/reader/download/?installer=Reader_9.5.5_English_for_Linux_(.rpm)&standalone=1) per la versione in inglese. Quest'ultima è consigliata perché è disponibile una versione più aggiornata.

Da terminale bisogna raggiungere la cartella dove è stato scaricato il pacchetto (probabilmente $HOME/Scaricati) e installarlo eseguendo da root

### Versione inglese

`# yum install AdbeRdr9.5.5-1_i486linux_enu.rpm libcanberra-gtk2.i686 adwaita-gtk2-theme.i686 PackageKit-gtk3-module.i686`

### Versione italiana

`# yum install AdobeReader_ita-8.1.7-1.i486.rpm libcanberra-gtk2.i686 adwaita-gtk2-theme.i686 PackageKit-gtk3-module.i686`

Se l'installazione è andata a buon fine, Adobe Reader potrà essere lanciato da terminale

`$ acroread `

<Categoria:Ufficio> [Categoria:Scrittura in corso](Categoria:Scrittura_in_corso "wikilink")
