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

- Download the Linux kernel from here https://kernel.org
- Click on the HTTP link and navigate to https://mirrors.edge.kernel.org/pub/linux/kernel/v5.x/
- Select the tar.gz file for the kernel you wish to download, we will use kernel 5.10.12 which has patches avvailable for the T2 macbook pro
- Once done navigate to the Downloads folder, cd ~/Downloads
- Unpack the tar.gz file, gunzip linux-5.10.12.tar.gz
- Unpack the tar file, tar -xvf linux-5.10.12.tar
- You should now have a folder in your downloads called linux-5.10.12 with the kernel source inside
- Let's clone aunali1's repo which has the patches for the T2 Macbook pro.
- git clone https://github.com/aunali1/;inux-mbp-arch
- you should now have two folders, one with the linux kernel sources named linux-5.10.12 and another with the macbook specific patches named linux-mbp-arch
