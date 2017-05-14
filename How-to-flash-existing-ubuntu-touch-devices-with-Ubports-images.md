**NOTE: THIS METHOD WILL WIPE YOUR DATA! PLEASE BACKUP BEFORE TRYING, We are working on a method that will not wipe your data, if you want to keep your data please wait until that's done or you use this backup method:**
```
rsync avz --delete /home/phablet <user>@<server>:<dirname>/phablet
```
**to send all Apps data to your server of choice, and later reverse the process to restore the data. Then follow these steps:** 

1. Reboot to bootloader (try holding volume (down, up or both) + power button)
2. Download the unlocked adb recovery for your device
3. Run this Ubuntu device flash command (try with sudo):

```
sudo ubuntu-device-flash --server=https://system-image.ubports.com/ touch \
--channel=ubports-touch/legacy --bootstrap \
--recovery-image=[Downloaded adb recovery image]
```

Please [[file a bug report|UBports Bug Trackers]] if you have any problem.

**NOTE: UNTESTED DEVICES MIGHT RUN INTO UNEXPECTED ISSUES, PLEASE BE PREPARED TO FIX YOUR DEVICE**

### Unlocked adb recovery:

BQ Aquaris E4.5
Codename: krillin
Status: <span style="color:green">Works, tested</span>
Adb recovery: http://cdimage.ubports.com/devices/recovery-krillin.img

BQ Aquaris E5
Codename: vegetahd
Status: <span style="color:green">Works, tested</span>
Adb recovery: http://cdimage.ubports.com/devices/recovery-vegetahd.img

BQ Aquaris M10 HD
Codename: cooler
Status: <span style="color:green">Works, tested</span>
Adb recovery: http://cdimage.ubports.com/devices/recovery-cooler.img

BQ Aquaris M10 FHD
Codename: frieza
Status: <span style="color:red">Update failes, tested</span>
Update fails due to the recovery cahce is missing 15MB, a workaround is needed here
Adb recovery: http://cdimage.ubports.com/devices/recovery-frieza.img

Meizu MX4
Codename: m75/arale
Status: <span style="color:black">Unknown, Not tested</span>
Adb recovery: http://cdimage.ubports.com/devices/recovery-arale.img

Meizu PRO 5
Codename: turbo
Status: <span style="color:green">Works, tested</span>
Adb recovery: http://cdimage.ubports.com/devices/recovery-turbo.img