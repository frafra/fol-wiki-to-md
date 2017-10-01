Con questa guida si vuole spiegare come installare e configurare vnc (Virtual Network Computing).
 Per prima cosa installare i pacchetti relativi a vnc. Su tutte le versioni di Fedora verificare i pacchetti relativi a vnc con questo comando:

`# dnf search vnc`
`tigervnc.i586 : A TigerVNC remote display system`
`tigervnc-server.i586 : A TigerVNC server`

Sopra sono elencati i pacchetti che serviranno, quindi, per installare:

`# dnf install tigervnc*`

Una volta terminata l'installazione, procedere a configurare il server vnc. Il consiglio è di non utilizzare l'utenza root per connettersi tramite vnc in quanto esso non ha connessione criptata e l'utenza root dovrebbe essere utilizzata solo in caso di estrema necessità, quindi, impostare la password per vnc:

`$ vncpasswd`
`Password: 123456`
`Verify: 123456`

Ovviamente sostituire 123456 con la password preferita.
Successivamente modificare il file, con l'editor preferito (nano, gedit, vim o altro):

`# nano /etc/sysconfig/vncservers`

Inserire i seguenti campi, alla fine del file di configurazione:

`VNCSERVERS="1:palir1927"`

`VNCSERVERARGS[1]="-geometry 1024x768"`

Avviare il servizio di vnc server:

`# service vncserver start`

Modificare il file .vnc/xstartup (si trova nella dir /home/utenza/.vnc/xstartup):

`# nano /home/palir1927/.vnc/xstartup`

sostituire **twm &** --&gt; con --&gt; '''gnome-session & '''

Dare per sicurezza:

`# service vncserver restart`

A questo punto la configurazione è terminata e ci si può collegare tramite un client vnc da qualsiasi OS al proprio Fedora 11, avviare il client su F11, che si può trovare in:
*'Applicazioni --&gt; Internet --&gt; TigerVNC Viewer **(questo per quanto riguarda gnome)
Quindi digitare:
**ip:5901*' (ad esempio 192.168.0.1:5901 dove 192.168.0.1 è l'ip della propria Fedora 11 dove si è configurato vnc e 5901 è la porta di default utilizzata da vncserver)
**password**
Ora dovrebbe essere tutto ok, e si dovrebbe essere in grado di connettersi tramite vnc.

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink")
