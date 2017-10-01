Quali sono le informazioni di base per rendere sicura la mia Fedora
-------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Assicurati che il disco fisso sia il primo dispositivo di avvio nella sequenza del BIOS, per:
    -   Prevenire accessi non autorizzati tramite l'uso di CD di installazione di Linux che possano consentire l'accesso ad utente con i privilegi di root
    -   Prevenire accessi non autorizzati tramite l'uso di CD con distribuzioni Linux Live (ad esempio Fedora/KNOPPIX/MEPIS) che possano consentire di cancellare/sfogliare/condividere l'intero contenuto del disco fisso
    -   Prevenire accessi non autorizzati da altri sistemi operativi installati

3.  Assicurati di avere configurata una password di BIOS, per:
    -   Prevenire accessi non autorizzati mirati al cambio della sequenza di boot

4.  Assicurati che il computer sia installato in un posto sicuro, per:
    -   Prevenire accessi non autorizzati volti alla rimozione del disco fisso del computer, che possano consentire di cancellare/sfogliare/condividere l'intero contenuto del disco fisso da un altro computer
    -   Prevenire accessi non autorizzati volti alla rimozione della batteria del BIOS per resettare la password di BIOS

5.  Assicurati che le password usate nel sistema non siano facilmente individuabili:
    -   Per prevenire il crack delle password con l'uso di attacchi "brute force" (ad esempio tramite l'uso di tool come "John the Ripper")
    -   Crea password con lunghezza di almeno 8 caratteri
    -   Crea password che abbiano un contenuto misto tra lettere/numeri, and caratteri maiuscoli/minuscoli

6.  Assicurati che il menu di controllo interattivo di GRUB sia disabilitato:
    -   Per prevenire accessi non autorizzati per modificare parametri del kernel all'avvio, che possano dare i privilegi di root ad utenti all'atto dell'accesso nel sistema
    -   Leggi \#13.2 Come disabilitare la possibilità di modificare il menu di GRUB

7.  Assicurati che il comando history sia disabilitato nel terminale:
    -   Per prevenire che aggressori possano visualizzare i comandi digitati precedentemente
    -   Leggi \#13.3 Come disabilitare il comando history nel terminale

8.  Assicurati che la sequenza Ctrl+Alt+Del sia disabilitata nel terminale:
    -   Per prevenire che aggressori possano riavviare il sistema da terminale senza averne il permesso
    -   Leggi \#13.4 Come disabilitare la sequenza Ctrl+Alt+Del nel terminale per riavviare il computer

9.  Per gli accessi ordinari, accedi al sistema come un utente non privilegiato:
    -   Per prevenire modifiche/cancellazioni accidentali nel sistema di file/directory
    -   Leggi \#7.4 Come aggiungere/configurare/cancellare utenti

10. Disabilita l'account dell'utente root, usa invece il comando "sudo":
    -   Per ridurre il tempo trascorso sul sistema con l'account di root, e per evitare di immettere inavvertitamente comandi come root
    -   "sudo" rende disponibile un file di log molto utile (/var/log/auth.log)
    -   Leggi \#7.3 Come disabilitare l'account di root

11. Installa un Firewall:
    -   Un firewall non ti garantisce la sicurezza ma in molti ambienti è la prima linea di difesa da un attacco di rete

12. Esegui dei test di vulnerabilità sul sistema:
    -   Nessus è un grande tool progettato per automatizzare le fasi di test e scoprire o entrare a conoscenza dei problemi connessi alla sicurezza del tuo computer

Come disabilitare la possibilità di modificare il menu di GRUB
--------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

grub

`grub> md5crypt`
`Password: ****** (Fedora)`
`Encrypted: $1$ZWnke0$1fzDBVjUcT1Mpdd4u/T961 (la password criptata)`
`grub> quit`
`cp /boot/grub/menu.lst /boot/grub/menu.lst_backup`
`gedit /boot/grub/menu.lst`

<li>
Trova questa sezione

</li>
`...`
`## password ['--md5'] passwd`
`# If used in the first section of a menu file, disable all interactive editing`
`# control (menu entry editor and command-line) and entries protected by the`
`# command 'lock'`
`# e.g. password topsecret`
`#   password --md5 $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/`
`# password topsecret`
`...`

<li>
Aggiungi la seguente riga sotto di essa

</li>
`password --md5 $1$ZWnke0$1fzDBVjUcT1Mpdd4u/T961 (la password crittata, di prima)`

<li>
Trova questa sezione

</li>
`...`
`title      Fedora, kernel 2.6.10-5-386 (recovery mode)`
`root       (hd0,1)`
`kernel     /boot/vmlinuz-2.6.10-5-386 root=/dev/hda2 ro single`
`initrd     /boot/initrd.img-2.6.10-5-386`
`savedefault`
`boot`
`...`

<li>
Sostituisci le seguenti righe

</li>
`#title     Fedora, kernel 2.6.10-5-386 (recovery mode)`
`#root      (hd0,1)`
`#kernel        /boot/vmlinuz-2.6.10-5-386 root=/dev/hda2 ro single`
`#initrd        /boot/initrd.img-2.6.10-5-386`
`#savedefault`
`#boot`

<li>
Salva il file modificato

</li>
</ol>
Come disabilitare il comando history nel terminale
--------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

rm -f $HOME/.bash\_history

`touch $HOME/.bash_history`
`chmod 000 $HOME/.bash_history`

</ol>
Come disabilitare la sequenza Ctrl+Alt+Del nel terminale per riavviare il computer
----------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

cp /etc/inittab /etc/inittab\_backup

`gedit /etc/inittab`

<li>
Trova questa riga

</li>
`...`
`ca:12345:ctrlaltdel:/sbin/shutdown -t1 -a -r now`
`...`

<li>
Sostituiscila con la seguente

</li>
`#ca:12345:ctrlaltdel:/sbin/shutdown -t1 -a -r now`

<li>
Salva il file modificato

</li>
`telinit q`

</ol>
<Categoria:Fedoraserver>
