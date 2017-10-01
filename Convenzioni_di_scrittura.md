Creare una nuova pagina
-----------------------

Per creare una nuova pagina esistono vari modi:

-   creare un link su una pagina esistente: per farlo è necessario includere il nome del link tra due parentesi quadre, come in questo \[\[esempio\]\]. Verrà creato un link rosso, che porterà ad una nuova pagina:
-   scrivere il titolo della nuova pagina direttamente nella barra degli indirizzi del browser. Per esempio è possibile sostituire nell'indirizzo di <http://doc.fedoraonline.it/wiki/Contribuisci> la parola &lt;&lt; Contribuisci &gt;&gt; con il titolo della nuova pagina da creare;
-   una buona guida dovrebbe iniziare con una introduzione, nella quale si presenta l'argomento e lo scopo della stessa. A questo scopo è bene iniziare con una sezione == Introduzione ==;
-   le fonti utilizzate vanno inserite in fondo alla pagina, raccogliendole sotto la voce == Bibliografia ==:
-   è preferibile non superare il quarto livello nelle sezioni dell'articolo, come specificato più avanti;
-   non abbiamo problemi di spazio, per cui occorre evitare abbreviazioni o parole sincopate: non verranno accettati;
-   è buona norma inserire le specifiche tecniche all’inizio della guida, come la versione Fedora utilizzata o qualche specifica hardware;
-   è **obbligatorio inserire la categoria finale di destinazione**, oltre a quella di appartenenza durante la scrittura (da fare, in corso, terminata), altrimenti la guida non sarà accessibile dalla pagina principale.

Impostazione base di un nuovo articolo
--------------------------------------

A meno di esigenze particolari uno schema base per la stesura di un nuovo articolo è il seguente:

``
`{{InCorso|autore=NomeRedattore}}`
`{{Autore|NomeAutore}}`
``
`== Introduzione ==`
``
`== Titolo 1 ==`
`Scrivi qui il contenuto dell’articolo.`
``
`== Riferimenti ==`
`* riferimento 1;`
`* riferimento 2.`
``
`[[:Categoria:Uno]]`
`[[:Categoria:Due]]`
``
`[[Categoria:Scrittura in corso]]`

Una volta che la guida è terminata, sarà sufficiente rimuovere il template “InCorso”, togliere la categoria “Scrittura in corso” e cancellare il “:” davanti alle categorie finali per pubblicare l’articolo definitivamente.

<Categoria:FedoraOnline>

Toolbar
-------

Dando un primo sguardo alla pagina risaltano, sul bordo superiore dell'area di scrittura, i tasti con i quali si avrà molto a che fare e che saranno molto utili durante la scrittura (la toolbar).
![toolbar](toolbar.jpg "fig:toolbar")
Lo scopo dei tasti è molto intuitiva ma è necessario comunque fornire una breve spiegazione:

|                                                                  |                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------------------------------------------------------|------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](toolbar_bold.jpg "toolbar_bold.jpg")                         | grassetto                                | **selezionare la frase, premere il pulsante e l'output risulterà essere grassetto**                                                                                                                                                                                                                                                                                                                                                  |
| ![](toolbar_italic.jpg "toolbar_italic.jpg")                     | corsivo                                  | *selezionare la frase, premere il pulsante e l'output risulterà essere in corsivo*                                                                                                                                                                                                                                                                                                                                                   |
| ![](toolbar_internal_link.jpeg "toolbar_internal_link.jpeg")     | link interno                             | prememere il pulsante e creare un link alla pagina del wiki che si vuole richiamare come la [Pagina\_principale](Pagina_principale "wikilink")                                                                                                                                                                                                                                                                                       |
| ![](toolbar_external_link.jpeg "toolbar_external_link.jpeg")     | link esterno                             | premere il pulsante e creare un link ad una pagina sul web che si vuole richiamare come [fedoraonline](http://www.fedoraonline.it) (occorre però ricordare, a parte il suffisso <http://> prima del www del sito, di inserire, dopo uno spazio, il nome del link, altrimenti comparirà l'indirizzo in forma di numerazione dei collegamenti della pagina, come in questo caso: [1](http://www.fedoraonline.it)).                     |
| ![](toolbar_header.jpeg "toolbar_header.jpeg")                   | modificare la formattazione in un titolo | <span style="font-size: 16px"> **selezionare la frase, premere il pulsante e la l'output risulterà essere un titolo (inserisce la possibilità di modifica del paragrafo e un "a capo" automatico)** </span>                                                                                                                                                                                                                          |
| ![](toolbar_image.jpeg "toolbar_image.jpeg")                     | caricare una immagine                    | selezionare il pulsante ed inserire il nome dell'immagine in questo formato: <font color=red><File:Esempio.jpg></font>, selezionando poi il link rosso (che evidenzia l'assenza del file), si avrà la possibilità di caricarla sul server prelevandola dal proprio computer. Per avere una panoramica sul posizionamento e sul formato delle immagini, si può leggere [questo documento](http://www.mediawiki.org/wiki/Help:Images). |
| ![](toolbar_media.jpeg "toolbar_media.jpeg")                     | caricare un file in formato media        | selezionare il pulsante ed inserire il nome del file media in questo formato: <font color=red>Media:Esempio.ogg</font>, selezionando poi il link rosso (che evidenzia l'assenza del file), si avrà la possibilità di caricarlo sul server prelevandolo dal proprio computer.                                                                                                                                                         |
| ![](toolbar_non_formatted.jpeg "toolbar_non_formatted.jpeg")     | inserire del testo non formattato        | da così "***selezionare la frase e premere il pulsante per toglierne la formattazione***" a così "selezionare la frase e premere il pulsante per toglierne la formattazione"                                                                                                                                                                                                                                                         |
| ![](toolbar_signature.jpeg "toolbar_signature.jpeg")             | inserire la firma                        | selezionando il pulsante si può inserire la propria firma in formato -- username ora, giorno mese anno (UTC).                                                                                                                                                                                                                                                                                                                        |
| ![](toolbar_horizontal_line.jpeg "toolbar_horizontal_line.jpeg") | inserire una linea orzzontale            | per inserire una linea orizzontale nella riga successiva, premere il pulsante e, come in questo caso, una linea separerà il testo.                                                                                                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     
                                                                                                               ------------------------------------------------------------------------                                                                                                                                                                                                                                                                                                                                                              |

Indice
------

L'indice (TOC - Table Of Contents) viene creato automaticamente nel momento in cui si inserisce nel documento almeno quattro intestazioni. Qualora si creasse la necessità di doverne creare uno con un numero di voci inferiore, occorre forzare mediawiki nel generarlo.
Nel momento in cui si crea una intestazione, in effetti si segnala a mediawiki che si sta creando un indice. In automatico questo indice viene inserito in alto a sinistra, ma è possibile variare quasi a piacimento la sua posizione.
Tutto ciò riguarda il TOC creato in automatico; ma nel caso fossero presenti meno di quattro voci, si è costretti a crearlo forzatamente, inserendo una delle seguenti "magic words" (prestare attenzione ai due underscore all'inizio ed alla fine della parola):

|                  |                                                                   |
|------------------|-------------------------------------------------------------------|
| \_\_TOC\_\_      | per posizionarlo nello stesso punto dove viene inserito il codice |
| \_\_FORCETOC\_\_ | per inserirlo nella posizione standard                            |

Vi è anche la possibilità di nascondere l'indice:

|               |                                            |
|---------------|--------------------------------------------|
| \_\_NOTOC\_\_ | nasconde il TOC e non viene più presentato |

Sezioni
-------

Sino ad ora si è visto che l'indice è il riepilogo delle intestazioni che vengono create e formattate con il tasto di intestazione di 2° livello, che non fa altro che applicare, prima e dopo la parola o la frase selezionata, un doppio segno dell'uguale (=), creando una *intestazione di 2° livello*.
Occorre cercare di evitare l'utilizzo di una *intestazione di 1°livello*, in quanto sarebbe uguale al titolo della pagina e creerebbe confusione.
Il segno uguale (=) ha in effetti una doppia funzione: quella di fomattare il testo per renderlo più evidente, e quella di inserire la parte di testo racchiusa tra essi nell'indice della pagina (vedere quanto detto in precedenza [nell'indice](Convenzioni_di_scrittura#indice "wikilink"))
Bisogna considerare al massimo 4 livelli per le sezioni e sottosezioni, contraddistinte da un numero differente di segni uguale (=):

|                         |
|:-----------------------:|
|    `==livello` `1==`    |
|   `===livello` `2===`   |
|  `====livello` `3====`  |
| `=====livello` `4=====` |

Il risultato è una pagina avente un indice composto dai vari livelli di intestazione: le sezioni, le sotto-sezioni e un ulteriore livello di sotto-sezioni.

Formattazione
-------------

Nella [ toolbar](Convenzioni_di_scrittura#Toolbar "wikilink") è stato spiegato come si formatta in grassetto, in corsivo, in entrambi oppure con nessuna formattazione perciò crediamo che, a questo punto, già si abbia tutti gli strumenti per poter procedere con la scrittura.
Per essere solo un po' più precisi e se proprio non si vuole ricorrere al tasto della toolbar, si deve sapere che esso non fa altro che aggiungere degli apici (') all'inizio ed alla fine della parola o frase che si vuole formattare (tranne nel caso di nessuna formattazione dove viene preposto il comando di markup &lt;nowiki&gt;, che viene poi chiuso, dopo la parola o frase, con il classico </nowiki>.
Nella tabella successiva è riportato qualche esempio di formattazione e il loro risultato:

| markup                          | sorgente                             | visualizzato                                                             |
|---------------------------------|--------------------------------------|--------------------------------------------------------------------------|
| doppio apice                    | ''corsivo''                          | *corsivo*                                                                |
| triplo apice                    | '''grassetto'''                      | **grassetto**                                                            |
| quintuplo apice (2+3)           | '''''corsivo e grassetto'''''        | ***corsivo e grassetto***                                                |
| &lt;nowiki&gt; </nowiki>        | &lt;nowiki&gt;nessuno stile</nowiki> | nessuno stile                                                            |
| linea orizzontale               | ----                                 |                                                                          
                                                                                                                                                    
                                                                          ------------------------------------------------------------------------  |
| uno spazio vuoto ad inizio riga | \[barra spaziatrice\]                | # cat /boot/grub/grub.conf (comando dato da root)                        
                                                                              $ ls -al (comando dato da utente)                                     |

Collegamenti
------------

I collegamenti possono essere di diversi tipi ma, fondamentalmente i due presenti nella [toolbar](Convenzioni_di_scrittura#Toolbar "wikilink") sono quelli fondamentali e quelli su ci si dovrà basare per la scrittura degli articoli.
Nella tabella qui sotto è proposto uno schema a cui ci si può riferire nel momento in cui si volesse personalizzare i link.

| descrizione                 | sorgente                                                   | visualizzato                                                  |
|-----------------------------|------------------------------------------------------------|---------------------------------------------------------------|
| Link interno                | `[[Pagina` `principale]]`                                  | [Pagina principale](Pagina_principale "wikilink")             |
| Link a categorie            | `[[:Categoria:Fedoraonline]]`                              | [:Categoria:FedoraOnline](:Categoria:FedoraOnline "wikilink") |
| Link con nome               | `[[Pagina` `principale|vai` `alla` `pagina` `principale]]` | [vai alla pagina principale](Pagina_principale "wikilink")    |
| Link a sezioni della pagina | `[[#toolbar]]`                                             | [\#Toolbar](#Toolbar "wikilink")                              |
| Link esterni                | `http://fedoraonline.it`                                   | <http://fedoraonline.it>                                      |
| Link a file                 | `[[media:toolbar.jpg]]`                                    | <media:toolbar.jpg>                                           |
| Link esterni,               
 con titolo                   | `[http://fedoraonline.it` `FOL]`                           | [FOL](http://fedoraonline.it)                                 |
| Link esterni,               
 senza titolo                 | `[http://fedoraonline.it]`                                 | [2](http://fedoraonline.it)                                   |
| mailto                      | `mailto:faccio@unesempio.it`                               | [mailto:faccio@unesempio.it](mailto:faccio@unesempio.it)      |
| mailto senza titolo         | `[mailto:faccio@unesempio.it]`                             | [3](mailto:faccio@unesempio.it)                               |
| mailto con titolo           | `[mailto:faccio@unesempio.it]`                             | [esempio](mailto:faccio@unesempio.it)                         |
| redirect                    | `#REDIRECT` `[[Pagina` `principale]]`                      | → [Pagina principale](Pagina_principale "wikilink")           |

Immagini
--------

Per quanto concerne le immagini, il wiki offre diverse possibilità di posizionamento e dimensione. Alcune non saranno consentite per motivi inerenti alle difficoltà di sistemazione perciò, per poter ottenere un documento razionale e ben impostato si dovrà utilizzare solo il codice che indicato in questa guida. E' già stato stabilito che utilizzando il pulsante della toolbar, viene richiesto il nome dell'immagine che successivamente si andrà a caricare, il cui relativo codice è

    [[File:Esempio.jpg]]

tuttavia per dare un nome all'immagine quando il mouse ci passa sopra, occorre completare quel codice con un simbolo del pipe (|) seguito dal nome, così

    [[File:Esempio.jpg | nome_da_mostrare]]

| descrizione                                         | sorgente                                                | visualizzato                                                                   |
|-----------------------------------------------------|---------------------------------------------------------|--------------------------------------------------------------------------------|
| Immagine a grandezza normale con nome               | `[[File:Esempio.jpg|nome_da_mostrare]]`                 | ![Banner Fedora](Banner.jpg "Banner Fedora")                                   |
| Thumbnail con nome (posizione left, right o center) | `[[File:Esempio.jpg|thumb|` `center|nome_da_mostrare]]` | <img src="Banner.jpg" title="Banner Fedora" alt="Banner Fedora" width="100" /> |
| Immagine ridotta con nome                           | `[[File:Esempio.jpg|50px|nome_da_mostrare]]`            | <img src="Banner.jpg" title="Banner Fedora" alt="Banner Fedora" width="50" />  |
| Thumbnail ridotta con nome                          | `[[File:Esempio.jpg|thumb|50px|` `nome_da_mostrare]]`   | <img src="Banner.jpg" title="Banner Fedora" alt="Banner Fedora" width="50" />  |
||

Tabelle
-------

Per inserire una tabella all'interno dell'articolo, è previsto un preciso markup.
Innanzitutto la tabella inizia sempre con un {| all'inizio di una nuova riga.
Se si volessero mettere dei titoli alla tabella, è necessario che inserire il !, uno per ogni colonna della tabella e sempre seguendo la logica dell'andare a capo ad ogni markup.
Occorre, poi, segnalare all'interprete che si vuole iniziare una riga e ciò si fa con |- (ricordati che anch'esso deve essere su una nuova riga. Infine bisogna scrivere il contenuto delle celle della tabella e, per questo, a capo, occorre usare |, per ogni contenuto sulla medesima riga. Se poi si deve cominciare una nuova riga bisogna riprendere |- e per ogni contenuto |.
Proseguire così fino alla fine della tabella, che dovrà poi essere chiusa con |}
Facendo l'esempio delle convenzioni usate per questo articolo, la tabella si presenta così:

| descrizione                                       | sorgente          | visualizzato                                               |
|---------------------------------------------------|-------------------|------------------------------------------------------------|
| Tabella con titoli e bordo, allineamento centrato | {|border="1"      
                                                     |-                 
                                                     !descrizione       
                                                     !sorgente          
                                                     !visualizzato      
                                                     |-                 
                                                     |riga 1 colonna 1  
                                                     |riga 1 colonna 2  
                                                     |riga 1 colonna 3  
                                                     |-                 
                                                     |riga 2 colonna 1  
                                                     |riga 2 colonna 2  
                                                     |riga 2 colonna 3  
                                                     |}                 | | descrizione      | sorgente         | visualizzato     | 
                                                                         |------------------|------------------|------------------|  
                                                                         | riga 1 colonna 1 | riga 1 colonna 2 | riga 1 colonna 3 |  
                                                                         | riga 2 colonna 1 | riga 2 colonna 2 | riga 2 colonna 3 |  |

Diciamo pure che questa è l'unica tipologia di tabella da poter utilizzare, anche se in giro per la rete è possibile trovare diversi esempi per qualsiasi tipo di formato, utilizzando anche attributi html o convenzioni css. L'unico attributo di cui si potrebbe aver bisogno nella redazione di documentazione su Fedora OnLine, è "colspan" per unire una o più colonne e "align" per impostarne l'allineamento:

| descrizione                                                                | sorgente                                          | visualizzato                                                   |
|----------------------------------------------------------------------------|---------------------------------------------------|----------------------------------------------------------------|
| Tabella con titoli e bordo, allineamento centrato e raggruppamento colonne | {|border="1"                                      
                                                                              |-                                                 
                                                                              !descrizione                                       
                                                                              !sorgente                                          
                                                                              !visualizzato                                      
                                                                              |-                                                 
                                                                              |riga 1 colonna 1                                  
                                                                              |riga 1 colonna 2                                  
                                                                              |riga 1 colonna 3                                  
                                                                              |-                                                 
                                                                              |colspan="2" align="center"| riga 2 colonna 1 e 2  
                                                                              |riga 2 colonna 3                                  
                                                                              |}                                                 | | descrizione          | sorgente         | visualizzato     | 
                                                                                                                                  |----------------------|------------------|------------------|  
                                                                                                                                  | riga 1 colonna 1     | riga 1 colonna 2 | riga 1 colonna 3 |  
                                                                                                                                  | riga 2 colonna 1 e 2 | riga 2 colonna 3 |                     |

Infine potresti aver bisogno dei titoli in orizzontale, anzichè in verticale:

| descrizione                                                                            | sorgente                                          | visualizzato                                                                  |
|----------------------------------------------------------------------------------------|---------------------------------------------------|-------------------------------------------------------------------------------|
| Tabella con titoli orizzontali e bordo, allineamento centrato e raggruppamento colonne | {|border="1"                                      
                                                                                          |-                                                 
                                                                                          !descrizione                                       
                                                                                          |riga 1 colonna 1                                  
                                                                                          |riga 1 colonna 2                                  
                                                                                          |riga 1 colonna 3                                  
                                                                                          |-                                                 
                                                                                          !sorgente                                          
                                                                                          |riga 2 colonna 1                                  
                                                                                          |riga 2 colonna 2                                  
                                                                                          |riga 2 colonna 3                                  
                                                                                          |-                                                 
                                                                                          !visualizzato                                      
                                                                                          |colspan="2" align="center"| riga 3 colonna 1 e 2  
                                                                                          |riga 3 colonna 3                                  
                                                                                          |}                                                 | | descrizione  | riga 1 colonna 1     | riga 1 colonna 2 | riga 1 colonna 3 | 
                                                                                                                                              |--------------|----------------------|------------------|------------------|  
                                                                                                                                              | sorgente     | riga 2 colonna 1     | riga 2 colonna 2 | riga 2 colonna 3 |  
                                                                                                                                              | visualizzato | riga 3 colonna 1 e 2 | riga 3 colonna 3 |                     |

Liste
-----

Qualora si avesse la necessità di elencare una lista da non formattare come nelle [sezioni](#Sezioni "wikilink"), si possono utilizzare dei markup specifici che possono aiutare nell'elencare senza farle rientrare nell'indice:

| markup                                                                                                                                     | sorgente                              | visualizzato                             |
|--------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|------------------------------------------|
| L'asterisco segnala il primo livello della lista, aumentando il numero di asterischi aumenta la sua profondità.                            | \* livello iniziale                   
                                                                                                                                              \*\* primo punto del secondo livello   
                                                                                                                                              \*\* altro punto del secondo livello   
                                                                                                                                              \*\*\* terzo livello livello           
                                                                                                                                              \*\*\*\* ecc.                          | -   livello iniziale                     
                                                                                                                                                                                          -   primo punto del secondo livello   
                                                                                                                                                                                          -   altro punto del secondo livello   
                                                                                                                                                                                              -   terzo livello                 
                                                                                                                                                                                                  -   ecc.                      |
| Il cancelletto segnala il primo livello della lista, aumentando il numero di cancelletti aumenta la sua profondità.                        | \# primo punto                        
                                                                                                                                              \#\# primo sottopunto del punto uno    
                                                                                                                                              \#\# secondo sottopunto del punto uno  
                                                                                                                                              \# secondo punto                       
                                                                                                                                              \#\# primo sottopunto del punto due    
                                                                                                                                              \#\# secondo sottopunto del punto due  
                                                                                                                                              \# terzo punto                         
                                                                                                                                              \# ecc.                                | 1.  primo punto                          
                                                                                                                                                                                          1.  primo sottopunto del punto uno    
                                                                                                                                                                                          2.  secondo sottopunto del punto uno  
                                                                                                                                                                                                                                
                                                                                                                                                                                      2.  secondo punto                         
                                                                                                                                                                                          1.  primo sottopunto del punto due    
                                                                                                                                                                                          2.  secondo sottopunto del punto due  
                                                                                                                                                                                                                                
                                                                                                                                                                                      3.  terzo punto                           
                                                                                                                                                                                      4.  ecc.                                  |
| La combinazione del punto e virgola(;) per i titoli con i due punti(:) per gli argomenti, permette la creazione di elenchi con tabulazioni | ;primo titolo                         
                                                                                                                                              : primo argomento del primo titolo     
                                                                                                                                              : secondo argomento del primo titolo   
                                                                                                                                              : terzo argomento del primo titolo     
                                                                                                                                              ;secondo titolo                        
                                                                                                                                              : primo argomento del secondo titolo   
                                                                                                                                              ;terzo titolo                          
                                                                                                                                              : primo argomento del terzo titolo     
                                                                                                                                              : secondo argomento del terzo titolo   
                                                                                                                                              ;ecc.                                  | primo titolo                             
                                                                                                                                                                                      primo argomento del primo titolo          
                                                                                                                                                                                                                                
                                                                                                                                                                                      secondo argomento del primo titolo        
                                                                                                                                                                                                                                
                                                                                                                                                                                      terzo argomento del primo titolo          
                                                                                                                                                                                                                                
                                                                                                                                                                                      secondo titolo                            
                                                                                                                                                                                      primo argomento del secondo titolo        
                                                                                                                                                                                                                                
                                                                                                                                                                                      terzo titolo                              
                                                                                                                                                                                      primo argomento del terzo titolo          
                                                                                                                                                                                                                                
                                                                                                                                                                                      secondo argomento del terzo titolo        
                                                                                                                                                                                                                                
                                                                                                                                                                                      ecc.                                      |

Categorie
---------

Al fine di poter catalogare e indicizzare correttamente le guide e gli articoli, come visto nell'articolo [ come contribuire](Contribuisci#Processo_per_la_creazione_o_la_modifica_di_un_nuovo_articolo "wikilink"), è necessario che venga inserita la categoria corretta dell'articolo in fondo alla pagina.
Il markup è esattamente quello riportato:

    [[:Categoria:Uno]]
    [[:Categoria:Due]]

    [[Categoria:Scrittura in corso]]

e, una volta terminato la guida sarà sufficiente togliere la categoria “Scrittura in corso” e cancellare il “:” davanti alle categorie finali per pubblicare l’articolo definitivamente.
Per definire la categoria, occorre seguire il processo di registrazione alla Mailing List di FedoraOnLine e seguire le istruzioni, come spiegato nella pagina [come contribuire](Contribuisci#Registrati_alla_Mailing_List_del_Wiki "wikilink").

Riferimenti
-----------

E' sempre bene citare la fonte ed eventuali pagine di approfondimenti che hanno contribuito alla redazione dell'articolo o guida, nonchè, qualora fossero stati usati i numeri di rimando per le note a piè di pagina, creare i relativi riferimenti. Utilizzando la combinazione tra i [ collegamenti](#Collegamenti "wikilink") e le [liste](#Liste "wikilink"), ci si può agevolmente destreggiare per compilare una lista di riferimenti davvero ben organizzata.

Modifiche
---------

Per quanto riguarda le modifiche all'articolo, è molto importante che venga avvisato il resto dell'utenza del fatto che l'articolo è in fase di modifica. Come sottolineato nella guida su [come contribuire](Contribuisci#Scrittura_in_corso "wikilink"), ciò deve avvenire utilizzando il template "InCorso", indicandone anche il nome di colui che redige la modifica o la revisione:

    {{InCorso|autore=NomeAutore}}

Esempio:

In questo caso il link è rosso perchè non esiste un utente *NomeAutore*.

<Categoria:FedoraOnline>

Redirect
--------

In alcune occasioni potrebbe esserci la necessità di cancellare un articolo in sostituzione di un'altra pagina. Nell'ambito di un'enciclopedia libera come la documentazione FOL questa procedura viene sconsigliata e viene preferito un reindirizzamento della vecchia pagina verso quella nuova.
Prima di effettuare un redirect vanno avvisati tutti i redattori attraverso la [Mailing List](Contribuisci#Registrarsi_alla_Mailing_List_del_Wiki "wikilink"), dove si discute e si valuta se è un'operazione necessaria da fare.
Per effettuare un redirect, ad esempio da *pagina\_1* a *pagina\_2*, si inserisce all'inizio della pagina da reindirizzare (*pagina\_1*) la seguente stringa:

    #REDIRECT [[pagina_2]]

Una volta fatto, qualunque altro contenuto presente in *pagina\_1* verrà ignorato e si verrà reindirizzati a *pagina\_2*.
La pagina\_1 sarà comunque sempre accessibile per eventuali modifiche aggiungendo nella barra degli indirizzi la variabile "redirect" impostata su "no" come nell'esempio seguente:

[`http://doc.fedoraonline.it/Convenzioni_di_scrittura/Esempio?redirect=no`](http://doc.fedoraonline.it/Convenzioni_di_scrittura/Esempio?redirect=no)

I template
----------

Sul wiki di Fedora Ondine sono disponibili una serie di template per facilitare la scrittura. Consultare [l’elenco dei template disponibili](:Categoria:Template "wikilink") per maggiori informazioni.
Di seguito qualche esempio sull’utilizzo dei template:

### Autore/i della guida

Per identificare l’autore della guida è opportuno inserire il suo nome:

`{{Autore|NomeAutore}}`

Questo creerà in automatico un link alla pagina personale dell’autore stesso.
E' bene assicurarsi che all’inizio della pagina sia presente questo template. Esempio:

### Collaboratori

Oltre all’autore si possono inserire anche i collaboratori. La sintassi è simile a quella degli autori:

`{{Collaboratori|NomeCollaboratore}}`

Esempio:

### Obsoleto

Per far notare a tutti i lettori che una pagina potrebbe non funzionare più a causa di problemi di obsolescenza, è disponibile il template:

`{{Obsoleto}}`

che produce questo risultato:

### Scrittura in corso

Ogni nuova guida in corso di stesura o in corso di modifica deve essere distinta con il template “InCorso”.

Oltre al messaggio per l’utente che legge, verrà creato un link alla pagina personale dell’autore della stesura o modifica.

`{{InCorso|autore=NomeAutore}}`

Esempio:

### Nota

Per inserire una nota all’interno di un articolo occorre utilizzare questo template:

`{{nota|Titolo della nota|Testo della nota}}`

Esempio:

### Suggerimento

Per inserire un suggerimento all’interno di un articolo occorre utilizzare questo template:

`{{suggerimento|Testo del suggerimento}}`

Esempio:

### Avviso importante

Se si vuole inserire un appunto importante o si vuole attirare l’attenzione del lettore a una specifica particolare, è necessario utilizzare il template "Warning":

`{{Warning|Testo dell'avviso}}`

La sintassi è molto semplice e non necessita di ulteriori commenti. Esempio:

### Convenzioni di scrittura

Per inserire il template per alcune convenzioni di scrittura all’interno dell’articolo, utilizzate:

`{{Scrittura|Regole e convenzioni di scrittura}}`

Questo template è da posizionare all’interno dell’introduzione per informare il lettore fin da subito della convenzione stessa. Esempio:
