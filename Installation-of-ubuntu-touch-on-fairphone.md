NOTE: This page is out of date and might contain information that is no longer accurate. See "[[How-to-install-UBports-on-your-device]]" for the latest installation guide.

There is a bug with the bootloader on fairphone devices, so normal install instrictions wont work on there devices.

The workaround for this bug is to flash boot.img and recovery.img using fastboot


1. Reboot to bootloader/fastboot mode (adb reboot bootloader or hold power + vol down)
2. Download boot.img and recovery.img https://dl.dropboxusercontent.com/u/56653875/ubuntu/fp2/FP2-boot-recovery.tar.xz
3. Extrack the tarball
4. Flash using fastboot
```
sudo fastboot flash boot boot.img
sudo fastboot flash recovery recovery.img
```
5. Reboot into recovery (hold power + vol up). You can also type fastboot reboot while pressing the power down button. There is no need to start sideload at this point.

6. Flash ubuntu touch using ubuntu-device-flash without --bootstrap
```
adb shell "mount -a"
sudo ubuntu-device-flash --server=http://system-image.ubports.com touch --channel=ubuntu-touch/stable --device=FP2
```