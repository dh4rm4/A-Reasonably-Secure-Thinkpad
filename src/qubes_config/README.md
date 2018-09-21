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

user_vm=$(qvm-ls -q --all --exclude sys-net --exclude sys-firewall | grep -E 'Running|Paused' | cut -d' ' -f1

echo '[+] Shutdown user VM(s)'
qvm-shutdown $user_vm --timeout 10
sleep 10

echo '[+] Shutdown sys-firewall'
qvm-shutdown sys-firewall --timeout 8
sleep 8

echo '[+] Shutdown sys-net'
qvm-shutdown sys-net --timeout 8
sleep 8

echo '[+] Shutdown Thinkpad'
shutdown now
```


# Create Personal VM

# Create Multimedia Fedora VM

```
sudo dnf config-manager --set-enabled rpmfusion-free rpmfusion-nonfree

sudo dnf install amrnb amrwb faad2 flac ffmpeg gpac-libs lame libfc14audiodecoder mencoder mplayer x264 x265 gstreamer-plugins-espeak gstreamer-plugins-fc gstreamer-rtsp gstreamer-plugins-good gstreamer-plugins-bad gstreamer-plugins-bad-free-extras gstreamer-plugins-bad-nonfree gstreamer-plugins-ugly gstreamer-ffmpeg gstreamer1-plugins-base gstreamer1-libav gstreamer1-plugins-bad-free-extras gstreamer1-plugins-bad-freeworld gstreamer1-plugins-base-tools gstreamer1-plugins-good-extras gstreamer1-plugins-ugly gstreamer1-plugins-bad-free gstreamer1-plugins-good

sudo dnf install vlc
```
