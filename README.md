# A-Reasonably-Secure-Thinkpad
How to build a reasonably secure t480s Thinkpad


## Bios Settings:
* :heavy_check_mark: : Enable
* :x:: Disable
* :o: : Permanently Disable
### Security
* :x: [Device Guard](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control):  Windows Only
```
Device Guard restricts devices to only run authorized apps [...], while simultaneously hardening the OS against kernel memory attacks [...]
```
* [Intel® SGX](https://software.intel.com/en-us/blogs/2013/09/26/protecting-application-secrets-with-intel-sgx)

## Why Qubes ?
### Pros:
1. Free and open-source software
2. Xen
3. Security by compartmentalization

### Cons:
1. Hardware Compatibility
2. Necessary RAM
