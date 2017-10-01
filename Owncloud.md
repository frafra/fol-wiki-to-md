Introduzione
------------

Owncloud è un software per la creazione di un sistema cloud personale.
Di seguito, la guida per l'installazione del software lato server su Fedora.

Installazione
-------------

Per installare il software, basta semplicemente uno:

`# dnf install owncloud`

### Configurazione certificato SSL

affinché le comunicazioni tra host e server siano crittografate, occorre generare una chiave ed un certificato

`# dnf install crypto-utils`

`# genkey `*`hostname`*

Rispondere no alla domanda "Would you like to send a Certificate Request (CSR) to a Certificate Authority (CA)?"

Affinché il servizio httpd possa utilizzare SSL, vanno installate le dovute dipendenze

`# dnf install mod_ssl openssl`

ed apportate le seguenti modifiche a

`/etc/httpd/conf.d/ssl.conf`

mettendo in fondo

`SSLCertificateFile /etc/pki/tls/certs/hostname.crt`
`SSLCertificateKeyFile /etc/pki/tls/private/hostname.key`

Per forzare l'utilizzo di SSL nel server Owncloud: [seguire la guida Owncloud](https://doc.owncloud.org/server/8.1/admin_manual/configuration_server/harden_server.html#redirect-all-unencrypted-traffic-to-https)

### Installazione MariaDB/MySQL

`# dnf install mariadb-server`
`# systemctl enable --now mariadb`
`$ mysql_secure_installation`

quando vi verrà chiesta la password di root premere invio senza scrivere alcunché. Alla richiesta di creare un utente root dire di sì ed immettere una password. Ora va creato un utente ed il database per l'utilizzo con owncloud

`$ mysql -u root -p`
`CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';`
`CREATE DATABASE IF NOT EXISTS owncloud;`
`GRANT ALL PRIVILEGES ON owncloud.* TO 'username'@'localhost' IDENTIFIED BY 'password';`
`FLUSH PRIVILEGES;`
`quit`

avendo cura di rimpiazzare username con un nome utente adatto. Un buon candidato potrebbe essere owncloud\_user. Non dimenticare di inserire i dati tra simboli '' In caso di password che contengono simboli, fare attenzione a non inserire caratteri che possano venir interpretati come escape chars (tipo /&gt;). In tal caso la procedura sembrerà andare a buon fine, salvo poi ricevere errori di autenticazione al DB da parte di Owncloud server.

Inizializzazione Owncloud server
--------------------------------

Per creare l'account amministratore di Owncloud inserire nel browser (ignorando i warning circa il certificato di sicurezza non firmato da terze parti)

`localhost/owncloud`

In caso di problemi di accesso riavviare il servizio Apache e tentare nuovamente

`# systemctl restart httpd`

Nella schermata di creazione dell'utente amministratore, c'è la possibilità di scegliere il motore database: SQLite, MariaDB/MySQL. Selezionare quest'ultimo.

### Configurazione del firewall

`# firewall-cmd --list-all-zones | grep active`

nel nostro caso

`public (default, active)`

quindi utilizzeremo la zona public e i seguenti comandi per abilitare l'accesso al servizio http e https

`# firewall-cmd --permanent --zone=public --add-service=http`
`# firewall-cmd --permanent --zone=public --add-service=https`
`# firewall-cmd --reload`

### Garantire l'accesso ad host remoti

Infine affinché Owncloud possa essere raggiunto anche da host remoti occorre modificare il file

`# /etc/owncloud/config.php`

aggiungendo l'indirizzo IP del server nella sezione 'trusted\_domains'

Bibliografia
------------

-   [Fedora Deployment\_Guide: Setting Up an SSL Server](http://docs.fedoraproject.org/en-US/Fedora/15/html/Deployment_Guide/ch-Web_Servers.html#s2-apache-mod_ssl)
-   [Fedora Wiki: Setup Owncloud](https://fedoraproject.org/wiki/OwnCloud#Setup_owncloud)

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink")
