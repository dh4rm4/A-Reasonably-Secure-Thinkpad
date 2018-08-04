### Fix _Suspend Functionnality_
There is an issue with the usb controler from Lenovo and Qubes.
You'll have to disable _USB3.0_ in \_sys_usb: Qubes Settings >> _Devices_
```
00.14.0 USB Controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
```

### SetUp power saving
Install in TemplattesVM + dom0 TLP to automaticcaly save power
**Template Fedora**
```
sudo dnf install tlp tlp-rdw
```
**Template Debian**
```
sudo apt-get install tlp tlp-rdw
```
**dom0**
```
qubes-dom0-update tlp tlp-rdw
```

If you want to be more power efficient, you can tune your config files thaks to the [documentation](https://linrunner.de/en/tlp/docs/tlp-configuration.html).
One settings worses chaging is the _TLP_DEFAULT_MODE_, which set what config to use in case a power source cannot be detected.
```
TLP_DEFAULT_MODE=BAT
```


## Scripts
Here are some useful scripts to automate and optimize tasks

**Shutdown Thinkpad**
```
#!/bin/sh

user_vm=$(qvm-ls -q --all --exclude sys-net --exclude sys-firewall | grep Running | cut -d' ' -f1

echo '[+] Shutdown user VM(s)'
qvm-shutdown $user_vm 2>&-
sleep 10
qvm-ls -q --all --exclude sys-net --exclude sys-firewall | grep Running && qvm-kill $user_vm

echo '[+] Shutdown sys-firewall'
qvm-shutdown sys-firewall
sleep 8
qvm-ls | grep -E 'sys-firewall.*Running' && qvm-kill sys-firewall

echo '[+] Shutdown sys-net'
qvm-shutdown sys-net
sleep 8
qvm-ls | grep -E 'sys-net.*Running' && qvm-kill sys-net

echo '[+] Shutdown Thinkpad'
shutdown now
```
