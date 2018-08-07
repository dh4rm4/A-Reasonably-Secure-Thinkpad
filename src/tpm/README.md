# Setup TPM2.0

## Steps

- [Enable TPM Chip in Bios](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/tree/master/src/bios_settings)
- Check if the TPM Kernel Module was loaded
```
$ dmesg | grep -i tpm
[...]
[   62.869080] tpm_tis STM7304:00: 2.0 TPM (device-id 0x0, rev-id 78)
```
- Check the presence of all module' files
```
$ ls -la /lib/modules/`uname -r`/kernel/drivers/char/tpm
total 272
drwxr-xr-x 2 root root   4096 Aug  5 15:02 .
drwxr-xr-x 8 root root   4096 Aug  5 15:02 ..
-rwxr--r-- 1 root root  12952 Jul 23 18:45 tpm_atmel.ko
-rwxr--r-- 1 root root  21672 Jul 23 18:45 tpm_crb.ko
-rwxr--r-- 1 root root  24752 Jul 23 18:45 tpm_infineon.ko
-rwxr--r-- 1 root root 125984 Jul 23 18:45 tpm.ko
-rwxr--r-- 1 root root  18400 Jul 23 18:45 tpm_nsc.ko
-rwxr--r-- 1 root root  31704 Jul 23 18:45 tpm_tis_core.ko
-rwxr--r-- 1 root root  17888 Jul 23 18:45 tpm_tis.ko
```
- Load modules
```
$ /sbin/modprobe tpm
$ /sbin/modprobe tpm_tis force=1 interrupts=0
```
Does linux kernel <4.4 have tpm2.0 driver natively ?

- Install tpm-tools and trousers to use the TPM API
```
qubes-dom0-update trousers 
```
