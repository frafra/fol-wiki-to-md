Introduzione
------------

Compiz è un compositing window manager per X Window System. Si tratta in sostanza di un software che gestisce sia l'estetica e il piazzamento delle finestre delle applicazioni, sia una serie di effetti che possono essere applicati a tali finestre.

Installazione
-------------

Per cominciare bisogna installare e attivare gli [RPMFusion](RPMFusion "wikilink") *free* e *non free*, dopodichè si apre la shell e si digita “da root”:

### Per Gnome:

`# yum install gnome-compiz* fusion*`

### Per KDE:

`# yum install compiz* emerald* fusion* `

Al termine dell'installazione è consigliato svuotare la cache di Yum:

`# yum clean all `

e riavviare il sistema:

`# reboot`

Configurazione
--------------

Per attivare i plugin unsupported di compiz, bisogna installare *Fedora Fusion* reperibili al link:
<http://www.dfm.uninsubria.it/compiz/fusion/>

Il pacchetto *Fedora Fusion* è:

`# compiz-fusion-release `

Fatto ciò si elimina Compiz-fusion (relativo agli rpm-fusion) con:

`# yum erase compiz-fusion `

e si reinstalla tutto da capo dando da schell:

`# yum install gnome-compiz* fusion* `

Ora si scarica dal link sopra citato il pacchetto ***unsupported*** & altri di vostro interesse come screensaver peek, ecc. Per rendere attivo compiz al riavvio del sistema basta aggiungere a *Sistema &gt; Preferenze &gt; Applicazioni d'avvio*:

`fusion-icon`

[Categoria:Ambiente Desktop](Categoria:Ambiente_Desktop "wikilink")
