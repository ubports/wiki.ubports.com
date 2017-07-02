# This page is under construction!
Some of the information is missing or incomplete.

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

Next, download repo. You can get and install it using the information [here](http://source.android.com/source/downloading.html "Repo Download"), in the "Installing Repo" section.
Then, make yourself a directory, `~/phablet`, then `cd` into it. This will be where your Android source tree goes. 

## Getting your branch

The first thing you'll want to do when setting up your tree is download the correct branch for your device. Here's what you'll need to know about each one and the command to download it:

*Please note that the Phablet repositories go down sometimes. You will get a 503 error when this happens. You can choose to wait a while or ask someone in the Ubuntu Touch IRC about it.*

### phablet_6.0.0_r1

First things first: We're pretty sure that this branch is broken as of October 2016. Maybe it'll get better in the future. However, it's the only one to use for phones that didn't ship with anything older than Android 6 Marshmallow. 
Phones that have Marshmallow AOSP ROMs like Paranoid Android can use this version. Documenting how to use it is outside the scope of this document.
To get it:
`repo init -u https://code-review.phablet.ubuntu.com/p/aosp/platform/manifest.git -b phablet-6.0.0_r1`

### phablet_4.4.2_r1
This is what the official Ubuntu phones, such as the Nexus 4, are built on. 
Devices that have KitKat-based AOSP ROMs can use this. Don't expect much help with this, though, as it's pretty much out of support except on the official phones.
`repo init -u https://code-review.phablet.ubuntu.com/p/aosp/platform/manifest.git -b phablet-4.4.2_r1`

### UBPorts' 5.1
A phone with a current UBPorts port, or a phone with CyanogenMod 12.1, will use our sources. 
`repo init -u https://github.com/ubports/android -b ubp-5.1`

## Adding your Device-Specific Stuff

Okay, so now you have the default manifest for Ubuntu Touch. This will enable you to download the basic Android sources used to build Ubuntu Touch, but you'll need to find device-specific files. These enable the build system to make Android for your device.

### The Local Manifest

If there's any part for you to make a mistake on, this will be the one. Finding the files isn't hard, but it might take you a couple of tries to get repo's local manifest created correctly.

First, you'll want to find the repositories for your device on [CyanogenMod's GitHub organization](https://github.com/CyanogenMod). You can do this by typing your device's codename into the search box. You'll want the device repository, `android_device_[manufacturer]_[device]`. Take down this name, as you'll need it later.

There will be a `cm.dependencies` file in that repository that will tell you all of the other repositories that your device is reliant upon. Keep this around as you will need it in a little bit.


Change into your `~/phablet` directory and create the directory `.repo/local_manifests`. Then, edit the file `.repo/local_manifests/[manufacturer]_[device].xml`. 

Paste the following into the file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>

</manifest>
```

This is the base information required for the file to be a local manifest.

If you're not using the UBPorts source, add this to between the `<manifest>` and `</manifest>` tags:

```xml
  <remote name="cm"
	fetch="http://github.com/CyanogenMod"
	revision="refs/heads/cm-12.1" />
```

#### The Device Repository

Next, we'll fill the manifest with information. Start with your device repository. Create the following line between the `<manifest>` and `</manifest>` tags, replacing the information inside the square brackets with your own.

```xml
<project path="device/[manufacturer]/[device]" name="[repository name]" remote="cm" revision="cm12.1" />
```

The manufacturer and device codename should be the same as they are in the repository name.

#### The dependencies

Now create more lines like the previous, using the cm.dependencies file you found earlier in your device repository. This file lists all of the other repositories that you need to build for your selected device. It's listed in a fairly straightforward way, so create a line for each of the entries in there using the following template.

```xml
<project path="[target_path]" name="[repository]" remote="cm" revision="cm12.1" />
```

And that should be it. Run `repo sync` to download all of the juicy sources for your tree. This will take a while as it must download anywhere from 12 to 18GB of files.

After it's finished, make sure that all of the directories specified in the `path` variables have been created and are populated. Then continue on to find the vendor blobs.


### Vendor Blobs

#### [REMOVE] If you have a Nexus or Pixel device

[TODO] This needs to go into a different article on building for Nexii.
Most Nexus and Pixel devices have their vendor blobs available from Google: https://developers.google.com/android/nexus/drivers
If you have a device that isn't listed on that page (such as the Nexus 9, 5X, or 6P), however, you can use the scripts from this repository to retrieve the blobs from a factory image: https://github.com/anestisb/android-prepare-vendor

The blobs go into the vendor/ folder in your tree, respecting the AOSP naming convention of `vendor/[manufacturer]/[device]/`. You can simply copy the files there, no need to go through any Repo nonsense.


#### If you do not have a Nexus device

This is a bit of a tough one because every device is slightly different. In general, though, you will want to find the CyanogenMod Wiki page on building CM for your device and follow the instructions there. For example, [here](https://wiki.cyanogenmod.org/w/Build_for_endeavoru#Extract_proprietary_blobs) is the one for the HTC One X. It will probably have you run an extract-files.sh script which will extract the blobs automatically. Please note that you will need a device that is currently running your desired version of CyanogenMod for this to work.


## Conclusion

If you followed all of these directions and the folders `device/[manufacturer]/[device]`, `vendor/[manufacturer]/[device]`, and the other directories specified in the cm.dependencies file are populated, then congratulations! You have a complete source tree (probably). We recommend you use `tar` to take a backup of this tree now so that you don't have to wait for the download if you break something.

If you'd like to learn more about the manifest, you can look at [CyanogenMod's page on the subject](http://wiki.cyanogenmod.org/w/Doc:_Using_manifests).