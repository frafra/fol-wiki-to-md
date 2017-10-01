Come installare MYSQL Database Server
-------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Usa Desktop -&gt; Impostazioni di Sistema -&gt; Aggiungere/Rimuovere Applicazioni

*oppure*

`yum -y install mysql`
`yum -y install mysql-server`
`yum -y install php-mysql`
`yum -y install MySQL-python`
`yum -y install libdbi-dbd-mysql`
`yum -y install mysql-devel`
`mysqladmin -u root password new_db_user_password`
`/etc/init.d/mysqld start`

</ol>
Come installare MYSQL Control Center
------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Leggi [Come aggiungere dei repositories extra](02_Repositories#Come_aggiungere_dei_repositories_extra "wikilink")
3.  Leggi [Come installare MYSQL Database Server](#Come_installare_MYSQL_Database_Server "wikilink")

yum -y install mysql-administrator

<li>
Applicazioni -&gt; Strumenti di Sistema -&gt; MySQL Administrator

</li>
</ol>
<Categoria:Fedoraserver>
