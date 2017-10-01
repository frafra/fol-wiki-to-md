Premessa: La miniguida fa riferimento a Gedit come editor ma è possibile utilizzare anche il proprio editor preferito in alternativa.

Piattaforma: Fedora 17 Software: Filezilla 3.5.3 Italiano

Filezilla permette tra le altre funzioni di verificare o modificare il contenuto di file XML, CSS, HTML, PHP, TXT ed in generale qualsiasi formato testo attraverso la propria interfaccia senza essere costretti ad aprire altre finestre per verificare (per esempio) il contenuto di un file da uplodare su un server.

Questa funzione non solo è comoda ma permette a Filezilla stesso (durante tutta la durate di una sessione) di "accorgersi" che avete fatto delle modifiche ad un file il che porterà ad una finestra di popup che chiede se volete che il file modificato sia caricato sul server (molto comodo quando si verificano online delle modifiche ad un file html/php per esempio).

Per far questo bisogna istruire Filezilla ad usare un programma editor. Dal momento che Gedit è solitamente installato di default nella distribuzione di Fedora utilizzeremo questo editor per attivare queste comododities.

Le operazioni da fare sono semplici:

1.  1) lanciare Filezilla
2.  2) Selezionare il menu in alto a destra "**Modifica**" e poi la voce "**Impostazioni**"
3.  3) nella finesta che si aprirà, selezionare nella parte destra la voce "**Modifica File**" (l'ultima). Si apriranno delle sotto-voci tra le quali "**Associazione Tipi di File**": cliccarci sopra con il tasto sinistro del mouse
4.  4) La parte destra mostrerà (se non avete già fatto altre associazioni) un pagina vuota con il alto la dicitura "**associazioni personalizzate**": in questo spazio inserite le estenzioni che volete editare direttamente da filezilla ed il programma che vogliate le apra con una sintassi semplice che è:

***\[estenzione\]*** (spazio) ***\[programma\]***
dove per ***\[estenzione\]*** si intende l'estensione del files che si vuole editare (per esempio txt) e per ***\[programma\]*** il programma che si intende utilizzare
N.B.: questa procedura è valida per qualsiasi associazioni (per esempio i files gzip) per cui si possono creare coppie \[estenzione|programma\] secondo necessità ma si consiglia di andare per passi per evitare di incorrere in errori con conseguente difficoltà ad identificarli
Il ***\[programma\]*** deve essere inserito con tutta la sua path e nonostante la guida reciti di inserirlo tra apici " " io ho provato anche senza con lo stesso risultato.
Di seguito alcuni esempi utilizzando gedit come editor di default per i file più comuni
xml /usr/bin/gedit
php /usr/bin/gedit
css /usr/bin/gedit
txt /usr/bin/gedit

<Categoria:Internet> [Categoria:Programmazione e Sviluppo](Categoria:Programmazione_e_Sviluppo "wikilink") [Categoria:Scrittura in corso](Categoria:Scrittura_in_corso "wikilink")
