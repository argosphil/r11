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

Building a working boot.img requires using the Google/Python version of mkbootimg.

After activating devtmpfs, I've activated ttyGS0, which seems to work fine. No fb driver yet, though.
