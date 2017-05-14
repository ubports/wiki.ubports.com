**NOTE: THIS METHOD WILL WIPE YOUR DATA! PLEASE BACKUP BEFORE TRYING, We are working on a method that will not wipe your data, if you want to keep your data please wait until that's done. As a simple backup method you can use:**
```
rsync avz --delete /home/phablet <user>@<server>:<dirname>/phablet
```
**to send all Apps data to your server of choice, and later reverse the process to restore the data. Then follow these steps:** 

1. Reboot to bootloader (try holding volume down + power button)
2. Download the unlocked adb recovery for your device
3. Run this Ubuntu device flash command (try with sudo):

```
ubuntu-device-flash --server=https://system-image.ubports.com/ touch \
--channel=ubports-touch/legacy --bootstrap \
--recovery-image=[Downloaded adb recovery image]
```

**NOTE: UNTESTED DEVICES MIGHT RUN INTO UNEXPECTED ISSUES, PLEASE BE PREPARED TO FIX YOUR DEVICE**

Unlocked adb recovery:

BQ Aquaris E4.5
krillin
Status: Works, tested
http://cdimage.ubports.com/devices/recovery-krillin.img

BQ Aquaris E5
vegetahd
Status: Unknown, Not tested
http://cdimage.ubports.com/devices/recovery-vegetahd.img

BQ Aquaris M10 HD
cooler
Status: Works, tested
http://cdimage.ubports.com/devices/recovery-cooler.img

BQ Aquaris M10 FHD
frieza
Status: Unknown, Not tested
http://cdimage.ubports.com/devices/recovery-frieza.img

Meizu MX4
m75/arale
Status: Unknown, Not tested
http://cdimage.ubports.com/devices/recovery-arale.img

Meizu PRO 5
turbo
Status: Works, tested
http://cdimage.ubports.com/devices/recovery-turbo.img