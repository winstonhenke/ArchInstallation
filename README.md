# Arch System Recovery

Currently works with the following

* Simple partition layout with LUKS
  * No LVM
* One partition schema
  * boot and root
* BIOS/MBR only
  * No UEFI/GPT support

This tool was designed to automate some of the processes defined in the official [Arch Installation Guide](https://wiki.archlinux.org/index.php/Installation_guide) to allow for a quick system install and basic configuration. This recovery model assumes all media/documents are backed up else where and does not handle syncing those items or creating any link to a network drive.

**Do not** blindly follow these instructions/run these scripts or you will have a bad time. I find them helpful for my needs but they may not fit yours.

## High Level Overview

At a high level the following steps should be taken

* Wipe the block device being used
* Boot into the Arch installation media
* Establish an internet connection
* Pull down repository
* Run the install script
* Post install

### Wipe Disk

This tool assumes a clean drive but will wipe the first the first few MBs to make sure the MBR is clean.

From any live system wipe the hard drive being prepped for the new system. This could take a while and may need to run overnight depending on the size of your disk.

Example

```plain text
sudo dd if=/dev/urandom of=/dev/sd? bs=64MB status=progress
```

### Boot Arch Installation Media

Boot the installation media. Not much else to say.

### Establish an Internet Connection

Try wifi-menu as a console interface to netctl which as of this writing is included in the Arch installation media.

```plain text
wifi-menu
```

### Pull Git Repo

Use the following command to pull down this repository. Fun fact, --output-document=- is needed so that documents will be printed to standard output allowing it to be piped into tar.

```plain text
wget --output-document=- https://github.com/winstonhenke/ArchInstallation/tarball/master | tar xz
```

### Run Install Script

Navigate into the the directory created when you pulled down the repo and run the Install command.

It will prompt for things like the block device you want to install to, the disk encryption key, root password(TODO - look to disable this), and a username and password for a new user with root privileges.

### Post Install

Things to do after installation

* [Sync dotfiles](https://github.com/winstonhenke/Dotfiles)