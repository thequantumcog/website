---
title: "Optimizing Linux Boot Time"
date: 2023-10-03T19:35:10+05:00
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
draft: true
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

## Using Alternative Init System <font size="2">(Not recommended for beginners)</font>
* Use init manager other than systemd
## Disable Splash
* Disable Bios Splash
* Disable Plymouth Splash
## Disable Terminal Output
On some fast systems using SSDs, The tty could also be a bottlneck meaning lesser the terminal output faster will be the boot.
## Staggered Spin-up on HDD

