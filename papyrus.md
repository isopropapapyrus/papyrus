# Welcome!

A brilliant but controversial pseudo-scientist-pirate has passed away, leaving behind a legacy cloaked in mystery. As one of a select group of his most trusted and cherished companions, you have been summoned to his home for a final challenge. Instead of a will, he has left behind cryptic instructions and a series of elaborate puzzles, claiming they lead to a hidden key for his safe. Only his closest confidants have a chance to open it. Inside lies something he described as "his life's work" - treasures so priceless he entrusted their discovery to only those he could completely depend on.

Can you and your team decipher the strange symbols, activate his enigmatic Rube Goldberg contraptions, and access the contents of the safe before they're lost forever?


# Instructions

Follow these instructions to unlock the first puzzle. You will need your 64 hex-digit personal key.

1. Boot a computer using the microSD card.

  - before booting, ensure the machine is not connected to a network.
  - a Windows/Linux compatible computer will be required; using a Mac is not likely to work.
  - a USB-microSD reader will be required; using an in-built SD-reader on a laptop is not likely to work. 

2. Confirm the microSD card is running the latest software.

  - run the command `iso-build-info` (if this command is not available you will need to use a later release of the software).
  - on a separate network connected device view the date of the latest release [here](https://github.com/isopropapapyrus/papyrus/releases/).
  - if you are not running the latest release download the .iso, copy it to a new USB disk and boot with it. 

3. Remove the microSD card / USB disk once the computer has finished booting.

4. Attach and mount _any one_ of the mad scientist's hard disk drives:

  - the drives are attached to the mad scientist's backup storage system; only one of them is required.
  - mount the disk by running this command: `zpool import -f -a -d /dev/disk/by-id -o readonly=on`
  - if no ZFS filesystem is found, try specifying the full path to the disk after the `-d` parameter.
  - `read-only` mode is used because no changes to the data should be required.
  - the drives contain ZFS encrypted filesystems; in the next step you will decrypt some of these filesystems.

5. Unlock a dedicated filesystem that contains further instructions specifically for you:

  - run the following command: `echo <your 64 hex-digit personal key> | berry reap crypt`
  - this will execute the `berry` tool to derive another key; the derived key is then automatically passed to another tool (`zcrypt`).
  - the `zcrypt` tool will use the derived key to decrypt a filesystem prepared specifically for you.
  - if successful, the command will display `Successfully unlocked and mounted /<your name>/epilogue`.

6. Read the deciphered instructions describing how to unlock the next puzzle:

  - to view the instructions run this command: `cat /<your name>/epilogue/read-me`


# Hints

* If the microSD card is outdated, lost, faulty, or fails to boot, make a USB boot disk from the .iso image in this [tarball](https://github.com/isopropapapyrus/papyrus/releases/download/isos/isopropyl.iso.tar.gz) (verify the download using this [hash](https://github.com/isopropapapyrus/papyrus/releases/download/isos/isopropyl.iso.sha256)).
* This downloaded .iso image may contain newer versions of the helper tools than the SD card.
* The `berry` tool derives "child" keys from a given "parent" key. `berry` also has functionality to pass the derived keys to other commands (for example, `berry reap crypt` calls `zcrypt` with all derived keys tagged to unlock ZFS encrypted filesystems). The `zcrypt` tool decrypts the appropriate ZFS filesystem for each given key.
* `berry`'s configuration is found in `~/.config/berry/berry.conf`. The external commands called by `berry reap <tag>` are configured here. The configured tools typically perform some action with the key data or convert it to an appropriate display format.
* `berry` requires some encrypted metadata to be available in the `/berries` directory (which is also configured in `~/.config/berry/berry.conf`). These "berry" files will automatically become available when one of the mad scientist's ZFS drives are imported. A backup copy of the berries is available [here](https://github.com/isopropapapyrus/berries).
* Further documentation and source code for `berry` and `zcrypt` is found on the ZFS drive in `/endure/public/repos/berry` and `/endure/public/repos/zcrypt`.
* These instructions work using `berry` version 1.2.1, `zcrypt` version 1.1.1, and ZFS version 2.2.6-1.
* Later versions of the `berry` and `zcrypt` tools may include bug fixes and enhancements; be sure to try these.
* If anything goes wrong during the process you may need help from a trusted technical expert. It is safe to share this document, the source code for `berry`/`crypt`, the berry files, the ZFS drive, and the test key (see below).


# Test Key

For all intents and purposes the test key below works in the above instructions, with the exception that it reveals no sensitive data. It can be shared with a third-party for assistance when trouble-shooting.

```
13e088987343f594d8322667bdc776fefb45558db9cea5a3d90df409042a025c
```



---
* File:     papyrus/papyrus.md
* Version:  2.0.0
* Date:     2026
---
