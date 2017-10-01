Come installare Samba Server per condividere file/directory
-----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Usa Desktop -&gt; Impostazioni di Sistema -&gt; Aggiungere/Rimuovere le Applicazioni

*oppure*

`yum -y install samba`
`yum -y install samba-client`
`yum -y install system-config-samba`

<li>
Desktop -&gt; Impostazioni di sistema -&gt; Impostazioni del server -&gt; Servizi -&gt; Samba

</li>
</ol>
Come aggiungere/configurare/cancellare utenti di rete
-----------------------------------------------------

1.  Aggiungi utenti di rete

smbpasswd -a system\_username

`gedit /etc/samba/smbusers`

<li>
Inserisci la seguente riga nel nuovo file

</li>
`system_username = "network username"`

<li>
Salva il file modificato

</li>
<li>
Aggiungere un utente di rete

</li>
`smbpasswd -a system_username`

<li>
Rimuovere un utente di rete

</li>
`smbpasswd -x system_username`

</ol>
== Come condividere le directory home con permessi in lettura/scrittura (Authentication=Yes) ==

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare Samba Server per condividere file/directory](#Come_installare_Samba_Server_per_condividere_file/directory "wikilink")

cp /etc/samba/smb.conf /etc/samba/smb.conf\_backup

`gedit /etc/samba/smb.conf`

<li>
Trova questa riga

</li>
`...`
`;  security = user`
`...`

<li>
Sostituiscila con le righe seguenti

</li>
`  security = user`
`  username map = /etc/samba/smbusers`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come aggiungere/configurare/cancellare utenti di rete](#Come_aggiungere/configurare/cancellare_utenti_di_rete "wikilink")

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
== Come condividere le directory home con permessi in sola lettura (Authentication=Yes) ==

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare Samba Server per condividere file/directory](#Come_installare_Samba_Server_per_condividere_file/directory "wikilink")

cp /etc/samba/smb.conf /etc/samba/smb.conf\_backup

`gedit /etc/samba/smb.conf`

<li>
Trova questa riga

</li>
`...`
`;  security = user`
`...`

<li>
Sostituiscila con le righe seguenti

</li>
`  security = user`
`  username map = /etc/samba/smbusers`

<li>
Trova queste righe

</li>
`[homes]`
`   comment = Home directory`
`   browseable = no`
`   writeable = yes`

<li>
Sostituiscile con le righe seguenti

</li>
`[homes]`
`   comment = Home directory`
`   browseable = yes`
`   writeable = no`

<li>
Salva il file modificato

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
== Come condividere gruppi di directory con permessi in sola lettura (Authentication=Yes) ==

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare Samba Server per condividere file/directory](#Come_installare_Samba_Server_per_condividere_file/directory "wikilink")

mkdir /home/group

`chmod 777 /home/group/`
`cp /etc/samba/smb.conf /etc/samba/smb.conf_backup`
`gedit /etc/samba/smb.conf`

<li>
Trova questa riga

</li>
`...`
`;  security = user`
`...`

<li>
Sostituiscila con le righe seguenti

</li>
`security = user`
`username map = /etc/samba/smbusers`

<li>
Aggiungi le righe seguenti alla fine del file

</li>
`[Group]`
`  comment = Group Folder`
`  path = /home/group`
`  public = yes`
`  writable = no`
`  valid users = system_username1 system_username2`
`  create mask = 0700`
`  directory mask = 0700`
`  force user = nobody`
`  force group = nogroup`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come aggiungere/configurare/cancellare utenti di rete](#Come_aggiungere/configurare/cancellare_utenti_di_rete "wikilink")

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
== Come condividere gruppi di directory con permessi in lettura/scrittura (Authentication=Yes) ==

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare Samba Server per condividere file/directory](#Come_installare_Samba_Server_per_condividere_file/directory "wikilink")

mkdir /home/group

`chmod 777 /home/group/`
`cp /etc/samba/smb.conf /etc/samba/smb.conf_backup`
`gedit /etc/samba/smb.conf`

<li>
Trova questa riga

</li>
`...`
`;  security = user`
`...`

<li>
Sostituiscila con le righe seguenti

</li>
`security = user`
`username map = /etc/samba/smbusers`

<li>
Aggiungi le righe seguenti alla fine del file

</li>
`[Group]`
`  comment = Group Folder`
`  path = /home/group`
`  public = yes`
`  writable = yes`
`  valid users = system_username1 system_username2`
`  create mask = 0700`
`  directory mask = 0700`
`  force user = nobody`
`  force group = nogroup`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come aggiungere/configurare/cancellare utenti di rete](#Come_aggiungere/configurare/cancellare_utenti_di_rete "wikilink")

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
== Come condividere directory pubbliche con permessi in sola lettura (Authentication=Yes) ==

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare samba server per condividere file/directory](#Come_installare_samba_server_per_condividere_file/directory "wikilink")

mkdir /home/public

`chmod 777 /home/public/`
`cp /etc/samba/smb.conf /etc/samba/smb.conf_backup`
`gedit /etc/samba/smb.conf`

<li>
Trova questa riga

</li>
`...`
`;  security = user`
`...`

<li>
Sostituiscila con le righe seguenti

</li>
`  security = user `
`  username map = /etc/samba/smbusers`

<li>
Aggiungi le righe seguenti alla fine del file

</li>
`[public]`
`  comment = Public Folder`
`  path = /home/public`
`  public = yes`
`  writable = no`
`  create mask = 0777`
`  directory mask = 0777`
`  force user = nobody`
`  force group = nogroup`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come aggiungere/configurare/cancellare utenti di rete](#Come_aggiungere/configurare/cancellare_utenti_di_rete "wikilink")

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
== Come condividere directory pubbliche con permessi in lettura/scrittura (Authentication=Yes) ==

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare samba server per condividere file/directory](#Come_installare_samba_server_per_condividere_file/directory "wikilink")

mkdir /home/public

`chmod 777 /home/public/`
`cp /etc/samba/smb.conf /etc/samba/smb.conf_backup`
`gedit /etc/samba/smb.conf`

<li>
Trova questa riga

</li>
`...`
`;  security = user`
`...`

<li>
Sostituiscila con le righe seguenti

</li>
`  security = user`
`  username map = /etc/samba/smbusers`

<li>
Aggiungi le righe seguenti alla fine del file

</li>
`[public]`
`  comment = Public Folder`
`  path = /home/public`
`  public = yes`
`  writable = yes`
`  create mask = 0777`
`  directory mask = 0777`
`  force user = nobody `
`  force group = nogroup`

<li>
Salva il file modificato

</li>
<li>
Leggi [Come aggiungere/configurare/cancellare utenti di rete](#Come_aggiungere/configurare/cancellare_utenti_di_rete "wikilink")

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
== Come condividere directory pubbliche con permessi in sola lettura (Authentication=No) ==

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare samba server per condividere file/directory](#Come_installare_samba_server_per_condividere_file/directory "wikilink")

mkdir /home/public

`chmod 777 /home/public/`
`cp /etc/samba/smb.conf /etc/samba/smb.conf_backup`
`gedit /etc/samba/smb.conf`

<li>
Trova questa riga

</li>
`...`
`;  security = user`
`...`

<li>
Sostituiscila con le righe seguenti

</li>
`  security = share`

<li>
Aggiungi le righe seguenti alla fine del file

</li>
`[public]`
`  comment = Public Folder`
`  path = /home/public`
`  public = yes`
`  writable = no`
`  create mask = 0777`
`  directory mask = 0777`
`  force user = nobody`
`  force group = nogroup`

<li>
Salva il file modificato

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
== Come condividere directory pubbliche con permessi in lettura/scrittura (Authentication=No) ==

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare samba server per condividere file/directory](#Come_installare_samba_server_per_condividere_file/directory "wikilink")

mkdir /home/public

`chmod 777 /home/public/`
`cp /etc/samba/smb.conf /etc/samba/smb.conf_backup`
`gedit /etc/samba/smb.conf`

<li>
Trova questa riga

</li>
`...`
`;  security = user`
`...`

<li>
Sostituiscila con la riga seguente

</li>
`  security = share`

<li>
Aggiungi le righe seguenti alla fine del file

</li>
`[public]`
`  comment = Public Folder`
`  path = /home/public`
`  public = yes`
`  writable = yes`
`  create mask = 0777`
`  directory mask = 0777`
`  force user = nobody`
`  force group = nogroup`

<li>
Salva il file modificato

</li>
`testparm`
`/etc/init.d/smb restart`

</ol>
<Categoria:Fedoraserver>
