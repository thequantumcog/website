---
title: "Installing Windows Only Using CMD"
date: 2023-10-06T18:38:39+05:00
description: "The Real Way to Install Windows!!"
url: "/shenanigan-free-windows-installation/"
# cover:
#     image: "images/2023-thumbs/computer.jpg"
#     alt: "Shenanigan Free Windows Installation"
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

### Partitioning

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

### Selecting Windows Version to Install

DISM is the tool that is actually used to install windows. You can use the following command to get index# of the Windows Version you want to install. 

```
DISM /Get-ImageInfo /imagefile:x:\sources\install.wim
```

**Note the Index: # that you want to install**

### Install Windows Data

Now we copy the windows data into the disk.

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
## Bypass OOBE For Windows 11

This bypasses Microsoft Account Requirement.  
**NOTE: DISCONNECT FROM INTERNET before booting!**

```
oobe\BypassNRO
```

System will restart after executing the command.    
Select `Continue with limited Setup` and name the device and create a local account.
## Running debloat script after boot
ChrisTitus created an awesome debloat script. We can use this to debloat windows and make it a little better.
```
irm https://christitus.com/win | iex
```
Also see:[this](https://github.com/massgravel/Microsoft-Activation-Scripts)
## Conclusion
This is probably an overkill way to install Windows that I stole from Titus ;) and this provides a really good insight to what actually happens when you click install in Windows Setup.

