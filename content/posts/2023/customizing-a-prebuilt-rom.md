---
title: "Customizing a Prebuilt Rom"
date: 2023-09-29T11:05:18+05:00
description: "Making Android the way you want"
url: "/customizing-a-prebuilt-rom/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: true
---
* Get system.img and boot.img by dumping using adb or fastboot, or from rom.zip
* Mount system.img
```
fuse2fs -o fakeroot,ro system.img <target>
```
* Make Changes
* convert to flashable zip
