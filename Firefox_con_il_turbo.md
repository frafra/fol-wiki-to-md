Questa guida è tratta dal sito [forevergeek](http://forevergeek.com/open_source/make_firefox_faster.php) e vista la netta differenza di velocità del browser Firefox si è deciso di pubblicarla qui. Naturalmente l'operazione non è senza rischio visto che si modificano alcune variabili del cuore di Firefox, ma si è notato un miglioramento di velocità. Ne vale la pena solo sui collegamenti Internet a banda larga, altrimenti lasciare tutto così com'è.
Le modifiche sono poche e si può tornare indietro in qualsiasi momento ripristinando i valori iniziali, se si vedono che le tabelle delle pagine web non vengono visualizzate in modo corretto ripristinate i valori di default.
Ora le cose da fare sono le seguenti:
Aprire il browser, digitare nella barra degli indirizzi *<about:config>* e dare l'invio.
Si apre una pagina piena di valori *true*, *false*, con numeri e il nome delle impostazioni. Con l'aiuto di Firefox "Filter" man mano cercare le impostazioni che interessano:

1.  Cercare **network.http.pipelining** e cliccare due volte sulla voce *false* in modo che assuma il valore **true**.
2.  Anche la voce **network.http.proxy.pipelining** è da impostare come **true** seguendo la procedura di prima.
3.  Cercare **network.http.pipelining.maxrequests** e impostare il valore a non più di 30, mettere **16** visto che il default è 4.
4.  Ora cliccare col tasto destro del mouse in un punto qualsiasi della pagina *<about:conf>*. Scegliere **new** dal menu e **integer**. Verrà chiesto il nome del parametro e lo si mette:

**nglayout.initialpaint.delay** e cliccando su OK si dovrebbe inserire il valore, metterlo a **0**. Questo è il tempo che il browser aspetta prima di agire sulle informazioni ricevute.
Fatto!

Se si hanno difficoltà basta cliccare sui singoli parametri col tasto destro del mouse e premete "reset" (azzera). <Categoria:Internet>
