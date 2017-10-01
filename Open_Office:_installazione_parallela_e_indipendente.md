Introduzione
------------

Con l'uscita della nuova versione della suite Open Office, la 3.0.0., gli utenti Fedora ancora legati alla 8 "Werewolf" (come il sottoscritto...) o sulla 9 "Sulphur", che andranno in pensione relativamente presto, NON la riceveranno tra gli aggiornamenti standard.
Dunque c'è chi si interroga sulla possibilità di affiancarla/sostituirla a quella fornita "di serie" dalla propria distro di riferimento.

Dopo aver letto su alcuni forum di esperienze infelici in tal senso, il mio consiglio spassionato è: NO.
Tenetevi quella che avete scaricato e installato tramite Yum (o Yumex, o Synaptic, o comunque dai repo 'ufficiali') e AGGIUNGETE A PARTE questa nuova. Avrete un sistema "pulito", in cui cioè potrete continuare a tenere distinte le due versioni, aggiornarle oppure anche eliminarne una delle due, senza pregiudicare il funzionamento dell'altra! Questo è possibile grazie alla flessibilità dei pacchetti RPM.
Il senso di questa guida è spiegarvi come fare, senza tante complicazioni, utilizzando pochi comandi giusti (in particolare si vedano i comandi 5 e 6).

La procedura
------------

Avviare il terminale e diventare root (notare come cambia il prompt tra il secondo e il terzo comando):

`$ su -`
`password di root`

navigare nel file system, mediante il comando *cd*, sino a posizionarsi nella cartella dove è stato scaricato il file (&gt; 150 MB da:<http://it.openoffice.org/> ) e scrivere:

`# tar zxvf OOo_3.0.0_LinuxIntel_install_it.tar.gz`

se è stata scaricata la versione "liscia", senza estensioni Java, altrimenti il comando è:

`# tar zxvf OOo_3.0.0_LinuxIntel_install_wJRE_it.tar.gz`

Poi dare i comandi seguenti:

`# cd OOO300_m9_native_packed-1_it.9358/RPMS/`
`# mkdir -p /opt/ooo3/.rpm`
`# rpm -ivh --dbpath /opt/ooo3/.rpm --nodeps --prefix /opt/ooo3 *.rpm`
`# exit`

con questo comando si torna utente normale; così si potrà verificare se funziona tutto regolarmente lanciando la suite da ufficio appena installata, digitando:

`$ /opt/ooo3/openoffice.org3/program/soffice`

Come ciliegina sulla torta è possibile a questo punto fare varie cose per semplificarsi ulteriormente l'esistenza:

1.  creare un alias in ~/.bash per avviare la suite con un comando più semplice da terminale (per esempio, oo3) -- NB: googlando si trova molta documentazione su come farlo;
2.  creare una scorciatoia e associare al comando un'icona per lanciarlo dal desktop (per esempio);
3.  idem, ma inserendola su un pannello a propria scelta;
4.  idem, ma creando anche le voci parallele in Applicazioni &gt; Ufficio, tramite la comoda utility Sistema &gt; Preferenze &gt; Aspetto e stile &gt; Main menu -- NB: difatti questa installazione NON aggiunge nulla ai menu, proprio per lasciare la massima libertà di scelta e autonomia fra le due versioni;
5.  decidere che la nuova versione non è soddisfacente: dopo tutta la fatica, per buttarla via basterà eliminare, da root, la directory /opt/ooo3;
6.  eliminare la versione 'standard' invece dell'ultima -- **Sconsigliato!**

Riferimenti
-----------

-   [PLIO](http://www.plio.it/).
-   [Pagina "Quality Assurance" del sito italiano di OOo](http://it.openoffice.org/qa).

<Categoria:Ufficio>
