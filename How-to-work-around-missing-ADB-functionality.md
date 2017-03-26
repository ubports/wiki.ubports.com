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
1. Copy this ramdisk to `phablet/ubuntu/ubuntu_prebuilt_initrd/` as `initrd.img-touch`
1. Inject `BOARD_USE_LOCAL_INITRD := true` into your device BoardConfig.mk. Without this, the build system will download an initramfs from Canonical.
1. Open your kernel config and find `CONFIG_CMDLINE` parameter, add `usb_debug` to the end of the string.
1. Probably you also want to set `CONFIG_CMDLINE_EXTEND="y"`. If you don't, the bootloader may ignore your options and use its own.
1. `make clean` and build.
1. Go into recovery and flash the modified boot.img. Reboot the phone normally. It will hang at the boot logo. 
1. Connect via USB and see if your computer finds a new RNDIS Ethernet adapter. It will gain an IP on the 192.168.2.x/24 subnet.
1. Telnet to 192.168.2.15
1. You will almost immediately be presented with a root Busybox shell.
1. Paste the following into the console:

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

1. You will lose the connection via RNDIS. After 15 seconds, the script will attempt to bring it back up. Watch your ifconfig or dmesg to see it reconnect.
1. DHCP may not be functioning when RNDIS comes back up. If not, manually configure your IP address e.g. 192.168.2.20/24
1. With some luck, you also get ADB! Try adb devices...