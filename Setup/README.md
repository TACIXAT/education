# Setup

## Background

In this module we'll be downloading the Linux operating system Xubuntu and installing it as a virtual machine in Virtual Box. This may sound foreign and scary but it is actually very simple. 

### What's a heckin Virtual Machine?

Your physical computer has physical hardware that runs your operating system. Your operating system might be Windows, OSX if you're on an Apple computer, or some Linux variant. In terms of virtual machines, the operating system (your current operating system) running the virtual machine software is referred to as the **host operating system** or host OS. 

Now, a virtual machine, or VM, is a virtual computer that runs as a program on your computer. All the hardware is emulated, or if you will, *virtual*. The software that orchestrates the virtual machines is sometimes referred to as a *hypervisor*. The virtualization software (i.e. the hypervisor) we will be using is VirtualBox. Some other popular virtualization software are VMWare (consumer and enterprise solutions), Parallels (OSX specific), and QEMU (more technical). 

We will be covering VirtualBox here, since it runs on all major platforms and is free. In order for the virtual machine to perform well, you'll want at least 4 GB of ram, and you should have 50 GB of disk space available, just to make sure you aren't cutting things too close. 

Go ahead and download the appropriate version of VirtualBox for your host OS from [virtualbox.org/](https://www.virtualbox.org/). Once you have it, click through the installer.

## Xubuntu

We will be installing Xubuntu in VirtualBox. This file is a bit bigger, so go ahead and start the download from [Xubuntu.org/download](https://Xubuntu.org/download). You will most likely want the 64 bit version. It is pretty rare that someone is running a 32bit CPU these days, but if you are, grab the 32bit version instead. If you have a torrent program installed, the torrent downloads will be considerably faster. If you have no clue what that is, just download it directly through the web via a mirror.

In this case, Xubuntu is referred to as the **guest operating** system as it will be running inside of the virtual machine. Xubuntu is the Ubuntu Linux distribution with the XFCE desktop environment. Ubuntu's default desktop environment, Gnome 3, is graphics heavy. While I like stock Ubuntu and use it as my goto OS, it isn't suitable for virtual machines due to their constrained resources. XFCE is a lot lighter, which is why we are using Xubuntu. The underlying system is still Ubuntu, just with a different desktop environment.

I've selected Ubuntu for this course. It is also what I use for my day-to-day work. Ubuntu is the most popular Linux distribution, becuase of this, a lot of software is built and tested to work on it which means an easier time for you. 

Ubuntu makes two major releases each year. One in April (04) and one in October (10). The releases are coded by the year and month that they are released. For example, 15.10 is the release from October 2015. The April realese on even years is a **Long Term Support release**, or LTS. These releases are supported and updated for 5 years, where every other release is supported for 9 months. This means you generally want to install a long term support release, unless you are planning on reinstalling the system in 9 months.

The most recent LTS release is 18.04, which is what we will be using for this course. If you are watching this and 20.04 has been released, you can use that but you might run into some minor inconsistencies with the videos or book, but I am confident you will be able to work through these with a little searching and fiddling. If all of this is very new, 18.04 is a safer choice. 

## Installation

At this point you should have clicked through the VirtualBox installer. So go ahead and run VirtualBox.

In VirtualBox we can click the blue New button in the upper left hand corner. Typing in Xubuntu as the name should automatically switch the drop downs the Type: Linux and Version: Ubuntu (64-bit). If not, go ahead and select those. If you downloaded the 32 bit version of Xubuntu, you'll want to use Ubuntu (32-bit) instead. Click Next. 

On this screen you select how much ram you want to allocate to the VM. If you have less than 8 gigs of ram on your system you can leave the memory at 1024 MB, if you have more than that, it should be fine to bump to 2048 MB. Click Next and we're going to create a virtual hard disk now. Click Next. The VDI format is fine, so we will click Next again. 

This page is whether you want the file that represents your virtual hard disk to grow as you use it, or if you want it to be the full size at start. Dynamically allocated is fine and will save some space on your hard drive, so we will click Next again. 

This screen allows you to select how much disk space you need. 20 GB is a good choice for temporary systems. You can also change the location of the disk on this page, but it should be fine in the default folder. Now we click Create and our system is ready to install. 

The first time you launch the VM, VirtualBox should prompt you to locate the install media. We can go and navigate to our Xubuntu ISO and select that. If you ever mess this up, which I am do quite often, you won't get the prompt and instead see a message `FATAL: No bootable medium found! System halted.`. Don't panic. Just power off the VM. Right click and go into Settings. Select the Storage tab. Under `Controller: IDE` click the CD icon that says Empty. Then click the CD icon with an arrow on the far right. Select `Choose Optical Virtual Disk File` and navigate to the Xubuntu ISO.

Now when we boot our system it will boot to the Xubuntu CD. VirtualBox will display some informational messages about capturing your mouse and keyboard, and how to release them, you should read those. The disk boots into a *live* version of the operating system. You can test it out from here, but we can just click Install Xubuntu to keep things moving. 

We'll check download updates while installing and install 3rd party software then clikc Continue. We will "erase" our virtual disk and install Xubuntu and click Install Now. Click Continue. On this screen select your timezone and click Continue. Then select your language and click Continue. Enter a name. The computer can be named xubuntu-vm. Then choose a password. Since this is an educational VM I think it is fine to log in automatically. Clicking Continue will begin the install. 

Once the install is finished we can click Restart Now. It will give us the opportunity to remove the install disk, since Xubuntu has already done that for us, we can just hit enter to launch the system.

## Booting

When you boot up you will get a list of options to boot. This is in the bootloader. This particular bootloader is GRUB, the GNU GRand Unified Bootloader. The default option, Ubuntu, is the latest kernel you have installed. If you go into Advanced Options you will see your current kernel, after a few updates you'll have a couple options in here. This is useful because sometimes you will update and there will be a kernel bug that affects something you are working on. You can then roll back to an older kernel to see if the kernel update was the cause. The other useful thing in here is Recovery Mode. Recovery Mode allows you to get a root shell on the system without any authentication. This is invaluable when something breaks, but means that anyone with physical access to your computer has root access. If that is something you need to consider in your threat model, you can disable recovery mode. Let's go back by hitting escape and select our default boot option.

Now, we're going to install VirtualBox Guest Additions. These are tools installed in the guest operating system that can communicate with the VirtualBox application. They make using a VM much nicer, for example, if you resize the window the guest additions will automatically adjust the resolution to match it. We'll install these by going to Devices, and then Insert Guest Additions CD. A file browser will pop up with the contents of the CD, but since we're running a shell script, we'll go ahead and close that and open a terminal by pressing `Ctrl` + `Alt` + `T`. You can also click the XFCE icon in the top left and select `Terminal Emulator`. You'll learn more about Linux and the command line in the Linux module, for now, you'll just need to trust me. Type in `/media/` then hit `tab` twice and you should have a path that looks like `/media/<username>/VBOXADDITIONS_numbers/`, you can then type an `a` and hit `tab` one more time and `autorun.sh` should complete. Hit `enter` to run this script and the system will prompt you for a password and install the VirtualBox Guest Additions. A new terminal window will appear, and eventually that will say to hit return to complete. Once that is done you can type `reboot` on the command line to restart the system. Once rebooted your desktop should automatically adjust to the window size. 

Real quick we will eject the guest additions CD by going to Machine > Settings > Storage, clicking on VBoxGuestAdditions.iso, then clicking the CD drop down on the far right and selecting Remove Disk from Virtual Drive. 

One really neat feature about Virtual Machines is that you can save their state at any point in time. For instnace, if you are going to run some malware in your virtual machine, you could take a snapshot beforehand, so after you run it and do your reverse engineering, you can simply revert your VM to revert it to its original state. Let's do this now by going to Machine > Take Snapshot. We'll name our snapshot Fresh Install and hit OK. If we wanted to restore the snapshot, we could power down the virtual machine, go into VirtualBox, select our VM, then select Snapshots in the upper right hand corner. We can right click Fresh Install and restore this snapshot. You'll want to deselect create a snapshot at the current state. Once restored we can boot up where we were.

You also do not need to shut down a virtual machine every time you close it. You can instead select `Save the machine state`. This will allow you to launch the VM right back to where you were, without closing out your applications or sitting through the boot process. 

We'll do some further set up and familiarization in the Linux module. 
