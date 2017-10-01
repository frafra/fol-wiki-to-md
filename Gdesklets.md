Introduzione
------------

Per chi utilizza Gnome come Desktop Manager e vuole personalizzare maggiormente il proprio desktop ci sono le *gdesklets*. Simile a *superkaramba* per KDE sono delle applet che permettono di far apparire sul desktop informazioni sul sistema: p.e. una barra di lancio, previsioni del tempo e molto più.
In questo articolo si prenderanno come esempio soltanto:

-   Previsioni meteo
-   Informazioni sul sistema
-   Starterbar

Installazione
-------------

Innanzitutto è necessario installare il pacchetto gdesklets, disponibile nei repository, quindi da terminale basterà digitare:

`# yum install gdesklets`

Con questo è stata creato la "piattaforma" sulla quale poi si possono aggiungere i desklets veri e propri. Andando in *Applicazioni &gt; Accessori &gt; gdesklets* si apre una finestra come questa: <img src="Gdesklets1.jpg" title="fig:Gdesklets come si presenta senza applet." alt="Gdesklets come si presenta senza applet." width="300" /> Le applets per gdesklets si possono trovare soprattutto su questi siti:

-   <http://gdesklets.gnomedesktop.org/>
-   <http://www.gnome-look.org/>

Per installare le desklets è sufficiente scaricare il file *tar.gz* e poi selezionarlo dal menu di gdesklets, ovvero:
***File &gt; Installa pacchetto***

Una volta installato basta cliccare due volte sull'applet che comparirà nella shell di gdesklets e lo si potrà trovare sul proprio desktop.
Con il mouse è possibile fin da subito posizionarlo dove si vuole e rilasciarlo con un ulteriore click.

Applet Previsioni Meteo
-----------------------

Per le previsioni meteo è stato scelto ***GoodWeather***: è molto facile da configurare e permette di selezionare la propria città, o almeno quella più vicina. Per fare questo bisogna inserire il codice internazionale del luogo in cui ci si trova. Lo si fa cliccando con il tasto destro del mouse sul desklet e selezionando "configure desklet".
Si segnala [questo link](http://it.weather.yahoo.com/Mediterraneo/Italia/index.html) dove è possibile scegliere la città, oppure fare una ricerca. Nella barra degli indirizzi comparirà un codice, per esempio *ITXX0007*. E' il codice da inserire nel "Location Code".

Applet Sensori di Sistema
-------------------------

I vari sensori del sistema, Ram, Cpu, connessione, hard disk ecc. si possono installare anche singolarmente. Un esempio sono le diffuse ***FTB***, che si trovano sui siti precedentemente elencati.
La procedura d'installazione è la stessa descritta prima, anche la configurazione rimane identica e una volta installati si possono facilmente adattare al proprio desktop.

Applet Starterbar
-----------------

La starterbar invece è scaricabile da [qui](http://www.gnome-look.org/content/show.php/Custom+Gdesklets+Starterbar?content=34782) e si installa come da procedura standard. Comparirà un'icona sola con la propria */home directory*. Una volta messa sul desktop si possono aggiungere alla barra quante icone si vogliono; è necessario inserire il nome che si vuole dare al lanciatore e specificare il percorso:
Per esempio: per *firefox* si metterà */usr/bin/firefox* e così via. Per la gran parte delle applicazioni da lanciare tramite starter-bar viene associata in automatico anche l'icona. Altrimenti si può selezionare una a proprio piacere.
 Se si volesse, per chi è un pochino pratico di codice html, è possibile modificare ulteriormente l'aspetto della barra che inizialmente appare un pochino grezza. Lo si può fare intervenendo direttamente sul codice, cliccando dal menu che si apre con il tasto destro del mouse "View source".
Per fare un esempio in questa guida sono stati eliminati lo sfondo e i bordi, in modo che la barra appaia integrata meglio nel desktop.

Il resto è personalizzabile utilizzando la propria fantasia, il desktop appena descritto, unito a uno sfondo un po' diverso, ora si presenta così: <img src="Gdesklets2.jpg" title="fig:Gli applet appena citati appaiono in questo modo." alt="Gli applet appena citati appaiono in questo modo." width="500" />

[Categoria:Ambiente Desktop](Categoria:Ambiente_Desktop "wikilink")
