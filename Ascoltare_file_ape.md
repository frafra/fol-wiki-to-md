Una delle cose a cui una persona è più affezionata, è senz'altro la "propria" musica, quella che ascolta più spesso.
Ma se una parte di essa è in formato .ape, l'impatto con Fedora10 (o altra distribuzione linux) potrebbe essere difficile in quanto non ci sono, apparentemente, le possibilità per ascoltarla.
In realtà i modi ci sono......e sono anche semplici.

La presente non vuole essere una guida, solo una raccolta di link che chiunque potrebbe trovare con un po' di pazienza.

Una possibilità è usare VLC, un programma sempre più diffuso, e molto versatile. Se non lo abbiamo già apriamo una shell, diventiamo root e lo installiamo con

`# dnf install vlc*`

Questo comando installerà un po' di roba: il programma vero e proprio, e tutte le librerie che servono per ascoltare i vari formati musicali, ma non gli ape.
Si risolve facilmente: andare qui:
<http://rpmfind.net/linux/rpm2html/search.php?query=libmac.so.2>
e scaricare il pacchetto mac-3.99-2.u4b5.fc7.i386.rpm (è per fedora 7 ma va benissimo per le successive).
Fatto ciò portarsi con una shell nella directory dove lo si è scaricato, e dare

`# rpm -ivh mac-3.99-2.u4b5.fc7.i386.rpm `

come root, per installarlo.
Il gioco è fatto, adesso VLC può riprodurre gli ape.
Alcuni sono probabilmente abituati a usare xmms per la loro musica, e vorrebbero continuare a farlo anche per gli ape. Fortunatamente è possibile!
Se non lo si possiede già, installare xmms e dipendenze varie con:

`# dnf install xmms*`

e in seguito andare qui:
<http://orion.lcg.ufrj.br/RPMS/myrpms-f8/repoview/repoview/xmms-mac-0-0.3.1-1.fc8.html>
e scaricare il pacchetto xmms-mac-0.3.1-1.fc8.i386.rpm
Portatesi quindi nella directory dove lo si è scaricato, e installarlo con

`# rpm -ivh xmms-mac-0.3.1-1.fc8.i386.rpm`

E' tutto, adesso xmms dovrebbe riprodurre senza problemi gli ape!

Buon ascolto :-D

<Categoria:Multimedia>
