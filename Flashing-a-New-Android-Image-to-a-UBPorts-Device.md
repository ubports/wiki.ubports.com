Sometimes you want to add your own build of Android to a device that already has a UBPorts port. In this case, it is not advisable to use Rootstock as you would for other devices, as some UBPorts ports have a slightly customized Ubuntu build. Also, it's nice to make sure that you're not introducing any bugs by using a different Ubuntu system. The following is what you'll need to do:

1. Install Ubuntu Touch using [magic-device-tool](https://github.com/MariusQuabeck/magic-device-tool/) or Ubuntu Device Flash.
1. After Ubuntu Touch has booted, reboot into Recovery
1. Plug your phone in to your computer which has adb installed
1. cd to the directory where your built system.img is located (Commonly out/target/product/[DEVICE]/
1. Run the following commands:

```
adb shell "mount -a"
adb shell "mkdir /image"
adb shell "mount /data/system.img /image"
adb push system.img /image/var/lib/lxc/android/system.img
adb reboot
```

And you're done. Your phone should now reboot into Ubuntu with your own build of Android running in the container.