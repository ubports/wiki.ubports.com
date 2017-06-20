Ubuntu Touch and now UBports is a modular, open system, so there are also multiple ways how to install it:

## Before you cry: Make a backup of your existing data

* Use the magic device tool: https://github.com/MariusQuabeck/magic-device-tool - It has a backup option built in for all our supported devices. Please read the instructions carefully!

## Non-Canonical devices

These instructions will help you install our OS on the "Core Devices" such as the Nexus 5 or Fairphone 2.

### Switch from Android, Canonical, or any other OS to UBports

* On any Linux distro with Snaps: Use the magic device tool: https://github.com/MariusQuabeck/magic-device-tool - Please read the instructions carefully!
* On Windows or MacOS (**beta!**): Use the [UBports GUI installer](https://github.com/ubports/ubports-installer/releases)
* On Ubuntu: Install using system-image server, [select your device here](https://devices.ubports.com/#/)

## Switch the channel on an existing UBports device

You can read about the channels you can choose from and learn how to switch on [[Release-Channels]]

## Official "Ubuntu for Devices" devices

These instructions will help you install to a device that ran an official Canonical build of Ubuntu for Devices, such as the BQ M10 or Meizu MX4

### Switch from Android to Ubuntu

***BE VERY CAREFUL!*** This can permanantly damage or brick your device. NEVER check the "Erase All" option in SP Flash Tool and carefully read everything that it tells you. Some users have destroyed the partition that holds their hardware IDs and can no longer connect to Wi-Fi or cellular networks.

* BQ devices: Download the official firmware from [here](http://www.mibqyyo.com/en-download/) and use [SP Flash Tool](https://spflashtool.com/) to flash it
* Meizu devices: [TODO]

### Get help from other users and the UBports team

See the links in the sidebar to learn how to get a hold of us!

### Developers: Install custom builds with recovery or rootstock-ng
* Use the recovery to transfer / load all files: [[Installation-using-UBports-Recovery]]