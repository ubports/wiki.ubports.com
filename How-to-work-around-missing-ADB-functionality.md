WORK IN PROGRESS!!!

It seems that getting ADB access can be a nightmare sometimes, especially for devices that cannot boot into GUI.

## The easiest possibility: build properties ##
Search your device tree for an .mk file which sets the default for the USB port:

    persist.sys.usb.config=mtp

and change it to:

    persist.sys.usb.config=mtp,adb

Clean your out directory from: boot.img, system & root folder. With a bit of luck that´s all you need to do. 

## The hardest one: Bypass via RNDIS adapter & timed configuration job ##
Thanks to Marius we also know about this method for some time. It is based on the possibility to switch the USB port to RNDIS mode after initrd has messed it up. Here are the steps:

- For this to work you need to grab a modified initrd from ubports - here.
- copy this ramdisk to phablet/ubuntu/ubunut_prebuilt_initrd as "initrd.img-touch"
- Inject BOARD_USE_LOCAL_INITRD := true into your device BoardConfig.mk
- Open your kernel config,