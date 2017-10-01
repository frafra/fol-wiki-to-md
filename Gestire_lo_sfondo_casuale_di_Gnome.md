Per gestire lo sfondo casuale con Gnome, apriamo con VIM il file random\_dektop:

`$ vim ~/random_desktop`

Digitiamo il seguente codice (ovviamente l'unica modifica che dovete apportare è l'indirizzo della cartella che contiene i vostri sfondi!):

`#!/usr/bin/perl`
`$dir_sfondi = "/home/luca/sfondi/";`
`` @elenco_sfondi = `ls -t ${dir_sfondi}*.JPG ${dir_sfondi}*.jpg`; ``
`chomp($sfondo = $elenco_sfondi[int(rand(@elenco_sfondi))]);`
`#Impostiamo l'opzione in modo da riempire tutto lo sfondo`
`system("gconftool-2", "--type", "string", "--set",`
`"/desktop/gnome/background/picture_options", "stretched");`
`#Impostiamo il nostro sfondo`
`system("gconftool-2", "--type", "string", "--set",`
`"/desktop/gnome/background/picture_filename", $sfondo);`

Per uscire da vim digitiamo:

`:wq`

Diamo i permessi di esecuzione al file così creato:

`$ chmod +x ~/random_desktop`

Ora possiamo inserire nella nostra sessione di avvio il programma! E quindi riapriamo vim:

`$ vim ~/.gnome2/session_manual`

ed inseriamo il seguente codice:

`[Default]`
`num_clients=1`
`0,RestartStyleHint=3`
`0,Priority=50`
`0,RestartCommand=~/random_desktop`
`0,Program=~/random_desktop`

Per uscire da vim digitiamo:

`:wq`

Finito, buon divertimento!

<Categoria:Fedoraserver>
