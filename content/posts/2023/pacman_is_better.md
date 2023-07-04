---
title: "Pacman is a way better Package Manager"
date: 2023-07-04T13:06:37+05:00
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: "Desc Text."
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
draft: false
---
I was trying to edit /etc/pam.d and fixing elogind on my Artix Installation that I messed up my pam.d directory. On almost every other distro, I have to _reinstall_ the distro to fix this. But on Arch Based Distro, You can check which files are owned by which package. Then by using this information, you can regenerate any directory by reinstalling the package.
## Command
You can regenerate directory by using the following Command:

`pacman -S $(pacman -Ql | grep /etc/pam.d/$ | awk '{print $1}')`

This is very useful specially for rolling and bleeding edge distros. Using this you can regenerate directories. If you want regenerate a specific files just substitute `/etc/pam.d/$` with the name of file.
