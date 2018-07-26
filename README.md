# A-Reasonably-Secure-Thinkpad
How to build a reasonably secure t480s Thinkpad


## Bios Settings:
* :heavy_check_mark: : Enable
* :x:: Disable
* :o: : Permanently Disable
### Security
:x: [Device Guard](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control):  Windows Only 
```
Device Guard restricts devices to only run authorized apps [...], while simultaneously hardening the OS against kernel memory attacks [...]
```
:heavy_check_mark: [Intel® SGX](https://software.intel.com/en-us/blogs/2013/09/26/protecting-application-secrets-with-intel-sgx):

From [Joanna Rutkowska](http://theinvisiblethings.blogspot.com/2013/08/thoughts-on-intels-upcoming-software.html):
```
Intel SGX is essentially a new mode of execution on the CPU, a new memory protection semantic, 
plus a couple of new instructions to manage this all. 
So, you create an enclave by filling its protected pages with desired code, then you lock it down,
measure the code there, and if everything's fine, you ask the processor to start executing the code 
inside the enclave.
```


## Why Qubes ?
### Pros:
1. Free and open-source software
2. Xen
3. Security by compartmentalization
Dom0: isolate from network

### Cons:
1. Hardware Compatibility
2. Necessary RAM
