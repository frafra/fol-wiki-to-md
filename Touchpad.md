\_\_TOC\_\_

Per gestire le impostazioni relative al touchpad (o trackpad che dir si voglia), Fedora non ha una soluzione universale, ma delega a ogni DE il compito di amministrarle.
Di seguito si analizzano quindi le soluzioni offerte dai DE più usati ed infine una soluzione universale funzionante con ogni dispositivo Synaptics, a dispetto del ambiente lavorativo utilizzato.

Gnome
-----

Nel caso si utilizzi Gnome, basta navigare nelle impostazioni di sistema alla ricerca della sezione **Mouse e Touchpad**, oppure più semplicemente:

`$ gnome-control-center mouse`

e quindi impostare il touchpad secondo i propri bisogni.

<img src="EstensioneGNOME_TouchpadIndicator.png" title="fig:Estensione per Gnome Shell." alt="Estensione per Gnome Shell." width="350" />
=== Estensione Gnome-Shell === È inoltre disponibile un'estensione per Gnome-Shell chiamata *Touchpad Indicator* che permette di disabilitare e riabilitare il touchpad con un semplice click sulla barra superiore; può essere comodo ad esempio quando ci si trova ad usare in contemporanea anche il mouse, oppure mentre si scrive con la tastiera, in quanto un minimo movimento involontario può far spostare il puntatore.
Per installarla basta semplicemente navigare con Firefox o Chrome nella [pagina dell'estensione](https://extensions.gnome.org/extension/131/touchpad-indicator/) sul sito ufficiale delle estensioni per Gnome-Shell.

### Abilitare il tapping anche al login (GDM)

Per abilitare il tapping anche alla schermata di login di Gnome (GDM) si può usare xorg.conf.
Si crea perciò un file:

`# nano /etc/X11/xorg.conf.d/10_tapping-gdm.conf`

e all'interno si inserisce:

`Section "InputClass"`
`      Identifier "tap-by-default"`
`      MatchIsTouchpad "on"`
`      Option "TapButton1" "1"`
`EndSection`

Fatto questo, al prossimo riavvio il tapping sarà attivo anche al login.

KDE
---

Per KDE si può gestire il touchpad, similmente a Gnome, dal pannello di controllo generale.

`$ systemsettings`

Una volta aperto navigare in **Dispositivi di immissione** nella sezione *Hardware*, quindi "Touchpad" ed infine nella scheda *Tapping*.
Fatto questo bisogna assicurarsi che la spunta *Enable tapping* sia selezionata e scegliere a cosa far corrispondere il tapping attraverso le associazioni

<div class="center" style="width: auto; margin-left: auto; margin-right: auto;">
**Tapping** ***\[nr. di volte\]*** **significa** ***\[azione\]***

</div>
XFCE
----

XFCE, dalla versione 4.10, e quindi da fedora 18, ha un proprio gestore del touchpad, molto simile a Gnome.
![Impostazioni touchpad nel pannello di controllo di Xfce.](XFCE_settings-mouse.png "fig:Impostazioni touchpad nel pannello di controllo di Xfce.")
Per le versioni precedenti di Xfce bisogna andare a modificare un file, come nel passaggio illustrato sotto.

Altri DE (LXDE, Mate, Openbox, ecc)
-----------------------------------

Si necessita del pacchetto contenente i driver per il dispositivo Synaptics, che generalmente è già installato. In ogni caso si può installare con:

`# yum install xorg-x11-drv-synaptics`

Si copia un file dal pacchetto appena installato:

`# cp /usr/share/X11/xorg.conf.d/50-synaptics.conf /etc/X11/xorg.conf.d/50-synaptics.conf`

ed infine lo si apre con un editor di testo, ad esempio nano:

`# nano /etc/X11/xorg.conf.d/50-synaptics.conf`

Il contenuto deve coincidere con il testo sottostante:

    Section  "InputClass"
    Identifier  "touchpad catchall"
    Driver  "synaptics"
    MatchIsTouchpad  "on"

    ####################################
    ## The lines that you need to add ##
    # Enable left mouse button by tapping
    Option  "TapButton1"  "1"
    # Enable vertical scrolling
    Option  "VertEdgeScroll"  "1"
    # Enable right mouse button by tapping lower right corner
    Option "RBCornerButton" "3"
    ####################################

    MatchDevicePath  "/dev/input/event*"
    EndSection

Per maggiori informazioni su come modificare i file delle impostazioni di xorg, consultare la relativa pagina di manuale:

`man xorg.conf`

Riferimenti
-----------

-   [Guida ufficiale](https://fedoraproject.org/wiki/How_to_enable_touchpad_click) del fedoraproject.org relativa al touchpad;
-   Pagina relativa all'[estensione per Gnome-Shell](https://extensions.gnome.org/extension/131/touchpad-indicator/);
-   [Articolo](http://www.lffl.org/2012/01/gnome-shell-attivare-o-disattivare-il.html) sull'estensione per Gnome-Shell;
-   [Discussione](http://forum.fedoraonline.it/viewtopic.php?pid=210752#p210752) sul forum di fedoraonline su come attivare il touchpad su KDE;
-   [Guida ufficiale](https://fedoraproject.org/wiki/Input_device_configuration#Example:_Tap-to-click) del fedoraproject.org ai dispositivi di input, con esempio di come attivare il tapping alla schermata di gdm.

<Categoria:Hardware> <Categoria:Ambiente_Desktop>
