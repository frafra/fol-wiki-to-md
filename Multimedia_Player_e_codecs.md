Introduzione
------------

Prima di cominciare è bene sapere che il Fedora Project **NON INCLUDE** tra i pacchetti ufficiali software che non sia completamente open source ed in ogni caso, **NON INCLUDE** le seguenti tipologie di software:

-   software proprietario;
-   software gravato da contenziosi legali;
-   software che viola le leggi degli Stati Uniti.

Per questi motivi, molti programmi e codecs devono essere installati prelevandoli dai repositori di terze parti (es. [RPMFusion](RPMFusion "wikilink")).
Peculiarità dei riproduttori multimediali è data dal fatto che taluni tra essi condividono plugins, codecs o librerie, per cui è difficile stabilire una procedura univoca di installazione, per cui le dipendenze potrebbero essere soddisfatte anche da altri programmi o dalla diversa sequenza di installazione. In linea di massima è utile procedere secondo la seguente logica:

1.  Installazione players audio, plugins, codecs;
2.  Installazione players video, plugins, codecs;
3.  Installazione software utile per audio e/o video.

Codecs
------

### GStreamer 0.x e GStreamer 1.x

I plugin GStreamer di solito includono la maggior parte dei codec audio-video del quale si ha bisogno. Per installarli eseguire il comando

`# dnf install gstreamer-{ffmpeg,plugins-{good,ugly,bad{,-free,-nonfree}}} gstreamer1-{plugin-mpg123,libav,vaapi,plugins-{base,bad-free{,world,-extras},good{,-extras},ugly}}`

Librerie per DVD
----------------

Librerie necessarie alla visione di dvd con contenuto protetto. Il pacchetto *libdvdcss* necessita del repository [Livna](Livna "wikilink") installato e configurato.

`# dnf --enablerepo=livna install libdvdcss libdvdread libdvdnav lsdvd`

<Categoria:Multimedia>
