### Visualizzare LV attivi

Per visualizzare la lista di tutti i LV attivi basterà utilizzare il comando lvs o lvscan (per far rieseguire il check della lista in precedenza in cache).

    [root@cellopc ~]# lvs
      LV      VG      Attr   LSize  Origin Snap%  Move Log Copy%  Convert
      lv_data vg_data -wi-ao 62.47G                                      
      lv_root vg_root -wi-ao 43.95G                                      
      lv_swap vg_root -wi-ao  4.88G                                      

    [root@cellopc ~]# lvscan
      ACTIVE            '/dev/vg_data/lv_data' [62.47 GB] inherit
      ACTIVE            '/dev/vg_root/lv_root' [43.95 GB] inherit
      ACTIVE            '/dev/vg_root/lv_swap' [4.88 GB] inherit

### Visualizzare informazioni di un LV

Per visualizzare i dettagli di un particolare LV basterà utilizzare il comando lvdisplay.

    [root@cellopc ~]# lvdisplay /dev/vg_data/lv_data
      --- Logical volume ---
      LV Name                /dev/vg_data/lv_data
      VG Name                vg_data
      LV UUID                TorkOs-CX97-AIbY-2ybE-F1cA-T6gr-01arHO
      LV Write Access        read/write
      LV Status              available
      # open                 1
      LV Size                62.47 GB
      Current LE             15992
      Segments               1
      Allocation             inherit
      Read ahead sectors     auto
      - currently set to     256
      Block device           253:0

Per visualizzare informazioni sul tipo di gestione dei LE basterà utilizzare l'opzione "-m".

    [root@cellopc ~]# lvdisplay -m /dev/vg_data/lv_data
      --- Logical volume ---
      LV Name                /dev/vg_data/lv_data
      VG Name                vg_data
      LV UUID                TorkOs-CX97-AIbY-2ybE-F1cA-T6gr-01arHO
      LV Write Access        read/write
      LV Status              available
      # open                 1
      LV Size                62.47 GB
      Current LE             15992
      Segments               1
      Allocation             inherit
      Read ahead sectors     auto
      - currently set to     256
      Block device           253:0
       
      --- Segments ---
      Logical extent 0 to 15991:
        Type        linear
        Physical volume /dev/sda3
        Physical extents    0 to 15991

### Creare un LV

Per poter creare un LV verificare che sul VG che ci sia dello spazio disponibile. Successivamente, passare il nome del VG dove creare il LV con l'opzione "-n". Per la dimensione del LV si potrà utilizzare l'opzione "-L" specificando la dimensione in MB, GB, KB o TB, mentre con l'opzione "-l" si potrà specificare la dimensione in percentuale.

    [root@localhost ~]# lvcreate -L 1024M vg_test -n lv_test1
      Logical volume "lv_test1" created

    [root@localhost ~]# lvcreate -l +100%FREE vg_test -n lv_test2
      Logical volume "lv_test2" created

### Eliminare un LV

Per eliminare un LV si dovrà invocare il comando lvremove, ricordandosi prima di eliminare di spostare i dati utili in esso contenuti.

    [root@localhost ~]# lvremove /dev/vg_test/lv_test2
      Logical volume "lv_test2" removed

### Espandere un LV

Per poter espandere un LV per prima cosa verificare che ci sia dello spazio disponibile su un VG. In seguito, utilizzare il comando lvextend utilizzando le opzioni "-l" e "-L" come nel comando lvcreate. È possibile utilizzare anche il comando lvresize.

    [root@vrhel5 ~]# lvextend -l +100%FREE /dev/VolGroup00/LogVol02
      Extending logical volume LogVol02 to 1.97 GB
      Logical volume LogVol02 successfully resized

### Ridurre un LV

Per poter ridurre un LV per prima cosa verificare che sia stato ridimensionato l'eventuale filesystem contenuto. Successivamente, utilizzare il comando lvreduce con le opzioni "-l" e "-L" come nel comando lvcreate. È possibile utilizzare anche il comando lvresize.

    [root@vrhel5 ~]# lvreduce -L 1G /dev/VolGroup00/LogVol02
      WARNING: Reducing active logical volume to 1.00 GB
      THIS MAY DESTROY YOUR DATA (filesystem etc.)
    Do you really want to reduce LogVol02? [y/n]: y
      Reducing logical volume LogVol02 to 1.00 GB
      Logical volume LogVol02 successfully resized

### Ricaricare i metadata di un LV

Per ricaricare a caldo i metadata di un LV basterà lanciare il comando lvchange con l'opzione --refresh.

    [root@cellopc ~]# lvchange --refresh /dev/vg_data/lv_data 

<Categoria:LVM>
