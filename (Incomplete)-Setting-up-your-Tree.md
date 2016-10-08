# This page is under construction!
Some of the information is missing or incomplete. Or wrong. You might not want to use it yet.

The device tree is all of the code and prebuilt binaries that go into your device's Android build. Your tree is going to be the most important part of your building journey, so it's important to set it up right! 
In this guide I'll be assuming that you want to use the CyanogenMod sources, which are the most common when building Ubuntu Touch for non-Nexus devices. So, with that, let's get a short lecture on your favorite tool for the duration of this task: Repo!

## What's Repo?

Repo is a tool written by the Android developers for working on Android source trees. It downloads large numbers of git projects into a repeatable directory structure, important for something as complicated as Android. To do this, Repo uses a manifest, which is simply an XML document that tells it what to get and where to put it. You can find a full reference for the repo command [here](https://source.android.com/source/using-repo.html "Repo command reference"), but we'll only be using the `repo init` and `repo sync` commands.

## Getting Started

### Installing prerequisites

First you'll need to install phablet-tools.
```
sudo add-apt-repository ppa:phablet-team/tools
sudo apt-get update
sudo apt-get install phablet-tools
```

Then, install the build requirements.

```
sudo apt-get install git gnupg flex bison gperf build-essential \
  zip bzr curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
  libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
  libgl1-mesa-dev g++-multilib tofrodos \
  python-markdown libxml2-utils xsltproc zlib1g-dev:i386 schedtool \
  g++-4.8-multilib
  ```

Next, download repo. You can get and install it using the information [here](http://source.android.com/source/downloading.html "Repo Download", in the "Installing Repo" section.
Then, make yourself a directory, `~/phablet`, then `cd` into it. This will be where your Android source tree goes. 

## Getting your branch

The first thing you'll want to do when setting up your tree is download the correct branch for your device. Here's what you'll need to know about each one and the command to download it:

*Please note that the Phablet repositories go down sometimes. You will get a 503 error when this happens. You can choose to wait a while or ask someone in the Ubuntu Touch IRC about it.*

### phablet_6.0.0_r1

First things first: We're pretty sure that this branch is broken as of October 2016. Maybe it'll get better in the future. However, it's the only one to use for phones that didn't ship with anything older than Android 6 Marshmallow. 
Phones that have CyanogenMod 13 can use this version.
To get it:
`repo init -u https://code-review.phablet.ubuntu.com/p/aosp/platform/manifest.git -b phablet-6.0.0_r1`

### phablet_4.4.2_r1
This is what the official Ubuntu phones, such as the Nexus 4, are built on. You'll also use it if you're trying to build for an older device that has nothing newer than CyanogenMod 11. 
`repo init -u https://code-review.phablet.ubuntu.com/p/aosp/platform/manifest.git -b phablet-4.4.2_r1`

### UBPorts' 5.1
A phone with CyanogenMod 12.1 will use our sources. 
`repo init -u https://github.com/ubports/android -b ubp-5.1`

## Adding your Device-Specific Stuff

Now that you have the base of the Android source, you'll need to find your device-specific toys. These enable the build tree to make Android for your device.

### The Local Manifest

If there's any part for you to make a mistake on, this will be the one. Finding the files isn't hard, but it might take you a couple of tries to get repo's local manifest created correctly.

First, you'll want to find the repositories for your device on [CyanogenMod's GitHub organization](https://github.com/CyanogenMod). You can do this by typing your device's codename into the search box. You can find the codename by going to the [CyanogenMod downloads site](https://download.cyanogenmod.org/) and finding your device in the sidebar. The lowercase word in parentheses is the codename of the device.
You'll want the device repository, `android_device_[manufacturer]_[device]`. There will be a cm.dependencies file in that repository that will tell you all of the other repositories that your device is reliant upon. 

### Vendor Blobs

#### [REMOVE] If you have a Nexus or Pixel device

[TODO] This needs to go into a different article on building for Nexii.
Most Nexus and Pixel devices have their vendor blobs available from Google: https://developers.google.com/android/nexus/drivers
If you have a device that isn't listed on that page (such as the Nexus 9, 5X, or 6P), however, you can use the scripts from this repository to retrieve the blobs from a factory image: https://github.com/anestisb/android-prepare-vendor

The blobs go into the vendor/ folder in your tree, respecting the AOSP naming convention of `vendor/[manufacturer]/[device]/`. You can simply copy the files there, no need to go through any Repo nonsense.


#### If you do not have a Nexus device

This is a bit of a tough one because every device is slightly different. In general, though, you will want to find the CyanogenMod Wiki page on building CM for your device and follow the instructions there.
[TODO] add the part where you cd to the device folder and run extract-files.sh