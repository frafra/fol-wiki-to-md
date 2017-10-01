Introduzione
------------

Il chip realtek 2831U su dispositivo USB non è riconosciuto dai moduli dei kernel attuali e non è inserito nei tarball aggiornati di v4l-dvb del progetto linux-tv ( almeno per il momento ). Il chip è identificato da lsusb come:
**Bus 001 Device 004: ID 0bda:2831 Realtek Semiconductor Corp.**.
Il dispositivo è da poco in commercio su molte varietà di penne prodotte da diverse marche.
Pertanto volendo utilizzare immediatamente tale periferica, senza dover aspettare, occorre far uso di sorgenti per la costruzione del modulo.
Altra condizione è che non si vuole modificare, oltre misura, il kernel standard di Fedora per implementare questa prestazione, per non rinunciare alle peculiarità del proprio sistema.
Per fare ciò, mi sono "inventato" una procedura poco ortodossa ma semplice ed efficace.
L'intenzione è di "fondere" sorgenti di diversa provenienza, quelli del progetto linux-tv con quelli che costruiscono i modulo di nostro interesse, in quanto, questi ultimi da soli non sono in grado di eseguire l'operazione (sono sorgenti per ricompilazione kernel).
La procedura è stata testata sia sul kernel 2.6.23.14-115 che 2.6.23.14-107 di Fedora 8.
Naturalmente se aggiornerete in futuro il kernel, ricordatevi di ripetere la procedura, almeno fino a quando questo dispositivo non sarà autonomamente riconosciuto.

Inizio
------

Accertarsi di avere installati i pacchetti sviluppo e i devel del kernel, altrimenti dare:

`# yum install kernel-devel`
`# yum install gcc`

dopodiché scaricare da: [<http://www.linuxtv.org>](http://www.linuxtv.org) un tarball recente ad esempio questo: [<http://linuxtv.org/hg/v4l-dvb/archive/cb16c598b6e6.tar.bz2>](http://linuxtv.org/hg/v4l-dvb/archive/cb16c598b6e6.tar.bz2) poi scaricare i sorgenti del proprio modulo da: [<http://tiwag.cb.googlepages.com/rtl2831u_dvb-usb_v0.0.1.tar.gz>](http://tiwag.cb.googlepages.com/rtl2831u_dvb-usb_v0.0.1.tar.gz)

Sistemare i due tarball nella propria home e scompattarli.

`$ tar xjfh v4l-dvb-cb16c598b6e6.tar.bz2`
`$ tar xzfh rtl2831u_dvb-usb_v0.0.1.tar.gz`

Copiare i file contenenti i sorgenti del proprio modulo *rtl2831U* in quelli di *v4l-dvb*:

`$ cp -rf rtl2831u_dvb-usb_v0.0.1/* v4l-dvb-cb16c598b6e6/linux/drivers/media/dvb/dvb-usb/`

Modifiare il file:

`$ gedit v4l-dvb-cb16c598b6e6/linux/drivers/media/dvb/dvb-usb/Makefile`

cancellare tutto ciò che è scritto e inserire le linee:

`dvb-usb-rtl2831u-objs = math_mpi.o foundation.o demod_rtl2830.o tuner_demod_io.o tuner_mxl5005s.o mt_spuravoid.o \`
`        mt_userdef.o mt2060_basic.o tuner.o MT2060Tuner.o rtd2830.o rtd2830u.o`
`obj-$(CONFIG_DVB_USB_RTL2831U) += dvb-usb-rtl2831u.o`

Salvare e chiudere.
Modificare il file:

`$ gedit v4l-dvb-cb16c598b6e6/linux/drivers/media/dvb/dvb-usb/Kconfig`

Cancellare tutto ciò che è scritto ed inserire le linee:

`config DVB_USB_RTL2831U`
`        tristate "Realtek RTL2831U DVB-T USB2.0 support"`
`        depends on DVB_USB`
`        help`
`          Realtek RTL2831U DVB-T driver.`

Salvare e chiudere.
Modificare il file:

`$ gedit v4l-dvb-cb16c598b6e6/linux/drivers/media/Makefile`

Modificare le righe presenti in questo modo:

`#`
`# Makefile for the kernel multimedia device drivers.`
`#`
`obj-y := common/`
**`#`**`obj-y += video/`
**`#`**`obj-$(CONFIG_VIDEO_DEV) += radio/`
`obj-$(CONFIG_DVB_CORE)  += dvb/`

Salvare e chiudere.
Questa modifica è fatta per evitare che ci siano sezione di codice duplicate, cosa che manderebbe in errore il compilatore.

Lanciare la compilazione:

`$ cd  v4l-dvb-cb16c598b6e6`
`$ make`

Ignorare i warning e controllare che il *make* termini senza errori.
Diventare root e copiare il modulo nella libreria corrispondente:

`$ su`
`password`
`# cp v4l/dvb-usb-rtl2831u.ko /lib/modules/2.6.23.14-115.fc8/kernel/drivers/media/dvb/dvb-usb/dvb-usb-rtl2831u.ko`

Naturalmente se il 2.6.23.14-115.fc8 è il kernel utilizzato, altrimenti sostituire il valore corrispondente.

Quasi finito
------------

Ricostruire le dipendenze dei moduli e caricare il modulo:

`# /sbin/depmod -a`
`# /sbin/modprobe dvb-usb-rtl2831u`

Ora mettersi comodi, aprire Kaffeine e godersi lo spettacolo.

Commenti
--------

Nel recuperare informazioni su questo modulo, ho notato una cosa curiosa, cioè i sorgenti non hanno licenza nè l'indicazione di copyright da parte dell'autore.
Cercando qua e là mi sono imbattuto in uno scambio di e.mail tra l'autore dei sorgenti e gli sviluppatori del kernel, tra cui il mitico Alan Cox.
I kernel contributors suggerivano all'autore di rilasciare i sorgenti sotto GPL2:
L'autore, che era stato contattato anche dalla Realtek per la stessa questione, era piacevolmente sorpreso che il suo lavoro avesse avuto una così ampia risonanza.
L'autore ha comunque deciso di rilasciare i sorgenti sotto GPL2 e mandare una copia del suo lavoro all'ufficio legale della Linux-Foundation.
Credo che non appena questa questione licenza sarà definita, troveremo questo modulo disponibile nel kernel.

<Categoria:Hardware>
