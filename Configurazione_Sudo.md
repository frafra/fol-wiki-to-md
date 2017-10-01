\_\_TOC\_\_

Introduzione
------------

Il programma **sudo** permette di eseguire dei programmi che normalmente vengono eseguiti da root, anche da utenti normali.
Essendo un comando abbastanza pericoloso, necessita di una certa attenzione nell'essere configurato.
Nelle occasioni di necessità è preferibile accedere come **utente root** anziche utilizzare sudo, in quanto si ha più coscienza delle proprie azioni; inoltre se viene rubata la password utente ed è configurato sudo, il malintenzionato avrà completo e facile accesso a tutti i dati del computer.

Fedora, come tutte le altre distribuzioni Linux, ha un utente root e singoli utenti.
L'utente root è il "superutente", qualcosa di simile all*'Amministratore* in Windows.

Occorre usare il proprio account personale creato all'installazione per gli usi quotidiani. Usare invece l'utente root solo per gli usi relativi all'amministrazione del computer, aggiornamento/rimozione programmi, modifiche a file di sistema, ecc..
**Sudo** permette di utilizzare l'utente normale come 'root', anteponendo il comando *sudo*.

Configurazione
--------------

Se si è configurato sudo al primo boot, si è già a posto così. Altrimenti si può configurare *sudo* manualmente, digitando, una volta loggati come root:

`# echo 'loginname ALL=(ALL) ALL' >> /etc/sudoers`

Dove **loginname** è il proprio account per l'utente individuale che si desidera far diventare amministratore. Va usato

`ALL=(ALL) NOPASSWD:ALL`

se si vuole che non venga richiesta una password.
Se viene richiesta una password durante l'uso di 'sudo', si dovrà fornire la password dell'utente, non quella di root!

### Esempio di configurazione

Esempio:

`[`**`mirandam`**`@charon ~]$ su`
`Password:   <--Inserire password di root`
`[root@charon mirandam]# echo `**`'mirandam`**` ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers`
`[root@charon mirandam]# exit`

Esempio di utilizzo
-------------------

Il seguente è un esempio di come sudo lascia eseguire i comandi di root:

`[mirandam@charon ~]$ du -sh /root`
`` du: `/root':  ``**`Permission` `denied`**`      <-- Errore senza sudo!!!`
`[mirandam@charon ~]$ sudo du -sh /root`
`163M    /root                       <-- Funziona con sudo!!!`

<Categoria:Sistema> <Categoria:Sicurezza>
