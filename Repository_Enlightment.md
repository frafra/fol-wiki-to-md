Repository Enlightenment
========================

Nei repo fedora esiste già la versione 16 di enlightenment, installabile semplicemente così:

`# yum install e16`

La guida seguente *serviva* per installare gli rpm della versione 17, quando i link funzionavano.

Ecco qui un repository che consente di installare il desktop manager Enlightment comodamente tramite yum. Basterà creare il file */etc/yum.repos.d/didier.repo* con il seguente contenuto:

`[Didier]`
`name=Didier's yum repository for e17 apps/lib`
`baseurl=`[`http://sps.nus.edu.sg/~didierbe/fedora/X/en/i386`](http://sps.nus.edu.sg/~didierbe/fedora/X/en/i386)
`        `[`http://dentrassi.de/e17/fedora/X/en/i386/RPMS.e17/`](http://dentrassi.de/e17/fedora/X/en/i386/RPMS.e17/)
`        `[`http://fedora.oceighty.net/e17/fedora/X/en/i386/RPMS.e17/`](http://fedora.oceighty.net/e17/fedora/X/en/i386/RPMS.e17/)
`        `[`http://dr17.saaf.co.uk/fedora/X/en/i386/RPMS.e17/`](http://dr17.saaf.co.uk/fedora/X/en/i386/RPMS.e17/)

Oppure più semplicemente si può scaricare il pacchetto <http://sps.nus.edu.sg/~didierbe/share/dc-fc4-yum-repo-1.3-1.fc4.noarch.rpm> ed installarlo con

`# rpm -Uvh dc-fc4-yum-repo-1.3-1.fc4.noarch.rpm`

Importare anche la chiave gpg con

`# rpm --import `[`http://sps.nus.edu.sg/~didierbe/RPM-GPG-KEY.didier.txt`](http://sps.nus.edu.sg/~didierbe/RPM-GPG-KEY.didier.txt)` `

Fatto questo si può installare Enlightenment tramite il comando

`# yum install enlightenment`

Nel caso si volesse vedere quali sono i pacchetti sul proprio sistema installate da questo repository, si può utilizzare il seguente comando:

`$ rpm -qa --queryformat "%{name} %{packager}n"|grep "didier@microtronyx.com"`

<Categoria:Repository> <Categoria:Yum>
