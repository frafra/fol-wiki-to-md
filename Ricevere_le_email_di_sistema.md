Come tutti ormai sanno, root è il superutente, l'account di sistema che ha pieni poteri sul sistema e che può decretarne vita, morte e miracoli. Tale account, tra le altre cose, è destinatario di una serie di email dal sistema stesso, che provvede ad informarlo di quanto accade in sua assenza.

Una di queste email (ma non è di certo l'unica) viene invata da *logwatch*, un programma che quotidianamente si preoccupa di analizzare i log di sistema e di fare un riepilogo di quanto accaduto.

Dato che l'utente root è un utente speciale ed è buona norma utilizzarlo solo quando serve, è pratica diffusa fare in modo che le email indirizzate a tale utente siano invece rigirate ad un utente normale, che si logga -a differenza di root- spesso nel sistema, in modo che quest'ultimo le possa leggere e comportarsi di conseguenza.

Essendo *sendmail* ad inviare le suddette email di sistema, per fare in modo che esse vengano re-indirizzate ad un altro utente (o ad altri utenti) è necessario modificare il file degli "alias" di sendmail, ovvero */etc/aliases*, inserendo quanto segue:

`root:           user_che_deve_ricevere_le_email_di_root`

dove, chiaramente, *user\_che\_deve\_ricevere\_le\_email\_di\_roo*t va sostituito con il nome di login dell'utente di sistema che diventerà il destinatario delle suddette email.
Fatto questo è necessario riavviare sendmail o, piu' semplicemente, fare in modo che lo stesso sappia che ci sono nuovi "aliases" nel sistema, dando questo comando:

`# newaliases`

Che fare adesso? Le email di root arriveranno quindi all'utente *user\_che\_deve\_ricevere\_le\_email\_di\_root* e, per la precisione, in */var//mail/user\_che\_deve\_ricevere\_le\_email\_di\_root*.
E' possibile fare in modo che il proprio programma di posta (ad esempio mail evolution le scarichi assieme ai vari account "pop" già configurati. La configurazione è abbastanza banale:

1.  In evolution andare nel menu' **modifica / preferenze**;
2.  Cliccare su **aggiungi** e quindi su **avanti**;
3.  Nella finestra *identità* indicare il vostro nome completo e l'indirizzo **email (user\_che\_deve\_ricevere\_le\_email\_di\_root@localhost)** e selezionare ancora **avanti**;
4.  Nella finestra *ricezione email* selezionare tipo di server = consegne locali e percorso = /var/mail/user\_che\_deve\_ricevere\_le\_email\_di\_root e cliccare **avanti**;
5.  Nella finestra *opzioni ricezione* scegliere se (e quando) evolution deve controllare se ci sono nuove email (esempio = ogni 10 minuti) e cliccare su **avanti**;
6.  Nelle finestra *invio email* scergliere **tipo di server = sendmail** e cliccare su **avanti**;
7.  Nella finestra *Gestione degli account* scegliere un nome mnemonico per il nuovo account (esempio "mail locale") e cliccare su **avanti**;
8.  Nella finestra *Completato* cliccare su **applica**.

Da questo momento in poi le email originariamente destinante al superuser arriveranno all'utente "user\_che\_deve\_ricevere\_le\_email\_di\_root" su mail evolution.

<Categoria:Sistema>
