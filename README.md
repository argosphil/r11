# The Google Pixel Watch (LTE)

Codenamed `r11`, it's a tiny round watch with a tiny display, a tiny
battery, and a power-hungry dual-core Exynos SoC. Removing the
wristband exposes four pogo pin pads: the usual USB connector.

It has 2 GB of RAM and 32 GB of flash, more than most
Asteroid-supported watches. It runs a 64-bit kernel but what appears
to be a 32-bit userspace.

Only three of the four USB pads (GND, D+, D-) are necessary for fastboot, but the Linux driver (userspace fastboot, adb, etc.) requires all four pads to be connected. Good luck not shorting your power supply.

The boot partitions are only 32 MB, which is a problem since the kernel is stored as an uncompressed Image. Not much room for a ramdisk.

The kernel builds fine, with the config extracted (zcat /proc/config.gz) from the live system.

Building a working boot.img requires using the Google/Python version of mkbootimg, because it uses a v2 Boot Image Header (https://source.android.com/docs/core/architecture/bootloader/boot-image-header).

After activating devtmpfs, I've activated ttyGS0, which seems to work fine. No fb driver yet, though.

You can get an OTA update containing a partition dump from Google (https:/developers.google.com/android/images-watch), which requires you to click-through a "no disassembling" T&C banner.

Magisk works using that image, though the process is a bit involved and involves some blind tapping as the UI doesn't fit the screen.

There's a TWRP port (https://github.com/shinyquagsire23/twrp_google_r11) that apparently worked at some point, but it no longer does since it breaks the 32 MB limit for recovery.img, at least directly following the build instructions.

* XDA Forum post about the Magisk rooting process: (https://xdaforums.com/t/how-to-root-google-pixel-watch-using-magisk.4592737/preview)