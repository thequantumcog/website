---
title: "Disable Core Dumps"
date: 2023-10-01T09:50:44+05:00
description: "Disabling heavy core dumps that are rarely useful"
url: "/disable-core-dumps/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
categories:
    - Linux
tags:
    - Linux
    - Optimizations
draft: false
---
## Setting Limits
* Edit `/etc/security/limits.conf`
* Append the following lines
```
* hard core 0
* soft core 0
```
## Disabling setgid and setuid programs from core dumping
* Edit `/etc/sysctl.d/9999-disable-core-dump.conf` or `/etc/sysctl.conf`
* Append the following lines
```
fs.suid.dumpable=0
kernel.core_pattern= |/bin/false
```

