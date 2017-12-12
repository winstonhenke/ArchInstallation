# Arch System Recovery

Currently has limited support for

* Simple partition layout with LUKS
  * No LVM(yet)
* BIOS/MBR only
  * No UEFI/GPT support(yet)
* One partition schema
  * boot and root(so far)

These tools were designed to automate some of the processes defined in the official [Arch Installation Guide](https://wiki.archlinux.org/index.php/Installation_guide) to allow for a quick full system recovery. This recovery model assumes all media/documents are backed up else where. This model will standup and configure the system. It will not currently restore media/documents from source control or a network drive.

**Do not** blindly follow these instructions and run these scripts or you will have a bad time. Take the time to understand them. I find them helpful for my needs but they may not fit yours.

## High Level Overview

At a high level the following steps should be taken

* Wipe the block device being used
* Boot into the Arch installation media
* Establish an internet connection
* Pull down repository
* Run the install scripts

### Wipe Disk

This tool assumes a clean disk and will attempt to wipe any old data away.

From any live system wipe the disk being prepped for the new system. This could take a while and may need to run overnight depending on the size of your disk.

Example

```plain text
sudo dd if=/dev/urandom of=/dev/sdXY bs=1M status=progress
```

### Boot Arch Installation Media

First boot the installation media, establish an internet connection, and pull down this git repository

Try wifi-menu as a console interface to netctl which as of this writing is included in the Arch installation media
```plain text
wifi-menu
```

Command to pull down the repository
```plain text
wget https://github.com/winstonhenke/ArchInstallation/tarball/master -O - | tar xz
```

