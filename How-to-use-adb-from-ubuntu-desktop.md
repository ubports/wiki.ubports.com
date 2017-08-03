First you have to install ubuntu-phablet-tools:
```sudo apt-get install phablet-tools```

If you own a [Fairphone 2](https://devices.ubports.com/#/FP2) you have to add your device to your desktop:
```echo "0x2ae5" >> ~/.android/adb_usb.ini```
Even if you own a [One Plus One (OPO)](https://devices.ubports.com/#/bacon) you have to do add it: 
```echo "0x9d17" >> ~/.android/adb_usb.ini```
Other devices don't need to be added manually.

Then you have to kill the adb server:
```adb kill-server```

And then with ```adb devices``` you get your adb device listed.

For available adb options have a look at the [Android Debug Bridge user guide](https://developer.android.com/studio/command-line/adb.html)