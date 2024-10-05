---
layout: default
title: Recovering Windows systems
description: For when you've done goofed
---

We've all been there. We did some modifications to our Windows systems, reboot aaaand... it's gone.

There are multiple ways to resolve this issue, depending on what exactly went wrong. 

## Prerequisites

You will need a copy of a Windows install disk. It doesn't matter if you have Windows 10/11 Pro installed but can only get your hands on a Windows 10/11 Home install USB. The only thing that matters is the architecture, whether it's 32-bit or 64-bit.

For most of the boot issues, you should be able to fix a Win 11 install with a Win 10 install USB and vice versa, but I haven't tried that.

The steps to get where we need to be for most fixes are as follows:

1. Boot the PC from your USB install key
2. Select your keyboard layout and region settings, but DO NOT click on the install button
3. Instead, press Shift + F10 to drop into a command line interface

### Unlocking BitLocker

Full Disk Encryption is great until you run into issues like this. To do most things here, you'll need to unlock your drive. Thankfully, this can easily be done using the command prompt window we just opened.

You might need to assign a drive letter to your partition first - on how to do this, please see the first section of *Stuck on "Checking and repairing drive"* - it *should* automatically be assigned letter C, but we don't know that without going into DiskPart and checking.

You can then issue one of the following commands, depending on if you have a password for the volume set or have your BitLocker recovery key handy:

```
Manage-BDE -Unlock C: -password [Password]
Manage-BDE -Unlock C: -recoverypassword [Recovery Key]
```

## Boot issues
### UEFI systems

Sometimes, for various reasons, the bootloader and the EFI entries can get messed up. To fix this, you can issue the following commands - and I will explain what each one does.

The first command you will want to run is

```
bootrec /scanos
```

This will scan your harddrives for Windows installs that a bootloader would detect. It can happen, or rather in most cases will happen, that the installer does not successfully identify your install. In that case, the prompt would look like this:

```
Scanning all disks for Windows installations.

Please wait, since this may take a while...

Successfully scanned Windows installations.
Total identified Windows installations: 0
The operation completed successfully.
```
Do not freak out yet.

In most cases, this just means that the EFI entries have been nuked from orbit. This can happen if you recently installed a UEFI update, if you've changed something about BitLocker drive encryption, or even due to a bodged Windows update.

You will want to just reinstall the bootloader files and reset the EFI entry. The command to do this is as follows:

```
bcdboot C:\Windows
```

After this, you want to run the following commands:

```
bootrec /scanos
bootrec /rebuildbcd
```

Which will rebuild the bootloader files, reinstall BCD, the Windows bootloader, and reset the EFI entry.

In most cases, you should already be cooking with gas and can reboot your PC into Windows. 

If this doesn't do the trick, or your issue is different, skip ahead to one of the other sections.

### MBR systems - legacy

It's your lucky day because fixing issues on an MBR system is way easier than on UEFI.

Instead of the commands for the UEFI system, just issue these in the cmd Window:

```
bootrec /fixmbr
bootrec /fixboot
```

That's really it.

If this doesn't do the trick, or your issue is different, skip ahead to one of the other sections.

## Stuck on "Checking and repairing drive"

I'll lead with the bad news: It's likely that your SSD or harddrive died or is on its way out, and that might be why Windows isn't booting.

There is, however, a tiny sliver of hope. For one, it's possible that CHKDSK, the NTFS disk check utility on Windows, is just stuck on something. Otherwise, you might be able to mount the drive on another system and at least pull some data off of it.

First, on the command window, issue

```
diskpart
```

This will put you into the DISKPART shell. You should now see ``DISKPART>`` before every command you type.

First, we will want to issue ``list volume`` which will tell you about the disks installed on your machine:

```
DISKPART> list volume

  Volume ###  Ltr  Label  Fs     Type        Size     Status     Info
  ----------  ---  -----  -----  ----------  -------  ---------  --------
  Volume 0         SSD    NTFS   Partition   3726 GB  Healthy  
  Volume 1         HDD    NTFS   Partition   2794 GB  Healthy  
  Volume 2         OS     NTFS   Partition    476 GB  Healthy    Boot
  Volume 3                FAT32  Partition    100 MB  Healthy    System
  Volume 4                NTFS   Partition    601 MB  Healthy    Hidden
```
Now, you will have to identify your Windows partition by size and/or label. My Windows partition is 476 GB and has the label "OS", so it's Volume 2.

Diskpart supports the long form commands or the short hand commands, which may be fun to read. I mean, come on, who doesn't get a chuckle out of ``ass letter``? You don't? Well, guess I did never really grow up.

Anyway, we're gonna use the long form because it tells us more about what a command actually does. 

First, we want to select Volume 2:

```
DISKPART> select volume 2
Volume 2 is the selected Volume.
```

You can confirm this by issuing ``list volume`` again, Volume 2 should now have an asterisk (--> * <--) next to it.

We now want to assign a drive letter to the volume, so we can run CHKDSK ourselves.

We would do this with the following command, and please make sure you use the exact syntax written down here. I'll be using letter N, because A, B, C, D and X are, to my knowledge, reserved in the Windows installer PE environment and we just want something in the middle.

```
DISKPART> assign letter=N
DiskPart successfully assigned the drive letter or mount point.
```

We will now drop out of the DISKPART shell with ``exit`` - this will give us the normal command prompt back.

Let's now manually run CHKDSK on drive N:

```
chkdsk N:
```

In its output, it will tell us if there were any issues found. First, it will warn us that we didn't specify /F and that it won't fix and issues that it finds, but that' ok. We just want to scan.

You can skip most of the output, the actual interesting part will be at the end:

```
Windows has scanned the file system and found no problems.
No further action is required.

  499371007 KB in total disk space.
  145571552 KB in 585090 files.
     322248 KB in 128957 indexes.
          0 KB in bad sectors.
     840155 KB in use by the system.
  352637052 KB available on disk.
  
       4096 Bytes in each allocation unit.
  124842751 total allocation units on disk.
   88159263 allocation units available on disk.
Total duration: 23.28 seconds (23284 ms).
```

The actually important part is ``0 KB in bad sectors`` - this means the drive should be good, but for some reason CHKDSK got stuck, especially so if it informed you about attibute errors or similar in the above text block.

Run it again with the fix parameter:

```
chkdsk /F N:
```
This should get you back up to speed.

Unfortunately, this won't help if you actually have a hardware problem.

However, if you do, and end up replacing the drive, I may kindly point you to my guide on [Setting up Windows like a pro](https://stepsysadmin.github.io/windows-setup-pro.html)

*I plan on expanding this article with more info in the future, but due to time constraints have published it now already.*

Last update: Fri, Oct 5, 2024