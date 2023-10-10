---
title: "Using Fingerprint for Sudo Password"
date: 2023-10-10T12:08:53+05:00
description: "Never type a sudo password again!"
url: "/using-fingerprint-for-sudo-password/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: false
---
Typing sudo password again and again becomes very frustrating at times. But there is a solution to this madness.
You can use fingerprint for this process which is not that secure but better than using a root account.
## For Linux
### Debian/Ubuntu Based Distros
- Run `sudo pam-auth-update`
- And use the space bar to enable Fingerprint authentication in the dialog
### Arch Based Distros
- Install `fprintd` and `imagemagick`   
**Note: Some devices may require a different fork of libfprint.[See Here](https://wiki.archlinux.org/title/fprint#Installation)**
- Enroll fingerprint with `fprint-enroll`
- Append these lines to `/etc/pam.d/sudo`
```
auth required pam_env.so
auth sufficient pam_fprintd.so
auth sufficient pam_unix.so try_first_pass likeauth nullok
auth required pam_deny.so
```

## For Mac
- Add `auth sufficient pam_tid.so` to `/etc/pam.d/sudo`

