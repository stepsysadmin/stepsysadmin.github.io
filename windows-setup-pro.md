---
layout: default
title: Setting up Windows like a pro
description: Faster, more secure and highly customized Windows. For everyone!
---
# Setting up Windows like a pro

*Note: There may be terminology here that isn't 100 % correct or diverges from the "official" terminology of some things. I trust that you will understand what I mean. I want to emphasize that you should not, under any circumstances, pirate software and that you're responsible for all changes you make to your software and hardware configuration.*

So you've chosen to install Windows. Whether this was a voluntary decision or not, here we are. Maybe you want to get your gaming fix and Proton didn't live up to the hype for you. Maybe you've tried switching and were uncomfortable with what you've experienced. Or, most likely, you're dissatisfied with Windows, but you need some Adobe Software, Microsoft Office and other things - or you want to at least go to the "dark side" of using Windows before you commit to jumping ship.

This guide is here to help you pick out a Windows edition that fits your needs, give you some tips and tricks for installing it, and maybe even help you configure it and find some cool software for you.

Let's begin.

## Choosing the right Edition of Windows

The only Windows versions worth your time nowadays should be Windows 10 or Windows 11. Any older versions are not fit for being daily driven - due to security implications and hardware aswell as software support. It's almost impossible to get a modern browser going on Windows 7, this should tell you all you need to know.

With that out of the way, we should take a look at which edition you should choose. There are different SKUs we should take a look at: The **Consumer SKU, Enterprise SKU** and **Server SKU.**

The **Consumer SKU** contains versions of Windows like Windows 10/11 Home and Windows 10/11 Pro. You're probably familiar with them because that's what 90+ % of people are running. This is precisely why you should stay away from them, but we'll take a look at that later.

The **Enterprise SKU** has other versions like Windows 10/11 (Pro) Education, Windows 10/11 Enterprise and the respective LTSC versions. This is where it gets interesting.

The **Server SKU** has Windows Server 2016/2019/2022 Standard and Datacenter. 

But which one to pick? I've compiled this table that you can take a look at and decide what you believe fits your use case best:

| Edition | SKU | Description |
| --- | ----------- | ----------- |
| Windows 10/11 Home | Consumer | The lowest tier of Windows licensing, with a lot of arbitrary limitations and ads in the start menu (like candy crush, etc.) |
| Windows 10/11 Pro | Consumer | No limitations on usage, but still comes with a lot of bloat and ads in the start menu and operating system. |
| Windows 10/11 (Pro) Education | Enterprise | Education and Pro Education are basically the same, they're focused on use within educational facilities and they're basically just normal Windows 10/11 Pro, except they don't have any ads in the OS. |
| Windows 10/11 Enterprise | Enterprise | The enterprise tier - basically a slightly debloated Windows 10/11 Pro without ads. |
| Windows 10/11 Business | Enterprise | A stub version of Windows that does not give you any benefit - it's regular Windows 10/11 Pro WITH ads, you get this by joining it to an Azure AD domain with an account that's connected to a M365 Business Premium subscription license. No other way to get this AFAIK. |
| Windows 10 Enterprise LTSC 21H2 | Enterprise | The Long Term Servicing Channel release on the 21H2 version of Windows 10, without many of the creature comforts like Windows Store. Will get updates until 2032. |
| Windows 10 IoT Enterprise LTSC 21H2 | Enterprise | The same as above, except en-US lang only (you can install other language packs via PowerShell), no Windows store, no other amenities (e.g. misses Snipping Tool) and also updated until 2032. This is as lean as it gets for basic Windows desktop functionality. |
| Windows 11 (IoT) Enterprise LTSC 24H2 | Enterprise | The same as the Windows 10 counterparts, just on a Windows 11 desktop base. |
| Windows Server 2016/2019/2022 Essentials/Standard/Datacenter | Server | It's Windows Server, dude. Do with that info what you will. |

Based on my experience and my testing, I've chosen to go with **Windows 10 IoT Enterprise LTSC** for the following reasons:
* It's easily the leanest Windows experience and everything else you need is easily installed back using the (initially unavailable, but enableable) Microsoft Store.
* It does not have any ads in the whole system, and it's a reasonably modern codebase with outstanding support for all Windows software out there.
* Most things work out of the box and won't need to be tweaked.

Now, you might say something like "But there's this Windows 10 GAMING EDITION or EXTREME EDITION ISO out there, it's got a ton of tweaks built in and software bundled and some cool themes and..." - yeah, it's an extraordinarily bad idea to install some random Windows on your PC that may or may not be infested with all kinds of viruses and cryptominers, and probably also comes with a ton of pirated software, too. All the "tweaks" these things have can be applied by yourself in a few minutes, but we'll get to that later.

## Installing Windows

You might say "I know how to do that, no need to tell me, everyone can install Windows" - well, for one, not everyone is a PC wizard, and also, there may be a tip here you haven't heard already so skip over this chapter if you believe this is beyond you.

There are two options to choose here: Installing via a **USB Install Key** or using **WDS (Windows Deployment Services).** Since I have a Windows Server running at home, I'm installing it using WDS. First, you will have to add the install.wim from the Windows ISO to the WDS Image Group, then you can boot over the network and go through the install wizard. You might have to convert the file first if your ISO comes with an install.esd file. I trust that you know how to do this if you have a WDS running on your network.

For everyone else, I recommend the **USB Install Key** method. Make sure you grab a nice, fast USB 3.0 flash drive with at least 8 GB of capacity. Then, deploy the ISO file to the USB key. You want to use the software **Rufus** for that.

Before we start, one last thing: You should always, always, always get a **genuine Microsoft ISO file** for your installs. Reputable sources would be Massgrave or Bob Pony. The download links on those websites are provided by none other than Microsoft themselves.

Alright, deploy the ISO to the USB key with Rufus, make sure to select UEFI as the boot method if your PC supports that. If not, go for the BIOS install version.

After that, boot your PC to the UEFI/BIOS menu and (if applicable) enable Secure Boot and Fast Boot. Set the USB key to be the first boot option and reboot. Then press any key to boot into setup. In there, choose your input method and locale, accept the license agreement and if the installer asks, select the edition of Windows you want. In my case, that would be **Windows 10 IoT Enterprise LTSC.**

Now, select the partition you want it installed on. Make sure you select the right one, double or triple check if needed. Really take your time on this, you could lose data if you're not careful!

*Top tip: If you're doing this for the first time or you're unsure what to choose here, physically open up your PC (after turning it off and disconnecting it from power) and unplug the data connector of all drives you don't want the OS on. This saves you from accidentally formatting something you don't want formatted.*

After choosing the correct partition, hit next and the install will commence. After a while, the PC will reboot. Make sure to **not** boot from the USB key now. You can also just pull it out of the PC at this point.

You will now enter a mode called **OOBE (Out Of Box Experience)** which you've probably seen before when setting up a machine for the first time. If you've installed via WDS or if you're setting up a machine with an OEM license on it (preinstalled Windows), it will now ask you to accept the license agreement.

*Top tip: If you're setting up Windows 11 Home or Pro, now is the time to pull out your Ethernet cable if you have one, and physically disable WiFi on the machine, if applicable. Then, press Shift+F10 which will bring up a command prompt. Type "oobe\bypassnro" (without quotes) to set up the OS without connecting to a Microsoft account.*

After this, you will be asked for your keyboard layout and locale once again - choose the options that apply to you. After setting up networking (and maybe rebooting again, on some machines) you will be asked for Microsoft account credentials. **You want to click on "Domain join instead"** in the lower left hand corner. You don't actually need to join a domain, just click it and type in your desired user name. If Windows tries to guilt trip you with some "great features" you're "missing out on", just ignore that and click continue without Microsoft account or whatever it's called now.

It will also ask you to enter a password for your account, however you can just hit enter to create an account without a password. If you want one, add one later (by hitting Ctrl+Alt+Delete when the setup is done) because then it will not ask you for security questions that way.

This should be it, you should now be presented with a Windows desktop after a couple of minutes of waiting.

## Post setup

So you've installed a clean copy of Windows. Nice! But what now? There are some tweaks that I deem absolutely essential and won't want to miss anymore. 

And would you look at that? I compiled a script that actually does just that for you! You can fetch it here: [stepsysadmin/stepsys-deploy](https://github.com/stepsysadmin/stepsys-deploy)

Additionally, it will install most of the software that I will cover later using WinGet. But first things first. Let's re-enable the Windows Store if you're on an Enterprise LTSC build.

To do this, right click your start menu button and click on "PowerShell (Admnistrator)". In the following prompt, click Yes. Now, type in the following command and hit enter: ``wsreset -i``

What this does is call the Windows Store reset script (wsreset) and pass the "-i" flag which tells wsreset to reinstall all Windows Store components. Once you did this, reboot your computer.

*Top tip: Rebooting in Windows is actually a lot different to shutting down and booting the machine back up. If I say "reboot" I mean actually going into the start menu and clicking "Reboot".*

*Top tip: If you want to run the script I linked, you will need to issue the command ``Set-ExecutionPolicy Unrestricted -Force``, otherwise, PowerShell will refuse to run a script downloaded from the internet. Read the instructions carefully whenever running scripts from an unknown source.*

The script leverages WinGet with the Microsoft store to install some commonly used software. Currently, this includes:

* 7-Zip
* Audacity
* Bulk Crap Uninstaller
* CPU-Z
* Discord
* Voidtools Everything
* ffmpeg
* OneDrive (not installed by default if IoT Enterprise LTSC)
* VSCode
* NAPS2 (Scanning software)
* GPU-Z
* Windows Terminal
* VLC media player
* WizTree
* Firefox
* Thunderbird
* nomacs (Image viewer)
* yt-dlp (Commandline)

Please remember that this is my configuration, so it makes sense that the script configures Windows and installs the software how *I* like it. You may have different preferences, so feel free to fork/modify the script to your liking!

It also sets some other settings and adds some registry tweaks, namely these:

* Enable verbose logon messages
* Disable spell check and auto correct
* Set "device usage mode" to "Gaming" (I actually don't know what this does, but it seems that it sets "game mode" to always on. I guess it can't hurt.)
* Enable Win32 long paths
* Show file extensions by default
* Disable hardware accelerated GPU scheduling (fixes the bug where playing ETS2 on one screen and watching YouTube on another one would make the video stutter)
* Enable Swap effect upgrade cache (optimizes performance for windowed games)
* Disable startup delay
* Disable app launch tracking
* Disable file history
* Disable find my device
* Disable shared experiences
* Disable ads, reset advertising ID, disable suggestions and disable Windows timeline
* Disable potentially unwanted application reporting within Defender
* Disable automatic sample submission within Defender

You might need to run [asheroto/winget-install](https://github.com/asheroto/winget-install) to actually be able to use WinGet before running the script.

Additionally, there are a ton of useful and trusted resources for you to get Windows set up in a more privacy respecting and user friendly way. The instructions can be found on the respective website. Here are a few:
* Chris Titus WinUtil if you prefer a graphical interface for tweaking: [WinUtil by Chris Titus](https://github.com/ChrisTitusTech/winutil)
* O&O ShutUp10 for privacy tweaks: [O&O ShutUp10!](https://www.oo-software.com/shutup10)
* Privacy.sexy for a large variety of privacy and security tweaks: [https://privacy.sexy](https://privacy.sexy)
* Microsoft PowerToys for some powerful software: [Microsoft PowerToys \| Microsoft Learn](https://learn.microsoft.com/en-us/windows/powertoys/)

Congrats! You've now made your Windows more private and have installed the software that you actually want to use.

*I plan on expanding this article with more info in the future, but due to time constraints have published it now already.*

Last update: Fri, Sep 6, 2024
