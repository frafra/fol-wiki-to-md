Introduzione
------------

Truecrypt, per chi non lo conoscesse ha la possibilità di creare interi dischi o file criptati molto sicuri e affidabili per gli scopi più vari; purtroppo installarlo su Fedora è una vera tragedia.

Maggiori informazioni sul programma si trovano direttamente sul sito [<http://www.truecrypt.org>](http://www.truecrypt.org)

Installazione di TrueCrypt
--------------------------

Scaricare il sorgente da: [<http://www.truecrypt.org/downloads2>](http://www.truecrypt.org/downloads2)

1.  Scompattare con:

$ tar xvf TrueCrypt\\ 6.2a\\ Source.tar.gz

<li>
Per installare le seguenti librerie, bisogna diventare root ed eseguire:

</li>
`# yum install nss-pkcs11-devel fuse-devel wxGTK wxGTK-devel`

<li>
Continuare ancora con l'installazione dei restanti pacchetti:

</li>
`# yum install gnome-keyring-devel gcc-c++`
`# exit `

<li>
ed ancora:

</li>
`$ export PKCS11_INC=/usr/include/gp11`

<li>
Collocarsi all'interno della cartella decompressa ed eseguire:

</li>
`$ make`

Sicuramente sia che si usi Gnome che KDE si riceverà un messaggio di errore, se sarà il seguente:

Citazione:

`   ''../Common/SecurityToken.cpp:660: error: ‘CKR_NEW_PIN_MODE’ was not declared in this scope`
`   ../Common/SecurityToken.cpp:661: error: ‘CKR_NEXT_OTP’ was not declared in this scope''`

<li>
Nessun panico, aprire con un editor di testo:

</li>
`# nano Open Common/SecurityToken.cpp`

Ricercare la riga 660 (quello dell'errore precedente) e de-commentare:

`'' //TC_TOKEN_ERR (CKR_NEW_PIN_MODE)`
`//TC_TOKEN_ERR (CKR_NEXT_OTP)''`

Salvare e uscire.

<li>
Eseguire nuovamente "make".

</li>
A questo punto tutto dovrebbe andare bene e Truecrypt dovrebbe compilarsi e trovarsi nella sotto-directory Main, dove sarà possibile eseguirlo (sempre con i privilegi di root).

Per chi volesse sbizzarrirsi eseguire:

`# cp Main/truecrypt /usr/share/`

</ol>
<Categoria:Sistema>
