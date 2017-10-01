Per chi avesse installato alcuni giochi che necessitano del pacchetto in oggetto, in questi ultimi giorni avrà sicuramente notato che yum propone una versione aggiornata di SDL\_gfx dal repo dries. In realtà queste librerie dovrebbero venire aggiornate dai repo di Fedora, in quanto appartengono al core di Fedora. Visto che con il passare dei giorni la situazione non si è normalizzata e stanco di dover fare:

`# yum --exclude=SDL_gfx update`

si è pensato di risolvere il problema sbloccando l'update (se lo si faceva da yum entravano in conflitto le librerie delle due versioni).

`# rpm -e --nodeps SDL_gfx.i386`
`# yum install SDL_gfx`

A questo punto la situazione si è invertita, si è passati da (situazione originaria):

`# yum list availble SDL_gfx`
`...............................`
`Installed Packages`
`SDL_gfx.i386                             2.0.13-7.fc6           installed`
`Available Packages`
`SDL_gfx.i386                             2.0.15-1.fc6.rf        dries`

a (situazione finale):

`# yum list availble SDL_gfx`
`...............................`
`Installed Packages`
`SDL_gfx.i386                             2.0.15-1.fc6.rf        dries`

La soluzione proposta, forse, è un po' brutale ma è efficace.

A questo punto, finalmente, si può fare il più comodo *yum update*.

<Categoria:Giochi> <Categoria:Sistema>
