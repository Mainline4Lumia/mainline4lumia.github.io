---
title: "Install guide"
summary: "Linux installation guide"
aliases: ["install", "guide"]
---

**This is not ready to be installed.**

While we have some features working, **a lot of basic features like charging or battery do not work.**

If you want to help bring up hardware on these devices, and know how to build the Linux kernel, talk to us in one of our chats listed in [About](/about).

Some useful resources:

- [WPInternals](https://github.com/ReneLergner/WPinternals) is used to unlock your device.
- [PostmarketOS's Windows Phone page](https://wiki.postmarketos.org/wiki/Windows_Phone#Guides) has some useful guides for enabling the boot menu and adding new entries to it.
- [BootShim](https://github.com/imbushuo/boot-shim/tree/elf-loader-pre3) is used to go from UEFI to our own bootloader.
- [lk2nd](https://github.com/msm8916-mainline/lk2nd) is the bootloader we use.
- These devices use ACPI to define their hardware, not device trees like Linux.
