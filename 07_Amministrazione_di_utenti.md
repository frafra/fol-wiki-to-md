Setta Sudo sul tuo PC
---------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

gedit /etc/sudoers

<li>
Trova questa linea

</li>
`# User privilege specification`
`root   ALL=(ALL) ALL`
`tuo_nome_utente ALL=(ALL)NOPASSWD: ALL`

<li>
Aggiungi il tuo nome utente sotto la linea dove dice root e copia il resto della riga così com'è:

</li>
La voce **"NOPASSWD:"** è opzionale. Se lavori in un ambiente in cui pensi che potrebbe essere un rischio usare questa opzione, **NON USARLA**. Rimuovi semplicemente quella sezione nella riga. Se non usi l'opzione **"NOPASSWD:"**, quando avvii un comando con sudo, devi digitare la tua password, NON quella di root.

</ol>
Come configurare/cambiare/abilitare la password di root
-------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

passwd root

</ol>
Come disabilitare l'account di root
-----------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

passwd -l root

</ol>
Come aggiungere/configurare/cancellare utenti
---------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Desktop -&gt; Impostazioni di Sistema -&gt; Utenti e Gruppi
3.  Utenti e Gruppi

Usa il Tab Utenti -&gt; Aggiungi utente.../Proprietà/Cancella

</ol>
Come aggiungere/configurare/cancellare gruppi di utenti
-------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Desktop -&gt; Impostazioni di Sistema -&gt; Utenti e Gruppi
3.  Utenti e Gruppi

Usa il Tab Gruppi -&gt; Aggiungi gruppo.../Proprietà/Cancella

</ol>
Come avere un accesso automatico a GNOME (non sicuro)
-----------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")
2.  Desktop -&gt; Impostazioni di Sistema -&gt; Finestra di Login
3.  Finestra di Login Setup

Tab Generale -&gt; Login Automatico -&gt;

`Abilitare il login automatico al primo avvio (da spuntare)`
`Utente per il login automatico: Seleziona "nome_utente"`

</ol>
Come cambiare i permessi a file/directory
-----------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

Fai click con il pulsante destro sul file/directory -&gt; Proprietà

`Usa il Tab Permessi -> Lettura/Scrittura/Esecuzione (definisci i permessi per l'utente/gruppo/altri)`

</ol>
Come cambiare il possesso di file/directory per un utente
---------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

chown nome\_utente /percorso\_al\_file\_o\_cartella

</ol>
Come cambiare il possesso di file/directory per un gruppo
---------------------------------------------------------

1.  Leggi [Premessa](01_Introduzione_a_Fedora#Premessa "wikilink")

chgrp nome\_gruppo /percorso\_al\_file\_o\_cartella

</ol>
<Categoria:Fedoraserver>
