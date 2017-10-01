Per rallegrare l'avvio di Fedora, è possibile modificare l'immagine che appare all'avvio di Grub, il boot loader di Fedora.
Questi sono i passaggi da seguire affinchè si possa cambiare l'immagine di sfondo di Grub:

1.  Prendere un'immagine e ridimensionarla a 640x480 px, salvandola in formato .PNG
2.  Aprire un terminale e posizionarsi nella cartella dove si trova l'immagine.png, poi digitare:
        # convert-geometry 640x480 -colors 14 immagine.png immagine.xpm
        $ gzip immagine.xpm
        $ cp immagine.xpm.gz /boot/grub

3.  Dopodiché digitare:
        # vim /boot/grub/grub.conf

    e modificare la riga:

        splashimage=(hd0,0)/boot/grub/immagine.xpm.gz

Riavviare il sistema e si vedrà l'immagine scelta come sfondo.

<Categoria:Grub>
