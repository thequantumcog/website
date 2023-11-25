---
title: "Create Swapfile"
date: 2023-11-15T19:15:49+05:00
#description: 
url: "/create-swapfile/"
tags: 
    - Linux
categories:
    - Linux
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: false
---
Swapfile and swap-partitions are rarely used now-a-days. But they still have one major use case which is hibernation. Use the following Commands to create and enable swapfile 

### Commands

```
sudo fallocate -l 6G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```
then change fstab (**/etc/fstab**) so it automatically mounts your swap file on startup

`/swapfile none swap sw 0 0`

Afterward, check if your swap file is operating properly with `htop`.


