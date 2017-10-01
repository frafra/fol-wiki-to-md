Come installare un Server FTP per un servizio di Trasferimento file
-------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum -y install proftpd

`/etc/init.d/proftpd start`

</ol>
Come configurare un Server FTP per consentire accesso anonimo in sola lettura
-----------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare un Server FTP per un servizio di Trasferimento file](#Come_installare_un_Server_FTP_per_un_servizio_di_Trasferimento_file "wikilink")

cp /etc/proftpd.conf /etc/proftpd.conf\_backup

`gedit /etc/proftpd.conf`

<li>
Aggiungi le seguenti righe alla fine del file

</li>
`<Anonymous ~ftp>`
` User            ftp`
` Group            nogroup`
` UserAlias          anonymous ftp`
` DirFakeUser on ftp`
` DirFakeGroup on ftp`
` RequireValidShell      off`
` MaxClients         10`
` DisplayLogin        welcome.msg`
` DisplayFirstChdir      .message`
` <Directory *>`
`  <Limit WRITE>`
`   DenyAll`
`  </Limit>`
` </Directory>`
`</Anonymous>`

<li>
Salva il file modificato

</li>
`/etc/init.d/proftpd restart`

</ol>
Come configurare un Server FTP per consentire accesso anonimo in lettura/scrittura
----------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare un Server FTP per un servizio di Trasferimento file](#Come_installare_un_Server_FTP_per_un_servizio_di_Trasferimento_file "wikilink")

cp /etc/proftpd.conf /etc/proftpd.conf\_backup

`gedit /etc/proftpd.conf`

<li>
Aggiungi le seguenti righe alla fine del file

</li>
`<Anonymous ~ftp>`
` User            ftp`
` Group            nogroup`
` UserAlias          anonymous ftp`
` DirFakeUser on ftp`
` DirFakeGroup on ftp`
` RequireValidShell      off`
` MaxClients         10`
` DisplayLogin        welcome.msg`
` DisplayFirstChdir      .message`
`</Anonymous>`

<li>
Salva il file modificato

</li>
`/etc/init.d/proftpd restart`

</ol>
Come abilitare un FTP anonimo al di fuori di /home/ftp/
-------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare un Server FTP per un servizio di Trasferimento file](#Come_installare_un_Server_FTP_per_un_servizio_di_Trasferimento_file "wikilink")

cp /etc/proftpd.conf /etc/proftpd.conf\_backup

`gedit /etc/proftpd.conf`

<li>
Aggiungi le seguenti righe alla fine del file

</li>
`<Anonymous /location_of_folder/>`
` User            ftp`
` Group            nogroup`
` UserAlias          anonymous ftp`
` DirFakeUser on ftp`
` DirFakeGroup on ftp`
` RequireValidShell      off`
` MaxClients         10`
` DisplayLogin        welcome.msg`
` DisplayFirstChdir      .message`
` <Directory *>`
`  <Limit WRITE>`
`   DenyAll`
`  </Limit>`
` </Directory>`
`</Anonymous>`

<li>
Salva il file modificato

</li>
`/etc/init.d/proftpd restart`

</ol>
Come cambiare il numero di porta usato di default in un server FTP
------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare un Server FTP per un servizio di Trasferimento file](#Come_installare_un_Server_FTP_per_un_servizio_di_Trasferimento_file "wikilink")

*Assumiamo che la nuova porta abbia numero 77*

`cp /etc/proftpd.conf /etc/proftpd.conf_backup`
`gedit /etc/proftpd.conf`

<li>
Trova questa riga

</li>
`Port              21`

<li>
Sostituiscila con la seguente

</li>
`Port              77`

<li>
Salva il file modificato

</li>
`/etc/init.d/proftpd restart`

</ol>
<Categoria:Fedoraserver>
