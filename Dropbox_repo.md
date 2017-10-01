\_\_TOC\_\_

Introduzione
------------

[Dropbox](https://www.dropbox.com/) è un servizio di file-hosting multipiattaforma che rende disponibile un proprio repository per Fedora. L'installazione è necessaria per installare il pacchetto **nautilus-dropbox**, che permette la gestione dei dati del proprio account direttamente da Nautilus. Il repo è disponibile per tutti le versioni di Fedora dalla 10 in poi.

Installazione
-------------

Si va a modificare il file *dropbox.repo* nella cartella /etc/yum.repos.d/ da root:

`# nano /etc/yum.repos.d/dropbox.repo`

con queste righe:

`[Dropbox]`
`name=Dropbox Repository`
`enabled=0`
`baseurl=`[`http://linux.dropbox.com/fedora/$releasever/`](http://linux.dropbox.com/fedora/$releasever/)
`gpgkey=`[`http://linux.dropbox.com/fedora/rpm-public-key.asc`](http://linux.dropbox.com/fedora/rpm-public-key.asc)

Il repository è ora configurato, essendo però un repository di terze parti è mantenuto disabilitato. Per installare o aggiornare nautilus-dropbox bisogna quindi attivare singolarmente il repository. Ad esempio:

`yum install --enablerepo=Dropbox nautilus-dropbox`

Bisognerà poi aprire Dropbox (Applicazioni &gt;&gt; Internet &gt;&gt; Dropbox) e seguire la guida iniziale per la gestione del proprio account.

<Categoria:Repository> <Categoria:Yum>
