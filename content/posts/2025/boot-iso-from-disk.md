---
title: "Boot ISOs Directly From Disk"
date: 2025-07-17T18:52:43+05:00
description: ""
url: "/boot-iso-from-disk/"
draft: false
---
## GRUB (Recommended Approach)

It is assumed that ISO images are stored in the `/boot-isos` directory on the **same filesystem** as GRUB.  
If stored elsewhere, you must prefix the path with device identification when using the `loopback` command, e.g.:

```grub
loopback loop (hd1,2)$iso_path
````

### Example GRUB Menu Entry

Add the following to either:

* `ESP/grub/grub.cfg`, or
* `/etc/grub.d/40_custom`

```grub
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

> **Note (Fedora-specific):**
> Fedora ISOs may fail to boot due to issues in setting volume labels when booting _directly_ from ISO.
> Replace `configfile /boot/grub/loopback.cfg` with the following boot directives instead:

```grub
probe --set isolabel --label (loop)
linux (loop)/isolinux/vmlinuz root=live:CDLABEL=${isolabel} rd.live.image verbose iso-scan/filename=${iso_path}
initrd (loop)/isolinux/initrd.img
```

---

### Booting ISOs From Another Partition

#### Global (outside any `menuentry`):

```grub
insmod search_fs_uuid
```

#### Inside each `menuentry`:

```grub
search --no-floppy --set=isopart --fs-uuid 123-456 #UUID-of-Partition
loopback loop ($isopart)$iso_path
```

---

## systemd-boot

> **Important Limitations:**
>
> * `loopback` booting from ISOs is **not supported**.
> * ISO **must be extracted**.
> * Kernel and initrd must reside on the **same disk** as the ESP.

### Extract ISO Contents

```bash
mkdir -p esp/EFI/archiso
bsdtar -v -x --no-same-permissions --strip-components 1 \
    -f archlinux-YYYY.MM.DD-x86_64.iso \
    -C esp/EFI/archiso arch
```

### Create Boot Entry

Create the file: `esp/loader/entries/arch-rescue.conf`

```ini
title   Arch Linux
linux   /EFI/archiso/boot/x86_64/vmlinuz-linux
initrd  /EFI/archiso/boot/x86_64/initramfs-linux.img
options archisobasedir=/EFI/archiso archisosearchfilename=/EFI/archiso/boot/x86_64/vmlinuz-linux
```

---

## Notes

* `ESP` refers to the EFI System Partition root (e.g., `/boot/efi`)
