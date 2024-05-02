---
layout: default
title: 2024 - The Year of the Linux desktop!
description: My adventures of going Linux as a daily driver
---

### How did we get here in the first place?

One day, yours truly was feeling adventurous and loaded up a copy of House Flipper 2. I played it for around 2 hours and noticed something weird: It was feeling like my guts were trying to turn inside out. I was so nauseous, I had to stop playing and catch some fresh air for a couple of minutes.

"Must have eaten something wrong. Was that milk in the coffee still good?" was my thought process. I thought nothing of it. The next day, I tried to play again and had the same sensation after 30 minutes of playing. I looked up motion sickness in conjunction with HF2, and apparently this game was notorious for causing it. I changed some settings as recommended by the Steam forums - it helped, but not a lot. I didn't play anymore after that, because the next day, I would go on vacation to Zurich and wouldn't want to feel bad on the 5 hour drive there.

Back from vacation, everything settled, apartment to myself - game time. I loaded up a classic. Rockstar Games Bully. I lasted around 25 minutes before the nausea hit. WTF? I did some more digging, and apparently, one day, motion sickness can just come back. I had it pretty severely as a kid, like I would throw up almost every drive over an hour if I tried to read something in the back of the car.

*One thing was crystal clear: For better or for worse, I would have to take a step back from gaming for a while.*

Having been fed up with Windows shenanigans over the years, Windows 11 generally sucking and having to use it for work, and now having no actual need for Windows around, I thought: **Why not give Linux on the desktop a spin again?** 

For daily driver usage, I have a perfectly fine M1 MacBook Air which runs the Office suite and is a pleasure to use when doing research, academic work, etc. I'm a seasoned Linux SysAdmin and it runs on all the servers at work. What could possibly go wrong?

### Preparations and choices

With the choice to switch to Linux made, I would have to prepare accordingly. The first step would be choosing a Distribution. I thought about this, used [Distrochooser](https://distrochooser.de) and talked to some friends, and adventurously hit up... [debian.org](https://debian.org). I know, it might be a weird choice for a desktop operating system because of its focus on stability and the slow updates. However, I'm extremely familiar with the Debian way of doing things, know my way around it, and have used it extensively on servers over the last 7 years.

With a fresh ISO of Debian 12 Bookworm in my Downloads folder and balenaEtcher loaded up, I was almost ready to dive in, until I remembered that I should probably decrypt my BitLocker drives. So I did that and promptly had to wait another 3 and a half hours before I could get started.

Then, I began the installation. To reiterate, my hardware consists of an AMD Ryzen 7 2700X, 32 GB of DDR4-3200 RAM, an NVidia GTX 1660 Ti and for the OS I'm running a 512 GB NVMe SSD. Yeah... an NVidia GPU. We'll see how that works out, even though some stuff is open sourced now.

I installed. Everything worked out quite smoothly with some hiccups here and there. There's no way to control my RAM RGB but I can live with that. First, I installed the MATE Desktop because of familiarity, I even riced it a bit for a retro look. One week in, I decided it would be best if I just switched to something more modern so I installed GNOME 43, the latest available GNOME for Debian.

### Distrohopping

...which is also my main gripe with Debian. I like the way Debian works and I'm familiar with it, but especially for a Desktop, having up to date packages would be quite nice.

For example, I tried to compile Linux 6.8.7 for shits and giggles. I managed to compile my own kernel and it booted, but I had no graphical output because for some reason, nvidia-dkms refused to install on the newer Kernel. So I switched back to Linux 6.1. GNOME was stuck on 43 and wouldn't get an update until Debian 13 which would likely drop in 2025.

But I wanted something more modern. So it was back to the drawing board again. Debian served me well for the 3 weeks I used it, but what would be next up? After thinking about it, I decided on giving Arch Linux a spin again since I've been using that for quite a while around 2019.

One quick ``dd`` followed by an ``archinstall`` and some painstaking ``rsync`` for config files later, we're looking at an up to date GNOME 46 desktop backed by Linux 6.8.8. Things are looking up!

### Arch ain't perfect

Except that I was running X11 when I wanted to be running Wayland. I talked to a buddy and we tried some fixes, but Wayland just wouldn't play ball - probably because of my GPU. The fix ended up being putting an obscure flag into ``/etc/environment``. 

Then, after some updates, my install of ``aurman`` broke and would just throw a Python error. I have no clue what caused it, so I removed it and if I need an AUR package, I'll just download the snapshot and manually install it using ``makepkg``. Only AUR packages I have are my printer drivers anyway.

Then, I wanted to install Blender for a small project I'm trying to do. It would install, but not launch. Checking on the commandline informed me that I was missing ``libdecor`` if I want Wayland support. Install that, we're up and running.

Arch Linux is a pretty refined distro, but there are some rough edges and one should be prepared for manual intervention here and there. If that's absolutely not an option, then... install Ubuntu I guess. Or Fedora. Many options out there.

### But what if you need Windows?

"But what if you need a Windows application?!" - I hear this all the time. Currently, there are two things I do if I absolutely need a Windows app and nothing else will work.

First, there's ``wine`` which has worked pretty well for most use cases. If that's not an option, I still have a Windows 10 Pro VM on my homeserver which I can RDP into. It runs an Intel Core i5-6500, 8 GB RAM and no GPU, but that's more than enough for most apps. For example, to scan directly into my Paperless-NGx instance, I have a copy of the Print&Scan software running in that VM that will push a PDF into a Samba share that's being read by Paperless and consumes the document.

If I need more performance, I have a beefy work laptop that I could run something on. So it ain't all looking too grim. However, until now I haven't come across anything I would hard need Windows for.

### What's next?

Since I'm actually experiencing some positive effects from not gaming, I'll probably stay on Linux for the foreseeable future.

It's been exactly 1 month since I switched and I could see my productivity increase - Linux works well and I love the package management which Windows lacks.

We'll see where we end up.
