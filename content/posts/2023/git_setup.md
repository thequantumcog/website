---
title: "Setting Git Global Configs"
date: 2023-08-06T15:18:17+05:00
description: "Save your time by setting git global configs"
disableHLJS: false
cover:
    image: "<image path/url>"
    alt: "<alt text>"
    caption: "<text>"
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
draft: false

---
Git is an important tool that every developer and even non-developers use to manage versions and handling conflicts of files. Below are some settings that I set globally for my git repos.

Auto Setting push remote
```
git config --global --add --bool push.autoSetupRemote true
```
