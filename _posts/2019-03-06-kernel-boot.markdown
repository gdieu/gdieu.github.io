---
layout: post
title: "How does a linux kernel boot?"
tags: tag1 tag2 tag3
date: 2019-03-06T18:38:17-05:00
---


Have you ever wondered what’s happening when your Linux system is powered on?
Understanding the big picture of the boot process and being able to dissect each stage of the process can help you to fix boot problems.
Let’s see what’s going behind the scenes when the BIOS starts.


The boot process can be broken down into 6 steps:

* **step 1:**The Basic Input/output System (BIOS) or boot firmware is the first one to be called.  After the Power-On Self-Test (POST), The BIOS searches for the boot loader (GRUB is one of the most popular) within the Master Boot Record (MBR), loads and runs it. The MBR is a small entry located in the first sector of the hard disk. The space is not enough to store the entire boot loader. From here,  the rest of the boot loader is inserted between the MBR and the first partition of the disl.
* **step2:**  The boot loader has the mission to find the kernel and its parameters somewhere on the root filesystem. The The boot loader creates the initrd image (initial ramdisk) with a set of parameters, loads it into memory and executes it. It’s a temporary file system in memory. initramfs is the successor of initrd. Linuxrc is the program that probed modules, creates temporary device nodes in /dev,
* **step3:** The kernel starts the hardware devices and associated drivers.
* **step4:** The kernel mounts the root file system as specified in the boot loader configuration file
* **step5:** The kernel spawns the first process called init with an ID equal to 1. At this point the user space is starting.
* **step6:** The rest of the system processes are sets in motion.

![boot load process](/assets/kernelBoot.jpg)


note about UEFI Secure boot:
The secure boot provided with recent system requires a signed boot loader by a trusted authority in order to work. Consequently, the unsigned boot loader you can find with Linux won’t correctly load. A workaround consists of disabling the secure boot in the settings but may be an issue with dual boot configuration. Since, Linux system is offering signed secure boot.