\_\_TOC\_\_

Introduzione
------------

Fedora-Chromium-Stable fa parte dei repository di **terze parti**.
L'installazione è necessaria se si sceglie di utilizzare il browser open source Chromium.

Installazione
-------------

Si crea un file */etc/yum.repos.d/fedora-chromium-stable.repo* digitando da root:

`# nano /etc/yum.repos.d/fedora-chromium-stable.repo`

e inserendo le seguenti righe:

`[fedora-chromium-stable]`
`name=Builds of the "stable" tag of the Chromium Web Browser`
`baseurl=`[`http://repos.fedorapeople.org/repos/spot/chromium-stable/fedora-$releasever/$basearch/`](http://repos.fedorapeople.org/repos/spot/chromium-stable/fedora-$releasever/$basearch/)
`enabled=0`
`skip_if_unavailable=1`
`gpgcheck=0`
`[fedora-chromium-stable-source]`
`name=Builds of the "stable" tag of the Chromium Web Browser - Source`
`baseurl=`[`http://repos.fedorapeople.org/repos/spot/chromium-stable/fedora-$releasever/SRPMS`](http://repos.fedorapeople.org/repos/spot/chromium-stable/fedora-$releasever/SRPMS)
`enabled=0`
`skip_if_unavailable=1`
`gpgcheck=0`

Salvare e chiudere.
Si può evitare questo passaggio recuperando il file direttamente dal repo, così:

`# yum-config-manager --add-repo=`[`http://repos.fedorapeople.org/repos/spot/chromium-stable/fedora-chromium-stable.repo`](http://repos.fedorapeople.org/repos/spot/chromium-stable/fedora-chromium-stable.repo)

Il repo è così pronto per l'uso, ma bisogna abilitarlo singolarmente ad ogni operazione con l'opzione *--enablerepo=fedora-chromium-stable* se si vuole installare/aggiornare un pacchetto da esso.

Installazione Chromium
----------------------

Per installare il browser di casa google attenersi alla relativa [documentazione](Chromium "wikilink").

Riferimenti
-----------

-   <http://fedoraproject.org/wiki/Chromium>

<Categoria:Repository>
