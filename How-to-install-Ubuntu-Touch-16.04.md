**WARNING:** 16.04-based Ubuntu Touch is in a *very* early state of development and far from usable at the moment. Do not expect your phone to be usable and back app all data you want to keep.

## Supported devices

 - Nexus 5

## How to install

Perform a sanity check and think about if you really need to do this. Remember, that there will not be a whole lot to see, allmost all higher system functionality is not there yet. If you're positive about that, boot your device to fastboot mode by powering it down completely and holding down the volume down and power key until the phone vibrates.

As soon as you see the bootloader mode, connect the device with a usb cable to your Linux PC and run this command:

```
sudo ubuntu-device-flash --server=http://system-image.ubports.com touch \
--device=hammerhead --channel=ubports-touch/16.04/devel --bootstrap --wipe
```

This will start the installation process. Depending on your internet connection, it can take up to 15 minutes. In the end, you will see the UBports logo on white background for a couple of minutes, with no indicator that something is happening, while the terminal command exits with ```Rebooting into recovery to flash```. Don't worry, that's expected. Your phone is still working its magic.

As soon as it's ready, the phone boots and you see the Ubuntu Touch setup menue. The menue itself is functional, but due to a bug, you can't exit it. Reboot your device to bootloader like you did before, select the entry "Recovery Mode" with the volume keys and comfirm that choice with the power key. As soon as you see the UBports Recovery, issue the following command on your pc:

```
adb shell mkdir -p /data/user-data/phablet.config/ubuntu-system-settings && \
adb shell touch /data/user-data/phablet.config/ubuntu-system-settings/wizard-has-run && \
adb reboot
```

That will get you into the system, where you can do absolutely nothing, but open the dash, the shiny new app-drawer and some indicators. If you try to do anything else, the system will probably crash, but (as promised), you can see the latest progress in the realms of 16.04 Ubuntu Touch!

## How to get a usable system back

You can just re-install [Ubuntu Touch 15.04 as usual](https://wiki.ubports.com/wiki/How-to-install-UBports-on-your-device) to get your device back to a usable state.