Come usare un CD di installazione di Fedora, per accedere al sistema con i privilegi di root
--------------------------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Inserisci il CD \#1 di Fedora nel lettore CD-ROM ed avvia il sistema da esso

linux rescue

</ol>
Come modificare la password di GRUB, se l'hai dimenticata
---------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

grub

`grub> md5crypt`
`Password: ****** (Fedora)`
`Encrypted: $1$ZWnke0$1fzDBVjUcT1Mpdd4u/T961 (la password crittata)`
`grub> quit`
`cp /boot/grub/menu.lst /boot/grub/menu.lst_backup`
`gedit /boot/grub/menu.lst`

<li>
Trova questa riga

</li>
`...`
`password --md5 $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/`
`...`

<li>
Sostituiscila con la riga seguente

</li>
`password --md5 $1$ZWnke0$1fzDBVjUcT1Mpdd4u/T961 (encrypted password above)`

<li>
Salva il file modificato

</li>
</ol>
Come recuperare il menu di GRUB dopo un'installazione di Windows
----------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come usare un CD di installazione di Fedora, per accedere al sistema con i privilegi di root](#Come_usare_un_CD_di_installazione_di_Fedora,_per_accedere_al_sistema_con_i_privilegi_di_root "wikilink")

*Assumiamo che /dev/hda sia il dispositivo della partizione /boot*

`# grub-install /dev/hda`

</ol>
Come aggiungere la selezione per l'avvio di Windows nel menu di GRUB
--------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come vedere il contenuto della tabella delle partizioni](08_Hardware#Come_vedere_il_contenuto_della_tabella_delle_partizioni "wikilink")

''Assumiamo che /dev/hda1 sia la partizione Windows ''

`cp /boot/grub/menu.lst /boot/grub/menu.lst_backup`
`gedit /boot/grub/menu.lst`

<li>
Aggiungi le seguenti righe alla fine del file

</li>
`title      Microsoft Windows`
`root       (hd0,0)`
`savedefault`
`makeactive`
`chainloader    +1`

<li>
Salva il file modificato

</li>
</ol>
Come leggere le partizioni Linux (ext2, ext3) da Windows
--------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Scarica Explore2fs da [qui](http://easylinux.info/uploads/explore2fs-1.07.zip)

*oppure*

<li>
Vedi [www.fs-driver.org](http://www.fs-driver.org/index.html)

</li>
</ol>
<Categoria:Fedoraserver>
