---
title: "Boot ISO Without Directly From Disk"
date: 2025-07-17T18:52:43+05:00
description: ""
url: "/boot-iso-from-disk/"
draft: false
---

*In Progress*
## GRUB
It is assumed that the ISO images are stored in the `/boot-isos` directory on the same filesystem where GRUB is installed. Otherwise it would be necessary to prefix the path to ISO file with device identification when using the `loopback` command, for example `loopback loop (hd1,2)$iso_path`. As this identification of devices is not persistent, it is not used in the examples in this section.

Add these to `ESP/grub/grub.cfg`
### If ISO is in a different partition 
```
# define globally (i.e outside any menuentry)
insmod search_fs_uuid
search --no-floppy --set=isopart --fs-uuid 123-456
# later use inside each menuentry instead
loopback loop ($isopart)$iso_path
```
### Example
```
menuentry '[loopback]archlinux-2023.10.14-x86_64.iso' {
	set iso_path='/boot-isos/archlinux-2023.10.14-x86_64.iso'
	export iso_path
	search --set=root --file "$iso_path"
	loopback loop "$iso_path"
	root=(loop)
	configfile /boot/grub/loopback.cfg
	loopback --delete loop
}
```
## Systemd-Boot

```(bash)
mkdir -p esp/EFI/archiso

# Extract the contents of the arch directory in there:
bsdtar -v -x --no-same-permissions --strip-components 1 -f archlinux-YYYY.MM.DD-x86_64.iso -C esp/EFI/archiso arch

```
### Creating Loader

`esp/loader/entries/arch-rescue.conf`
```(bash)
title   Arch Linux
linux   /EFI/archiso/boot/x86_64/vmlinuz-linux
initrd  /EFI/archiso/boot/x86_64/initramfs-linux.img
options archisobasedir=/EFI/archiso archisosearchfilename=/EFI/archiso/boot/x86_64/vmlinuz-linux
```

**Note**
ESP = EFI Partition Root
