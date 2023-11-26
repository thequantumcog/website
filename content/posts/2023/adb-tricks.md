---
title: "Useful Adb Commands"
date: 2023-10-08T12:30:09+05:00
description: "Cool adb tricks to save you some time"
url: "/adb-tricks/"
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
## Backup Apks
### Get list of installed apps
`adb shell pm list packages -f -3`
### Fetch Apks of all Installed Apps
```
for APP in $(adb shell pm list packages -3 -f)
do
  adb pull $( echo ${APP} | sed "s/^package://" | sed "s/base.apk=/base.apk /").apk
done
```
### Fetch Apk of One App
`adb pull /data/app/appFolderNameHere/base.apk app.apk`
## Getting Partitions Imgs
### Backup
`adb pull /dev/block/by-name/SYSTEM system.img`
### Restore
`adb push system.img /sdcard/`  
Then  
`dd if=/sdcard/system.img of=/dev/block/by-name/SYSTEM`

## Logcat
`adb logcat -v color`
