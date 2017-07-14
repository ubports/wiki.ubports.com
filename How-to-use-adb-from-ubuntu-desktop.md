First you have to install ubuntu-phablet-tools:
```sudo apt-get install phablet-tools```
Than you have to add your device to your desktop. In my case for the [Fairphone 2](https://devices.ubports.com/#/FP2):
```echo "0x2ae5" > ~/.android/adb_usb.ini```
For the [One Plus One (OPO)](https://devices.ubports.com/#/bacon) it is 
```echo "0x9d17" » ~/.android/adb_usb.ini```
Then you have to kill the adb server:
```adb kill-server```
And than with ```adb devices``` you get your adb device listed.
For available adb options have a look at the [Android Debug Bridge user guide](https://developer.android.com/studio/command-line/adb.html)