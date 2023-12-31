---
layout: default
title: Home server setup
description: My little home server and how I set it up
---

We all want a home server. You may not know it, but you want one. Why though? It's pretty simple: You can make your life a lot easier and automate many things that you'd otherwise have to painfully do manually. I've been running a home server for many years now and have a nice assortment of services that I run on it.

### The dinosaur

My old, "dinosaur" home server, which I used to run for many hours a day, was a very inefficient machine but it did most things I needed it to do. Here's the hardware specs:

- HP ProLiant DL380 G6
  - 2x Intel Xeon E-5530 4C/8T
  - 72 GB DDR3-ECC RAM
  - No GPU
  - 4x Broadcom NetXtreme Gigabit Ethernet
  - HP Smart Array P410i RAID Controller
    - 1x 120 GB Intenso SSD (boot)
    - 2x 500 GB Toshiba 2.5" HDD
    - 1x 2 TB WD 2.5" HDD
    - 1x 750 GB Seagate 2.5" HDD

This chonker pulls a cool 120 Watts at **idle** and more than 400 watts at full load. The fans scream bloody murder everytime you use that full power, and in my configuration, that's just 40% fan speed. The two redundant PSUs could pull up to **one kilowatt** once fully loaded.

Clearly, this was starting to cut into the power budget with electricity being near unaffordable over here (0,37€/kWh).

So, what do? I still had that box around from when I used to run a custom router, so...

### The turtle

I spun up the turtle. Hardware specs:

- Advantech SYS-2USM02-6M01E
  - Intel Atom D510 (2C/4T) @ 1.6 GHz
  - 2 GB DDR3
  - 4 TB Samsung 870 QVO SSD

It sounds about as slow as it was, BUT it did serve me very well. In the end, it ran all the services I needed:

* Jellyfin 
* Opengist 
* WordPress for local development only
* Paperless-NGx
* nginx Proxy Manager
* Baikal
* Technitium DNS Server

Not exactly very fast, mind you, but it did run them. It's been a real trooper, it's served me very well and still does, but it is just time to let go. My ever growing Paperless library is bringing it to its knees almost daily, and I can fit a lot more stuff into the power envelope of 15-20W that it uses.

So I started looking for some mode modern options.

### The kolibri

I have since taken to doing some streamripping, i.e. recording things that are on streaming services like Netflix, Disney+ and so on. Pros are that you can easily make a list of what you want to see and are then able to record it all, over night for example (some services working better than others) and using ffmpeg to slice the files like needed.

**Hardware:**

* Fujitsu Esprimo D756/E90+
* Intel Core i5-6500
* 16 GB Crucial DDR4-2666

**USB Devices:**

* 1x Generic HDMI USB Capture card
* 1x Generic HDMI splitter that strips HDCP from content (power only)

**Storage:**

* Micron NVMe SSD 512 GB (from decommissioned laptop), Proxmox boot + VM storage, ext4
* Samsung QVO 840 4096 GB (decommissioned from work but 100% SMART and 170 TBW / rated for 9000 TBW), media storage, ext4
* Western Digital HDWD20EZRZ 2048 GB (bought myself), file storage
* 1x Toshiba 2.5" 500 GB HDD (from Telekom media receiver, never written to)
* 1x Random old 750 GB HDD (idk where this is from honestly but it works, I wouldn't store anything important on it)

Measured power in current configuration, 2 VMs, idling: Fluctuating between 17W and 21W

**Software:**

Operating System: Proxmox Virtual Environment 8.3

**VMs:**

Debian 12
Windows Server 2022 Standard

**LXC containers:**

Debian 12 container template

**Running on Debian 12 VM:**

**Native:**

* smbd
* sshd

**Docker:**

* nginx Proxy Manager
* Baikal
* Apache Guacamole
* Jellyfin
* MeTube
* OpenGist
* Paperless-ngx
* Stirling PDF
* binhex/arch-delugevpn
* OBS-Web
* benphelps Homepage

**Running on Windows Server 2022 Standard:**

* Windows Deployment Services (WDS)
* Microsoft DHCP Server
* Microsoft DNS Server (fallback for Technitium DNS)
* Microsoft Samba Server
* Microsoft SSH Server
* OBS Studio
* HandBrake

**Running on Debian 12 LXC Container:**

* Technitium DNS Server

**Roadblocks and drawbacks of this setup:**

I have the iGPU passed through to the Windows VM which might sound weird because the main reason I upgraded was to have hardware transcoding in Jellyfin. So that's stupid... or is it? When recording via OBS (streamripping), the framedrops when using the software encoder are just too much, so I absolutely need the hardware acceleration from the iGPU, no question about it. This means that I record on Windows, transcode the footage into a Jellyfin friendly format on Windows, and SMB it to the Linux VM and SSD for playback in Jellyfin. This is an alright solution for me and it's serving me very well.

However, Intel QuickSyncVideo support on Windows... sucks! For some reason, you can either QSV DECODE or QSV ENCODE, which in the default configuration leads to HandBrake crashing on selecting the hardware accelerated encoder with a cryptic error message. To fix this, one needs to quit OBS (the hardware accelerated preview cannot be running during this), go into the HandBrake settings and DISABLE "Prefer using QuickSync for decoding video" while simultaneously ENABLING "If available, use low power QuickSync hardware". After that, select "Encoder: H264 (QSV)" and you're cooking with gas.

I ran into some [Windows Server 2022 Audio issues](./ws2022-audio.html) which I was thankfully able to fix as outlined in that post.

Why not pass the iGPU to Linux, transcode on there and record there, too? I'd have to use the ffmpeg commandline for everything, and I'm not a masochist.

Also even if there's no playback on the Fire TV Stick happening, and OBS is just running in the background, it will use around 10% of the CPU, causing power spikes. Not the end of the world, but something to be aware of.