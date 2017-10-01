Il seguente piccolo script permette di filtrare attraverso iptables il traffico verso siti "indesiderati".

Si suppone di avere due schede di rete tra le quali è interposto un firewall come nel seguente schema:
**|INTERNET|&lt;-----------------&gt;|eth0|&lt; ---&gt; firewall&lt;---&gt;|eth1|&lt;----&gt;|switch|**

Il listato che imposta le regole di filtraggio è questo.

`#!/bin/bash`
`set -x`
`INET=eth0`
`LAN=eth1`
`LOCALNET=192.168.1.0/24`
`IPT=$(which iptables)`
`WORDS="$(cat /etc/wordlist)"`
`for i in ${WORDS}`
`do`
`${IPT} -A FORWARD -i ${INET} -o ${LAN} -p tcp -s 0/0 --sport 80 -d ${LOCALNET} -m state --state NEW,ESTABLISHED,RELATED \`
`-m string --string "$i" --algo kmp -j LOG --log-prefix "$i"`
`${IPT} -A FORWARD -i ${INET} -o ${LAN} -p tcp -s 0/0 --sport 80 -d ${LOCALNET} -m state --state NEW,ESTABLISHED,RELATED \`
`-m string --string "$i" --algo kmp -j DROP`
`done`

salvare il codice in un file opportuno, e renderlo eseguibile dal solo root.

Nel file /etc/wordlist inserire l'elenco dei siti che si vogliono "evitare":

`# gedit /etc/wordlist`

ed inserire ad esempio:

`facebook`
`youtube`
`etc...`

Il filtraggio avverrà dal momento del lancio dello script.

Un saluto da Mandela900

[Categoria:Rete e Server](Categoria:Rete_e_Server "wikilink") <Categoria:Sicurezza>
