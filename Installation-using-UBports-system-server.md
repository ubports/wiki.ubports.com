You can find instructions for each device here: [devices.ubports.com](https://devices.ubports.com)

NOTE! THIS WILL WIPE YOUR PHONE AND REMOVES ALL YOUR USERDATA!

1. Install the required tools:
```sudo apt-get install ubuntu-device-flash phablet-tools```

2. Reboot your device into fastboot mode (vol up + power) and Connect your device with an USB cable to your computer.

3. Flash your device
```ubuntu-device-flash -v --server=http://system-image.ubports.com touch --channel=ubuntu-touch/stable --device=[device] --bootstrap```
Channels available: ubuntu-touch/stable ubuntu-touch/rc - (daily) ubuntu-touch/devel - (daily dev)