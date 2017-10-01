LAMP - Installazione di un Web-Server
-------------------------------------

LAMP e' un acronimo che indica la piu' famosa piattaforma per lo sviluppo di applicazioni web e che prende il nome dalle iniziali dei componenti software con cui e' realizzata, ovvero: (**L**inux, **A**pache, **M**ySQL, **P**HP).

### Installazione del server Mysql

`# dnf install mysql mysql-server`

### Installazione del server Apache e di Php

`# dnf install httpd php php-common`

### Supporti

Per far sì che il server Apache funzioni anche per i supporti più comuni, installare i seguenti pacchetti:

`# dnf install php-pear php-pdo php-mysql php-pgsql php-pecl-memcache php-gd php-mbstring php-mcrypt php-xml`

### Il web server Apache

A questo punto l'ambiente LAMP e' pronto per l'uso. La cartella */var/www/html* e' la location di default, detta anche "root document path", per i propri file web.
Con un piccolo script in Php si può facilmente verificare la versione e i supporti installati. A questo scopo si crea un file di test:

`# gedit /var/www/html/test.php`

all'interno del quale si inserisce:

<?php
     phpinfo();
 ?>
E' il momento di lanciare il server Apache:

`# systemctl start httpd.service`

Si potrà subito verificare se il server funziona correttamente, inserendo il seguente indirizzo nella barra degli indirizzi del proprio browser:
<http://localhost/test.php>

### Abilitare le user directory

In alcuni casi, come nei sistemi multiutente, c'è la possibilità di avere il sito web nella propria home usando la direttiva *UserDir*. In questo caso il sito sarà accessibile da <http://localhost/~username/>. Di seguito sono indicati i passaggi per abitare le user directory.

-   Modificare il file /etc/httpd/conf.d/userdir.conf in modo che la parte riguardante il modulo userdir sia configurata in questo modo:

<IfModule mod_userdir.c>
`    #`
`    # UserDir is disabled by default since it can confirm the presence`
`    # of a username on the system (depending on home directory`
`    # permissions).`
`    #`
`    #UserDir disabled`
`    #`
`    # To enable requests to /~user/ to serve the user's public_html`
`    # directory, remove the "UserDir disabled" line above, and uncomment`
`    # the following line instead:`
`    # `
`    UserDir public_html`
</IfModule>

-   Per poter garantire che il web server possa accedere correttamente alla propria user directory bisogna settare correttamente i permessi:

`$ chmod a+x $HOME`
`$ chmod a+rx $HOME/public_html`

-   SELinux

`# setsebool -P httpd_enable_homedirs 1`
`# chcon -R -t httpd_sys_content_t ~user/public_html`

### Mysql

Come per Apache è necessario avviare il server Mysql:

` # systemctl start mysqld.service`

Per una facile gestione dei database MySQL si può utilizzare una semplice interfaccia web, phpmyadmin:

`# dnf install phpmyadmin`

Per poter utilizzare questo tool è necessario impostare una password per l'amministratore dei database Mysql (root).

`# mysqladmin -u root password TUA_PASSWORD`

Al posto di TUA\_PASSWORD inserire una parola chiave a scelta.
Ora si può utilizzare phpmyadmin, digitando nella barra degli indirizzi del browser l'indirizzo:
<http://localhost/phpmyadmin>

Per accedere si dovrà inserire l'utente (=root) e la password scelta un attimo fa.
Infine, se tutto funziona, si può fare in modo che i servizi *httpd* e *mysqld* vengano avviati in automatico ad ogni avvio della macchina:

`# systemctl enable httpd.service`
`# systemctl enable mysqld.service`

<Categoria:Rete_e_Server>
