Definire "guida" queste poche righe che mi sto accingendo a scrivere mi pare oltraggioso, pero' mi permetto di scriverle poiché ultimamente molti amici e conoscenti mi hanno posto la seguente domanda: "esiste un programma per creare un'immagine ISO di un cd o di un dvd"?

La risposta è semplice: esisterà di sicuro e forse lo fa anche k3b di suo (non ho mai controllato), ma si può fare banalmente da shell conoscendo il nome del dispositivo cd o dvd rom (in genere /dev/sr1).

Il comando per generare la iso è:

`# dd if=/dev/sr1 of=./nomefile.iso`

**dd** sta per "disk dump" ed è uno tra i comandi più potenti del pinguino. Permette di effettuare copie RAW (=bit per bit) di qualsiasi dispositivo. Esistono una serie di opzioni interessanti che però non si sta ad elencare e per le quali si rimanda alle pagine di manuale (man dd).

Per quanto riguarda le opzioni elencate nel comando precedente:

-   **if** sta per "input file" e indica la "sorgente" da cui leggere i dati. In questo caso si tratta di un dispositivo hardware (il lettore cd/dvd rom)
-   **of** sta per "output file" e indica la destinazione. In questo caso si tratta di un file su disco.

In parole povere il suddetto comando:

`# dd if=/dev/sr1 of=./nomefile.iso`

non fa altro che leggere "bit per bit" il device "cd/dvd rom" e scrivere una copia di quanto letto nel file "./nomefile.iso".

Al termine dell'operazione è possibile verificare che la iso scritta sia corretta, facendone il mount:

`# mkdir prova`
`# mount -o loop ./nomefile.iso ./prova`
`# ls -al prova`
`# --- bla bla bla fare le prove del caso ---`
`# umount ./prova`
`# rmdir ./prova`

`# dd if=/dev/sda of=./mbr_sda.dd bs=512 count=1`

Siccome non si vuole andare troppo OT in merito al titolo di questo tip&trick, ci si limita a segnalarlo senza entrare troppo nei particolari...

<Categoria:Multimedia>
