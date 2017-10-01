Introduzione
------------

Può capitare che ci sia la necessità di condividere la connessione a internet di un computer (chiamiamolo gateway) con un altro (il client), avendo a disposizione un cavo ethernet per collegare i due. I passi da fare non sono banali, soprattutto per un principiante. Nel presente articolo si vuole riassumere questi comandi in un unico script che permette di automatizzare il tutto in modo semplice e sufficientemente flessibile.

L'obiettivo
-----------

Supponiamo di avere un gateway "casalingo" (cioè un semplice PC) collegato a internet, ad esempio con un modem USB-ADSL o una chiavetta HSDPA. Tipicamente il gateway ha un'interfaccia denominata ppp0 per il collegamento tramite modem, attraverso la quale passano i pacchetti TCP/IP di rete. Non solo: il gateway ha un indirizzo IP che gli e' stato comunicato dal provider insieme ai server DNS da usare. La configurazione di rete e' dinamica perché viene comunicata al volo dal provider al momento della connessione col modem.
Se vuoi condividere la connessione internet col client e' necessario che:

1.  I due computer siano in grado di comunicare reciprocamente, devono formare cioè una piccola rete privata;
2.  Il gateway sia in grado, quando gli viene richiesto, di gestire il traffico del client da e verso internet.

Utilizzando uno schema l'obiettivo dovrebbe essere questo:

`             Rete privata                Rete pubblica`
`[ Client ]<--------------->[ Gateway ]<--------------->[ Internet ]`
`IP privato            IP privato e IP pubblico `

Il client ed il gateway devono avere ciascuno un proprio indirizzo IP nella rete che li unisce. Il gateway ha anche un secondo indirizzo IP, quello pubblico, associato all'interfaccia ppp0. Inoltre deve essere in grado di fare da "passacarte" per le richieste di rete del client, attraverso una tecnica chiamata NAT (Network Address Translation). Infatti l'indirizzo del gateway e' unico su internet, mentre i computer che devono comunicare sono due. Affinché il client possa spedire e ricevere pacchetti e' necessario che il gateway interceda, mascherando questi pacchetti come fossero suoi (e cioè associati al suo IP pubblico).

Lo script
---------

Lo script realizzato per lo scopo, denominato "icshare" (Internet Connection Share), e' il seguente:

`#!/bin/bash`
`#*****************************************************************************`
`# Internet Connection Share utility`
`#*****************************************************************************`
`# This program is primarily designed for RedHat/Fedora systems,`
`# although it should be adaptable for others.`
`#`
`# The purpose of the program is to configure a computer connected to Internet`
`# (typically using the ppp0 interface) as a gateway/dns/dhcp for computers`
`# connected to a local LAN trough a trusted interface (typically eth0).`
`#`
`# You must be root to run this script.`
`#*****************************************************************************`
`# Internet interface`
`INET_IFACE="ppp0"`
`# Local network and interface`
`LAN_IFACE="eth0"`
`LAN_IP="192.168.123.1"`
`LAN_NET="192.168.123.0/24"`
`LAN_NETMASK="255.255.255.0"`
`LAN_DHCP_RANGE="192.168.123.2,192.168.123.254"`
`# The return value of this script`
`RETVAL=0`
`exit_if_fail() {`
`    [ $1 -eq 0 ] || exit $1`
`}`
`lan_iface_up() {`
`    print_verbose "Bringing down local interface $LAN_IFACE..."`
`    ifconfig $LAN_IFACE down`
`    exit_if_fail $?`
`    print_verbose "Bringing up local interface $LAN_IFACE..."`
`    ifconfig $LAN_IFACE $LAN_IP up`
`    exit_if_fail $?`
`    [ -n "$OPT_VERBOSE" ] && ifconfig $LAN_IFACE`
`}`
`lan_iface_down() {`
`    print_verbose "Bringing down local interface $LAN_IFACE..."`
`    ifconfig $LAN_IFACE down`
`}`
`dnsmasq_start() {`
`    print_verbose "Starting dnsmasq service..."`
`    dnsmasq --interface=$LAN_IFACE \`
`        --dhcp-range=$LAN_IFACE,$LAN_DHCP_RANGE,$LAN_NETMASK,12h`
`    exit_if_fail $?`
`}`
`dnsmasq_status() {`
``   DNSMASQ_PID=`pidof dnsmasq` ``
`  if [ -n "$DNSMASQ_PID" ]; then`
`    echo "dnsmasq pid is $DNSMASQ_PID"`
`  else`
`    echo "dnsmasq is not running"`
`  fi`
`}`
`dnsmasq_stop() {`
`    print_verbose "Shutting down dnsmasq service..."`
``     kill `cat /var/run/dnsmasq.pid` ``
`}`
`iptables_setup() {`
`    print_verbose "Setting iptables rules... "`
`    # INPUT Chain`
`    # Accept broadcast from local interface (useful for DHCP)`
`    iptables -I INPUT -p ALL -i $LAN_IFACE -j ACCEPT \`
`        -m pkttype --pkt-type broadcast `
`    # Rules for the private network (accessing gateway system itself)`
`    iptables -I INPUT -p ALL -i $LAN_IFACE -s $LAN_NET -d $LAN_IP -j ACCEPT`
`    # FORWARD Chain`
`    # Route from local LAN to local LAN`
`    iptables -I FORWARD -p ALL -o $LAN_IFACE -s $LAN_NET -d $LAN_NET -j ACCEPT`
`    # Route from local LAN to Internet`
`    iptables -I FORWARD -p ALL -i $LAN_IFACE -o $INET_IFACE -s $LAN_NET -j ACCEPT`
`    # Deal with responses from the internet`
`    iptables -I FORWARD -i $INET_IFACE -o $LAN_IFACE -d $LAN_NET -j ACCEPT \`
`        -m state --state ESTABLISHED,RELATED `
`    # POSTROUTING chain`
`    iptables -A POSTROUTING -t nat -o $INET_IFACE -j MASQUERADE`
`    [ -n "$OPT_VERBOSE" ] && iptables_status`
`}`
`iptables_restore() {`
`    print_verbose "Restore iptables rules... "`
`    service iptables restart`
`    [ -n "$OPT_VERBOSE" ] && iptables_status`
`}`
`iptables_status() {`
`    iptables -n -L -v`
`}`
`ipv4_forward_set() {`
`  if [ -n "$OPT_VERBOSE" ]; then`
`     echo -n "Setting kernel parameter: "`
`     sysctl -w net.ipv4.ip_forward=$1`
`  else`
`    sysctl -n -q -w net.ipv4.ip_forward=$1`
`  fi`
`}`
`print_usage() {`
`  echo \`
`"Usage: icshare [-i,--inet-iface interface] [-l,--lan-iface interface] [-v,--verbose] \`
`{help|start|stop|status}`
`Options:`
`  -i,--inet-iface    Interface connected to Internet (default ppp0)`
`  -l,--lan-iface    Local network interface (default eth0)`
`  -v,--verbose        Print additional output messages`
`Commands:`
`  help        Print this help message`
`  start        Start the connection sharing`
`  stop        Stop the connection sharing`
`  status    Print info about the connetion sharing`
`"`
`  exit $RETVAL`
`}`
`print_verbose() {`
`  [ -n "$OPT_VERBOSE" ] && echo $*`
`}`
`# Parse options`
`` args=`getopt -u -o i:l:v -l inet-iface:,lan-iface:,verbose -- $*` ``
`RETVAL=$? && [ $RETVAL -ne 0 ] && print_usage`
`# Sets positional parameters to command?line arguments`
`set -- $args`
`for arg in $*; do`
`  case $1 in`
`    -i|--inet-iface)`
`        INET_IFACE=$2; shift;;`
`    -l|--lan-iface)`
`        LAN_IFACE=$2; shift;;`
`    -v|--verbose)`
`        OPT_VERBOSE=$1;;`
`     --)`
`        shift; break;;`
`    *)`
`        print_usage;;`
`  esac`
`  shift`
`done`
`[ -z "$1" ] && print_usage    # No command found`
`case $1 in`
`  start)`
`    lan_iface_up`
`    dnsmasq_start`
`    ipv4_forward_set "1"    `
`    iptables_setup`
`    ;;`
`  stop)    `
`    dnsmasq_stop`
`    lan_iface_down`
`    ipv4_forward_set "0"`
`    iptables_restore`
`    ;;`
`  status)`
`    dnsmasq_status`
`    iptables_status`
`    ;;`
`  help)`
`    print_usage`
`    ;;`
`  *)`
`    echo "Invalid command: $1"`
`    print_usage`
`    ;;`
`esac`
`exit $RETVAL`

Utilizzo
--------

Una volta creato il file icshare (collocalo in /root/bin) è necessario renderlo eseguibile:

`# chmod ugo+x icshare`

Lo script va eseguito sul gateway come utente root, e ha un piccolo help:

`# icshare help`
`Usage: icshare [-i,--inet-iface interface] [-l,--lan-iface interface] [-v,--verbose] {help|start|stop|status}`
`Options:`
`  -i,--inet-iface    Interface connected to Internet (default ppp0)`
`  -l,--lan-iface    Local network interface (default eth0)`
`  -v,--verbose        Print additional output messages`
`Commands:`
`  help        Print this help message`
`  start        Start the connection sharing`
`  stop        Stop the connection sharing`
`  status    Print info about the connetion sharing`

La modalità di utilizzo e' analoga a quella di yum, cioè prevede opzioni e comandi. I comandi principali sono start/stop per avviare/chiudere la condivisione della connessione.
L'opzione *-i* serve per specificare l'interfaccia della rete pubblica, quella *-l* e' per la rete privata. Le interfacce predefinite sono ppp0 per la rete pubblica ed eth0 per quella privata: se vengono utilizzate queste, non occorre specificarle. Se invece il gateway e' connesso con rete wireless accessibile tramite interfaccia wlan0, allora si può condividere questa connessione con:

`# icshare -i wlan0 start`

Funzionamento
-------------

Il client deve essere configurato per collegarsi in rete tramite protocollo DHCP (di fatto, quello predefinito nella maggior parte dei PC). Lo script va eseguito sul gateway prima di collegare il client.
Quando si avvia la condivisione della connessione, il gateway diventa un server DHCP e DNS grazie a *dnsmasq*. Il gateway viene abilitato ad effettuare l'IP forwarding (con sysctl) ed il suo firewall viene impostato (con iptables) per eseguire il NAT dei pacchetti. Il gateway accetterà richieste solo dalla rete privata "192.168.123.0/24": si possono cambiare questi parametri modificando alcune variabili all'inizio dello script.
Al momento della connessione tra client e gateway, il client riceverà automaticamente le impostazioni per collegarsi (indirizzo IP e DNS) e potrà condividere la connessione messa a disposizione dal gateway.
Da notare che il client può avere un qualunque sistema con DHCP, non necessariamente Linux.

Conclusioni
-----------

Lo script e' stato realizzato per condividere al volo una connessione "domestica" su ethernet, non e' inteso per uso professionale. I modem-router moderni fanno sentire meno l'esigenza, tuttavia la necessita' di "attaccare" un computer ad un altro potrebbe esserci e di conseguenza lo script potrebbe rivelarsi utile in molte situazioni.
Il codice dello script è già abbastanza strutturato: naturalmente ciascuno potrà apportare le modifiche e gli adattamenti che ritiene opportuni.

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink")
