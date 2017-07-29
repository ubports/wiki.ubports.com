-----------------

## You probably want a different page than this

This page has been rolled into our newer, better page, [[How to install UBports on Your Device|How-to-install-UBports-on-your-device]]

-----------------


Use this method if device does not have an image on our system-image server

1. Download the install zip file for your device
2. Download ubports recovery and boot.img for your device
3. Reboot to bootloader/fastboot
4. Flash recovery.img and boot.img
```
sudo fastboot flash recovery recovery.img
sudo fastboot flash boot boot.img
```
5. Reboot to recovery
6. Push the install zip for your device
```
adb push [install zip] /data
```
7. In recovery menu on your device choose "Ubuntu actions" -> "Install ubuntu zip" then choose the install zip
8. reboot