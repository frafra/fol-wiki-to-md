A differenza delle versioni precedenti, il file di configurazione di **X** in fedora core 6 è piuttosto scarno:

        # Xorg configuration created by system-config-display

        Section "ServerLayout"
        Identifier "single head configuration"
        Screen 0 "Screen0" 0 0
        InputDevice "Keyboard0" "CoreKeyboard"
        EndSection

        Section "Files"
        ModulePath "/usr/lib/xorg/modules"
        EndSection

        Section "InputDevice"
        Identifier "Keyboard0"
        Driver "kbd"
        Option "XkbModel" "pc105"
        Option "XkbLayout" "it"
        EndSection

        Section "Device"
        Identifier "Videocard0"
        Driver "nv"
        EndSection

        Section "Screen"
        Identifier "Screen0"
        Device "Videocard0"
        DefaultDepth 24
        SubSection "Display"
        Viewport 0 0
        Depth 24
        Modes "1024x768" "800x600" "640x480"
        EndSubSection
        EndSection

Essendo la TNT2 una scheda datata, non viene supporata che dai driver della serie 7 (siano essi proprietari che presenti nel repo livna), con grande disappunto perchè non si può utilizzare freshrpms che offre una gestione dei moduli del kernel meno "impegnativa" con dkms.
Tant'è che, per comodità, non si farà uso in questa miniguida dei moduli proprietari dal sito NVidia, bensì quelli presenti su *livna*.

1.  Fare una copia di backup del xorg.conf originale, secondo il solito sistema:
        cp /etc/X11/xorg.conf /etc/X11/xorg.confBKP

2.  Verificare che la propria scheda video sia riconosciuta (anche se vedendo il driver "nv" impostato automaticamente nel file xorg.conf, sicuramente viene rilevata correttamente).
        # lspci | grep -i vga
        01:00.0 VGA compatible controller: nVidia Corporation NV5M64 [RIVA TNT2 Model 64/Model 64 Pro] (rev 15)

3.  La TNT2 è supportata fino al driver della serie 7, per cui se si digita:
        # yum --disablerepo=* --enablerepo=livna list available kmod-nvidia

    si riceverà questo output:

        Available Packages
        kmod-nvidia.i686                         1.0.9746-1.2.6.19_1.28 livna
        kmod-nvidia.i586                         1.0.9746-1.2.6.19_1.28 livna

    e non vanno bene, allora si farà:

        # yum --disablerepo=* --enablerepo=livna list available kmod-nvidia-legacy

    presenta:

        Available Packages
        kmod-nvidia-legacy.i686                  1.0.7184-3.2.6.19_1.28 livna

    per cui si installano con:

        # yum install kmod-nvidia-legacy

    Attendere ovviamente che yum faccia il suo lavoro installando sia i driver che le relative dipendenze.

4.  Se si dovesse provare adesso ad uscire e rientrare in **X**, ci si troverebbe con la spiacevolissima sorpresa che non funzioni più nulla, per cui bisogna andare a modificare il file xorg.conf per fare in modo che non succeda.
    Ecco il file xorg.conf modificato:
            # Xorg configuration created by system-config-display

            Section "ServerLayout"
            Identifier "single head configuration"
            Screen 0 "Screen0" 0 0
            InputDevice "Keyboard0" "CoreKeyboard"
            EndSection

            Section "Files"

            ModulePath "/usr/lib/xorg/modules/extensions/nvidia"
            ModulePath "/usr/lib/xorg/modules"
            EndSection

            Section "Module"

            Load "extmod"
            Load "fbdevhw"
            Load "freetype"
            Load "type1"
            Load "glx"
            EndSection

            Section "InputDevice"
            Identifier "Keyboard0"
            Driver "kbd"
            Option "XkbModel" "pc105"
            Option "XkbLayout" "it"
            EndSection

            Section "Monitor"

            Identifier "Monitor0"
            ModelName "Monitor 1024x768"
            HorizSync 31.5 - 57.0
            VertRefresh 50.0 - 70.0
            Option "dpms"
            EndSection

            Section "Device"

            # Option "NoLogo" "false"
            Identifier "Videocard0"
            Driver "nvidia"
            VendorName "nVidia Corp."
            BoardName "NVIDIA RIVA TNT2 64 Pro"
            Option "AddARGBGLXVisuals" "True"
            EndSection

            Section "Screen"
            Identifier "Screen0"
            Device "Videocard0"
            Monitor "Monitor0"
            DefaultDepth 24
            SubSection "Display"
            Depth 24
            Modes "1024x768" "800x600" "640x480"
            EndSubSection
            EndSection

            Section "DRI"
            Mode 0666
            EndSection

            Section "Extensions"
            Option "Composite" "Disable"
            EndSection

5.  Se si vuole abilitare gli effetti grafici si dovrà fare diventare l'ultima sezione così:
            Section "Extensions"
            Option "Composite" "Enable"
            EndSection

    Sparirà il direct rendering ma si potrà giocare un po' con Beryl.

6.  Provare il 3d con:
        $ glxgears

    che dà questo risultato:

        # glxgears
        1978 frames in 5.0 seconds = 395.418 FPS
        1976 frames in 5.0 seconds = 395.184 FPS
        1978 frames in 5.0 seconds = 395.588 FPS
        1977 frames in 5.0 seconds = 395.400 FPS
        1978 frames in 5.0 seconds = 395.501 FPS
        1978 frames in 5.0 seconds = 395.418 FPS

[Categoria:Schede grafiche](Categoria:Schede_grafiche "wikilink")
