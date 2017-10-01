Poichè non tutti utilizzano prodotti Microsoft, ci si può imbattere in file di formato *docx*, ed avere difficoltà per il loro utilizzo. Questa semplice procedura, ripresa da varie fonti ed adattata a Fedora 8, permette la loro conversione in formato Open Document.

1.  Prima di tutto si installano *rpm2cpio* e *cpio* dai repository ufficiali, nel caso non fossero presenti:
2.  yum install cpio rpm

se yum comunicherà *nothing to do* vuol dire che le applicazioni richieste sono già installate.

<li>
Scaricare il file *odf-converter* per sistemi i386 ad esempio da [qui](http://download.go-oo.org/red-carpet/ooo-680/sled-10-sp-i586/odf-converter-1.1-7.i586.rpm),
oppure *odf-converter-1.1-5.x86\_64.rpm* per sistemi x86\_64 da [qui](http://download.go-oo.org/red-carpet/ooo-680/sled-10-sp-x86_64/odf-converter-1.1-7.x86_64.rpm)

</li>
<li>
Dare i seguenti comandi da root:

</li>
`# cd /home/utente/Desktop   ( supponendo che il file in questione sia stato salvato sul desktop)`
`# rpm2cpio odf-converter*rpm | cpio -ivd`
`# cp usr/lib/ooo-2.0/program/OdfConverter /usr/bin`

<li>
L'estrazione dal file rpm creerà due directory sul desktop che si possono tranquillamente cancellare:

</li>
`# rm -rf opt`
`# rm -rf usr`

L'applicazione viene gestita tramite linea di comando.

<li>
Per utilizzarla basta dare un:

</li>
`$ OdfConvert /I Nome_File.docx`

verrà così convertito il formato docx in formato Open Document e il file sarà presente nella directory corrente. Richiamando esclusivamente il comando *OdfConvert* l'applicazione restituirà tutte le opzioni disponibili.

</ol>
<Categoria:Ufficio>
