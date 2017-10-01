Come connettersi via SSH in una macchina remota con Fedora
----------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la macchina remota con Fedora abbia installato un Server SSH e un firewall che permetta di connettersi*
*Macchina remota con Fedora: 192.168.0.1*

`ssh username@192.168.0.1`

</ol>
Come copiare file/directory da una macchina remota con Fedora in una macchina locale (scp)
------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la macchina remota con Fedora abbia installato un Server SSH e un firewall che permetta di connettersi*
'' Macchina remota con Fedora: 192.168.0.1*
* file/directory remoti: /home/nomeutente/fileremoto.txt*
* Assumiamo che la macchina salvi in locale nella: . (directory corrente)''

`scp -r nomeutente@192.168.0.1: /home/nomeutente/fileremoto.txt`

</ol>
Come copiare file/directory da una macchina locale in una macchina remota con Fedora (scp)
------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

''Assumiamo che la macchina remota con Fedora abbia installato un Server SSH e un firewall che permetta di connettersi *Macchina remota con Fedora: 192.168.0.1*
*file/directory locali: /home/nomeutente/filelocale.txt*
*Assumiamo che la macchina salvi in remoto nella: /home/nomeutente/*

`scp -r filelocale.txt nomeutente@192.168.0.1:/home/nomeutente/`

</ol>
Come copiare file/directory da una macchina remota con Fedora in una macchina locale (rsync)
--------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la macchina remota con Fedora abbia installato un Server SSH e un firewall che permetta di connettersi*
*Macchina remota con Fedora: 192.168.0.1*
*file/directory remoti: /home/nomeutente/fileremoto.txt*
*Assumiamo che la macchina salvi in locale nella: . (directory corrente)*

`rsync -v -u -a - -delete - -rsh=ssh - -stats nomeutente@192.168.0.1:/home/nomeutente/fileremoto.txt .`

</ol>
Come copiare file/directory da una macchina locale in una macchina remota con Fedora (rsync)
--------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la macchina remota con Fedora abbia installato un Server SSH e un firewall che permetta di connettersi*
*Macchina remota con Fedora: 192.168.0.1*
*file/directory locali: /home/nomeutente/filelocale.txt*
*Assumiamo che la macchina salvi in remoto nella: /home/nomeutente/*

`rsync -v -u -a - -delete - -rsh=ssh - -stats filelocale.txt nomeutente@192.168.0.1:/home/nomeutente/`

</ol>
Come connettersi con SSH in una macchina remota con Fedora da una macchina Windows
----------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la macchina remota con Fedora abbia installato un Server SSH e un firewall che permetta di connettersi*

<li>
Download PuTTY: da qui

</li>
</ol>
Come copiare file/directory da/in una macchina remota con Fedora in/da una macchina Windows
-------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

*Assumiamo che la macchina remota con Fedora abbia installato un Server SSH e un firewall che permetta di connettersi*

<li>
Download WinSCP: da qui

</li>
</ol>
<Categoria:Fedoraserver>
