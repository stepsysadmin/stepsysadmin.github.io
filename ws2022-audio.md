---
layout: default
title: Windows Server 2022 Audio issues
---

I ran into this while setting up my [Home Server](./homeserver.html) and am documenting it for anyone that might face a similar issue at some point.

**I'm running Windows Server in a VM in Proxmox, have a video capture device passed through (capture card/webcam), video is working. but I don't get any Audio output and can't capture the audio using any recording software!**

The reason for this behavior is that Windows Server doesn't automatically create any "Windows Audio Endpoints" and thus doesn't create an input device for your capture card. It also doesn't create an audio input device if there are no audio output devices present. To fix this, do the following, exactly in this order (we're assuming a fresh Windows Server setup):

**In Windows:**

* Run, services.msc
* Set service "Windows Audio" and "Windows Audio Endpoint Builder" to start automatically
* Reboot the VM
* Settings, Privacy, Allow apps to use the Camera & Microphone: ON
* SHUT DOWN the VM

**In Proxmox:**

* Open the VM, then go to hardware, add
* Add an audio device, device=ich9-intel-hda (Will show up as generic HD Audio Device in Windows), and use "None (dummy device)" for the backend driver
* Fire up the VM

**In Windows again:**

* Settings, Audio settings, set default output device to one of the speakers
* Default input device should be the device you want to capture from (in this case the physical capture card)

Congrats, you can now boot OBS to record from your device.

**I did all of this but as soon as I end the RDP session, the audio recording stops, but recording video still works**

That's because RDP automatically creates an audio device called "Remote Audio" and forcibly overrides all of the other configs present at the moment. So far, there's no fix for this as force disabling RDP Audio in the registry means disabling all audio functionality, placing us back at square one.

To circumvent this, just connect via literally any other protocol (I'm using VNC with TightVNC server, it's free)

