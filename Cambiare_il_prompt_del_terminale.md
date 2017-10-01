L'aspetto del prompt viene controllato dalla variabile della shell PS1. Per modificare l'aspetto del prompt, occorre cambiare questa variabile. Per fare esperimenti, si può cambiare la stringa PS1 direttamente al prompt e vedere immediatamente i risultati (questo influenza solo la sessione corrente e i cambiamenti spariscono quando si fa il log-out). Se si vuole rendere permanente un cambiamento del prompt, modificare il file (nascosto) .bashrc nella propria home e aggiungere lì la nuova definizione di PS1 sotto la riga \# User specific aliases and functions.

Il prompt più semplice sarebbe un singolo carattere, come:

`[utente@hostname myhome]$ PS1=$`
`$ls`
`bin   mail`
`$ `

Se invece si vuole inserire ad esempio uno spazio bianco dopo il prompt per renderlo più leggibile

`$PS1="$ "`
`$ ls`
`bin mail`
`$`

Bash permette di personalizzare queste stringhe di prompt inserendo vari caratteri di escape speciali che vengono interpretati come segue:

`      a     il carattere ASCII beep (07)`
`      d     la data nel formato "Giorno-della-settimana Mese Data"`
`             (e.g., "Tue May 26")`
`      e     un carattere di escape ASCII (033)`
``       h     l'hostname fino al primo `.' ``
`      H     l'hostname`
`      n     il carattere "newline"`
`      r     il carattere "carriage return"`
`      s     il nome della shell, il nome base di $0`
`             (la parte che segue lo slash finale)`
`      t     l'ora corrente nel formato 24-ore HH:MM:SS`
`      T     l'ora corrente nel formato 12-ore HH:MM:SS`
`      @     l'ora corrente nel formato 12-ore am/pm`
`      u     lo username dell'utente corrente`
`      v     la versione di bash (e.g., 2.00)`
`      V     la release di bash, versione + patchlevel`
`             (e.g., 2.00.0)`
`      w     la directory di lavoro corrente`
`      W     il nome di base della directory di lavoro corrente`
`      !     il numero cronologico (history number) di questo comando`
`      #     il numero di questo comando`
`      $     se l'UID effettivo è 0, un #, altrimenti un $`
`      nnn   il carattere corrispondente al numero ottale nnn`
`      \     un backslash`
`      [     comuncia una sequenza di caratteri non stampabili, che`
`             potrebbero essere usati per inserire una sequenza di`
`             controllo del terminale nel prompt`
`      ]     termina la sequenza di caratteri non stampabili`

Due esempi:

`[utente@hostname myhome]$ PS1="u@h W> "`
`utente@hostname myhome> ls`
`bin   mail`
`utente@hostname myhome>`

Questo è simile al prompt predefinito di molte distribuzioni. Per visualizzare ad esempio l'ora:

`utente@hostname myhome> PS1="[t][u@h:w]$ "`
`[16:27:18]][utente@hostname:~]$ ls`
`bin   mail`
`[16:27:18]][utente@hostname:~]$ `

Si può così personalizzate il proprio prompt come più piace.

Colori
------

I colori sono caratteri di escape non stampabili e pertanto devono essere racchiusi fra

$$\\033\[

e$$
`   `

Devono anche essere seguiti da una m minuscola.

Questi di seguito sono i valori dei colori:

`Nero           0;30     Grigio Scuro  1;30`
`Blu            0;34     Blu Chiaro    1;34`
`Verde          0;32     Verde Chiaro  1;32`
`Ciano          0;36     Ciano Chiaro  1;36`
`Rosso          0;31     Rosso Chiaro  1;31`
`Viola          0;35     Viola Chiaro  1;35`
`Marrone        0;33     Giallo        1;33`
`Grigio Chiaro  0;37     Bianco        1;37`

Due esempi da provare:

Prompt e testo blu

`PS1="`
$$\\033\[0;34m$$
`(\t)[\u@\h:\w]$ "`

Prompt rosso e testo nero

`PS1="`
$$\\033\[0;31m$$
`(\t)[\u@\h:\w]$`
$$\\033\[0;30m$$
` "`

I colori possono risultare utili oltre che dare un bell'aspetto al prompt.

<Categoria:Sistema>
