Come aggiungere Sfondi extra, Temi ed Icone
-------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Aggiungere sfondi extra

wget -c <http://easylinux.info/uploads/backgrounds.tar.gz>

`tar zxvf backgrounds.tar.gz -C /usr/share`
`rm -f backgrounds.tar.gz`

Verifica se hai il file <i>backgrounds.xml</i> nella tua directory <i>.gnome</i>

`ls $HOME/.gnome2/ | grep "backgrounds.xml"`

Se viene restituito <i>"backgrounds.xml"</i> lancia:

`cp --preserve=ownership $USER_HOME/.gnome2/backgrounds.xml $USER_HOME/.gnome2/backgrounds.xml_backup`
`sed -n -e '1,3p' $USER_HOME/.gnome2/backgrounds.xml_backup > $USER_HOME/.gnome2/backgrounds.xml`
`cat /usr/share/backgrounds/frog.xml >> $USER_HOME/.gnome2/backgrounds.xml`
`sed -n -e '4,$p' $USER_HOME/.gnome2/backgrounds.xml_backup >> $USER_HOME/.gnome2/backgrounds.xml`

<li>
**ALTRIMENTI** lancia:

</li>
`cp /usr/share/backgrounds/backgrounds.xml $USER_HOME/.gnome2/backgrounds.xml`
`chmod 777 $USER_HOME/.gnome2/backgrounds.xml`

<li>
Per aggiungere Temi ed Icone lancia:

</li>
`wget -c href="`[`http://easylinux.info/uploads/icons.tar.gz`](http://easylinux.info/uploads/icons.tar.gz)
`tar zxvf icons.tar.gz -C $USER_HOME`
`rm -f icons.tar.gz`
`wget -c href="`[`http://easylinux.info/uploads/themes.tar.gz`](http://easylinux.info/uploads/themes.tar.gz)
`tar zxvf themes.tar.gz -C $USER_HOME`
`rm -f themes.tar.gz`

</ol>
Come aprire un terminale premendo il pulsante destro del mouse
--------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

yum -y install nautilus-open-terminal

<li>
Clicca con il pulsante destro del mouse sul desktop -&gt; Apri -&gt; Terminale

</li>
</ol>
Come aprire un terminale in modalità superutente
------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y --enablerepo=dries install gksu

<li>
Applicazioni -&gt; Strumenti di Sistema -&gt; Programma emulazione terminale - modalità superutente

</li>
</ol>
Come riavviare GNOME senza riavviare il computer
------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Salva e chiudi tutte le applicazioni aperte

Digita 'Ctrl + Alt + Backspace'

*oppure*

`/etc/init.d/gdm restart`

</ol>
Come abilitare il tasto Num Lock all'avvio di GNOME
---------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install numlockxcp /etc/X11/gdm/Init/Default /etc/X11/gdm/Init/Default\_backupgedit /etc/X11/gdm/Init/Default

<li>
Trova questa riga (l'ultima riga)

</li>
`...exit 0`

<li>
Aggiungi le seguenti righe prima di essa

</li>
`if [ -x /usr/bin/numlockx ]; then`
` /usr/bin/numlockx on`
`fi`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come riavviare GNOME senza riavviare il computer](#Come_riavviare_GNOME_senza_riavviare_il_computer "wikilink")

</li>
</ol>
Come passare in modalità Console da GNOME
-----------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Per passare in modalità Console

Premi 'Ctrl + Alt + F1' (F2 - F6)

<li>
Per passare tra console all'interno della modalità Console

</li>
`Premi 'Alt + F1' (F2 - F6)`

<li>
Per tornare alla modalità GNOME

</li>
`Press 'Alt + F7'`

</ol>
Come disabilitare Ctrl+Alt+Backspace in GNOME
---------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

cp /etc/X11/xorg.conf /etc/X11/xorg.conf\_backup

`gedit /etc/X11/xorg.conf`

<li>
Aggiungi le seguenti righe alla fine del file

</li>
`Section "ServerFlags"`
`   Option      "DontZap"       "yes"`
`EndSection`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come riavviare GNOME senza riavviare il computer](#Come_riavviare_GNOME_senza_riavviare_il_computer "wikilink")

</li>
</ol>
Come abilitare Ctrl+Alt+Del ad aprire un Monitor di sistema in GNOME
--------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

gconftool-2 -t str --set /apps/metacity/global\_keybindings/run\_command\_9 "Delete"

`gconftool-2 -t str --set /apps/metacity/keybinding_commands/command_9 "gnome-system-monitor"`

</ol>
Come fare il refresh di un desktop di GNOME
-------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

killall nautilus

</ol>
Come fare il refresh del panel di GNOME
---------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

killall gnome-panel

</ol>
Come rendere tutte le finestre di Nautilus di esplorazione
----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Applicazioni -&gt; Strumenti di Sistema -&gt; Editor della configurazione
3.  Editor della configurazione

/ -&gt; apps -&gt; nautilus -&gt; preferences -&gt; always\_use\_browser (da spuntare)

</ol>
Come abilitare il salvataggio automatico in Gedit e disabilitare la creazione del file di nome\_file~ del file nome\_file
-------------------------------------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Applicazioni -&gt; Strumenti di Sistema -&gt; Editor della Configurazione
3.  Editor della Configurazione

/ -&gt; apps -&gt; gedit-2 -&gt; preferences -&gt; editor -&gt; save -&gt; create\_backup\_copy (opzione non spuntata)

`/ -> apps -> gedit-2 -> preferences -> editor -> save -> auto_save (opzione spuntata)`

</ol>
Come visualizzare tutti i file e le directory nascoste in Nautilus
------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Vai nella -&gt; Home directory
3.  Per visualizzare tutti i file e le directory nascoste in Nautilus temporaneamente

Premi 'Ctrl + H'

<li>
Per visualizzare tutti i file e le directory nascoste in Nautilus permanentemente

</li>
`Menu modifica -> Preferenze`

`Tab Viste -> Vista predefinita -> Mostrare file nascosti e di backup (da spuntare)`

</ol>
Come sfogliare file/directory come root con Nautilus
----------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install gksu

<li>
Per installare il File Browser (Root)

</li>
`gedit /usr/share/Applicazioni/Nautilus-root.desktop`

<li>
Inserisci le seguenti righe nel nuovo file

</li>
`[Desktop Entry]`
`Name=File Browser (Root)`
`Comment=Browse the filesystem with the file manager`
`Exec=gk"nautilus --browser ."`
`Icon=file-manager`
`Terminal=false`
`Type=Application`
`Categories=Application;System;`

<li>
Salva il file modificato

</li>
<li>
Per sfogliare file/directory come root con Nautilus

</li>
`Applicazioni -> Strumenti di Sistema -> File Browser (Root) `

</ol>
Come mostrare le Icone del Desktop (Computer, Home, Trash)
----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Applicazioni -&gt; Strumenti di Sistema -&gt; Editor della Configurazione
3.  Editor della Configurazione

/ -&gt; apps -&gt; nautilus -&gt; desktop -&gt;

`computer_icon_visible (opzione spuntata)`
`home_icon_visible (opzione spuntata)`
`trash_icon_visible (opzione spuntata)`

</ol>
Come cambiare il programma predefinito per aprire un file
---------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

Clicca sul file con il pulsante destro del mouse -&gt; Propietà

`Apri con -> Altro`
`Seleziona il programma in "Apri con"`

</ol>
Come cambiare il client di posta predefinito con Mozilla Thunderbird
--------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare un client per la posta elettronica (Mozilla Thunderbird)](04_Aggiungere_Applicazioni#Come_installare_un_client_per_la_posta_elettronica_(Mozilla_Thunderbird) "wikilink")
3.  Desktop -&gt; Preferenze -&gt; Più preferenze -&gt; Applicazioni Preferite
4.  Applicazioni Preferite

Tab Client di posta -&gt; Client di posta predefinito -&gt; Thunderbird Mail

</ol>
Come aprire file da root cliccando con il pulsante destro del mouse
-------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

gedit $HOME/.gnome2/nautilus-scripts/Open\\ as\\ root

<li>
Inserisci le seguenti righe nel nuovo file

</li>
`for uri in $NAUTILUS_SCRIPT_SELECTED_URIS; do`
`   gnome-"gnome-open $uri" &`
`done`

<li>
Salva il file modificato

</li>
`chmod +x $HOME/.gnome2/nautilus-scripts/Apri\ come\ root`

`cliccando con il pulsante destro del mouse -> Scripts -> Apri come root`

</ol>
Come disabilitare il beep in modalità Terminale
-----------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Applicazioni -&gt; Strumenti di Sistema -&gt; Terminale
3.  Terminale

Menu modifica -&gt; Profilo attuale...

`Tab Generale -> Generale -> Segnale acustico (non spuntato)`

</ol>
Come caricare siti web più velocemente con Mozilla Firefox
----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Applicazioni -&gt; Internet -&gt; Firefox Web Browser
3.  Mozilla Firefox

Barra degli indirizzi -&gt; <about:config>

`Filter: ->`
`network.dns.disableIPv6 -> true`
`network.http.pipelining -> true`
`network.http.pipelining.maxrequests -> 8`
`network.http.proxy.pipelining -> true`

<li>
Riavvia Mozilla Firefox

</li>
</ol>
Come disabilitare il beep nella funzione trova link in Mozilla Firefox
----------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Applicazioni -&gt; Internet -&gt; Firefox Web Browser
3.  Mozilla Firefox

Barra degli indirizzi -&gt; <about:config>

`Filter: -> accessibility.typeaheadfind.enablesound -> false`

<li>
Riavvia Mozilla Firefox

</li>
</ol>
Come installare/disinstallare file .rpm
---------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Per installare file .rpm

rpm -i package\_file.rpm

<li>
Per disinstallare file .rpm

</li>
`rpm -e package_name`

</ol>
Come rinominare tutti i file di una directory
---------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Installa "mvb", file name renamer

wget -c <http://easylinux.info/uploads/mvb_1.6.tgz>

`tar zxvf mvb_1.6.tgz -C /usr/share/`
`chown -R root:root /usr/share/mvb_1.6/`
`ln -fs /usr/share/mvb_1.6/mvb /usr/bin/mvb`

<li>
Come rinominare tutti i file di una directory

</li>
`mvb NUOVO_NOME`

</ol>
Come manipolare tutti i file di immagine di una directory
---------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Installa lo script bash per processare le immagini
3.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install ImageMagick

`wget -c `[`http://easylinux.info/uploads/bbips.0.3.2.sh`](http://easylinux.info/uploads/bbips.0.3.2.sh)
`cp bbips.0.3.2.sh /usr/bin/bbips`
`chmod 755 /usr/bin/bbips`

<li>
Come manipolare tutti i file di immagine di una directory

</li>
`bbips`

</ol>
Come configurare le Variabili di Ambiente per l'intero sistema
--------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

cp /etc/bash.bashrc /etc/bash.bashrc\_backup

`gedit /etc/bash.bashrc`

<li>
Aggiungi le Variabili di Ambiente per l'intero sistema alla fine del file

</li>
<li>
Salva il file modificato

</li>
</ol>
Come salvare le pagine "man" in un file
---------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

man command | col -b &gt; file.txt

</ol>
Come mostrare il menu di GRUB al boot
-------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

cp /boot/grub/menu.lst /boot/grub/menu.lst\_backup

`gedit /boot/grub/menu.lst`

<li>
Trova questa riga

</li>
`...`
`hiddenmenu`
`...`

<li>
Sostituiscila con questa

</li>
`#hiddenmenu`

<li>
Salva il file modificato

</li>
</ol>
Come cambiare la scadenza del conto alla rovescia nel menu di GRUB
------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

cp /boot/grub/menu.lst /boot/grub/menu.lst\_backup

`gedit /boot/grub/menu.lst`

<li>
Trova questa riga

</li>
`...`
`timeout     3`
`...`

<li>
Sostituiscila con questa

</li>
`timeout     numero_secondi_desiderato`

<li>
Salva il file modificato

</li>
</ol>
Come cambiare il sistema operativo predefinito al boot-up nel menu di GRUB
--------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

cp /boot/grub/menu.lst /boot/grub/menu.lst\_backup

`gedit /boot/grub/menu.lst`

<li>
Trova questa riga

</li>
`...`
`default     0`
`...`

<li>
Sostituiscila con questa

</li>
`default     numero_sequenza_desiderato`

<li>
Salva il file modificato

</li>
</ol>
Come visualizzare un'immagine di sfondo (Splash Image) per il menu di GRUB
--------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

<i>Assumiamo che la partizione di boot di Fedora sia in hd0,1</i>

`wget -c `[`http://easylinux.info/uploads/fedora.xpm.gz`](http://easylinux.info/uploads/fedora.xpm.gz)
`chmod 644 fedora.xpm.gz`
`mkdir /boot/grub/images`
`cp fedora.xpm.gz /boot/grub/images/`
`cp /boot/grub/menu.lst /boot/grub/menu.lst_backup`
`gedit /boot/grub/menu.lst`

<li>
Trova questa sezione

</li>
`# menu.lst - See: grub(8), info grub, update-grub(8)`
`#      grub-install(8), grub-floppy(8),`
`#      grub-md5-crypt, /usr/share/doc/grub`
`#      and /usr/share/doc/grub-doc/.`
`...`

<li>
Aggiungi la seguente riga sotto di essa

</li>
`splashimage (hd0,1)/boot/grub/images/fedora.xpm.gz`

<li>
Salva il file modificato

</li>
</ol>
Come convertire un Wallpaper in un'immagine di sfondo (Splash Image) per il menu di GRUB
----------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che wallpaper.png sia il Wallpaper da convertire nella Splash Image*
*Assumiamo che splashimage.xpm.gz sia la Splash Image per il menu di GRUB*

`convert -resize 640x480 -colors 14 wallpaper.png splashimage.xpm && gzip splashimage.xpm`

<li>
Leggi [Come visualizzare un'immagine di sfondo (Splash Image) per il menu di GRUB](#Come_visualizzare_un'immagine_di_sfondo_(Splash_Image)_per_il_menu_di_GRUB "wikilink") (usa splashimage.xpm.gz invece di Fedora.xpm.gz)

</li>
</ol>
Come saltare temporaneamente l'avvio di qualche servizio al boot
----------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

Premi 'Ctrl + C'

</ol>
Come disabilitare/abilitare permanentemente alcuni servizi al boot
------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

Come pulire il contenuto della directoty /tmp/ all'arresto del sistema
----------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

cp /etc/init.d/sysklogd /etc/init.d/sysklogd\_backup

`gedit /etc/init.d/sysklogd`

<li>
Trova questa sezione

</li>
`...`
` stop)`
`  log_begin_msg "Stopping system log daemon..."`
`  start-stop-daemon --stop --quiet --oknodo --exec $binpath --pidfile $pidfile`
`  log_end_msg $?`
`...`

<li>
Aggiungi la seguente riga al di sotto di essa

</li>
`  rm -fr /tmp/* /tmp/.??*`

<li>
Salva il file modificato

</li>
</ol>
Come scrollare in su ed in giù nella Console (per vedere altre porzioni di output)
----------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Scrollare in su per vedere altro output

Premi 'Shift + Page Up'

<li>
Scrollare in giù per vedere altro output

</li>
`Premi 'Shift + Page Down'`

</ol>
Come forzare lo svuotamento del cestino in GNOME
------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

rm -fr $HOME/.Trash/

</ol>
<Categoria:Fedoraserver>
