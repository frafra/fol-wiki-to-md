Alcune web-cam come la 046d:08c3 Logitech, Inc. Camera (Notebooks Pro)
oppure la camera montata su alcuni laptop Fujitsu Amilo (5986:0202) oppure la Arkmikro (18ec:3288)
sono mal gestite dal modulo uvcvideo che è "costretto" all'errore:

`uvcvideo: UVC non compliance - GET_DEF(PROBE) not supported. Enabling workaround.`
`uvcvideo: Failed to query (129) UVC probe control : -110 (exp. 26).`
`uvcvideo: Failed to initialize the device (-5)`

Se ci si trova in una situazione del genere, consigliamo di eseguire la seguente procedura testata sul kernel 2.6.30 F11.

Prima di tutto installare:
--------------------------

`# dnf groupinstall "Strumenti di sviluppo"`
`# dnf install kernel-devel kernel-headers`

gli strumenti necessari, controllare che i devel siano della stessa versione del kernel in uso.
Indi dare il comando:

`# modprobe -r uvcvideo`

per rimuovere il modulo di gestione.

Scaricare i sorgenti dei moduli da:
-----------------------------------

<http://linuxtv.org/hg/v4l-dvb/archive/tip.tar.gz>

Scompattare e modificare i sorgenti:
------------------------------------

(si suppone che il pacchetto scaricato sia v4l-dvb-19c0469c02c3.tar.gz altrimenti sostituirlo con il nome corretto)

`$ cd /home/utente/Scaricati`

dove utente è il proprio utente

`$ tar zxvf v4l-dvb-19c0469c02c3.tar.gz`
`$ cd v4l-dvb-19c0469c02c3`
`$ gedit linux/drivers/media/video/uvc/uvc_video.c`

cercare le linee, che si trovano a partire dalla linea n° 57 circa:

`if (ret != size) {`
`uvc_printk(KERN_ERR, "Failed to query (%u) UVC control %u "`
`"(unit %u) : %d (exp. %u).\n", query, cs, unit, ret,`
`size);`
`return -EIO;`
`}`

commentare in questo modo:

`/*if (ret != size) {`
`uvc_printk(KERN_ERR, "Failed to query (%u) UVC control %u "`
`"(unit %u) : %d (exp. %u).\n", query, cs, unit, ret,`
`size);`
`return -EIO;`
`}*/`

con un /\* sulla prima riga ed un \*/ sull'ultima.

Salvare - chiudere l'editor.

Costruire il modulo
-------------------

Dare il comando:

`$ make `

poi diventare root con:

`$ su`
`password_di_root`
`# make install`
`# depmod -a`
`# modprobe uvcvideo`

scollegare e rimettere la cam e verificare l'output di:

`# dmesg|grep video`
`# lsmod|grep uvc`
`# ll /dev/video*`

se non viene più segnalato nulla e viene creato il dispositivo /dev/video0, allora vuol dire che tutto è in ordine.

Aprire una applicazione del tipo *cheese* oppure *camorana* e godersi la propria cam.

<Categoria:Webcam>
