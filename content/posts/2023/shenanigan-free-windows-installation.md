---
title: "Shenanigan Free Windows Installation"
date: 2023-10-06T18:38:39+05:00
description: "The Real Way to Install Windows!!"
url: "/shenanigan-free-windows-installation/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
tags:
    - Windows
categories:
    - Windows
draft: false
---

## The Installer
Download and Launch the Windows Installer.  
Launch Command Prompt with `Shift+F10`

### Partitions

- List Disks with `list disk`
- Select desired disk with `sel disk #`
- Check to verify there is NO partitions `list partition`
- (Optional) Delete any existing partitions `del part #`  
**NOTE: THIS ERASES ALL DATA**
- You can also use `clean` for deleting all partions.
- Check to verify DISK is GPT `list disk` and use `convert gpt`   
**If GPT is not Enabled**
- Create Boot partition `create partition efi size=100`
- Create Data partition `create partition primary size=*`
- Select Boot `sel partition 1`
- Format Boot `format fs=FAT32 quick`
- Assign Boot partition `assign letter=g:`
- Select Data `sel par 2`
- Format Data `format fs=NTFS quick`
- Assign Data partition `assign letter=c:`   
**NOTE: You may need to UNASSIGN an existing C: drive**

### Verify the Windows Version to Install

DISM is at the heart of every Windows installation. You need to do a verification on your installation ISO to figure out the source index # that you will install. 

```
DISM /Get-ImageInfo /imagefile:x:\sources\install.wim
```

Note the Index: # that you want to install

### Install Main Windows Data

Now we copy over the operating system in its entirety.

```
DISM /apply-image /imagefile:x:\sources\install.wim /index:2 /applydir:c:
```
### English (World) Debloating Trick
This will remove a lot of tiles from windows start menu and provides overall clean experience
```
dism /Image:c: /Set-UserLocale:en-001
```
### Copy Boot Files to EFI

Copy the boot files to complete the EFI partition to boot into our windows.

```
bcdboot c:\Windows /s G: /f ALL
```
## Running debloat script after boot
ChrisTitus created an awesome debloat script. We can use this to debloat windows and make it a little better.
```
irm https://christitus.com/win | iex
```

## Bypass OOBE For Windows 11

The Out of Box Experience is changing all the time. The requirement to be online or only use a Microsoft account. Bypass it with this command and using `Shift+F10` to bring up the command prompt.  
**NOTE: DISCONNECT FROM INTERNET before booting!**

```
oobe\BypassNRO
```

System will restart after executing the command.    
Select `Continue with limited Setup` and name the device and create a local account.
## 
