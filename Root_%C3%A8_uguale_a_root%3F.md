Diventare root spesso non ci da tutti i permessi, perchè? Dipende dai diritti e dalla path che usiamo.
Loggarsi come root da terminale permette di eseguire le varie operazioni di amministrazione, installazione o configurazione del proprio sistema. Guardando meglio, però, root non è uguale a root... ovvero, digitando il seguente comando nel terminale:

`$ su`
`password`
`[root@localhost utente]#`

Si è loggati come root (\#), ma quello che non si vede è che si è mantenuto il path di accesso del proprio user per i comandi bash. Questo path viene indicato in /root/.bash-profile e tiene conto della directory in cui ci si logga quando si diventa root.
Provare a dare un comando:

`# ifconfig`
`bash: ifconfig: command not found`

Non trova il comando, ma noi sappiamo che esiste e possiamo anche cercarlo:

`# whereis ifconfig`
`ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz`
`# /sbin/ifconfig`
`eth0      Link encap:Ethernet  HWaddr 00:0D:61:08:0C:1A`
`          inet addr:192.168.0.22  Bcast:192.168.0.255  Mask:255.255.255.0`
`          inet6 addr: fe80::20d:61ff:fe08:c1a/64 Scope:Link`
`          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1`
`          RX packets:7591 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:7130 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:1000`
`          RX bytes:7220234 (6.8 MiB)  TX bytes:886635 (865.8 KiB)`
`          Interrupt:11 Base address:0xe800`
`lo        Link encap:Local Loopback`
`          inet addr:127.0.0.1  Mask:255.0.0.0`
`          inet6 addr: ::1/128 Scope:Host`
`          UP LOOPBACK RUNNING  MTU:16436  Metric:1`
`          RX packets:2085 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:2085 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:0`
`          RX bytes:2443680 (2.3 MiB)  TX bytes:2443680 (2.3 MiB)`

Quindi per poter utilizzare il proprio comando bash bisogna indicare anche il percorso in cui ci si trova, ma solo perché non ci si trova nella path "giusta" di root.
Per ovviare a questo inconveniente basta cambiare leggermente il comando per diventare root (superuser), da utente digitare:

`$ su -`
`password`
`[root@localhost ~]#`

Ora si è root, e oltretutto nella sua directory dove si hanno tutti i permessi senza dover digitare il path completo, provare:

`# ifconfig`
`eth0      Link encap:Ethernet  HWaddr 00:0D:61:08:0C:1A`
`          inet addr:192.168.0.22  Bcast:192.168.0.255  Mask:255.255.255.0`
`          inet6 addr: fe80::20d:61ff:fe08:c1a/64 Scope:Link`
`          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1`
`          RX packets:7631 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:7155 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:1000`
`          RX bytes:7224168 (6.8 MiB)  TX bytes:888523 (867.6 KiB)`
`          Interrupt:11 Base address:0xe800`
`lo        Link encap:Local Loopback`
`          inet addr:127.0.0.1  Mask:255.0.0.0`
`          inet6 addr: ::1/128 Scope:Host`
`          UP LOOPBACK RUNNING  MTU:16436  Metric:1`
`          RX packets:2085 errors:0 dropped:0 overruns:0 frame:0`
`          TX packets:2085 errors:0 dropped:0 overruns:0 carrier:0`
`          collisions:0 txqueuelen:0`
`          RX bytes:2443680 (2.3 MiB)  TX bytes:2443680 (2.3 MiB)`

Una sottile differenza con un effetto molto diverso.

<Categoria:Sistema>
