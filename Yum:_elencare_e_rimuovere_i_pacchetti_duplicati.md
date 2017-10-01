L'aggiornamento dei pacchetti di sistema effettuato con yum è composto da varie fasi:

1.  ricerca dei pacchetti e delle eventuali dipendenze
2.  download dei files rpm
3.  installazione degli aggiornamenti
4.  cancellazione delle versioni precedenti

Può capitare che yum venga però interrotto prima di aver terminato il suo lavoro (a causa di un bug, per un calo di tensione, per un "kill" inviato per errore da un utente distratto o per qualsiasi altro motivo) e che la fase di clean-up di cui al precedente punto 4) non abbia esito positivo, lasciando quindi nel sistema pacchetti doppi.

Girovagando per internet molto tempo fa ho trovato sul sito del [Fedora Project](http://www.fedoraproject.org) un utilissimo script di shell che interroga il database di rpm verificando appunto la presenza dei suddetti doppioni nonchè di ulteriori problematiche relative a sistemi x86\_64 (nel caso in cui yum non abbia aggiornato sia le librerie i386 che quelle x86\_64)

Riporto di seguito lo script in questione (**duplicates.sh**), dato che può tornare utile in varie circostanze:

`#!/bin/sh`
`# Add any package here that is OK to have duplicates`
`dups="gpg-pubkey kernel kernel-devel kernel-smp kernel-smp-devel"`
`# This function removes any word that matches the dups above`
`filter() {`
`        while [ $# -ge 1 ]`
`        do`
`                skip=0`
`                for d in $dups`
`                do`
`                        if [ "$1" = "$d" ] ; then`
`                                skip=1`
`                                break`
`                        fi`
`                done`
`                if [ $skip -eq 0 ] ; then`
`                        echo $1`
`                fi`
`                shift`
`        done`
`}`
`# Test 1. Look for multiple versions of the same package. This can occur`
`# when something prevents yum/rpm from completing an upgrade.`
`# We use # as a separator so that we can remove it later. # is not in any`
`# package name that I know of and that's the basis of using it.`
`` list=`rpm -qa --queryformat "%{NAME}#%{ARCH}\n" | sort | uniq -c | \ ``
``         tr '#' ' ' | awk '$1 > 1 { print $2 } '` ``
`` list2=`filter $list` ``
`if [ x"$list2" != "x" ] ; then`
`        echo "Duplicates were found:"`
`        echo $list2 | xargs rpm -q`
`        exit 1`
`fi`
`# Test 2. Check for mismatched versions. This can occur on a multilib system`
`# when yum does not upgrade both x86_64 and i386 packages at the same time.`
`# Get all packages with 2 entries`
`` list=`rpm -qa --queryformat "%{NAME}\n" | sort | uniq -c | \ ``
``         awk '$1 == 2 { print $2 }'` ``
`` list2=`filter $list` ``
`if [ x"$list2" = "x" ] ; then`
`        exit 0`
`fi`
`# Of those, see which ones only have 1 version of the package`
`` list=`echo $list2 | tr ' ' '\n' | xargs rpm -q --queryformat \ ``
`        "%{NAME}-%{VERSION}-%{RELEASE}\n" | sort | uniq -c | \`
``         awk '$1 == 1 { print $2 }'` ``
`if [ x"$list" = "x" ] ; then`
`        exit 0`
`fi`
`echo "Version mismatches were found:"`
`for l in $list`
`do`
`        rpm -q --queryformat "%{NAME}-%{VERSION}-%{RELEASE}.%{ARCH}\n" $l`
`done`
`exit 1`

E' sufficiente lanciarlo con i privilegi di root per visualizzare l'elenco dei pacchetti "in conflitto" tra loro:

`# duplicates.sh `
`Duplicates were found:`
`lam-libs-7.1.2-11.fc9.i386`
`lam-libs-7.1.4-1.fc10.i386`

A questo punto è possibile rimuovere il pacchetto vecchio:

`# rpm -e --noscripts lam-libs-7.1.2-11.fc9.i386`

Il mio consiglio è di provare a disinstallare il pacchetto senza tale opzione e di aggiungerla qualora rpm restituisca errori tipo il seguente:

`# rpm -e lam-libs-7.1.2-11.fc9.i386`
`errore: scriptlet %preun(lam-libs-2:7.1.2-11.fc9.i386) fallita, uscita con stato 2`

<Categoria:Yum>
