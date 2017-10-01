\_\_TOC\_\_ La procedura seguente permetterà di installare un simpatico quanto leggero ed efficiente player musicale per linea di comando:
MOC - Music On Console

Operazioni preliminari
----------------------

Controllare di avere gli strumenti di sviluppo installati, in caso negativo dare un:

`$ su`
`password_di_root`
`# yum groupinstall "Strumenti di sviluppo"`

installare le librerie di sviluppo riguardanti i codecs e le librerie grafiche ncurses:

`# yum install ncurses-*`
`# yum install flac-devel libsamplerate-devel curl-devel libsndfile-devel speex-devel ffmpeg-devel`
`# yum install libmad-devel libid3tag-devel libmpcdec-devel taglib-devel libogg-devel libvorbis-devel  `

fare la seguente modifica al sistema mediante link simbolici:

`# ln -s /usr/include/ffmpeg/libavformat/avformat.h /usr/include/ffmpeg/avformat.h`
`# ln -s /usr/include/ffmpeg/libavformat/avio.h /usr/include/ffmpeg/avio.h`
`# ln -s /usr/lib/libavcodec.so.52 /usr/lib/libavcodec.so`
`# exit`

Installazione
-------------

Scaricare i sorgenti (si tratta della versione stabile):

`$ wget `[`http://downloads.sourceforge.net/project/moc/moc%20stable/2.4.4/moc-2.4.4.tar.bz2`](http://downloads.sourceforge.net/project/moc/moc%20stable/2.4.4/moc-2.4.4.tar.bz2)

quindi:

`$ tar xfj moc-2.4.4.tar.bz2`
`$ cd moc-2.4.4`
`$ ./configure`
`$ make`

infine da root:

`$ su`
`password_di_root`
`# make install`
`# exit`

Lanciare il player
------------------

`$ mocp`

se si ha bisogno di ulteriori informazioni su moc rimando alle pagine

`$ man mocp`

oppure al sito di sviluppo : <http://moc.daper.net/>

Buon ascolto con moc.

<Categoria:Multimedia>
