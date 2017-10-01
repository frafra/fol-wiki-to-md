Con Linux è possibile creare un tunnel SSH tra due sistemi in modo che si apra un canale criptato via SSH facendo comunicare due porte differenti tra loro.
Ad esempio se si ha un server di destinazione con un webserver che risponde alla porta 80, ma dal proprio pc non si riesce a raggiungerlo, con il tunnel SSH, si può far passare tutto il traffico verso la porta 80, su una porta a propria scelta di localhost. Per l'implementazione il comando è:

`ssh -L `<portalocale>`:localhost:`<portaremota>` `<utente>`@`<hostremoto>

In questo esempio ci si collega all'host sulla porta 8888 passando sulla porta 9000 locale.

`[cello@cellopc-mini ~]$ ssh -L 9000:localhost:8888 root@cw-stto-mgm01-admin`

Verificando le connessioni attive si nota che viene aperta una connessione ssh verso l'host e poi aperta la porta locale per ricevere le richieste da inoltrare al server remoto.

`[cello@cellopc-mini ~]$ ps -ef | ssh`
`cello     6762  6255  0 14:55 pts/3    00:00:00 ssh -L 9000:localhost:8888 root@cw-stto-mgm01-admin`
`[cello@cellopc-mini ~]$ netstat -antp | grep 6762`
`(Not all processes could be identified, non-owned process info`
`will not be shown, you would have to be root to see it all.)`
`tcp        0      0 127.0.0.1:9000              0.0.0.0:*                   LISTEN      6762/ssh            `
`tcp        0      0 172.29.7.93:40133           10.175.18.213:22            ESTABLISHED 6762/ssh            `
`tcp        0      0 ::1:9000                    :::*                        LISTEN      6762/ssh`

Ora provando a fare una richiesta sulla porta 9000 tramite firefox o wget potremmo navigare il webserver sul nostro pc locale.

`[cello@cellopc-mini ~]$ wget localhost:9000/admin/`
`--2010-10-23 15:00:54--  http://localhost:9000/admin/`

`Resolving localhost... 127.0.0.1`
`Connecting to localhost|127.0.0.1|:9000... connected.`
`HTTP request sent, awaiting response... 200 OK`
`Length: 7690 (7.5K) [text/html]`
`Saving to: “index.html”`

`100%[================================================================>] 7,690       --.-K/s   in 0s      `

`2010-10-23 15:00:54 (106 MB/s) - “index.html” saved [7690/7690]`

Si potranno fare anche più connessioni simultanee verso lo stesso host, sfruttando porte differenti.

`[cello@cellopc-mini ~]$ ssh -L 9000:localhost:8888 root@cw-stto-mgm01-admin`
`[cello@cellopc-mini ~]$ ssh -L 9001:localhost:8080 root@cw-stto-mgm01-admin`

`` [cello@cellopc-mini ~]$ for i in `ps -ef | grep "ssh -L" | grep -v grep | awk '{print $2}' ``
`` ` ; do netstat -antp | grep $i ; done ``
`(Not all processes could be identified, non-owned process info`
` will not be shown, you would have to be root to see it all.)`
`tcp        0      0 127.0.0.1:9000              0.0.0.0:*                   LISTEN      6762/ssh            `
`tcp        0      0 172.29.7.93:40133           10.175.18.213:22            ESTABLISHED 6762/ssh            `
`tcp        0      0 ::1:9000                    :::*                        LISTEN      6762/ssh            `
`(Not all processes could be identified, non-owned process info`
`will not be shown, you would have to be root to see it all.)`
`tcp        0      0 127.0.0.1:9001              0.0.0.0:*                   LISTEN      6799/ssh            `
`tcp        0      0 172.29.7.93:57619           10.175.18.213:22            ESTABLISHED 6799/ssh            `
`tcp        0      0 ::1:9001                    :::*                        LISTEN      6799/ssh`

<Categoria:Rete_e_Server> <Categoria:Sicurezza>
