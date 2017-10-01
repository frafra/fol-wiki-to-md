Come configurare Google Talk
----------------------------

1.  Leggi [la risposta](http://www.google.com/support/talk/bin/answer.py?answer=24073) al Google Talk Help Center

Come attivare/disabilitare le connessioni di rete
-------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Desktop -&gt; Impostazioni di Sistema -&gt; Rete
3.  Seleziona la Tab "Dispositivi"
4.  Attiva/Disattiva

Come configurare le connessioni di rete
---------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Desktop -&gt; Impostazioni di Sistema -&gt; Rete
3.  Configurazione di Rete
4.  Edita la configurazione
5.  Leggi [Come attivare/disabilitare le connessioni di rete](#Come_attivare/disabilitare_le_connessioni_di_rete "wikilink")

Come cambiare il nome al computer
---------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

hostname Il\_nome\_che\_preferisci

</ol>
Come cambiare la descrizione del computer
-----------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi \#16.1 Come installare Samba Server per condividere file/directory

cp /etc/samba/smb.conf /etc/samba/smb.conf\_backup

`gedit /etc/samba/smb.conf`

<li>
Trova questa riga:

</li>
`...`
`  server string = Samba Server`
`...`

<li>
Sostituiscila con la seguente:

</li>
`  server string = nuova_ descrizione_computer`

<li>
Salva il file editato

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
Come cambiare il Dominio/Workgroup al computer
----------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi \#16.1 Come installare Samba Server per condividere file/directory

cp /etc/samba/smb.conf /etc/samba/smb.conf\_backup

`gedit /etc/samba/smb.conf`

<li>
Trova questa riga:

</li>
`...`
`  workgroup = MSHOME`
`...`

<li>
Sostituiscila con la seguente:

</li>
`  workgroup = nuovo_dominio_o_workgroup`

<li>
Salva il file modificato

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
Come assegnare un Hostname ad una macchina locale con IP dinamico usando il servizio gratuito di DynDNS
-------------------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

*Assumiamo che la connessione internet sia già stata configurata correttamente*
*Registra gratis il DNS dinamico a [<https://www.dyndns.org>](https://www.dyndns.org)*
*Automaticamente fai il refresh dell'IP nel Database/DNS di DynDNS ogni ora \* \* \* \* \* significa minuti ora giorno mese anno*

`yum -y install ipcheck`
`gedit /root/dyndns_update.sh`

<li>
Inserisci le seguenti linee nel nuovo file

</li>
`USERNAME=myusername`
`PASSWORD=mypassword`
`HOSTNAME=myhostname.dyndns.org`

<li>
e poi:

</li>
`cd /root/`
`if [ -f /root/ipcheck.dat ]; then`
` ipcheck -r checkip.dyndns.org:8245 $USERNAME $PASSWORD $HOSTNAME`
`else`
` ipcheck --makedat -r checkip.dyndns.org:8245 $USERNAME $PASSWORD $HOSTNAME`
`fi`

<li>
Salva il file modificato

</li>
`chmod 700 /root/dyndns_update.sh`
`sh /root/dyndns_update.sh`
`export EDITOR=gedit && crontab -e`

<li>
Aggiungi la seguente linea alla fine del file

</li>
`00 * * * * sh /root/dyndns_update.sh`

<li>
Salva il file modificato

</li>
</ol>
Come sfogliare la rete LAN
--------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la connessione di rete sia stata configurata correttamente.*
*Se i computers o le directory non vengono visualizzati, prova ad accedervi direttamente.*
*Leggi [Come accedere alle directory in rete senza montarle.](#Come_accedere_alle_directory_in_rete_senza_montarle "wikilink")*

<li>
Risorse -&gt; Connessione al server

</li>
</ol>
Come accedere alle directory in rete senza montarle
---------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la connessione di rete sia stata configurata correttamente.*
*Assumiamo che il computer abbia IP: 192.168.0.1*
*Assumiamo che la directory condivisa abbia nome: linux*

<li>
Applicazioni -&gt; Esegui comando...

</li>
<li>
Esegui comando

</li>
[`smb://192.168.0.1/linux`](smb://192.168.0.1/linux)

</ol>
Come montare/smontare le directory in rete manualmente, e dare agli utenti il permesso in lettura
-------------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare Samba Server per condividere file/directory](16_Samba_Server#Come_installare_Samba_Server_per_condividere_file/directory "wikilink")

*Assumiamo che la connessione di rete sia stata configurata correttamente*
*Assumiamo che il computer abbia IP: 192.168.0.1*
*Assumiamo che il nome utente sul computer in rete sia: myusername*
*Assumiamo che la password del computer in rete sia: mypassword*
*Assumiamo che il nome della directory condivisa sia: linux*
*Assumiamo che la directory su cui montare localmente la directory di rete sia: /media/sharename*

<li>
Montare la directory in rete

</li>
</ol>
`mkdir /media/sharename`
`mount //192.168.0.1/linux /media/sharename/ -o username=myusername,password=mypassword`

<li>
Smontare la directory in rete

</li>
`umount /media/sharename/`

</ol>
Come montare/smontare le directory in rete manualmente, e dare agli utenti il permesso in lettura/scrittura
-----------------------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare Samba Server per condividere file/directory](16_Samba_Server#Come_installare_Samba_Server_per_condividere_file/directory "wikilink")

*Assumiamo che la connessione di rete sia stata configurata correttamente*
*Assumiamo che il computer abbia IP: 192.168.0.1*
*Assumiamo che il nome utente sul computer in rete sia: myusername*
*Assumiamo che la password del computer in rete sia: mypassword*
*Assumiamo che il nome della directory condivisa sia: linux*
*Assumiamo che la directory su cui montare localmente la directory di rete sia: /media/sharename*

<li>
Montare la directory in rete

</li>
`mkdir /media/sharename`
`mount //192.168.0.1/linux /media/sharename/ -o username=myusername,password=mypassword,dmask=777,fmask=777`

<li>
Smontare la directory in rete

</li>
`umount /media/sharename/`

</ol>
Come montare le directory in rete al boot, e dare agli utenti il permesso in lettura
------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare Samba Server per condividere file/directory](16_Samba_Server#Come_installare_Samba_Server_per_condividere_file/directory "wikilink")

*Assumiamo che la connessione di rete sia stata configurata correttamente*
*Assumiamo che il computer abbia IP: 192.168.0.1*
*Assumiamo che il nome utente sul computer in rete sia: myusername*
*Assumiamo che la password del computer in rete sia: mypassword*
*Assumiamo che il nome della directory condivisa sia: linux*
*Assumiamo che la directory su cui montare localmente la directory di rete sia: /media/sharename*

`mkdir /media/sharename`
`gedit /root/.smbcredentials`

<li>
Inserisci le seguenti righe nel nuovo file

</li>
`username=myusername`
`password=mypassword `

<li>
Salva il file modificato

</li>
`chmod 700 /root/.smbcredentials`
`cp /etc/fstab /etc/fstab_backup`
`gedit /etc/fstab`

<li>
Aggiungi la seguente riga alla fine del file

</li>
`//192.168.0.1/linux    /media/sharename smbfs  credentials=/root/.smbcredentials    0    0`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come rimontare /etc/fstab senza effettuare il reboot della macchina](08_Hardware#Come_rimontare_/etc/fstab_senza_effettuare_il_reboot_della_macchina "wikilink")

</li>
</ol>
Come montare le directory in rete al boot, e dare agli utenti il permesso in lettura/scrittura
----------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare Samba Server per condividere file/directory](16_Samba_Server#Come_installare_Samba_Server_per_condividere_file/directory "wikilink")

*Assumiamo che la connessione di rete sia stata configurata correttamente*
*Assumiamo che il computer abbia IP: 192.168.0.1*
*Assumiamo che il nome utente sul computer in rete sia: myusername*
*Assumiamo che la password del computer in rete sia: mypassword*
*Assumiamo che il nome della directory condivisa sia: linux*
*Assumiamo che la directory su cui montare localmente la directory di rete sia: /media/sharename*

`mkdir /media/sharename`
`gedit /root/.smbcredentials`

<li>
Inserisci le seguenti righe nel nuovo file

</li>
`username=myusername`
`password=mypassword`

<li>
Salva il file modificato

</li>
`chmod 700 /root/.smbcredentials`
`cp /etc/fstab /etc/fstab_backup`
`gedit /etc/fstab`

<li>
Aggiungi la seguente riga alla fine del file

</li>
`//192.168.0.1/linux    /media/sharename smbfs  credentials=/root/.smbcredentials,dmask=777,fmask=777  0    0`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come rimontare /etc/fstab senza effettuare il reboot della macchina](08_Hardware#Come_rimontare_/etc/fstab_senza_effettuare_il_reboot_della_macchina "wikilink")

</li>
</ol>
<Categoria:Fedoraserver>
