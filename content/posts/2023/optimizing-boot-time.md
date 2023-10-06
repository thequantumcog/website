---
title: "Optimizing Linux Boot Time"
date: 2023-10-05T17:35:10+05:00
description: "Boot your Linux Machine instantly"
url: "/optimizing-boot-time/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
series:
    - Optimizing Your Linux System
tags:
    - Linux
    - Optimizations
categories:
    - Linux
draft: false
---
Boot time is how much time it takes to boot your computer when you press your power button. A lot of things can slow down your boot on Linux. In this article we will discuss this in detail.

## Systemd optimizations
### Disabling unnecessary services
`systemd-analyze` is a command available on systemd distros (which most distros are). It shows which service is using more time to load and you can disable that service. Just don't disable any important service or your computer won't boot at all.\
You can also use the sub-command `systemd-analyze blame` for more clearer output.
### Using `.socket` instead of `.service` for starting service
`.socket` are used to initiate the service process when its needed while `.service` starts the process on boot which costs boot time and unnecessary for services like `cups`
## Slimming Down initramfs
### Mkinitcpio
#### Using Systemd instead of Busybox on early init
By default, the Mkinitcpio configuration uses the `base` and `udev` hooks for building the initramfs. Faster boot times can be achieved by replacing them with systemd
#### Removing Unnecessary Hooks
Use `autodetect` hook for initramfs which auto detects the require hooks
#### Using lz4 compression
lz4 compression is slightly faster than zstd or gzip compressions. You can change this in `/etc/mkinitcpio.conf` 
### Switch to Dracut
Dracut can generate unified kernel images with smaller size if configured correctly. This allows faster kernel loading.

## Using Alternative Init System <font size="2">(Not recommended for beginners)</font>
Systemd started as an init manager but now has absorbed many services and processes. Other init systems such as runit,dinit,s6,etc. are much lighter and allows much faster boot time than systemd
## Disable Splash
 Disabling **Bios Splash and Plymouth Splash** can also speed up the boot because splash adds a delay in boot
## Disable Terminal Output
On some fast systems using SSDs, The tty could also be a bottlneck meaning lesser the terminal output faster will be the boot.
## Staggered Spin-up on HDD
On HDDs staggered spin can also be a problem but it can be fixed by checking dmesg output,i.e, `sudo dmesg | grep SSS`.\
If there is output of this command, then add `libahci.ignore_sss=1` to kernel parameters.
## Conclusion
This is barely scratching the surface in terms of optimization. You can always do some more optimization. Linux is already way faster than Windows and lighter in terms of resource usage. Then on top of that you can optimize it more to get **single digit boot times!**
