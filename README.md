<p align="center">
<img src=https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/blob/master/src/img/a_resonably_secure_thinkpad.png?raw=true />
</p>


# A Reasonably Secure Thinkpad
How to build a reasonably secure t480s Thinkpad.

# Considerations
One major componenent to build a resonably secure laptop, is the use of the _Static Root of Trust for Measurements_ from your _Trusted Platform Module_. 

But this functionnality comes with high risks:

If one hash in your PCRs tables comes to change, you won't be able to recover your data. (_This could be an easy way to disrupt your hard work_)

Before you start playing with some important stuff, you should consider a safe solution to store your data:
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
* [Bios Settings](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/tree/master/src/bios_settings)
* [Install Qubes](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/tree/master/src/qubes_installation)
* [Qubes Config](https://github.com/dh4rm4/A-Reasonably-Secure-Thinkpad/tree/master/src/qubes_config)
* [Setup TPM]()
