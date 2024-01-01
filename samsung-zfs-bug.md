---
layout: default
title: Samsung SSD Firmware Bugs and ZFS
description: A song of them not working all that well together
---

A while ago, around 2021, I was tasked with ordering a server for the company I work at. It was the first enterprise server we really purchased, and so we went through a vendor and I made sure to get their opinion. The server itself was a beautiful machine. 

AMD EPYC 7002P 32-core CPU, 128 GB of DDR4-ECC RAM. Supermicro IPMI, and for the system drives, two Samsung PM935 datacenter SSDs. The vendor had an official compatibility matrix, and everything was said to run A-OK with Proxmox VE 7.

A couple of weeks later, the server arrived. I set it up, installed Proxmox VE 7 and set up the PM935s as a ZFS-RAID 1 to boot the OS off of. Everything worked smoothly for about 2 weeks, when I got an e-mail from the server:

```
The number of I/O errors associated with a ZFS device exceeded acceptable levels. ZFS has marked the device as faulted.

 impact: Fault tolerance of the pool may be compromised.
    eid: 154
  class: statechange
  state: FAULTED
   host: pve-main
   time: 2023-01-04 12:33:29+0100
  vpath: /dev/disk/by-id/ata-SAMSUNG_MZ7L3240HCHQ-00A07_(serial)-part3
  vguid: (redacted)
   pool: (redacted)

```

...which is great news if you've just built a brand new server! In any case, I thought it was pretty weird, so I hit up the support team of our server vendor and opened a ticket with them. They asked me for some more info, like a full ``pvereport`` from all of the nodes in the cluster and the ZFS info. Interestingly enough, issuing ``zpool status`` showed only one of the SSDs (Samsung PM935 256 GB) was experiencing write errors in excessive numbers:

```
root@pve-main:~# zpool status
  pool: rpool
 state: DEGRADED
  scan: scrub repaired 0B in 00:07:36 with 0 errors on Wed Jan 4 12:33:29 2023
  status: One or more devices are faulted in response to persistent errors. Sufficient replicas exist for the pool to continue working in a degraded state.
  action: Replace the faulted device, or use 'zpool clear' to mark the device repaired.
config:

        NAME                                                 STATE      READ WRITE CKSUM
        rpool                                                ONLINE        0     0     0
          mirror-0                                           ONLINE        0     0     0
            ata-SAMSUNG_MZ7L3240HCHQ-00A07_(serial)-part3    FAULTED       0   216     0
            ata-SAMSUNG_MZ7L3240HCHQ-00A07_(serial)-part3    ONLINE        0     0     0
```

While the ticket was being worked on with the support team, I checked the ``zpool status`` again the next day, and what do you know:

```
root@pve-main:~# zpool status
  pool: rpool
 state: DEGRADED
  scan: scrub repaired 0B in 00:07:36 with 0 errors on Thu Jan 5 12:37:52 2023
  status: One or more devices are faulted in response to persistent errors. Sufficient replicas exist for the pool to continue working in a degraded state.
  action: Replace the faulted device, or use 'zpool clear' to mark the device repaired.
config:

        NAME                                                 STATE      READ WRITE CKSUM
        rpool                                                ONLINE        0     0     0
          mirror-0                                           ONLINE        0     0     0
            ata-SAMSUNG_MZ7L3240HCHQ-00A07_(serial)-part3    FAULTED       0   216     0
            ata-SAMSUNG_MZ7L3240HCHQ-00A07_(serial)-part3    DEGRADED      0   318     0
```

I escalated the ticket with the vendor, and their reply was something like this (translated by me):

> The issue you're outlining in your ticket is similar to an issue another customer with the same drive brought to our attention. 
>
> At the moment, our best guess is that there is a bug in the Firmware on Samsung SSDs that will trigger write errors in ZFS which aren't present in the raw data that's actually being written to the drive. Our recommendation is a replacement of both SSDs in your system.
>
> **We're currently evaluating the issue with the Proxmox devs and the ZFS development team.**
>
> The other customer's issue was fixed by replacing the drives with Intel D3 SSDs, which is what we can offer you at the moment, at our expense, of course. If you give me the go ahead and confirm the shipping address, I can have the drives out for express shipping by noon.

They did indeed send over the Intel SSDs which I replaced the Samsung SSDs with. That fixed the issues and they're running 24/7 at zero errors since.

Around 10 months after the first rodeo, I got another e-mail from another Proxmox node in our cluster:

```
The number of I/O errors associated with a ZFS device exceeded acceptable levels. ZFS has marked the device as faulted.

 impact: Fault tolerance of the pool may be compromised.
    eid: 110
  class: statechange
  state: FAULTED
   host: pve-1
   time: 2023-11-02 16:12:35+0100
  vpath: /dev/disk/by-id/ata-Samsung_SSD_870_EVO_1TB_(serial)-part1
  vphys: pci-0000:08:00.0-ata-2.0
  vguid: 0xBA8E3409028F6E59
  devid: ata-Samsung_SSD_870_EVO_1TB_(serial)-part1
   pool: vmstor-ssd-pve-1 (redacted)
```

This one should explain itself.

So far, I have personally seen, or been reported this error on the following drives:

* Samsung PM935 Datacenter SSD, 256 GB
* Samsung 870 QVO SSD, 4 TB and 8 TB
* Samsung 870 EVO SSD, 256 GB


I only stumbled upon this because I was looking up server configurations recently, and found that when I last checked (Dec 22, 2023), our server vendor has marked **all** Samsung SSDs as **incompatible with ZFS.**

So, beware when picking which drives to use!
