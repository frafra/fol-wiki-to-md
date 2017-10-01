Come far funzionare il lettore di impronte digitali con fedora 10?
La risposta è semplice e sul web si trovano un sacco di guide interessanti e utili.
Provo a scrivere una mini guida anch'io perché ho trovato delle difficoltà con fedora 10 a far funzionare bene il software per il lettore di impronte biometrico presente sul mio portatile: Dell XPS M1530.

Fondamentalmente per linux esistono due progetti che permettono l'utilizzo del proprio dispositivo:

1.  [ThinkFinger](http://thinkfinger.sourceforge.net/index.php)
2.  [fprint project](http://www.reactivated.net/fprint/wiki/Main_Page)

Per tutta la documentazione sui due progetti vi rimando ai siti ufficiali.

Prima di tutto però bisogna capire se il nostro lettore di impronte è riconosciuto da fedora e se è supportato da uno dei due progetti [1)](#ThinkFinger "wikilink") [2)](#Fprint "wikilink"):

`$ lsusb |grep print`
`Bus 003 Device 002: ID 0483:2016 SGS Thomson Microelectronics Fingerprint Reader`

Questo è quello che c'è nel mio portatile.

E' riconosciuto e vedo che è supportato, ora la scelta del software da installare:

ThinkFinger
-----------

**ThinkFinger** l'ho provato e funziona bene ma c'è solo un problema: non è compatibile con kdm e kde. E' un bug che al momento in cui scrivo non è stato risolto.
Per gli utilizzatori di Gnome però la cosa non dovrebbe arrecare problemi e possono procedere così per l'installazione:
Installazione con yum da utente root:

`# yum install thinkfinger`

Una volta installato si può procedere con la verifica del suo funzionamento:

`# tf-tool --acquire`
`# tf-tool --verify`

Il primo comando chiederà di passare il dito sul lettore 3 volte per acquisire temporaneamente l'informazione che poi verrà verificato con il secondo comando. Se tutto funziona bene si può impostare fedora in modo tale che permetta l'autenticazione con le impronte digitali. Per farlo bisogna modificare la configurazione di PAM, con l'editor di testo preferito, io uso vim:

`# vim /etc/pam.d/system-auth`

Ora bisogna inserire la regola nel posto giusto:

`#%PAM-1.0`
`# This file is auto-generated.`
`# User changes will be destroyed the next time authconfig is run.`
`auth        required      pam_env.so`
`auth        sufficient    pam_thinkfinger.so       # <-------- riga da aggiungere`
`auth        sufficient    pam_unix.so nullok try_first_pass`
`auth        requisite     pam_succeed_if.so uid >= 500 quiet`
`auth        required`
`pam_deny.so`
`[...tutte le altre regole da non toccare]`

Meglio impostare con "sufficient", ciò significa che per fare l'autenticazione basterà l'autenticazione con l'impronta digitale, nel caso non ci si riesca si può utilizzare la password classica. Meglio evitare di mettere "required".

Ora per impostare l'autenticazione per gli utenti basta usare questo comando:

`# tf-tool --add-user $USERNAME`
`$USERNAME è il nome dell'utente. `

E qui dovrebbe essere tutto a posto e si dovrebbe essere in grado di fare le autenticazioni con la propria impronta digitale senza dover mettere per forza la password.
Non ho provato personalmente se funziona con il mio sistema, come detto con kdm e kde esiste un bug e io uso kde e kdm e il sistema continua ad andare in crash.

Fprint
------

Altra possibilità di fare funzionare il lettore è usare **fprint**.
(Meglio fare una installazione pulita per cui se si sono eseguite delle operazioni precedenti meglio riportare il sistema come era prima).
Installazione di fprint:

`# yum install fprint fprintd-pam fprint_demo`

fprint\_demo è un programma in gtk che aiuterà in modo grafico ad utilizzare fprint.
fprint-pam è il modulo di fprint per pam.

Ora bisogna vedere se tutto funziona per cui sempre da shell dare questo comando per avere un aiuto:

`# pam_fprint_enroll --help`

E proviamo ad acquisire l'impronta del dito indice della mano destra:

`# pam_fprint_enroll --enroll-finger 7`

Se tutto è funzionato bene senza alcun problema allora si può configurare PAM in modo tale che ci permetta l'autenticazione con il lettore di impronte digitali (la procedura è identica a prima ma cambia la regola da dare, ovviamente:

`# vim /etc/pam.d/system-auth`

Ora bisogna inserire la regola nel posto giusto:

`#%PAM-1.0`
`# This file is auto-generated.`
`# User changes will be destroyed the next time authconfig is run.`
`auth        required      pam_env.so`
`auth        sufficient    pam_fprint.so       # <-------- riga da aggiungere`
`auth        sufficient    pam_unix.so nullok try_first_pass`
`auth        requisite     pam_succeed_if.so uid >= 500 quiet`
`auth        required pam_deny.so`
`[...tutte le altre regole da non toccare]`

Ora per configurare fprint basta che ogni utente lanci questi comandi per acquisire la loro impronta digitale:

`$ pam_fprint_enroll`

oppure se si preferisce in modo grafico:

`$ fprint_demo`

Riavviare il sistema e al prossimo tentativo di autenticazione pam chiederà con fprint di scorrere il dito che si è scelto e configurato con i comandi precedenti.

Risoluzione dei problemi con fprint:
------------------------------------

Io con fedora 8 seguendo i passaggi precedenti non ho avuto alcun tipo di problema, con fedora 10 a 64 bit però dopo aver installato fprint ho avuto il seguente problema:
pam\_fprint\_enroll ed fprint\_demo erano utilizzabili solamente dall'utente root e gli utenti "normali" non avevano la possibilità così di impostare il loro "dito".
Il problema l'ho discusso e risolto sul forum di fedoraonline a \[<http://www.fedoraonline.it/modules/newbb/viewtopic.php?topic_id=8159&viewmode=flat&order=ASC&type>=&mode=0&start=0 questo indirizzo\]. Stranamente quando si lancia pam\_fprint\_enroll ottengo questo errore:

`$ pam_fprint_enroll`
`This program will enroll your finger, unconditionally overwriting any selected print`
`that was enrolled previously. If you want to continue, press enter, otherwise hit Ctrl+C.`
`Found device claimed by UPEK TouchStrip driver`
`fp:error [fp_dev_open] device initialisation failed, driver=upekts`
`Could not open device.`

Semplicemente bisogna dare le regole corrette a udev in modo tale che il dispositivo possa essere aperto anche dagli utenti con meno privilegi dell'utente amministratore e un gruppo apposito che abbia i permessi di accesso al dispositivo:

-   creare la regola per udev specifica per il proprio dispositivo (da utente root ovviamente con l'editor di testo preferito, il mio vim, se non esiste il file si può creare tranquillamente:

`# vim /etc/udev/rules.d/99-impronte.rules`

Inserire le seguenti regole:

`SUBSYSTEM=="usb", ACTION=="add", ATTR{idVendor}=="0483", ATTR{idProduct}=="2016", GROUP="impronte", MODE="0664", OPTIONS+="last_rule"`

Si può vedere con lsusb(sono quelli che qui ho evidenziato):

`$ lsusb |grep print`
`Bus 003 Device 002: ID `**`0483:2016`**` SGS Thomson Microelectronics Fingerprint Reader`

-   Ora bisogna creare il gruppo e aggiungere gli utenti che si vuole possano utilizzare tranquillamente il dispositivo:

`# groupadd impronte`
`# usermod -a -G impronte $USERS`

al posto di $USERS si sostituisce l'utente.
Per sicurezza dare un riavvio del sistema e poi gli utenti potranno utilizzare tranquillamente pam\_fprint\_enroll o fprint\_demo.

Riferimenti
-----------

-   [<http://blog.marionline.it>](http://blog.marionline.it/?p=57)
-   [How to per abilitare il lettore di impronte digitali con thinkfinger](http://www.thinkwiki.org/wiki/How_to_enable_the_fingerprint_reader_with_ThinkFinger#Fedora.2FFedora_Core)
-   \[<http://www.fedoraonline.it/modules/newbb/viewtopic.php?topic_id=8159&viewmode=flat&order=ASC&type>=&mode=0&start=0 Discussione forum Fedoraonline\]
-   [Progetto ThinkFinger](http://thinkfinger.sourceforge.net/index.php)
-   [Progetto fprint](http://www.reactivated.net/fprint/wiki/Main_Page)
-   [Bug di kde con thinkfinger](https://bugs.kde.org/show_bug.cgi?id=116682)

Sviluppi futuri in Fedora:
--------------------------

Nel progetto fedora pare che si stia implementando un sistema che semplifichi l'utilizzo dei dispositivi per leggere le impronte digitali tramite fprint e l'utilizzo di un demone particolare: fprintd.
Per queste novità il riferimento è su fedoraproject.org a [questo indirizzo](https://fedoraproject.org/wiki/Features/Fingerprint).

<Categoria:Hardware>
