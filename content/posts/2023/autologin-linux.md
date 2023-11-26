---
title: "Autologin Linux"
date: 2023-09-09T08:45:55+05:00
description: "For One Click Boot"
url: /autologin-linux
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
tags:
    - Linux
draft: false
---
Getting one click boot is very satisfactory but you should know the security risks asscoiated with it. Nevertheless, here is the guide to Setup Autologin.
## Configuring TTY
* Replace ar0177417 with your username

```
/sbin/agetty -n -N -i -a ar0177417 tty1 38400 linux
```
## Autostarting Display Server
* Replace Hyprland or startx with your desired WM or startx for xorg
### For Fish Shell
* Add this to your fish config
```
 if status is-login
     if test -z "$DISPLAY" -a "$XDG_VTNR" = 1
         export LIBSEAT_BACKEND=logind
         exec dbus-run-session Hyprland &> /dev/null
     end
 end
if status is-interactive
    # Commands to run in interactive sessions can go here
end
```
### For Bash Shell
* Add this to ~/.bash_profile
```
if [ -z "${DISPLAY}" ] && [ "${XDG_VTNR}" -eq 1 ]; then
  exec startx
fi
```
