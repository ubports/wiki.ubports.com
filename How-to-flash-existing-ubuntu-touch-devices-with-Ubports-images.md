1. Reboot to bootloader
2. Download the unlocked adb recovery for your device here: https://wiki.ubuntu.com/Touch/Devices
3. Run Ubuntu device flash

ubuntu-device-flash --server=https://system-image.ubports.com/ touch
--channel=ubports-touch/legacy --bootstrap --recovery-image=[Downloaded adb recovery image]