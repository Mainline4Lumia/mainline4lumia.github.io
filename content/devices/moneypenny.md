---
title: "Nokia Lumia 630/632/635/638"
summary: "(moneypenny)"
---

![Nokia Lumia 630 front and back](/img/moneypenny.png)
# Support matrix
| Feature | Supported |
| --- | ----------- |
| Touch | Yes |
| Display | Yes |
| WiFi | No |
| Battery statistics | No |
| Charging | No |
| Accel/Gyro | Yes |
| Audio | No |
| Bluetooth | No |
| Camera | No |
| GPS | No |
| Mobile data | No |
| SMS | No |
| Calls | Partial |
| NFC | Yes |
| LED(s) | No |
| ALS/PRX | Yes |

# Notes

# Installation

## Step 1: Unlock bootloader
Download WPInternals (from https://github.com/ReneLergner/WPinternals/releases/latest) and Windows Device Recovery Tool (from https://support.microsoft.com/en-us/windows/windows-device-recovery-tool-faq-2b186f06-7178-ed11-4cb6-5ed437f0855b). WPInternals is a tool designed to unlock the bootloader and/or secure boot of select Lumia devices made by Nokia and Microsoft. Windows Device Recovery Tool is installed because it automatically installs all the drivers WPInternals will need.

Once you have installed both tools, Click on "Unlock Bootloader" and follow the instructions to unlock your phone's bootloader.
## Step 2: Install developer menu and bootshim

After you have unlocked the bootloader of your phone, you will have to install the developer menu and bootshim onto your phone. This is made easy by our LumiaQuickStart script. To use it, clone the LumiaQuickStart repo (https://github.com/Mainline4Lumia/LumiaQuickStart). Then, use WPInternals to reboot your phone into mass storage mode. Now run `install.ps1` as administrator. Provide the path to EFIESP (Windows might also have mounted it inside MainOS). After the script is finished, you can install the 2nd stage bootloader(lk2nd).

## Step 3: Install lk2nd
Download `lk2nd-msm8226.img` from https://github.com/chmod-rwx/mainline4lumia.github.io/blob/main/data/emmc_appsboot.mbn. Then, copy `emmc_appsboot.mbn` to your phone's EFIESP folder. Now, unmount mass storage and restart your phone by holding the volume down and power buttons for a few seconds.

## Step 4: Boot linux
After you restart back to Windows Phone OS, restart your device once more. Hold the volume up button while the "NOKIA" logo is visible. If all goes well, your phone will boot lk2nd. From lk2nd, you can use the fastboot interface to boot linux.

Download the Android SDK Platform Tools (from https://developer.android.com/studio/releases/platform-tools) to use fastboot. Ensure your phone is connected to your computer. Rename your kernel image to `boot.img`. Then, run `fastboot boot boot.img` to boot the kernel on your phone.
