Ecco come configurare una connessione wireless wpa2-psk su un portatile ACER ASPIRE 5315 con la seguente scheda integrata:

`# lspci | grep Atheros`
`06:00.0 Ethernet controller: Atheros Communications, Inc. AR5006EG 802.11 b/g Wireless PCI Express Adapter (rev 01`

(si veda anche [questa pagina](http://madwifi.org/ticket/1679) per maggiori dettagli sui drivers madwifi)

-   Inserire in black list i drivers **ath5k** già presenti nel kernel

`# echo "blacklist ath5k" >> /etc/modprobe.d/blacklist`

-   Scaricare [i drivers madwifi](http://snapshots.madwifi.org/madwifi-ng/madwifi-ng-r2756-20071018.tar.gz) e [questa patch](http://madwifi.org/attachment/ticket/1679/madwifi-ng-0933.ar2425.20071130.i386.patch?format=raw)

<!-- -->

-   Estrarre i drivers madwifi, applicare la patch ed eseguirne l'installazione

`# tar xvfz madwifi-ng-r2756-20071018.tar.gz`
`# cd madwifi-ng-r2756-20071018`
`# patch -p0 < ../madwifi-ng-0933.ar2425.20071130.i386.patch`
`# make`
`# make install`

-   Installare **wpa\_supplicant** e modificarne il file di configurazione **/etc/wpa\_supplicant/wpa\_supplicant.conf**

`# yum install wpa_supplicant`
`# vi /etc/wpa_supplicant/wpa_supplicant.conf # utilizzate il vostro editor preferito... a me piace il "vi"!`

il nuovo file di configurazione dovrà essere fatto in questo modo:

`ctrl_interface=/var/run/wpa_supplicant`
`ctrl_interface_group=wheel`
`network={`
`        ssid="SSID_DELLA_MIA_RETE"`
`        psk="BLA_BLA_BLA_QUESTA_E_LA_MIA_PASSKEY_BLA_BLA_BLA"`
`        key_mgmt=WPA-PSK`
`        proto=WPA2`
`        pairwise=CCMP TKIP`
`}`

...naturalmente "SSID\_DELLA\_MIA\_RETE" e "BLA\_BLA\_BLA\_QUESTA\_E\_LA\_MIA\_PASSKEY\_BLA\_BLA\_BLA" andranno modificati secondo le impostazioni del proprio access point

-   Creare lo script **/root/bin/connessione\_wireless.sh** che verrà utilizzato per attivare l'interfaccia wireless e connettersi all'access point:

`#!/bin/bash`
`ifdown eth0`
`service wpa_supplicant stop`
`wpa_supplicant -c/etc/wpa_supplicant/wpa_supplicant.conf -iwlan0 -Dwext -dd -B`
`iwconfig wlan0 key BLA_BLA_BLA_QUESTA_E_LA_MIA_PASSKEY_BLA_BLA_BLA ap MAC_ADDRESS_MIO_ACCESS_POINT \`
`essid SSID_DELLA_MIA_RETE mode Managed`
`ifconfig wlan0 MIO_IP netmask MIA_NETMASK up`
`route add default gw MIO_DEFAULT_GATEWAY`

anche in questo caso sostituire "BLA\_BLA\_BLA\_QUESTA\_E\_LA\_MIA\_PASSKEY\_BLA\_BLA\_BLA", "MAC\_ADDRESS\_MIO\_ACCESS\_POINT", "SSID\_DELLA\_MIA\_RETE", "MIA\_NETMASK" e "MIO\_DEFAULT\_GATEWAY" in base alle proprie esigenze ed assegnare ad esso i permessi corretti di esecuzione

`# chown root:root /root/bin/connessione_wireless.sh`
`# chmod 770 /root/bin/connessione_wireless.sh`

-   Riavviare il computer per verificare che al boot vengano caricati i drivers corretti:

`# shutdown -g0 -i6 -y # mi piace scriverlo così!`
`...e dopo il riavvio...`
`# lspci | grep ath`

I drivers caricati dovranno essere gli "ath\_pci" e non gli "ath5k"

-   Eseguire la connessione wireless

`# connessione_wireless.sh`

e verificarne il corretto funzionamento e le corrette impostazioni:

`# iwconfig`
`# ifconfig wlan0`
`# ping IP_ACCESS_POINT`
`# ping www.fedoraonline.it`
`# traceroute IP_DI_NON_SO_CHI`
`# ecc. ecc. ecc.`

<Categoria:Wi-Fi>
