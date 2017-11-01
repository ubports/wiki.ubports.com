**WARNING:** 16.04-based Ubuntu Touch is in an early state of development and is not usable as a daily driver for the moment.

## Supported devices

 - Nexus 5 (*hammerhead*)
 - Oneplus One (*bacon*)
 - Fairphone 2 (*FP2*) (Only UBports installer)

## How to install

You can install your device using the [UBports installer](https://github.com/ubports/ubports-installer). Select the 16.04/devel channel and check the wipe option. The installation will overwrite all of the phones internal memory.

Alternatively (except on the Fairphone 2 where this method does not work), boot your device to fastboot mode by powering it down completely and holding down the volume down and power key until the phone vibrates.

As soon as you see the bootloader mode, connect the device with a usb cable to your Linux PC and run this command:

```
sudo ubuntu-device-flash --server=http://system-image.ubports.com touch \
--device=[DEVICE-CODENAME] --channel=ubports-touch/16.04/devel --bootstrap --wipe
```

That's it!

## How to get a usable system back

You can just re-install [Ubuntu Touch 15.04 as usual](https://wiki.ubports.com/wiki/How-to-install-UBports-on-your-device) to get your device back to a usable state.
