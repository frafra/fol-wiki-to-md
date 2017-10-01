Come installare un Web Server
-----------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")

yum install httpd mod\_ssl httpd-manual mod\_perl mod\_auth\_mysql crypto-utils mod\_python

`/etc/init.d/httpd start`

<li>
<http://localhost>

</li>
</ol>
Come installare il supporto a PHP in un Web Server
--------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare un Web Server](#Come_installare_un_Web_Server "wikilink")

yum -y install php

`yum -y install php-mysql`

`/etc/init.d/httpd restart`
`gedit /var/www/html/testphp.php`

<li>
Inserisci la riga seguente nel file

</li>
`<?php phpinfo(); ?>`

<li>
Salva il file modificato

</li>
<li>
<http://localhost/testphp.php>

</li>
</ol>
Come installare MYSQL
---------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare un Web Server](#Come_installare_un_Web_Server "wikilink")
4.  Leggi [Come installare il supporto a PHP in un Web Server](#Come_installare_il_supporto_a_PHP_in_un_Web_Server "wikilink")
5.  Leggi [Come installare MYSQL Database Server](#Come_installare_MYSQL_Database_Server "wikilink")

/etc/init.d/httpd restart

</ol>
Come fare in modo che URLs raggiungano directory al di fuori di /var/www/
-------------------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare un Web Server](#Come_installare_un_Web_Server "wikilink")

gedit /etc/httpd/conf.d/alias

<li>
Inserisci le seguenti righe nel file

</li>
`Alias /URL-path /location_of_directory/`

`<Directory /location_of_directory/>`
`  Options Indexes FollowSymLinks`
`  AllowOverride All`
`  Order allow,deny`
`  Allow from all`
`</Directory>`

<li>
Salva il file modificato

</li>
`/etc/init.d/httpd restart`

<li>
<http://localhost/URL-path>

</li>
</ol>
Come cambiare il numero di porta di default in Apache HTTP Server
-----------------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come installare un Web Server](#Come_installare_un_Web_Server "wikilink")

<i>Assumiamo che il nuovo numero di porta sia il 78</i>

`cp /etc/httpd/ports.conf /etc/httpd/ports.conf_backup`
`gedit /etc/httpd/ports.conf`

<li>
Trova questa riga

</li>
`Listen 80`

<li>
Sostituiscila con la seguente

</li>
`Listen 78`

<li>
Salva il file modificato

</li>
`/etc/init.d/httpd restart`

<li>
<http://localhost:78>

</li>
</ol>
<Categoria:Fedoraserver>
