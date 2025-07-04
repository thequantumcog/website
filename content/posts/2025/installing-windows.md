---
title: "Installing Usable Windows the Improper Way"
date: 2025-07-04T11:12:13+05:00
description: "Just a quick consolidation of all my tweaks in one place"
url: "/installing-windows/"
tags:
 - Windows
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
#draft: true
---
Installing Windows is not about _installing_ anymore. It is about disabling all the garbage, ads and tracking microsoft has put into windows. Even though I am a Linux user, I still sometimes have to use windows for university/helping someone.

Here are some tweaks I always do while setting up a new system.
## Tweaks
* I found autounattend to be extremely helpful, you can disable all the telemetry in one place and auto crete accounts [UnattendGenerator](https://schneegans.de/windows/unattend-generator/)
* To Activate Windows, I use massgrave from powershell `irm https://get.activated.win | iex`
* Then I run the CTT utility which makes it easy to make essential changes and run O&O Shutup from one place. `irm christitus.com/win | iex`  
* I mostly install Windows for MSOffice. I use [Office Tool Plus](https://otp.landian.vip/en-us/) to download office. **_I know_** you can also use Office Deployment Tool, but the benefit of OTP is that you can generate ISOs so you don't have to download office again if installing on multiple computers.

