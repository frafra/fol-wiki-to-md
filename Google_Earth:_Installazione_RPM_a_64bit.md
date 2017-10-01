\_\_TOC\_\_

Introduzione
------------

Google Earth, famoso programma in grado di virtualizzare immagini del nostro pianeta, da tempo è disponibile a 32 bit, mentre per PC a 64bit fino ad ora esisteva soltanto la compilazione dai file sorgente.
Ora è disponibile un RPM a 64bit, anche se per un corretto funzionamento l'installazione necessità comunque di alcuni pacchetti a 32bit.

Installazione dipendenze
------------------------

Il pacchetto obbligatorio per Google Earth è:

`# dnf install redhat-lsb.i686`

Installazione pacchetto
-----------------------

Installati i pacchetti è possibile installare [Google Earth](http://www.google.it/intl/it/earth/download/ge/agree.html).
Occorre scegliere tra la versione a 32 bit e quella 64 bit e, una volta scaricato il file è possibile installarlo, spostandosi nella cartella in cui si trova, con:

`# dnf install /percorso/al/file/google-earth-stable_current_*.rpm`

Peccato che Google non abbia pensato di dotare il pacchetto RPM delle informazioni necessarie per risolvere in automatico eventuali dipendenze mancanti.
A questo proposito, visto che sono stati installati i pacchetti in precedenza, l'installazione dovrebbe avvenire con successo e l'uso di Google Earth compenserà gli sforzi fatti con una nuova veste grafica.

<Categoria:Internet>
