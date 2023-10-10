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
```
adb shell pm list packages -f -3
```
### Fetch Apks of installed Apps
```
for APP in $(adb shell pm list packages -3 -f)
do
  adb pull $( echo ${APP} | sed "s/^package://" | sed "s/base.apk=/base.apk /").apk
done
```
### Fetch Apk of One App
```
adb pull /data/app/org.fedorahosted.freeotp-Rbf2NWw6F-SqSKD7fZ_voQ==/base.apk freeotp.apk
```
## Backup Data
### Backup Data of One App
```
adb backup -apk org.fedorahosted.freeotp -f freeotp.adb
```
### Backup All Data Files of installed apps
```
adb backup -f all -all -apk -nosystem
```
### Backup All Data Files seperately
```
for APP in $(adb shell pm list packages -3)
do
  APP=$( echo ${APP} | sed "s/^package://")
  adb backup -f ${APP}.backup ${APP}
done

```
## Restore
### Method 1
First, you have to install the saved apk with adb:

`adb install application.apk`

Then restore the datas:

`adb restore application.backup`
### Method 2
f you have problems using adb backup (empty files, no prompts, other oddness), you can give a try to bu backup through adb shell. Thanks to @nuttingd comment.
#### Backing up
```
adb shell 'bu backup -apk -all -nosystem' > backup.adb
```
#### Restoring
```
adb shell 'bu restore' < backup.adb
```
## Partitions
### Backup
```
adb pull /dev/block/by-name/SYSTEM system.img
```
### Restore
`adb push system.img /sdcard/`
Then
`dd if=/sdcard/system.img of=/dev/block/by-name/SYSTEM`
