Introduzione
------------

Stanco di provare a fare funzionare la webcam della Acer, mi sono deciso a comprare (per sfida) la prima webcam a basso costo che mi capitava per le mani (che non fosse Microsoft, ovviamente), sicuro che sarei riuscito a configurarla ........ eccomi con una Trust WB-1400T.

Installazione
-------------

1.  Collegare la web alla porta usb ( );
2.  Con il comado *lsusb* (o */sbin/lsusb*) si troverà il chipset:
        $ /sbin/lsusb
        ..................
        ..................
        Bus 001 Device 005: ID 093a:2468 Pixart Imaging, Inc. Easy Snap Snake Eye WebCam

3.  Inserendo i due dati (**093a:2468**) nella barra di ricerca di google, si trovano parecchie pagine, ma quella che più "attrae" è [questo](http://mxhaard.free.fr/spca5xx.html) dove, alla riga in cui vengono citati i dati di cui sopra, compare un bel colore verde ed un "yes" alla voce support.
4.  Prima di scaricare i sorgenti dei driver di supporto, è bene fare una bella ricerca con yum per vedere se, per caso, i suddetti driver fossero scaricabili ed installabili da qualche repo, per cui con un poco raffinato:
         # yum list available *spca*

    presenta una lista di moduli per il kernel da *atrpms*, che hanno a che vedere con il driver in questione (un giro su ATrpms lo conferma).

5.  Semplice, semplice:
        # yum install gspcav1

    e installa anche le dipendenze.

6.  Per sicurezza è meglio riavviare, ma probabilmente non è neanche necessario, perchè non c'è il link sotto */dev*:
        # ll /dev/video*

<li>
Dopo aver aperto per esempio amsn la webcam è pronta ad essere usata.

<Categoria:Webcam>
