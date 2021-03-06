---
layout: post
title: "How to Setup a Home Lab in Virtualbox"
description: Learn how to use Virtualbox to create your own cybersecurity or development environment without affecting your primary OS
categories: Hacking
---

## Introduction
This tutorial will serve as a how-to for setting up an environment in [Virtualbox](https://www.virtualbox.org/manual/ch01.html), a cross-platform virtualization app that millions use for security research, software development, and other computer-related activities. The reason almost every security researcher and software developer uses virtualization technology such as Virtualbox is to isolate their work from the primary operating system they use for other activities that contain private information (banking, email, etc.). This ensures that any personal research or development does not compromise the stability, security, or privacy of your primary computer system.

Before we begin, you need the following things:
1. A computer that you are able to install applications on (Windows, Linux, or Mac doesn't matter)
2. Internet connection
3. ~40GB free hard drive space. This is just a rough estimate, but by the end you will have created at least 3 virtual machines that need at least 10GB each along with other programs.

## Download Resources
Please visit the following sites and, if applicable, download the appropriate versions for your current operating system:
* [Virtualbox](https://www.virtualbox.org/wiki/Downloads)
* [Virtualbox Guest Additions](https://download.virtualbox.org/virtualbox/) - Select the version that matches the Virtualbox app, and then download the Guest Additions ISO
* [Kali Linux ISO](https://www.kali.org/downloads/) - 32bit or 64bit depending on host OS
* [Ubuntu 17.10 ISO](https://www.ubuntu.com/download/desktop)
* Windows ISO - Use your Google skills to find a Windows ISO. Should be Windows XP or newer, but I don't recommend Windows 10 due to its built-in "Windows Defender" and other security features that might mess with your workflow.

## Initial Setup
To start, install Virtualbox with all the default settings. A few adapters will be created on your host OS for network connectivity. Once the installation completes, click the "New" button to create a new virtual machine.

To create a virtual guest machine, you need to know the following things:
* How much available disk space you have to set aside for the guest machine
* How much RAM you are willing to devote to the virtual machine

For this tutorial, I will assume that you have a system with 2GB of RAM and 10GB of disk space available for each virtual machine. The creation process is the same for both. Press the *New* button to start. For Linux, choose Linux for *Type* and Ubuntu 64-bit for *Version*. Windows will depend on which version you chose.  Select 2048 for memory size. For everything related to virtual disk, choose the default settings except for the size, which should be 10GB for Kali/Ubuntu and 20GB for Windows.

After following the above steps for the three machines, you should see three guest machines in your Virtualbox manager. Right-click on each one and go to Settings -> Storage and click on the CD disk image. The top right should have a drop-down menu with the same disk image icon. Select the ISO file you downloaded earlier for the respective guest machine. This disk will serve as your boot image while you install it to the virtual disk (the .vdi file also visible in the Storage settings screen).

Once you have virtually inserted the ISO into the CD drive, turn on the virtual machines. Go through the installation process for each machine. At some point it will ask to overwrite or format a drive. **Dont' panic!** This is the virtual *.vdi* drive that you saw earlier, not your actual host drive. Nothing that you do within the guest machine installation process will affect your host machine, so if something breaks, just delete the Virtualbox guest folder and try again.

Now that you have your machines installed, you need to eject the installation CD before you can actually start using the guest machine. Go back to the Settings -> Storage screen and click on the drop-down menu to remove the disk from the virtual drive. After that, the CD drive should be empty and you can boot your guest machine. If you forget this step, your machine will keep trying to boot from the installation medium.

## Networking
Now that you have working guest machines, we can now get into customizing the machines for our needs. For example, reverse engineers might not want any network connectivity in order to isolate malware, while pentesters might want the guest machines to communicate with other guest machines in order to send exploits across a virtual network. Software developers might need to connect to a remote server frequently to send/receive data and as a result need full Internet connectivity. Virtualbox makes it very easy to configure networking on each guest so that any of these above configurations work.

Virtualbox supports the following modes of networking:
* Bridged - This mode uses the host network adapter directly and allows the guest machine to be in the same subnet as the host machine. It is effectively equivalent to another device being placed on the wireless or wired network as your host. This mode is best for software developers and other users who are not worried about having their work share the same network as their host machines, and is not a good idea for researchers reversing malware or other potentially malicious programs.
* NAT - This mode creates a seperate network for your guest machines by placing it behind a virtual router. DNS and DHCP are all automatically configured but can be modified in the manager settings. Most of the time, you won't need to customize anything. This mode gives you Internet access, connects your guest machines, but isolates your guest virtual network from the host network. This is the default network mode since it is how your home network is probably configured and is the most familiar to users
* Host-only adapter - Very similar to NAT in terms of functionality for the guests, but now the host can now directly access the guest machines.
* Not attached - No network functionality. The guest machine has no network adapter whatsoever.

**TLDR**: Use NAT in most cases, bridged if you need to access the guest directly from outside the host, and host-only if you need to access the guest directly from the host but not outside the host. NAT and bridged provide Internet connectivity, while host-only does not.

## Other Settings
Besides networking and basic OS installation, there are a few other settings you should configure.
* Display -> Video Memory - I usually maximize this setting if my guest uses a GUI. Otherwise, just keep it at the default if you are using CLI or remotely connecting to it via SSH.
* System -> Processor -> Enable PAE/NX - You should enable this if you use more than 4GB (4096 MB) of RAM for a single guest OS.
* Processor -> If you have multiple cores on your CPU, you can configure a guest to utilize multiple cores. 

## Conclusion
That's about it! Now you are able to do any infosec or software development work to your heart's content without affecting your host OS. Feel free to try new things and hack away without worrying about the stability or security of your host computer or paying money for a VPS or seperate system. 
