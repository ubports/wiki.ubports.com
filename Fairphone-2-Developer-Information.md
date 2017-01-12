## Overview

The Fairphone 2 (FP2), released in December of 2015, shipped with Android 5.1 Lollipop. The current Cyanogenmod base should be sufficient to get it stable.

This page contains the information that you'll need to develop on the Fairphone 2. This includes instructions to get the source tree, patches, and changes to make after building.

Development repositories for the Fairphone 2 are located on [the ubports GitHub](https://github.com/ubports). You may submit pull requests against this source and they will be reviewed by UBPorts developers. You might want to give us a heads-up in the UBPorts IRC as well.

Please remember to make a complete backup of your phone before doing any flashing operations, assuming you have anything that you want to keep on it. Then, copy the backup to your computer. Your phone may be wiped during this procedure.

## Development status

Current devel rc proposed builds:
GUI -> Working
Wifi -> Working
Audio -> working
Camera ->working
Bluetooth -> Working
GSM -> Partial (Registration and SMS work, incoming calls and data do not)
Motion sensor ->Working
GPS -> WIP

We're currently experimenting with the GUI since we're experiencing screen corruption caused by an interaction between the Adreno drivers, Libhybris, and Mir.

## Current goals

GSM data and audio are not functional
GPS is not functional

## Building

### Install Prerequisites

```sudo apt-get install git gnupg flex bison gperf build-essential \
zip bzr curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
libgl1-mesa-dev g++-multilib tofrodos \
python-markdown libxml2-utils xsltproc zlib1g-dev:i386 schedtool \
g++-4.8-multilib phablet-tools```


### Set up the tree

Simple, as always.

Start by creating yourself a development directory, then move into it. Run `repo init -u https://github.com/ubports/android5 -b ubp-5.1 --depth=1` in this directory.

Next, `mkdir .repo/local_manifests`, then create the file `.repo/local_manifests/fp2.xml`. Paste the following into the file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>

  <remote name="smoose"
        fetch="http://github.com/smoose-nils"
        revision="refs/heads/ubp-5.1" />

  <project path="kernel/fairphone/FP2" name="android_kernel_fairphone_fp2" remote="ubp" />
  <project path="device/fairphone/FP2" name="android_device_fairphone_fp2" remote="ubp"  />
  <project path="device/qcom/common" name="android_device_qcom_common" remote="cm" />
  <project path="vendor/fairphone" name="proprietary_vendor_fairphone" remote="smoose"/>
```

Then, run `repo sync -j4` (increase the job value if your computer and Internet connection can handle it). It'll download about 20GB of sources.

### Build the source

This is a simple operation.

```
. build/envsetup.sh
lunch cm_FP2-eng
make -j8
```

Feel free to increase or decrease the number of jobs for Make.

### Flash the images

Please ensure that you have a backup of your phone before continuing.

First, flash your boot.img and recovery.img using Fastboot:

```
cd out/target/product/fp2/
sudo fastboot flash boot boot.img
sudo fastboot flash recovery recovery.img
```

Now, we can't use Rootstock to install these images since UBPorts' Ubuntu Touch is patched slightly. Do the following to finish the flashing process:

1. Use [Magic Device Tool](https://github.com/MariusQuabeck/magic-device-tool/) or ubuntu-device-flash to put Ubuntu Touch onto your phone
1. After the phone has booted into Ubuntu Touch, reboot into recovery
1. Run the following from the directory that your system.img is in:

```
adb shell "mount -a"
adb shell "mkdir /image"
adb shell "mount /data/system.img /image"
adb push system.img /image/var/lib/lxc/android/system.img
adb reboot
```

Then you can reboot your phone to have your shiny new system.img

## That is it.

Have fun! Look back at the Current Goals heading at the top of the article to see what you can work on. Be sure to let us know if you find any fixes over at #ubports on Freenode. If there are any fixes that involve the repositories on GitHub, please feel free to submit a pull request.