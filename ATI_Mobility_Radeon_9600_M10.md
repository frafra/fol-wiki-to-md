Si vogliono installare i driver per la scheda video in oggetto in modo da avere l'accellerazione 3D. Ovviamente prima bisogna sapere quale essa sia.
Il comando per ottenere tale informazione è:

`# lspci `

che restituisce:

`01:00.0 VGA compatible controller: ATI Technologies Inc RV350 `
`[Mobility Radeon 9600 M10]`

Configurazione
--------------

Prima di tutto, eseguire:

`# system-config-display `

si configura il monitor come *generic LCD Panel 1024x768* Poi si passa all'installazione dei driver con:

`# yum --enablerepo=livna install xorg-x11-drv-fglrx kmod-fglrx `

Quando il processo di installazione è terminato riavviare. Dopo il login il comando: **fglrxinfo** restituisce:

`display: :0.0 screen: 0`
`OpenGL vendor string: Mesa project: www.mesa3d.org`
`OpenGL renderer string: Mesa GLX Indirect`
`OpenGL version string: 1.2 (1.5 Mesa 6.5.1)`

Il driver ATI non è attivo, per cui bisogna modificare il file xorg.conf in questo modo:

`Section "Device"`
`   Identifier "Videocard0"`
`   Driver "radeon"<<<<<------- al posto di radeon metto fglrx`
`EndSection `

Riavviare, ma al login eseguendo:

`$ fgl_glxgears`

non farà partire il classico cubo rotante con dentro gli ingranaggi che girano. Allora è necessario aggiungere nel file xorg.conf quanto segue:

    Section "ServerFlags"
       Option   "AIGLX"  "off"
    EndSection
    Section "DRI"
       Group   0
       Mode   0666
    EndSection
    Section "Extensions"
       Option   "Composite" "False"
    EndSection
    Section "Module"
       Load   "extmod"
       Load   "glx"
       Load   "dri"
    EndSection

E riavviare nuovamente. Poi si impartisce in ordine:

`# aticonfig --initial`
`# service ati-fglrx restart`
`# ati-fglrx-config-display enable`
`# fglrxinfo`

che restituisce:

`display: :0.0 screen: 0`
`OpenGL vendor string: ATI Technologies Inc.`
`OpenGL renderer string: MOBILITY RADEON 9600 Generic`
`OpenGL version string: 2.0.6174 (8.31.5)`

Adesso sembra OK.

`$ fgl_glxgears`

fa partire il cubo e questo è quello che si ottiene:

`2452 frames in 5.0 seconds = 490.400 FPS`
`2828 frames in 5.0 seconds = 565.600 FPS`
`2798 frames in 5.0 seconds = 559.600 FPS`
`2862 frames in 5.0 seconds = 572.400 FPS`
`3132 frames in 5.0 seconds = 626.400 FPS`
`3076 frames in 5.0 seconds = 615.200 FPS`
`2865 frames in 5.0 seconds = 573.000 FPS`
`3000 frames in 5.0 seconds = 600.000 FPS`
`2899 frames in 5.0 seconds = 579.800 FPS`
`2950 frames in 5.0 seconds = 590.000 FPS`

Non ci si può lamentare.

[Categoria:Schede grafiche](Categoria:Schede_grafiche "wikilink")
