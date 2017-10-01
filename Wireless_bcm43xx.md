L'installazione della scheda wireless bcm43xx è stata più volte richiesta; di seguito si riassumeranno i passi per farla funzionare.

Premetto che devo ringraziare il buon Virus il quale mi ha sempre aiutato (diciamo che ha fatto tutto lui) nell'impresa di far funzionare tale scheda. La mia scheda è stata configurata per funzionare sia in F9 che F11 (penso che anche per F10 non ci siano problemi). Se si è effettuata un'installazione tipica la scheda sarà riconosciuta dal proprio sistema ma non si sarà in grado di gestirla.

1.  Procedere a verificare che siano installati i driver in questo modo:
2.  rpm -qa | grep broadcom-wl

`broadcom-wl-5.10.91.9-1.fc11.noarch`

<li>
Se non è presente procedere con l'installazione.

</li>
**IMPORTANTE:** i repo rpm-fusion non-free non devono essere attivi.

`# yum install --disablerepo=rpmfusion-nonfree* broadcom-wl`

<li>
Procedere ora all'installazione del firmware:

</li>
`# yum install b43-fwcutter`

<li>
Scaricare il seguente pacchetto: [questo](http://mirror2.openwrt.org/sources/broadcom-wl-4.150.10.5.tar.bz2).

</li>
<li>
Scompattare ed eseguire i seguenti comandi:

</li>
`# modprobe -r b43`
`# b43-fwcutter -w /lib/firmware /home/utente/Scaricati/broadcom-wl-4.150.10.5/driver/wl_apsta_mimo.o`
`# modprobe b43`

<li>
In fine eseguire un reboot, e finalmente sarà a disposizione la scheda wireless.

</li>
</ol>
<Categoria:Wi-Fi>
