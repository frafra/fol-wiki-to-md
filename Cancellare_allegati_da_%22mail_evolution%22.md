Introduzione
------------

Se come me siete affezionati al client di posta "evolution" avrete senz'altro notato che non esiste l'opzione per cancellare gli allegati dalle email inviate e/o ricevute... Ecco un trucchetto per ovviare all'inconveniente....

Procedura
---------

1.  Se non presente nel sistema installare Thunderbird;
2.  Una volta installato è necessario aprirlo per la prima volta, senza inserire alcun account pop, per poi chiuderlo;
3.  Cercare nella propria home la directory contenente i file di Thunderbird (sostituendo "zod" con il proprio nome utente)
    Dopodiché:
         $ find ~zod/ -name Inbox | grep .thunderbird

    Si otterrà un esito piu' o meno cosi':

        /home/zod/.thunderbird/fas0ocpz.default/Mail/Local Folders/Inbox

4.  A questo punto eliminare sia il file *Inbox* (mail ricevute) che *Outbox* (mail inviate)... Nel caso di questa guida:
        rm -rf "/home/zod/.thunderbird/fas0ocpz.default/Mail/Local Folders/Inbox" "/home/zod/.thunderbird/fas0ocpz.default/Mail/Local Folders/Sent"

5.  Creare i link da *evolution* a *thunderbird*...
    Nel caso specifico:
        ln -s "/home/zod/.evolution/mail/local/Sent" "/home/zod/.thunderbird/fas0ocpz.default/Mail/Local Folders/Sent" 
        ln -s "/home/zod/.evolution/mail/local/Inbox" "/home/zod/.thunderbird/fas0ocpz.default/Mail/Local Folders/Inbox"

    Facendo cosi' i mailbox (inbox e sent) di evolution saranno visibili a thunderbird, come link.

6.  Quando si desidererà cancellare qualche allegato sara' sufficiente chiudere evolution, aprire thunderbird, utilizzare il suo menu' di eliminazione allegati, selezionare la voce "compatta questa cartella" e quindi ri-chiudere thunderbird e tornare in mail evolution.

<Categoria:Internet>
