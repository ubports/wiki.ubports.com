## What works
Works
Not working
Not Tested

Graphics
Boot process
Rotation
Cellular Radio
BT
Wireless network
Sound
Touch
Camera
Video Decode
Suspend/Resume


# How to install Ubuntu Touch
NOTE!!! THIS WILL WIPE YOUR PHONE!!!! THIS WILL REMOVE ALL YOUR USERDATA!!

1. Install the required tools:
´´´
sudo apt-get install ubuntu-device-flash phablet-tools
´´´
2. Reboot your device into fastboot mode (vol up + power) and Connect your device with an USB cable to your computer.

3. Flash your device

ubuntu-device-flash -v —server=http://system-image.ubports.com touch —channel=ubuntu-touch/stable —device=bacon --bootstrap
Channels available: ubuntu-touch/stable ubuntu-touch/rc - (daily) ubuntu-touch/devel - (daily dev)

4. Wait 15 minutes, if it's still stuck on the boot logo, then run:

adb reboot

How to install Ubuntu Touch using MultiRom
1. Download the temporally version of Multirom manager (I send the updates to the Multirom developer) (MultiROMMgr-UT.apk)

2. Install the .apk file (if you have Multirom manager installed you need uninstall it)

Using file browser: stackoverflow

Using adb:

adb install MultiROMMgr-UT.apk
3. Open the app and install Multirom v32j, Recovery 2015-06-07 (It will say you have it already installed, this is just a workaround to get ubuntu touch work. YOU NEED TO INSTALL THIS ANYWAY) and kernel for your android version

4. When it's done installing and booted back up, you can install Ubuntu Touch.


How to update the android container (OLD METHOD)
1. Download [replace android system tool]

2. Download the latest system.img

3. Run this command:

./replace-android-system system.img

4. Done, your system is updated.

How to install using rootstock (OLD METHOD)
Flash on you device, THIS MAY BRICK YOUR DEVICE!!!!! DON'T DO THIS IF YOU DON'T KNOW WHAT YOU ARE DOING!!!!!

FIRST DO A BACKUP! YES, DO IT!

1. Download UbuntuTouch-opo-installer.zip, UbuntuTouch-20150413-bacon-DEV.zip (contains: boot.img, system.img) and wily-preinstalled-touch-armhf.tar.gz

2. Reboot the device into fastboot mode

3. Flash boot.img using fastboot

Code:

fastboot flash boot boot.img

4. Boot the device back to recovery (I recommend twrp, but anything should work!)

5. Wait until adb has started (use "adb devices" to check if it has started)

6. Extract UbuntuTouch-opo-installer.zip, remember to have the configs folder in the same folder as the script.

7. Flash ubuntu root system and system.img using rootstock installer

Code:

./OnePlusOne-rootstock-installer wily-preinstalled-touch-armhf.tar.gz system.img

8. After that it should boot ubuntu.

Unziped images (note: UbuntuTouch-20150302-bacon-DEV.zip contains, boot.img and system.img) boot.img, system.img

Alternative to MultiRom using rootstock installer (OLD METHOD)
I see that there is a lot of people that want multirom, I found a easy alternative to that in the mean time while we wait for the ota server (need that for multirom). This will be using TWRP and it's backup function.

Please do a full backup first, This should not wipe anything, but do it to be sure!

1. Download UbuntuTouch-opo-installer.zip, UbuntuTouch-20150413-bacon-DEV.zip (contains: boot.img, system.img)and wily-preinstalled-touch-armhf.tar.gz

2. Backup your current bootimage

3. Go into advanced -> File manager -> sdcard -> TWRP -> BACKUPS -> [Random created folder] -> [Your newest created backup of bootimage] Then press select -> Rename to "Android"

4. Extract UbuntuTouch-opo-installer.zip, remember to have the configs folder in the same folder as the script.

5. Reboot the device into fastboot mode

6. Flash boot.img using fastboot Code:

fastboot flash boot boot.img

7. Boot the device back to recovery

8. Now do a backup of the bootimage

9. Go into advanced -> File manager -> sdcard -> TWRP -> BACKUPS -> [Random created folder] -> [Your newest created backup of bootimage] Then press select -> Rename to "Ubuntu"

10. Go to restore an check if there is one named "Ubuntu" and one named "Android"

11. Flash ubuntu root system and system.img using rootstock installer Code:

/OnePlusOne-rootstock-installer wily-preinstalled-touch-armhf.tar.gz system.img


You can now quickly swap between Ubuntu and Android, all you have to do is go to TWRP (recovery) and select restore and choose what you want to boot (android or ubuntu) and just restore the bootimage

The reason why you can do this, is because ubuntu do not use the system partition at all, it only uses boot partition and a system.img file that is placed inside /data (this is the file system of ubuntu)

Using MultiRom: Coming soon


Build server: http://ci.mariogrip.com/ Donwload server: http://download.mariogrip.com/ Nightly builds: http://download.mariogrip.com/Ubuntu-Touch/OnePlus-One/nightly

Report bugs and errors here: https://github.com/ubuntu-touch-oneplus-one/ubuntu-touch-for-oneplus-one/issues

Build
See this page OnePlus_One_Build