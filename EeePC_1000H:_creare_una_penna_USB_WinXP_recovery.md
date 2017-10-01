Introduzione
------------

I Netbook con sistemi Linux preinstallati sono ormai spariti, per cui molti sceglieranno il dual boot su questi piccoli portatili. I netbook, però, non hanno DVD, per cui crearsi una penna USB per mantenere la possibilità di recovery Windows potrebbe essere molto utile (da crearsi prima di installare Fedora).
La procedura seguente viene descritta prendendo come esempio un eeepc 1000H, ma dovrebbe essere corretta, al limite con piccole correzioni, anche per altri netbook se si utilizza Win XP.

Prerequisiti
------------

Tutto quello che serve è:

-   una penna USB con almeno 4GB di capacità
-   Il CD di supporto incluso con l'Asus eeepc 1000H
-   [Winrar](http://www.rarlab.com)
-   [PeToUSB](http://http://gocoding.com/page.php?al=petousb)

Inoltre si avrà necessità dei seguenti file, che si trovano sul CD di supporto:

-   WINPE.ISO (nella directory root del CD)
-   EEEPCAH.GHO (nella directory "Recovery")

**WINPE.ISO** è una versione light di Win XP e contiene inoltre il file GHOST32.EXE, della nota casa di salvataggio file.
**EEEPCAH.GHO** contiene l'immagine del disco dopo l'installazione della fabbrica, e può essere installato con Symantec Ghost.

Estrazione dei file da WINPE.ISO
--------------------------------

Per primo biasogna creare una nuova directory "WINPE" su un disco con abbastanza spazio libero. Aprire Winrar e selezionare il file WINPE.ISO dal disco di supporto: <img src="Winpe.png" title="fig:WinPE.ISO è un archivio WinRAR." alt="WinPE.ISO è un archivio WinRAR." width="350" /> Per far partire l'estrazione cliccare su "extract to" e selezionare la cartella /Winpe appena creata come destinazione. Confermare con *OK* e tutti i file verranno estratti nella directory.

Symantec Ghost come applicazione di default all'avvio
-----------------------------------------------------

Questa operazione è importantissima per far partire Ghost all'avvio del sistema. Per fare questa modifica bisogna fare doppio click su WINPESHL.INI che si trova in \\WINPE\\I386\\SYSTEM32 e cambiare le seguenti righe:

`[launchApp]`
`AppPath=x:\EPCRecover.exe`
`....deve diventare....`
`[launchApp]`
`AppPath=x:\GHOST32.EXE`

Dopodiché basta salvare il file senza cambiare il nome del file.

Formattazione penna USB e copia dei file
----------------------------------------

Per iniziare la formattazione inserire la penna USB nel netbook e far partire l'applicazione PeToUSB. La penna dovrebbe apparire sotto la voce "destination drive".
A questo punto bisogna selezionare le voci **USB removable, Enable Disk Format** e **Enable file copy**.
Alla fine si seleziona la cartella sorgente /Winpe che è stata creata pochi minuti fa. <img src="Petousb.png" title="fig:Ecco come appare l&#39;applicativo per la creazione della penna USB." alt="Ecco come appare l&#39;applicativo per la creazione della penna USB." width="350" /> Ci vorrà un po' di tempo, alla fine si può confermare con *OK* e chiudere PeToUSB.

Copiare il file immagine
------------------------

Per copiare il file immagine sulla penna USB ora è necessario copiare il file immagine EEEPCAH.GHO, presente nella cartella "Recovery" del CD di supporto, ***nella root directory*** della penna USB. Questa copia necessita di un po' di pazienza, in quanto sono circa 2,5GB.
Ora la penna USB è pronta, per finire una breve descrizione sull'utilizzo.

Utilizzo della penna USB Recovery
---------------------------------

L'utilizzo della penna è abbastanza semplice:

-   Inserire la penna nel netbook e accenderlo, premendo ESC per accedere al boot menu, dal quale bisogna selezionare l'avvio da penna USB;
-   Al termine del processo di boot, Symantec farà partire Ghost;
-   Premere OK e poi selezionate *Local &gt; Disk &gt; From Image*;
-   Dal menu a tendina ora si dovrà scegliere la penna USB, che per esempio potrebbe essere X: , e successivamente l'immagine EEEPCAH.GHO;
-   Selezionare il disco di destinazione o la partizione di destinazione;

Riferimenti
-----------

-   [Myeeeguides](http://myeeeguides.wordpress.com/).

<Categoria:Hardware> <Categoria:Installazione>
