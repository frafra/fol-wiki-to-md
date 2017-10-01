\_\_TOC\_\_

Introduzione
------------

Vediamo come installare la chiavetta USB Hauppauge! WinTV Aero su Fedora 11 x86\_64. Potremmo guardare il digitale terrestre comodamente sul nostro computer, mentre leggiamo FedoraOnLine.

Preso dall'invidia mi sono comprato una bella chiavetta usb per la ricezione del digitale terrestre, una chiavetta Hauppauge! WinTV Aero.
WinTV?? La vedo un po' male.... Dove c'è win si piange (in genere). Comunque, mi metto all'opera....

Procedura
---------

Dopo aver inserito la chiave digitare, da root:

`# lsusb`
`Bus 003 Device 002: ID 045e:00d2 Microsoft Corp.`
`Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub`
`Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub`
`Bus 002 Device 004: ID 2040:5520 Hauppauge`
`Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub`
`Bus 001 Device 003: ID 0bda:0116 Realtek Semiconductor Corp. Mass Storage Device`
`Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub`

e poi:

`# tail /var/log/messages`

che restituisce:

`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb_onresponse: line: 73: error, urb status -2, 0 bytes`
`Aug 29 01:26:30 gabri kernel: smsusb: probe of 2-3:1.0 failed with error -2`
`Aug 29 01:26:30 gabri firmware.sh[4166]: Cannot find  firmware file 'dvb_nova_12mhz_b0.inp'`

Poi vedere il:

`# dmesg`

che (tra il resto) dice:

    Initializing USB Mass Storage driver...
    scsi6 : SCSI emulation for USB Mass Storage devices usbcore:
    registered new interface driver usb-storage USB Mass Storage support registered.
    usb-storage: device found at 3 usb-storage: waiting for device to settle before scanning
    cfg80211: Calling CRDA to update world regulatory domain acpi device:20:
    registered as cooling_device2
    input: Video Bus as /devices/LNXSYSTM:00/device:00 /PNP0A03:00/device:1c/input/input10
    ACPI: Video Device [VGA] (multi-head: yes  rom: no  post: no)
    usb 2-3: firmware: requesting sms1xxx-hcw-55xxx-dvbt-02.fw
    forcedeth 0000:00:0a.0: ifname eth0, PHY OUI 0x732 @ 1, addr 00:1d:60:2f:f6:f8
    forcedeth 0000:00:0a.0: highdma pwrctl mgmt timirq lnktim msi desc-v3
    smscore_set_device_mode: error -2 loading firmware: sms1xxx-hcw-55xxx-dvbt-02.fw,
    trying again with default firmware
    usb 2-3: firmware: requesting dvb_nova_12mhz_b0.inp
    smscore_set_device_mode: error -2 loading firmware: dvb_nova_12mhz_b0.inp
    smsusb_init_device: line: 381: smscore_start_device(...) failed
    smsusb_onresponse: line: 73: error, urb status -2, 0 bytes
    smsusb_onresponse: line: 73: error, urb status -2, 0 bytes
    smsusb_onresponse: line: 73: error, urb status -2, 0 bytes
    smsusb_onresponse: line: 73: error, urb status -2, 0 bytes
    smsusb_onresponse: line: 73: error, urb status -2, 0 bytes
    smsusb_onresponse: line: 73: error, urb status -2, 0 bytes
    smsusb_onresponse: line: 73: error, urb status -2, 0 bytes
    smsusb_onresponse: line: 73: error, urb status -2, 0 bytes
    ACPI: PCI Interrupt Link [LNED] enabled at IRQ 19
    alloc irq_desc for 19 on cpu 0 node 0
    alloc kstat_irqs on cpu 0 node 0
    ath5k 0000:05:00.0: PCI INT A -> Link[LNED] -> GSI 19 (level, low) -> IRQ 19
    ath5k 0000:05:00.0: setting latency timer to 64
    ath5k 0000:05:00.0: registered as 'phy0'
    wmaster0 (ath5k): not using net_device_ops yet
    phy0: Selected rate control algorithm 'minstrel'
    smsusb: probe of 2-3:1.0 failed with error -2
    usbcore: registered new interface driver smsusb

Viene richiesto il firmware sms1xxx-hcw-55xxx-dvbt-02.fw, per cui bisogna spostarsi nella cartella del firmware:

`# cd /lib/firmware`

e digitare:

`# wget `[`http://steventoth.net/linux/sms1xxx/sms1xxx-hcw-55xxx-dvbt-02.fw`](http://steventoth.net/linux/sms1xxx/sms1xxx-hcw-55xxx-dvbt-02.fw)

Succede questo:

`# tail /var/log/messages`
`Aug 29 01:35:43 gabri kernel: usb 2-3: New USB device found, idVendor=2040, idProduct=5520`
`Aug 29 01:35:43 gabri kernel: usb 2-3: New USB device strings: Mfr=1, Product=2, SerialNumber=3`
`Aug 29 01:35:43 gabri kernel: usb 2-3: Product: WinTV MiniStick`
`Aug 29 01:35:43 gabri kernel: usb 2-3: Manufacturer: Hauppauge Computer Works`
`Aug 29 01:35:43 gabri kernel: usb 2-3: SerialNumber: f067a7d5`
`Aug 29 01:35:43 gabri kernel: usb 2-3: configuration #1 chosen from 1 choice`
`Aug 29 01:35:43 gabri kernel: usb 2-3: firmware: requesting sms1xxx-hcw-55xxx-dvbt-02.fw`
`Aug 29 01:35:44 gabri kernel: smscore_set_device_mode: firmware download success:`
`sms1xxx-hcw-55xxx-dvbt-02.fw`
`Aug 29 01:35:44 gabri kernel: DVB: registering new adapter (Hauppauge WinTV MiniStick)`
`Aug 29 01:35:44 gabri kernel: DVB: registering adapter 0 frontend 0`
`(Siano Mobile Digital MDTV Receiver)`

Lsusb è sempre quello iniziale...

`# lsusb`
`Bus 003 Device 002: ID 045e:00d2 Microsoft Corp.`
`Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub`
`Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub`
`Bus 002 Device 004: ID 2040:5520 Hauppauge`
`Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub`
`Bus 001 Device 003: ID 0bda:0116 Realtek Semiconductor Corp. Mass Storage Device`
`Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub`

Partendo con Kaffeine, trova i canali ma non si vedono. Il motore che usa kaffeine è xine, probabilmente mancano i codecs....
Provare con:

`# yum install xine-ui xine-lib-extras xine-lib-extras-freeworld`

Risultato?

Ora si vede la tv digitale terrestre, con canone RAI già pagato...

Riferimenti
-----------

-   <http://www.hauppauge.com/pages/faq/support_faq_linux.html>
-   <http://www.linuxtv.org/>
-   <http://linuxtv.org/wiki/index.php/Hauppauge>

<Categoria:Multimedia> <Categoria:Hardware>
