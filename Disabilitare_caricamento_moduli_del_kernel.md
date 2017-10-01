E' possibile disabilitare il caricamento di particolari moduli del kernel.

-   Nel file **/etc/modprobe.d/blacklist** vengono inseriti i moduli del kernel da non caricare. Di default sono già presenti alcuni moduli in blacklist, quindi per aggiungerne di nuovi basterà incrementare una nuova entry blacklist .

`[root@vrhel5 ~]# cat /etc/modprobe.d/blacklist`
`#                                             `
`# Listing a module here prevents the hotplug scripts from loading it.`
`# Usually that'd be so that some other driver will bind it instead,`
`# no matter which driver happens to get probed first.  Sometimes user`
`# mode tools can also control driver binding.`
`#`
`# Syntax:  driver name alone (without any spaces) on a line. Other`
`# lines are ignored.`
`#`
`# watchdog drivers`
`blacklist i8xx_tco`
`# framebuffer drivers`
`blacklist aty128fb`
`blacklist atyfb`
`blacklist radeonfb`
`blacklist i810fb`
`blacklist cirrusfb`
`blacklist intelfb`
`blacklist kyrofb`
`blacklist i2c-matroxfb`
`blacklist hgafb`
`blacklist nvidiafb`
`blacklist rivafb`
`blacklist savagefb`
`blacklist sstfb`
`blacklist neofb`
`blacklist tridentfb`
`blacklist tdfxfb`
`blacklist virgefb`
`blacklist vga16fb`
`# ISDN - see bugs 154799, 159068`
`blacklist hisax`
`blacklist hisax_fcpcipnp`

-   Nell'esempio è mostrato come disabilitare i moduli del kernel relativi ad iptables. I moduli coinvolti sono ip\_tables e x\_tables. Per sicurezza verranno bloccati e disabilitati al boot.

`[root@vrhel5 ~]# lsmod | grep tables`
`ip_tables             18053  1 iptable_filter`
`x_tables               17349  4 ipt_REJECT,ip6t_REJECT,xt_tcpudp,ip6_tables`
`[root@vrhel5 ~]# vim /etc/modprobe.d/blacklist`
`blacklist ip_tables`
`blacklist x_tables`
`[root@vrhel5 modprobe.d]# service iptables stop`
`Flushing firewall rules:                                   [  OK  ]`
`Setting chains to policy ACCEPT: filter                    [  OK  ]`
`Unloading iptables modules:                                [  OK  ]`
`[root@vrhel5 modprobe.d]# chkconfig iptables off`
`[root@vrhel5 ~]# chkconfig --list iptables`
`iptables        0:off   1:off   2:off   3:off   4:off   5:off   6:off`
`[root@vrhel5 ~]# lsmod | grep tables`

-   In alcuni casi però anche avendo inserite le entry nel file blacklist, i moduli vengono ricaricati. Infatti con iptables, lanciando un qualsiasi comando legato al modulo, viene comunque ricaricato il modulo disabilitato (anche se viene disabilitato al boot il servizio iptables).

`[root@vrhel5 ~]# lsmod | grep tables                                                              `
`[root@vrhel5 ~]# iptables -L                      `
`Chain INPUT (policy ACCEPT)                       `
`target     prot opt source               destination         `
`Chain FORWARD (policy ACCEPT)`
`target     prot opt source               destination         `
`Chain OUTPUT (policy ACCEPT)`
`target     prot opt source               destination         `
`[root@vrhel5 ~]# lsmod | grep tables                         `
`ip_tables              17029  1 iptable_filter               `
`x_tables               17349  1 ip_tables                    `
`[root@vrhel5 ~]# chkconfig --list iptables`
`iptables        0:off   1:off   2:off   3:off   4:off   5:off   6:off`

-   Quindi e' possibile aggiungere al file **/etc/modprobe.d/blacklist** una entry per modulo, da poi poter fermare con la sintassi **install /bin/true**. Così facendo, quando verrà cercato di installare il modulo, il sistema restituirà il valore vero, anche se non realmente caricato.

`[root@vrhel5 ~]# vim /etc/modprobe.d/blacklist`
`# Iptables`
`blacklist ip_tables`
`blacklist x_tables`
`install ip_tables /bin/true`
`install x_tables /bin/true`

-   Nel caso di iptables, eseguendo questa modifica, il modulo resterà bloccato; anche se dovessimo richiamare il comando **iptables**, si otterrà:

`[root@vrhel5 ~]# lsmod | grep tables`
`[root@vrhel5 ~]# iptables -L        `
`` iptables v1.3.5: can't initialize iptables table `filter': iptables who? (do you need to insmod?) ``
`Perhaps iptables or your kernel needs to be upgraded.`

<Categoria:Sistema>
