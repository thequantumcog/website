---
title: "Make GSI RW (For Ext4)"
date: 2024-02-07T17:00:35+05:00
description: "Get back the write access to System Partition"
url: "/make-gsi-rw/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: false
---
TWRP/ORFR is optional for this but its easier so I will be using that method.
```
adb shell
lptools resize product_a 335872 # Do not change this value
lptools resize system_a 5368709120 #4617089843 or 5368709120 (4.3GB or 5GB system)
```
- Reboot Recovery after this
- Flash [product_gsi](https://xdaforums.com/attachments/product_gsi-img.5371179/)
```
e2fsck -f /dev/block/by-name/system
resize2fs /dev/block/by-name/system 5G 
e2fsck -E unshare_blocks /dev/block/by-name-system
```
