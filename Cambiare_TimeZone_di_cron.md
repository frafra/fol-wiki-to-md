\_\_TOC\_\_

Introduzione
------------

Cron è una utility che consente di eseguire comandi ad intervalli regolari per mezzo del demone crond.
Inoltre consente di specificare nel file ***/etc/crontab*** i comandi da eseguire e la data/ora (oppure l'intervallo di tempo) in cui andranno eseguiti. Nello specificare l'ora di esecuzione potrebbe essere utile voler specificare una *TimeZone* diversa da quella dell'orologio di sistema.
Per esempio, avendo un orologio di sistema impostato sulla zona Europe/Rome si potrebbe comunque volere che il demone crond interpreti gli orari specificati nel file /etc/crontab come orari UTC.

Impostazione e utilizzo
-----------------------

Per ottenere quanto descritto nell'esempio sopra occorre modificare nel file ***/etc/rc.d/init.d/crond*** la riga:

`daemon $prog $CRONDARGS && success || failure`

facendola diventare così:

`daemon TZ=UTC $prog $CRONDARGS && success || failure`

dove TZ=UTC specifica al demone cron a quale TimeZone fare riferimento. Nell'esempio si utilizza UTC, ma in generale le varie TimeZone sono contenute nella cartella ***/usr/share/zoneinfo***.
Dopo aver effettuato le modifiche, è necessario riavviare il demone crond, da root:

`# service crond restart`

Ora gli orari specificati nel file crontab saranno interpretati secondo la nuova TimeZone.

<Categoria:Sistema>
