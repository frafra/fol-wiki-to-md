### Prefazione

Network Time Protocol è un protocollo per sincronizzare gli orologi dei computer all'interno di una rete. L'NTP è un protocollo client-server appartenente al livello applicativo ed è in ascolto sulla porta UDP 123.

### Installazione

Per installare il pacchetto ntp da consolle digitare

`  # dnf install ntp`

### Configurazione

Terminata l'installazione dovremmo andare ad editare il file /etc/ntp.conf il quale contiene tutte le direttive circa i server ai quali vogliamo collegarci per reperire l'orario corretto e le informazioni su quali reti il server stesso deve servire.

La prima cosa che andremo ad editare è la direttiva che descrive su quali sottoreti il demone restituirà il timestamp, andiamo quindi ad editare il file di configurazione con:

`  # vi /etc/ntp.conf`

e andiamo a togliere il segno di commento ("\#") dalla riga

`  #restrict 192.168.1.0 mask 255.255.255.0 nomodify notrap`

andandola a modificare in base alle vostre esigenze.

Se, ad esempio, la vostra rete locale sulla quale volete erogare il servizio è 192.168.35.0/24 allora dovrete modificare la direttiva sopra citata in:

`  restrict 192.168.35.0 mask 255.255.255.0 nomodify notrap`

In alternativa, se avete più reti da voler servire, allora aggiungerete altre direttive così:

`  restrict 192.168.35.0 mask 255.255.255.0 nomodify notrap`
`  restrict 192.168.8.0 mask 255.255.255.0 nomodify notrap`
`  restrict 172.21.0.0 mask 255.255.0.0 nomodify notrap`

**NOTA TECNICA**

**nomodify:** direttiva che impedisce ai client della sottorete specificata di modificare il timestamp sul server.

**notrap:** Inibisce il servizio di "message trap" (sottosistema del ntpdq utilizzato solo per il logging remoto degli eventi)

Sempre all'interno dello stesso file di configurazione possiamo vedere la sezione riguardante i server pubblici ai quali il nostro sistema si collegerà per reperire lui stesso in prima battuta il timestamp corrente.

`  server 0.centos.pool.ntp.org iburst`
`  server 1.centos.pool.ntp.org iburst`
`  server 2.centos.pool.ntp.org iburst`
`  server 3.centos.pool.ntp.org iburst`

Possiamo lasciare questa sezione invariata oppure andarla a modificare in base alle nostre esigenze, andando ad aggiungere o togliere server seguendo la stessa sintassi:

`  server `<indirizzo_ip_o_fqdn>` iburst`

**NOTA TECNICA**

L'opzione *iburst* invia una serie di pacchetti (burst) solo se non riesce ad ottenere una connessione al primo tentativo. Questa opzione è altamente consigliata

Terminata la configurazione, abilitiamo il firewall ad accettare connessioni sulla porta 123 del protocollo UDP. Da consolle quindi digitiamo:

`  # firewall-cmd --permanent --add-port=123/udp `
`  # firewall-cmd --reload`

[:Rete\_e\_Server](:Rete_e_Server "wikilink")
