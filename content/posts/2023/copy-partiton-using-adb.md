---
title: "Copy Partiton Using Adb"
date: 2023-10-08T12:30:09+05:00
description: "Desc Text."
url: "/copy-partiton-using-adb/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
tags:
    - Android
categories:
    - Android
draft: false
---
```
adb pull /dev/block/by-name/SYSTEM system.img
```
