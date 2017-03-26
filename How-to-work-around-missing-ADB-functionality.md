WORK IN PROGRESS!!!

It seems that getting ADB access can be a nightmare sometimes, especially for devices that cannot boot into GUI. This guide will help you get that access.

## The easiest possibility: build properties ##
Search your device tree (use `grep -r "string"`) for an .mk file which sets the default for the USB port:

```
persist.sys.usb.config=mtp
```

and change it to:

```
persist.sys.usb.config=mtp,adb
```

It's recommended to do a full `make clean` at this point, though you could also remove the `boot.img`, `system/` & `root/` folders from `out/`.

## The hardest one: Bypass via RNDIS adapter & timed configuration job ##
We took this method from Sailfish a little while ago, and it's a huge help during early porting - not just for ADB access, but also to diagnose early boot problems and the Android LXC container failing.

For this to work you need to grab a modified initrd from ubports - [here](https://drive.google.com/open?id=0B9Ee5skiHSnncUJBZERSS3IyWlE). 
- Copy this ramdisk to `phablet/ubuntu/ubuntu_prebuilt_initrd/` as `initrd.img-touch`
- Inject `BOARD_USE_LOCAL_INITRD := true` into your device BoardConfig.mk. Without this, the build system will download an initramfs from Canonical.
- Open your kernel config and find `CONFIG_CMDLINE` parameter, add `usb_debug` to the end of the string.
- Probably you also want to set `CONFIG_CMDLINE_EXTEND="y"`. If you don't, the bootloader may ignore your options and use its own.
- `make clean` and build.
- go into recovery and flash the modified boot.img
- It should stop at the boot logo. Connect via USB and see if your desktop recognizes an RNDIS adapter
- On the first round, there will be dhcp available, so try to telnet to 192.168.2.15
- you should get into BusyBox minimalistic shell.
- paste the following shellscript  into the console:

```bash
cat <<EOF > start.sh
#!/bin/sh
echo "continue" > /init-ctl/stdin
sleep 15
mkdir -p /sys
mount sys -t sysfs /sys
echo 0 > /sys/class/android_usb/android0/enable
sleep 1
echo 18D1 > /sys/class/android_usb/android0/idVendor
echo D001 > /sys/class/android_usb/android0/idProduct
echo rndis,adb > /sys/class/android_usb/android0/functions
echo 1 > /sys/class/android_usb/android0/enable
sleep 1
start adb
ifconfig rndis0 192.168.2.15
ifconfig rndis0 up
EOF
chmod +x start.sh
./start.sh &
```

- You will loose now again the connection via RNDIS. Fear not, after the 15sec timer the script will try to reestablish it!
- In the second round you will probably not have DHCP again. You need to manually configure your IP address e.g. 192.168.2.20/24
- With some luck, you also get ADB! Try adb devices...