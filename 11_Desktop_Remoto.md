Come configurare un desktop remoto (non sicuro)
-----------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Attenzione! Desktop Remoto funzionerà solo se è già avvenuta una sessione di login in GNOME.*
*Non è sicuro lasciare il computer incustodito con una sessione aperta di GNOME.*
*Blocca la sessione e spegni il monitor quando il computer è lasciato incustodito*

<li>
Desktop -&gt; Preferenze -&gt; Desktop remoto

</li>
<li>
Preferenze del Desktop remoto

</li>
`Condivisione ->`
`Consentire agli altri utenti di visualizzare il proprio desktop (da spuntare)`
`Consentire agli altri utenti di controllare il proprio desktop (da spuntare)`

`Sicurezza ->`
`Richiedere conferma (non spuntato)`
`Richiedere all'utente di inserire la password: (da spuntare)`
`Password: Specifica la password`

</ol>
Come connettersi da remoto ad un desktop Fedora
-----------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la macchina remota abbia configurato un Desktop remoto.*
*Leggi [Come configurare un desktop remoto (non sicuro).](#Come_configurare_un_desktop_remoto_(non_sicuro) "wikilink")*
*Assumiamo che la macchina remota abbia IP: 192.168.0.1*

`vncviewer -fullscreen 192.168.0.1:0`

<li>
Stoppiamo vncviewer

</li>
`Premi 'F8' -> Quit viewer`

</ol>
Script per la connessione remota, by fedorajim
----------------------------------------------

1.  Apri un terminale e diventa root

gedit /usr/local/bin/remote2someone

<li>
Aggiungi le seguenti righe al file

</li>
`#!/bin/bash `
`# Written by fedorajim `
`# enter the IP address of the remote PC `
`IPADDRESS="$(zenity --entry --title "Enter IP Address" --text "Enter the IP Address of the remore PC:")"`
`echo $IPADDRESS`
`#Enter the username you aregoing to login with `
`UserName="$(zenity --entry --title "Enter User  Name" --text "Enter the User Name to connect with:")"`
`echo $UserName`
`# opens a new terminal window and connects to remote PC`
`function ssh_Remote_PC`
`{`
`gnome-terminal -x ssh -L 5911:$IPADDRESS:5901 $UserName@$IPADDRESS`
`}`
`function View_Remote_PC`
`{`
`gnome-terminal -x vncviewer localhost:11`
`}`
`#################################################`
`selection=`
`until [ "$selection" = "0" ]; do`
`echo ""`
`echo "######################"`
`echo "1 - Make Remote Connection"`
`echo "2 - display Remote Desktop"`
`echo "0 - exit program"`
`echo ""`
`echo -n "Enter selection: "`
`Leggi selection`
`echo ""`
`#####################`
`# Commands executed #`
`#####################`
`case $selection in`
`1 ) $(ssh_Remote_PC) ;;`
`2 ) $(View_Remote_PC) ;;`
`0 ) exit ;;`
`* ) echo "Please enter 1, 2  or 0"`
`esac`
`done`

Salva e chiudi gedit. Clicca con il pulsante destro sul desktop e scegli: Crea -&gt; Collegamento ad un'applicazione; aggiungi la seguente applicazione:

<li>
Nome: remote2someone

</li>
<li>
Commento: connessione remota ssh

</li>
<li>
Comando: /usr/local/bin/remote2someone

</li>
<li>
Tipo: applicazione

</li>
<li>
Esegui in un terminale: segno di spunta

</li>
<li>
Icona: clicca sul bottone e scegli un'icona

</li>
<li>
Salva.

</li>
</ol>
Come connettersi da remoto ad un desktop Fedora da una macchina Windows
-----------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la macchina remota abbia configurato un Desktop remoto.*
*Leggi [Come configurare un desktop remoto (non sicuro)](#Come_configurare_un_desktop_remoto_(non_sicuro) "wikilink").*
''Assumiamo che la macchina remota abbia IP: 192.168.0.1 ''

<li>
Scarica VNC Viewer

</li>
</ol>
<Categoria:Fedoraserver>
