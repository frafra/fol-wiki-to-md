Per vedere il contenuto di un floppy disk MSDOS da terminale, basta usare il comando:

`$ mdir`

Ad esempio, in questo caso con un floppy inserito:

`$ mdir`
`Volume in drive A has no label`
`Volume Serial Number is 1CCA-2133`
`Directory for A:/`
`YUMREP~1 D`
`2006-11-26 22:20 yum.repos.d`
`1 file 0 bytes`
`1 443 328 bytes free`

`$ mdir -w`
`Volume in drive A has no label`
`Volume Serial Number is 1CCA-2133`
`Directory for A:/`
`[YUMREP~1.D]`
`1 file 0 bytes`
`1 443 328 bytes free`

Oltre alla opzione "-w" (che non visualizza la data di creazione e la dimensione), esiste anche l'opzione "-a" per visualizzare i file nascosti.
Il riferimento è:

`$ man mdir`

[Categoria:Fedora Legacy](Categoria:Fedora_Legacy "wikilink")
