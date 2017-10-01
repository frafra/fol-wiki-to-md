Avrete notato un'attenzione, a volte maniacale, verso il problema sicurezza da parte di molti membri della nostra comunità, questo articolo cerca di spiegarvi il perchè.
Questa non vuole essere una guida specifica riguardo alla sicurezza, ma semplicemente una raccolta di comportamenti "virtuosi".
Inoltre non vogliamo analizzare qui i motivi per i quali un aggressore voglia violare il Vostro sistema.
L'articolo è indirizzato ad utenti desktop e/o server di piccola caratura.

Premessa
--------

Cominciamo col dire che sistemi basati sul kernel Linux e sulla struttura Gnu sono molto sicuri, ma non sono inviolabili.
Essi sono sostanzialmente immuni da tanti problemi di sicurezza che affliggono altri sistemi, ma presentano altre forme di vulnerabilità, che possono venire confinati in un ambito di rischio accettabile mediante comportamenti adeguati.
I motivi per cui i sistemi basati su Linux sono considerati particolarmente sicuri sono, grosso modo, i seguenti:

1.  Lo sviluppo kernel è continuo, mediamente una nuova versione kernel è disponibile con una frequenza mensile.
2.  La suddivisione kernel-space - user-space è netta, cioè lo spazio entro cui "gira" il kernel è separato da quello dove "girano" le applicazioni utente.
3.  L'architettura sistema segue una struttura strettamente gerarchica, i permessi delle applicazioni, dei file, degli utenti seguono "politiche" precise e difficilmente violabili.
4.  Le diverse distribuzioni adottano configurazioni differenti, ciò implica che uno script "malevolo" che giri su Debian non è detto che faccia danni su Fedora.
5.  Le tecniche di sicurezza sono parecchie e sommative, basti citare una accoppiata difficilmente "scavalcabile", iptables + Selinux.
6.  Il software è aggiornato pressochè quotidianamente, ciò significa che il software che presenta vunerabilità viene corretto molto rapidamente.
7.  L'elemento umano è più smaliziato, che sperimenta di continuo e comunica i propri risultati, permettendo uno stato di attenzione verso la sicurezza molto alto.

Vogliamo fissare l'attenzione proprio sul settimo punto e fornirvi indicazioni di massima per comportarvi in modo "smaliziato".

Accesso fisico al sistema.
--------------------------

Se un potenziale aggressore ha accesso fisico al sistema, sono veramente poche le possibilità che abbiamo per difenderci.
Potrebbe tranquillamente asportare ( o copiare ) le nostre memorie di massa e analizzarle con calma in altro sistema.
L'unica vera arma in situazioni come questa consiste nella criptazione dei contenuti e/o del filesystem con algoritmi ad alta cifratura.
Vedete per maggiori informazioni: <http://fedoraproject.org/wiki/Security_Guide/LUKSDiskEncryption>
Se il Vostro sistema è ben custodito e sotto la Vostra stretta sorveglianza questo problema non è particolarmente rilevante, basterà evitare che il sistema usi il login automatico e che usi password robuste.
Analizziamo, ora, un caso molto più diffuso:

### Accesso da remoto al sistema.

Se il nostro sistema è connesso ad una rete, per quanto essa possa essere affidabile, allora il nostro sistema è potenzialmente in pericolo.

Provate ad "abbassare" il firewall ed attivare contemporaneamente un servizio "esposto" al web che usi un protocollo come ssh, ftp oppure http, navigate nel web magari attraverso qualche sito "sospetto" ed osservate contemporaneamente i log di sicurezza, li vedrete riempire nel giro di pochi minuti di segnalazioni di tentativi di accesso non autorizzato.
Siete sotto attacco.
Il "chi" e "perchè" faccia una operazione del genere non sono per noi rilevanti (che ci crediate o no attualmente nel web è in corso una vera e propria cyber-war tra opposte fazioni appoggiate e sovvenzionate da precise entità politiche/militari/economiche); è il come che ci interessa.

Vie di attacco
--------------

Ci sono molte vie di attacco ad un sistema, noi ne analizzeremo solo alcune, quelle che possono avere un senso rispetto all'utenza alla quale è rivolto questo articolo:

### Attacco a forza bruta

Per attacco a forza bruta si intende un attacco eseguito mediante applicazioni particolari che cercano di "indovinare" le vostre password di accesso ( non importa quale, sia utente che root ) ad un determinato servizio.
Questo processo può essere condotto a patto di due condizioni:
\* fattore tempo - l'attaccante ha bisogno di tempo per concludere positivamente i propri intendimenti

-   potenza di calcolo - l'attaccante ha bisogno di macchine ad elevata potenza di calcolo per portare avanti i suoi obiettivi.

Entrambi i fattori sono funzione esponenziale della robustezza delle vostre password.
Tenete presente che, l'utente che per definizione non soggiace alla struttura dei permessi ed ha accesso a tutto il sistema è root.
Se un potenziale aggressore riesce ad avere credenziali root, egli avrà piena disponibilità del sistema.
Questo fatto **obbliga** ad avere password root di una certa difficoltà, quindi la scelta di una password di root piuttosto lunga con caratteri non fonetici ad esempio: Lp&'Jj§exT^£-=YdK49, metterà in crisi un attacco a forza bruta, infatti questa è una password che aumenterà in maniera insostenibile i fattori a. b. per l'attaccante.
Se l'attaccante riesce ad "indovinare" la password utente, passerà alla seconda fase del suo piano: l'escalation ai privilegi di root; è quindi molto utile avere password utente dello stesso tipo di quelle root per rendere la vita più difficile.
Una volta che l'attaccante sia riuscito ad avere accesso root al vostro sistema, procederà a:

1.  Cancellare le tracce dai log di sistema di tutto quanto è avvenuto
2.  Aprire backdoors che gli consentano di "visitare" il vostro sistema a suo piacimento
3.  Installare software "maligno", quali root-kit, per avere il pieno possesso del sistema
4.  Confinarvi in un limbo apparentemente tranquillo, e voi sarete ignari di quanto sta accadendo

i punti 1/4 saranno, di solito, realizzati se l'attaccante ha interesse verso il vostro sistema, cioè dopo averlo adeguatamente esplorato. In caso contrario, abbandonerà l'attacco e non si farà più vedere ( cosa improbabile).

Questo tipo di attacco viene eseguito, di solito, mediante script automatici ( i cosiddetti scanner ) e non a "manina" ovvero con l'intervento personale dell'attaccante, in un caso del genere le cose diventano molto più "divertenti".

Come possiamo impiantare la nostra difesa preventiva:

1.  Firewall adeguatamente configurato
2.  Servizi che non usino porte standard e che non permettano l'accesso a root
3.  Password utente e root assai robuste
4.  Confinare i servizi esposti ( chroot )
5.  Costante verifica dei log di sicurezza, cosa che potrete ottenere con il comando:

`# cat /var/log/secure`

oppure

`# tail -f /var/log/secure`

Cosa fare se vi accorgete di essere sotto attacco:

-   Raffinare le regole di iptables
-   Modificare runtime le vostre password, rendendole sempre più complesse
-   Attivare Selinux
-   Svuotare l'history della shell
-   Se proprio vi vedete persi, buttate giù il servizio.

### Attacco via "exploit"

Immaginiamo di attivare il servizio ntp nel nostro sistema.
Cosa fa il servzio ntp ? Preleva la data e l'ora esatta da un server web e reimposta l'ora del nostro sistema se essa non coincide.
E' un servizio assai utile se vogliamo tenere sincronizzati gli orologi delle macchine appartenenti ad una stessa rete. Vi accorgerete, però, anche della sua pericolosità:

-   Dialoga via web
-   Imposta l'ora del nostro sistema ( vi ricordo che per impostare l'ora del sistema occorrono i privilegi root )

Se il nostro servizio è basato su software che contiene qualche vunerabilità (tutti software contengono vulnerabilità), esso potrebbe essere utilizzato per violare il sistema.
In che modo?
Esistono gli exploit, ovvero delle procedure in grado di "inoculare" codice da far eseguire al servizio in maniera non autorizzata, codice che per esempio potrebbe provocare l'apertura di una shell root sul terminale dell'aggressore. E' evidente la pericolosità di una situazione del genere.
Fortunatamente questo tipo di attacco, è sferrato dagli aggressori solo verso sistemi di particolare interesse e per cui ne vale la pena.
Essi infatti sono "costosi" sotto il profilo del tempo e delle risorse da impiegare, perchè il sistema "preda" deve essere messo sotto osservazione per un certo periodo di tempo per scoprirne qualità e difetti.
Come ci si può difendere da essi, se spesso operazioni del genere sono silenti, ovvero difficilmente lasciano tracce?
\# Naturalmente non usando quella applicazione e/o servizio

1.  Se il vostro ip di accesso alla rete è dinamico ( come nella maggioranza delle reti domestiche e/o da piccolo ufficio ), esso cambierà prima che l'aggressore riesca a definire un'utile strategia di attacco, anzi sarà lo stesso aggressore che rinuncerà all'attacco non appena si rende conto di ciò.
2.  Se esiste un "exploit" conosciuto relativo al vostro servizio e/o applicazione, ed esso è noto ad un aggressore, esso potrebbe essere noto anche a Voi, per esempio tenendo d'occhio i vari siti di avvisi di sicurezza della nostra distribuzione e/o del progetto che si occupa dello sviluppo. Di solito assieme all'avviso è pubblicato anche il modo per porvi rimedio.
3.  Aggiornando spesso i pacchetti di quel servizio e/o applicazione, in maniera tale che l'aggressore debba ricominciare daccapo ad ogni modifica.
4.  Non usate **mai** il login grafico da root, in una situazione del genere mettete l'aggressore nelle condizioni di poter eseguire un exploit con risultati positivi in pochi minuti.
5.  un vettore molto utilizzato per questo tipo di attacco è il software peer to peer, evitatelo se possibile.

### Man in the middle

La tecnica del "*Man In The Middle*" (abbreviata frequentemente con *MITM*) non è una vera e propria tecnica di attacco, bensì una tecnica di osservazione del sistema oggetto dell'attacco.

L'idea su cui si basa questa tecnica, consiste in una redirezione del traffico in modo da far passare il flusso attraverso la macchina dell'attaccante, e poter osservare i pacchetti ("sniffare") al loro passaggio. Esistono tool specifici per realizzare il man in the middle.

Difendersi da una tecnica del genere non è difficile, basta far passare le informazioni sensibili, attraverso protocolli criptati. Naturalmente occorre prestare attenzione sulla genuinità dei pacchetti che riceviamo (vedi par.installazione di software).

### I virus

I virus, propriamente detti, non hanno alcun effetto su sistemi Linux.
I sistemi antivirus su Linux sono inutili, essi hanno un senso solo se la vostra macchina ridireziona il traffico web verso altre macchine attrezzate con altri sistemi operativi vulnerabili ai virus. In questo caso esse possono filtrare e proteggere le macchine vunerabili presenti nella vostra rete.
Esistono, però, i cosidetti "proof of concept", ovvero studi teorici di virus che "potrebbero" girare su macchine linux. Abbiamo detto teorici, perchè non vi è alcuna notizia sul fatto che questi studi funzionino sul serio, anzi si sa del contrario, ovvero, che non funzionano.
Nel caso abbiate timore che questi pericoli teorici possano essere usati contro di voi, spesso basta una contromisura molto semplice: l'opzione noexec sul mount della vostra home.

Installazione di software
-------------------------

Terminiamo la nostra analisi con quello che riteniamo il pericolo più grande per gli utenti di un sistema desktop.
La pericolosità di installare software non sicuro è enorme rispetto alla pericolosità dei punti 1,2,3 analizzati in questo articolo (facendo sempre riferimento all'utenza verso la quale l'articolo stesso è rivolto).
Fate sempre uso dei repository ufficiali e non usate **mai** l'opzione --nogpgcheck in dnf o rpm, questa opzione rinuncia al controllo della firma del pacchetto in fase di installazione, unica cosa che ne garantisce la genuinità cioè il controllo della firma garantisce che il pacchetto è identico a quello depositato nel repository ufficiale.
Vi ricordo che a seguito di un attacco ai server Fedora (agosto 2008), la comunità internazionale decise di cambiare le firme dei pacchetti in Fedora otto e nove a scopo precauzionale.
Supponiamo, per esempio, che qualcuno voglia fare uno scherzo e realizzi un pacchetto rpm contenente una simpatica applicazione.
L'applicazione vi piace e decidete di installarla.
Supponiamo che nel pacchetto che scaricate vi sia uno script che inserisce nello startup del sistema una cosa del genere:

`:(){ :|:& };:`

Questo codice è una fork-bomb.
Se lanciata da root (fedora impedisce l'esecuzione di fork da utente), essa bloccherà il sistema, esaurendo le risorse in un istante.
Se non individuerete dov'è e/o non reinstallerete il sistema, essa continuerà a bloccarvi la macchina.
Quindi, vi esorto ad usare solo repository rpm affidabili e sicuri.
Evitate di installare applicazioni dai sorgenti anche se i siti dai quali prelevate il software sono sicuri.
Con la tecnica del "man in middle", qualcuno potrebbe modificare il pacchetto a suo piacimento, magari "infilandoci" una fork-bomb oppure qualcosa di peggio, cosa che con l'uso dei repository ufficiali e con il controllo della firma, sarebbe impossibile.

<Categoria:Sicurezza>
