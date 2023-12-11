---
title: "Android tips"
summary: "Android handbook for mainlined devices"
draft: true
---

While bringing up Linux for these devices is our main focus, we would also like to make it work with Android. We think that Android is a good way to "stress" all the devices' features and it might also be a good way to gain more users and have more reports.

This page will contain some useful information regarding Android and its support for mainline kernels.

For reference, we maintain a common Android device tree that is used for all of our supported devices. You can find it [here](https://github.com/Mainline4Lumia/android_device_linux_mainline-common).

## Kernel

Typically tagged Android releases (aka major releases like Android 13) only works with LTS kernels.

If you want to directly use the latest mainline kernel, it is highly recommended to use the `main` branch of the Android Open Source Project (AOSP). Use the `android-mainline` branch from Android common kernel tree to make sure you have all the required patches. You will also need to apply the Android config fragment to your kernel config.

The fastest way to get started is to build the latest AOSP release and build a LTS GKI (Generic Kernel Image). You can then use the `gki_defconfig` kernel config and write a GKI fragment making sure only the drivers your devices needs will be built.

NXP wrote a nice introduction to GKI for their products, you can find it [here](https://community.nxp.com/t5/i-MX-Processors-Knowledge-Base/i-MX-Android-12-GKI-General-Kernel-Image-development-tips/ta-p/1600993).

Bonus: If you build a custom ROM like LineageOS, you will be able to build the kernel inline with the ROM, which will make it easier to build the kernel together with the required modules.

## Graphics

### Without GPU

Android is able to boot even when the GPU hasn't been bringed up yet, of course, you must have something to draw onto, typically achieved with a framebuffer provided by the bootloader.

All you have to do is:
- Make sure `/dev/fb0` exists and works (you can try booting the Android recovery to quickly check if Android likes it)
  - If it doesn't exist, try to set the `video` kernel command line parameter (e.g. with efifb, set it to `video=efifb`)
- Build `android.hardware.graphics.composer@2.2-service` (the framebuffer adapter doesn't implement the methods required by newer versions, `@2.1` would work too)
- Build `gralloc.default` together with `@2.0` allocator and `@2.1` mapper HIDL implementations
- Build `ANGLE` + SwiftShader's `pastel` Vulkan HAL

### With GPU

Android supports using mesa as a hardware composer and a graphics allocator. This is the recommended way to use a GPU with Android. Refer to device/linaro/dragonboard configuration for this case.
