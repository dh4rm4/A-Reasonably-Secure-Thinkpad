<p align="center">
<img src=https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/a_resonably_secure_thinkpad.png?raw=true />
</p>


# A-Reasonably-Secure-Thinkpad
How to build a reasonably secure t480s Thinkpad


## Bios Settings:
* :heavy_check_mark: : Enable
* :x: : Disable
* :o: : Permanently Disable
* :eight_spoked_asterisk: : Needed for Qubes

### Security
**Category** |  **Field**       | **Action**           | **Reason**   | **Infos**   | Reading
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
            


## Why Qubes ?
### Pros:
1. Free and open-source software
2. Xen
3. Security by compartmentalization
Dom0: isolate from network

### Cons:
1. Hardware Compatibility
2. Necessary RAM


# Install Qubes
### Get ISO
```
wget https://mirrors.edge.kernel.org/qubes/iso/Qubes-R4.0-x86_64.iso
```
### Get ISO Digest
```
wget https://mirrors.edge.kernel.org/qubes/iso/Qubes-R4.0-x86_64.iso.DIGESTS
```
### Get ISO Signature
```
https://mirrors.edge.kernel.org/qubes/iso/Qubes-R4.0-x86_64.iso.asc
```
### Get Qubes PGO Key
```
wget https://keys.qubes-os.org/keys/qubes-release-4-signing-key.asc
```

## Qubes GPG Master Key
### Get Master Key
```
gpg --fetch-keys https://keys.qubes-os.org/keys/qubes-master-signing-key.asc
```
### Verify Master Key Fingerprint
It is necessary to check with multiple source that the fingerprint you obtain is similar to the one everyone get.
```
gpg --fingerprint qubes
pub   4096R/36879494 2010-04-01
      Key fingerprint = 427F 11FD 0FAA 4B08 0123  F01C DDFA 1A3E 3687 9494
uid   Qubes Master Signing Key
```
List bellow are way *I* use to verify the fingerprint. You may add others sources.

[Qubes Website](https://www.qubes-os.org/security/verifying-signatures/) | [Twitter](https://twitter.com/rootkovska/status/496976187491876864) | [Github](https://github.com/QubesOS/qubes-secpack/blob/master/canaries/canary-001-2015.txt/) | [WikiData](https://www.wikidata.org/wiki/Q7269652) | [Wikipedia]() | [Reddit](https://www.reddit.com/r/Qubes/comments/5sgmtg/on_verifying_signatures/)
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
