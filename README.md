<p align="center">
<img src=https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/a_resonably_secure_thinkpad.png?raw=true />
</p>


# A Reasonably Secure Thinkpad
How to build a reasonably secure t480s Thinkpad.

# Considerations
One major componenent to build a resonably secure laptop, is the use of the _Static Root of Trust for Measurements_ from your _Trusted Platform Module_. 

But if you encrypted disk, this functionnality comes with high risks:

If one hash in your PCRs tables changes, you will never be able to recover your data. (_This could be an easy way to disrupt your hard work_)

Before you start playing with some important stuff, you must consider differents solution for your data sotrage:
* version control system
* backup on personnal physical device
* cloud storage provider (with dual encryption)
* ...

## Why Qubes ?
### Pros:
1. Free and open-source software
2. Xen
3. Security by compartmentalization
Dom0: isolate from network

### Cons:
1. Hardware Compatibility
2. Necessary RAM


## Contents
* [Bios Settings](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/README.md#bios-settings)
* [Install Qubes](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/README.md#install-qubes)
* [Setup TPM]()
* [Disk Encryption]()
* [Qubes Config]()

## Bios Settings
<center>
  
   **Symbol**           |  **Meaning**
:-----------------------|:-----------:
:heavy_check_mark:      | Enable
:x:                     | Disable
:o:                     | Permanently Disable
:eight_spoked_asterisk: | Needed for Qubes

</center>

### Security
**Category** |  **Field**       | **Action**           | **Reason**   | **Infos**   | **Reading**
:-----------:|:----------------:|:--------------------:|:------------:|:-----------:|:---:
[Device Guard](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/device_guard.png?raw=true) | [Device Guard](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control)     | :x:                  | Windows Only | Device Guard restricts devices to only run authorized apps, while simultaneously hardening the OS against kernel memory attacks [...] | [:spades:](https://blogs.technet.microsoft.com/ash/2016/03/02/windows-10-device-guard-and-credential-guard-demystified/)
[Intel SGX](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/intel_sgx.png?raw=true) | [Intel SGX](https://software.intel.com/en-us/blogs/2013/09/26/protecting-application-secrets-with-intel-sgx)         | :heavy_check_mark:   | Good security for apps builded around SGX | Creates an isolated memory enclave, fills it with the app code, and if the enclave' hash is validated, then the app is launched | [:spades:](https://software.intel.com/en-us/blogs/2013/09/26/protecting-application-secrets-with-intel-sgx) [:spades:](http://theinvisiblethings.blogspot.com/2013/08/thoughts-on-intels-upcoming-software.html)
[Anti-Theft](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/anti_theft.png?raw=true) | [Computrace](https://www.wikiwand.com/en/LoJack_for_Laptops) |  :o:                 | Assumed Backdoor | Laptop tracking software with features including the abilities to remotely lock, delete files from, and locate the _stolen_ laptop on a map | [:spades:](https://securelist.com/absolute-computrace-revisited/58278/)               
[Secure Boot](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/secure_boot.png?raw=true) | [Secure Boot](https://docs.microsoft.com/en-us/windows-hardware/design/device-experiences/oem-secure-boot)       | :x:                  | [UEFI](https://www.wikiwand.com/en/Unified_Extensible_Firmware_Interface) only / Incompatible with [TrustGrub2](https://github.com/Rohde-Schwarz-Cybersecurity/TrustedGRUB2) | | [:spades:](https://www.howtogeek.com/116569/htg-explains-how-windows-8s-secure-boot-feature-works-what-it-means-for-linux/)
[Internal Device Access](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/internal_device_access.png?raw=true) | Bottom Cover Tamper Detection | :heavy_check_mark: | Adds light physical security | Supervisor password is required when a bottom cover tamperis detected. This option is not functional until a supervisor password is set |
[Internal Device Access](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/internal_device_access.png?raw=true) | Internal Storage Tamper Detection | :heavy_check_mark: | Adds light physical security |  If you remove the internal storage device while the computer is in sleepmode, the computer will shut down when you wake it up, and any unsaved data will be lost |
[Virutalization](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/virtualization.png?raw=true) |[Intel VT-d](https://www.intel.com/content/www/us/en/virtualization/virtualization-technology/intel-virtualization-technology.html?iid=tech_vt+tech) :eight_spoked_asterisk: | :heavy_check_mark: | Bring more security and isolation for virtualization i/o | The overall concept behind VT-d is hardware support for isolating and restricting device accesses to the owner of the partition managing the device. | [:spades:](https://software.intel.com/en-us/blogs/2009/06/25/understanding-vt-d-intel-virtualization-technology-for-directed-io) [:spades:](https://software.intel.com/en-us/articles/intel-virtualization-technology-for-directed-io-vt-d-enhancing-intel-platforms-for-efficient-virtualization-of-io-devices)
[Virutalization](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/virtualization.png?raw=true) | [Intel VT-x]() :eight_spoked_asterisk: | :heavy_check_mark: | |
[Fingerprint](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/fingerprint.png?raw=true) | [Predesktop Authentification]() | :x: | Windows Only | | [:spades:](https://www.avg.com/en/signal/3-reasons-to-never-use-fingerprint-locks) [:spades:](https://blog.elcomsoft.com/2012/08/upek-fingerprint-readers-a-huge-security-hole/)
[Security Chip](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/scurity_chip.png?raw=true) | [Security Chip](https://trustedcomputinggroup.org/resource/trusted-platform-module-tpm-summary/) | :heavy_check_mark: | Necessary for Trusted Computing | Ensure that the boot process starts from a trusted combination of hardware and software, and continues until the operating system has fully booted and applications are running. | [:spades:](http://www.jhuapl.edu/techdigest/TD/td3202/32_02-Osborn.pdf) [:spades:](https://lenovopress.com/lp0599-technical-introduction-tpm-20-with-linux)  [:spades:](https://link.springer.com/chapter/10.1007/978-1-4302-6584-9_3) [:spades:](https://link.springer.com/book/10.1007/978-1-4302-6584-9)
[Memory Protection](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/memory_protection.png?raw=true) | [Execution Prevention](https://www.wikiwand.com/en/NX_bit) |  
            


# Install Qubes
## Content
* [Qubes GPG Master Key](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/README.md#qubes-gpg-master-key)
* [Qubes GPG Release Key](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/README.md#get-the-release-key)
* [Qubes ISO](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/README.md#qubes-iso)
* [Burn Qubes on Usb Device](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/README.md#burn-qubes-on-usb-device)

**Bellow is a short version of the already [superb documentation](https://www.qubes-os.org/security/verifying-signatures/) from QUbes Offical Website:**.
If you want to understand a specific output, you could probably find the infos on he official doc.

## Qubes GPG Master Key
### Get Master Key
```
gpg --fetch-keys https://keys.qubes-os.org/keys/qubes-master-signing-key.asc
```
### Verify Master Key Fingerprint
It is necessary to check with multiple sources that you obtained good the fingerprint.
```
gpg --fingerprint qubes
pub   4096R/36879494 2010-04-01
      Key fingerprint = 427F 11FD 0FAA 4B08 0123  F01C DDFA 1A3E 3687 9494
uid   Qubes Master Signing Key
```
Listed bellow are the sources *I* use to attest the fingerprint validity. 
You may want to add others.

[Qubes Website](https://www.qubes-os.org/security/verifying-signatures/) | [Twitter](https://twitter.com/rootkovska/status/496976187491876864) | [Github](https://github.com/QubesOS/qubes-secpack/blob/master/canaries/canary-001-2015.txt/) | [WikiData](https://www.wikidata.org/wiki/Q7269652) | [Wikipedia]() | [Reddit](https://www.reddit.com/r/Qubes/comments/5sgmtg/on_verifying_signatures/) | [Qubes Keys Server](https://keys.qubes-os.org/keys/) |
:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:----:


**When you finally decide to trust the Master key you got, you can say to GPG to _ultimately_ trust this key**

```
$ gpg --edit-key 0x36879494
gpg (GnuPG) 1.4.18; Copyright (C) 2014 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.


pub  4096R/36879494  created: 2010-04-01  expires: never       usage: SC
                     trust: unknown       validity: unknown
[ unknown] (1). Qubes Master Signing Key

gpg> fpr
pub   4096R/36879494 2010-04-01 Qubes Master Signing Key
 Primary key fingerprint: 427F 11FD 0FAA 4B08 0123  F01C DDFA 1A3E 3687 9494

gpg> trust
pub  4096R/36879494  created: 2010-04-01  expires: never       usage: SC
                     trust: unknown       validity: unknown
[ unknown] (1). Qubes Master Signing Key

Please decide how far you trust this user to correctly verify other users' keys
(by looking at passports, checking fingerprints from different sources, etc.)

  1 = I don't know or won't say
  2 = I do NOT trust
  3 = I trust marginally
  4 = I trust fully
  5 = I trust ultimatelyh
  m = back to the main menu

Your decision? 5
Do you really want to set this key to ultimate trust? (y/N) y

pub  4096R/36879494  created: 2010-04-01  expires: never       usage: SC
                     trust: ultimate      validity: unknown
[ unknown] (1). Qubes Master Signing Key
Please note that the shown key validity is not necessarily correct
unless you restart the program.

gpg> q
```

## Get the release Key
```
$ wget https://keys.qubes-os.org/keys/qubes-release-X-signing-key.asc
$ gpg --import ./qubes-release-X-signing-key.asc
```

Check if the release key is signed by the master key
```
$ gpg --list-sigs "Qubes OS Release X Signing Key"
pub   rsa4096 2017-03-06 [SC]
      5817A43B283DE5A9181A522E1848792F9E2795E9
uid           [  full  ] Qubes OS Release X Signing Key
sig 3        1848792F9E2795E9 2017-03-06  Qubes OS Release X Signing Key
sig          DDFA1A3E36879494 2017-03-08  Qubes Master Signing Key
```

## Qubes ISO
### Get ISO
```
wget https://mirrors.edge.kernel.org/qubes/iso/Qubes-R4.0-x86_64.iso
```

### Authenticity
```
$ gpg -v --verify Qubes-RX-x86_64.iso.asc Qubes-RX-x86_64.iso
gpg: armor header: Version: GnuPG v1
gpg: Signature made Tue 08 Mar 2016 07:40:56 PM PST using RSA key ID 03FA5082
gpg: using PGP trust model
gpg: Good signature from "Qubes OS Release X Signing Key"
gpg: binary signature, digest algorithm SHA256
```

### Integrity
#### Check Digest Authenticity
```
$ gpg -v --verify Qubes-RX-x86_64.iso.DIGESTS 
gpg: armor header: Hash: SHA256
gpg: armor header: Version: GnuPG v2
gpg: original file name=''
gpg: Signature made Tue 20 Sep 2016 10:37:03 AM PDT using RSA key ID 03FA5082
gpg: using PGP trust model
gpg: Good signature from "Qubes OS Release X Signing Key"
gpg: textmode signature, digest algorithm SHA256
```

#### Check Iso Integrity
```
$ md5sum -c Qubes-RX-x86_64.iso.DIGESTS
Qubes-RX-x86_64.iso: OK
md5sum: WARNING: 23 lines are improperly formatted

$ sha1sum -c Qubes-RX-x86_64.iso.DIGESTS
Qubes-RX-x86_64.iso: OK
sha1sum: WARNING: 23 lines are improperly formatted

$ sha256sum -c Qubes-RX-x86_64.iso.DIGESTS
Qubes-RX-x86_64.iso: OK
sha256sum: WARNING: 23 lines are improperly formatted

$ sha512sum -c Qubes-RX-x86_64.iso.DIGESTS
Qubes-RX-x86_64.iso: OK
sha512sum: WARNING: 23 lines are improperly formatted
```

## Burn Qubes on Usb Device
### Clean Usb device
To fully erase the device content, _dd_ will do the job.
_Be sure to replace **sdX** by your usb device_
```
dd if=/dev/zero of=/dev/sdX bs=1048576
dd if=/dev/urandom of=/dev/sdX bs=1048576
```

### Copy file from Iso to Usb Drive
```
dd if=Qubes-R4-x86_64.iso of=/dev/sdX bs=1048576 && sync
```

# After Completed Installation
### Update qubes from dom0
```
sudo qubes-dom0-update
```

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
