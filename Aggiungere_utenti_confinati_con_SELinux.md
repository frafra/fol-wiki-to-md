Introduzione
------------

Nei sistemi Fedora è possibile creare un certo numero di utenti definiti "confinati", cioé sottoposti a delle restrizioni dettate dalle security policy di SELinux: certi utenti non possono avviare X Window System, altri non hanno accesso alla rete, ad altri non è permesso acquisire i permessi di root.

Interrogazione
--------------

Gli utenti appena descritti sono mappati dal sistema e visualizzabili dal seguente comando:

`# /usr/sbin/semanage login -l`
`Login Name                SELinux User              MLS/MCS Range            `
`__default__               unconfined_u              s0-s0:c0.c1023           `
`root                      unconfined_u              s0-s0:c0.c1023           `
`system_u                  system_u                  s0-s0:c0.c1023`

Creazione utente confinato
--------------------------

Ogni *confined user* ha delle restrizioni :

1.  Gli **user guest\_u, xguest\_u, user\_u** nei rispettivi domini non possono diventare root, ne tramite il comando *su* ne tramite *sudo*. Possono avviare applicazioni nei limiti imposti da SELinux (ad esempio *passwd*);
2.  Gli **staff\_u** possono acquisire permessi (non di root) solo con il comando sudo, definito a sua volta dall'amministratore;
3.  Gli **guest\_u** non hanno accesso ad internet, possono comunicare solo tramite ssh e non con sistemi esterni;
4.  Gli **xguest\_u** hanno accesso alla rete solo tramite Firefox;
5.  Di default, gli utenti nei domini **guest\_t e xguest\_t** non possono avviare programmi dalla loro home directory o /tmp/. Quelli nei domini **user\_t e staff\_t** lo possono fare di default; tutti comunque sono settabili dall'amministratore.

Esempio
-------

Si vuole far usare Fedora alla sorellina poco pratica (user) sullo stesso pc che usa l'amministratore; si può creare un utente confinato nel dominio *xguest\_t* al quale è permesso avviare il sistema grafico, navigare solo con Firefox, mentre non gli è permesso avviare software dalla propria home directory (può usare solo il parco software installato dall'amministratore) e non gli è permesso acquisire i permessi di root in alcun modo.

Creazione utente confinato:

`# useradd sorellina`

Configurazione policy SELinux:

`# /usr/sbin/semanage login -a -s xguest_u sorellina`

Definizione della password:

`# passwd sorellina`

Verifica:

`# /usr/sbin/semanage login -l`
`Login Name                SELinux User              MLS/MCS Range            `
`__default__               unconfined_u              s0-s0:c0.c1023           `
`root                      unconfined_u              s0-s0:c0.c1023           `
`sorellina                 xguest_u                  s0                       `
`system_u                  system_u                  s0-s0:c0.c1023 `

<Categoria:Sicurezza>
