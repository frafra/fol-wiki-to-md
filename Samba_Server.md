Prefazione
----------

Questa guida ha come scopo quello di installare e configurare un file server con Fedora: la versione di riferimento con la quale sono stati eseguiti i test è **Fedora 22 Server**, ma sono confidente che possa essere facilmente riprodotta anche su altre release e veriticalizzazioni.

Per prima cosa bisogna andare a spiegare cos'è un file server e le sue modalità di funzionamento: quando parliamo di file server ci riferiamo ad una macchina - sia essa fisica o virtuale - la quale metta a disposizione su di una rete spazio disco dove l'utenza possa leggere o scrivere file e cartelle secondo regole e autorizzazioni. Le regole e le autorizzazioni vengono descritte dentro al nostro file di configurazione (/etc/samba.smb.conf), le autorizzazioni a livello di utente o gruppo possono essere o locali (utenti di macchina) o ereditate da altri sistemi (quali ad esempio active directory).

Questa guida verrà quindi divisa in due macro categorie:

-   **Samba server con autenticazione locale**
-   **Samba server con autenticazione Microsoft Active Directory**

Si lascia ovviamente al lettore la scelta su cosa sia meglio implementare nella propria rete.

Samba server con autenticazione locale
--------------------------------------

### Scenario

In questo scenario andremo a simulare un file server di un'azienda standard, di seguito utenti e mansioni:

| Username | Reparto         | Gruppo          |
|----------|-----------------|-----------------|
| carlo    | Amministrazione | amministrazione |
| giulia   | Amministrazione | amministrazione |
| roberta  | Amministrazione | amministrazione |
| simone   | Marketing       | marketing       |
| sandro   | Sales           | sales           |
| katia    | Sales           | sales           |
| mauro    | IT Dpt.         | itdpt           |
||

### Condivisioni

Ogni utente avrà una sua home direcotry dove avrà accesso solo lui.

Inoltre andremo a creare le condivisioni dipartimentali le quali autorizzazioni saranno a livello di gruppo di appartenenza: avremo quindi uno share amministrazione al quale potranno solo accedere gli utenti dell'amministrazione, lo share sales solo agli utenti delle vendite, uno share comune a tutta l'organizzazione e così via. Andremo anche ad inserire l'utente "mauro" in ogni condivisione in qualità di amministratore del sistema. In ultima battuta andremo a creare degli share ai quali i singoli utenti di diversi gruppi potranno accedere.

Nel nostro ambiente di test andremo quindi a creare queste condivisioni dipartimentali:

| Condivisione    | Gruppo           | Utenti impattati               | Privilegi           |
|-----------------|------------------|--------------------------------|---------------------|
| amministrazione | amministrazione  | carlo giulia roberta **mauro** | lettura e scrittura |
| marketing       | marketing        | simone **mauro**               | lettura e scrittura |
| marketing       | marketing        | simone **mauro**               | lettura e scrittura |
| sales           | sales            | sandro katia **mauro**         | lettura e scrittura |
| comune          | Tutti gli utenti | tutti gli utenti               | lettura e scrittura |
| install         | Tutti gli utenti | tutti gli utenti               | sola lettura        |
| progetto\_alpha |                  | simone katia **mauro**         | lettura e scrittura |

### Suddivisione spazio disco

Per prima cosa mostro nella mia situazione a livello di storage

`  # lsblk`
`  NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT`
`  sda      8:0    0 238,5G  0 disk `
`  ├─sda1   8:1    0   500M  0 part /boot`
`  ├─sda2   8:2    0   230G  0 part /`
`  └─sda3   8:3    0     8G  0 part [SWAP]`
`  sdb      8:16   0 465,8G  0 disk `
`  └─sdb1   8:17   0 465,8G  0 part /home`
`  sdc      8:16   0 465,8G  0 disk `
`  └─sdc1   8:17   0 465,8G  0 part /opt`

In questo scenario andrò ad utilizzare il mount point /opt per le mie cartelle condivise

[:Rete\_e\_Server](:Rete_e_Server "wikilink")
