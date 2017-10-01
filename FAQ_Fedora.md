Fedora: domande generiche
-------------------------

### Perchè dovrei usare Fedora?

Dovresti usare Fedora perchè è la migliore e più aggiornata collezione di software robusti, liberi e open source. L'\[<https://fedoraproject.org/wiki/It_IT/Overview>| Anteprima\] spiega nel dettaglio molti dei punti di forza di Fedora.

### Come si accede al cosiddetto "terminale"?

Il terminale è un simulatore di una shell all'interno di un ambiente grafico. Serve per poter dare dei comandi testuali e si accede semplicemente da:
*Applicazioni --&gt; Strumenti di sistema --&gt; Terminale*

### Come installo nuovi software in Fedora?

Il programma yum ti aiuta a gestire il software sul tuo sistema. yum accede a specifici siti web, chiamati repositori, per scaricare e installare le ultime versioni dei pacchetti software. Inoltre i sistemi Fedora includono un'interfaccia grafica per yum, disponibile alla voce di menu Applicazioni &gt; Aggiungi/Rimuovi Software.
Nella nostra sezione "Guide" puoi leggere come fare per configurare Yum.

### Fedora può mantenersi aggiornata automaticamente?

Si, sebbene l'aggiornamento automatico non sia la scelta più indicata per ogni tipo di sistema. Puoi impostare le opzioni preferite alla voce di menu *Applicazioni --&gt; Strumenti di sistema --&gt; Aggiornamenti software*.
Fedora usa PackageKit per informarti automaticamente quando ci sono aggiornamenti disponibili.

### Perchè Fedora non supporta i formati proprietari come MP3 o MPEG?

I formati MP3 e MPEG sono vincolati da brevetti, e i proprietari di tali brevetti non hanno rilasciato queste tecnologie sotto licenze compatibili con i requisiti di Fedora.
Fedora include e supporta solamente il software libero ed open source. Le tecnologie coperte da diritti d'autore o vincolate da restrizioni imposte da brevetti non vengono incorporate in Fedora.

### Perchè Fedora non include programmi proprietari come Adobe Acrobat Reader, Adobe Flash Player o RealPlayer?

Fedora include e supporta solamente il software libero ed open source. Nessun programma proprietario viene incluso in Fedora. Molti di questi programmi sono disponibili per Fedora, e sei libero di scaricarli da un altro fornitore software e installarli.
Per maggiori informazioni, visita la pagina \[<https://fedoraproject.org/wiki/ForbiddenItems>| ForbiddenItems\].

### Posso aggiornare la mia versione di Fedora all'ultima release?

Si. Per maggiori informazioni sulle opzioni di aggiornamento, fai riferimento alla pagina \[<https://fedoraproject.org/wiki/Upgrading/it>| Upgrading\].

Fedora: questioni tecniche
--------------------------

### Cos'è la virtualizzazione? Dove posso imparare ad utilizzarla?

Fedora include un esteso supporto per la virtualizzazione; cio permette che piu sistemi operativi siano in esecuzione simultaneamente sulla stessa macchina, con un piccolo impatto sulle prestazioni generali del sistema. Ad ogni sistema operativo viene allocata una parte delle risorse del computer ospitante. Gli amministratori possono inoltre spostare tra diverse macchine un sistema operativo in esecuzione, senza interrompere o mandare in errore i servizi.
La pagina \[<https://fedoraproject.org/wiki/Virtualization>| Virtualizzazione\] ti aiuterà ad ambientarti in questa implementazione.

### Chi è root?

Root è l'amministratore del sistema. Quando utilizzi Fedora dovresti essere loggato sempre come utente normale, MAI come root, per non rischiare di fare danni irreversibili al tuo sistema. Anche nel terminale, root si identifica facilmente tramite la shell:
\# questa è la shell di root

`$ questa è la shell di un utente normale`

Se inserisci nel terminale su (super-user), viene chiesta la password di root:
$ su -

`password`

`# (eccoti loggato come root)`

### Dopo un aggiornamento il sistema non parte più. Cosa è successo?

Gli aggiornamenti vanno fatti con una certa razionalità, a volte aggiornare un pacchetto o più librerie all'ultima versione appena uscita comporta l'esposizione a qualche rischio in più. Se il sistema funziona bene e non si tratta di aggiornamenti di sicurezza o simili, è consigliato tenere il sistema così com'è.
Se sei indeciso e prima di dire "sì" all'aggiornamento di 283 pacchetti che si tirano dietro 150 dipendenze, chiedi consiglio sul nostro Forum.

### E' utile aggiornare sempre tutto e accettare gli aggiornamenti proposti da Fedora?

No, anzi, seguendo un famoso detto si direbbe: "squadra che vince non si cambia!" Nel senso che se il sistema funziona bene e non ci sono aggiornamenti di sicurezza o di bugfix, non è necessario aggiornare il sistema. Si potrebbe ottenere anche l'opposto con l'aggiornamento, perchè a volte i pacchetti nuovi sono poco testati e potrebbero compromettere il corretto funzionamento del sistema.
E' sconsigliato, tranne dopo l'installazione, aggiornare tutto se vengono proposti centinaia di pacchetti. Piuttosto fai un aggiornamento mirato e controllato, scegliendo i pacchetti uno ad uno. Se hai dei dubbi chiedi prima sul Forum.

### Perchè Fedora non mi fa accedere come root al login grafico?

Fedoraproject ha deciso di togliere a partire da Fedora 10 la possibilità di loggarsi come root per una questione di sicurezza del sistema. Eventuali operazioni, per le quali si necessità i permessi di root, si possono fare anche da utente, inserendo la password di root quando richiesta, oppure utilizzando direttamente il terminale.

<Categoria:FAQ>
