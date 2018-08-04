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
