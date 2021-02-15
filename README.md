# PatchingAndBuildingLinuxKernel
Guide on how to patch and build the Linux kernel for the T2 Mackbook.

# Preamble
This is a quick tutorial on how to patch and compile the linux kernel.

As an example we will be using aunali1's patches for the T2 macbooks and we will use the linux kernel version 5.10.12

This can be pretty much used for other situations, this is not specific for macbooks, this can be used to apply patches and compile kernels for other devices.

## Why are we doing this?
No particular reason apart from the fact of running a more recent kernel that has less issues and works as good as the 5.7.19 kernel (which has been the golden version untill last week)

## What does this tutorial assume?
- Some familiarity with linux;
- you want to patch the kernel for a T2 macbook pro;
- you want to compile the kernel;
(Again as said above this can be used as a general guideline for other kernels patches and devices)

# Tutorial

Let's begin!

- Download the Linux kernel from here https://kernel.org;
- Click on the HTTP link and navigate to https://mirrors.edge.kernel.org/pub/linux/kernel/v5.x/;
- Select the tar.gz file for the kernel you wish to download, we will use kernel 5.10.12 which has patches avvailable for the T2 macbook pro;
- Once done navigate to the Downloads folder, `cd ~/Downloads`
- Unpack the tar.gz file, `gunzip linux-5.10.12.tar.gz`
- Unpack the tar file, `tar -xvf linux-5.10.12.tar`
- You should now have a folder in your downloads called linux-5.10.12 with the kernel source inside;
- Let's clone aunali1's repo which has the patches for the T2 Macbook pro;
- git clone https://github.com/aunali1/linux-mbp-arch;
- You should now have two folders, one with the linux kernel sources named linux-5.10.12 and another with the macbook specific patches named linux-mbp-arch;
- Go into the linux-mbp-arch, `cd linux-mbp-arch`;
- Delete every file that doesn't have a .patch extension;
- Go back `cd..` and go into the linux kernel folder `cd linux-5.10.12`;
- Let's apply the patches!
- `for n in ~/Downloads/linux-mbp-arch/\*.patch; do patch -p1 --verbose <$n; done`
- We now have the kernel patched, all we need to do is compile it;
- Go back to your kernel folder `cd ../linux-5.10.12/`
- Let's download a few dependencies;
- apt-get install libncurses-dev libssl-dev flex bison build-essential;
- Let's take care of the configuration, there are three ways to approach this:
  - First option is to run menuconfig and select the modules and componentes that you need for the Macbook (this is complicated and not recommended at all, this is ok for seasoned linux users mostly);
  - Second option is to generate a config file based on the hardware of your computer and what is working/connected right now, that compiles a very light kernel, but if you try to connect something to your macbook and the kernel module is not present it won't work;
  - Third option and the one we are going to follow is to copy the config file that comes with your distribution and use it as base for the new kernel (safest option since if everything is working on the kernel you run now, everything will still be working on the new kernel you are compiling, unless something goes terribly wrong);
- We are going for option 3 it's less of a hassle and everything that is woring right now should be woring on your new kernel;
- Let's copy the config then, `cp /boot/config-$(uname -r) ./.config`
- Time to compile the kernel, we will use two cores to speed the compilation process a little bit, i don't want to overdo on the compilation part as i don't want the cpu to catch fire in the process, two cores should be more than enough, run the following, `make -j 2 deb-pkg`
- Wait for about an hour or so and you should have your deb packages waiting for you in your parent folder, `cd ..`
- to install them, `dpkg -i package-name.deb`, install them in this order:
  - Libc6
  - Linux-Image
  - Linux-Headers
 - Reboot your Macbook, boot into the new kernel.
 - you should now be on 5.10.12 with everything workin, verify by running, `uname -r`
 
 # Acknowldgements
 Thanks to Redecorating for the support and reponding to DMs at 2AM.
 
 Thanks to networkException for sending some nice resources and overall good talk.
