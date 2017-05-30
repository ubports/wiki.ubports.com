This document provides a high-level overview of the code used in the Ubports 15.04 images. It reflects the state of our build system as-is around June 2017. Changes here and there are possible in the future!

## Where did it come from?

Most of the 15.04 code comes straight from Canonical and replicates the code used for  Ubuntu for Devices before it  was officially dropped. There are also some new additions by Ubports (such as Geoclue support for AGPS) which have been developed since UBports took over the hosting of the code.

## The life and build of an image

A UBports image consists of two major pieces: The Ubuntu root filesystem and the Android container. These are built separately and then joined into the final image that the Ubuntu Recovery  builds as it installs the image on your device. Here we will discuss both of these images for UBports devices.

### Android container

***Warning***: This information will be deprecated with the forthcoming introduction of HALIUM, which handles the Android HAL of a Linux stack. For more information on HALIUM, please read their documentation [here](https://halium.org/)

The Android container is a copy of Android with as much as possible stripped out (e.g. Dalvik VM since Ubuntu does not use Java apps, vendor customizations, etc.), leaving only the HAL in place that is used by a program called LibHybris to allow our Linux distribution to use the Android drivers needed for hardware like the GPU, WiFi, Bluetooth on your device.

The container is built in a way that will be familiar to anyone that's ever ported Cyanogen or LineageOS... because it is the same container LineageOS uses.

First, you download the code specified in [this manifest](https://github.com/ubports/android), then the files in [this manifests](https://github.com/ubports/build-scripts/blob/master/devices.xml) are added to the tree for a specific device. Repo does all of the downloading for you, but you need to put the manifests in place for Repo to find. The process for this is outside the scope of this document.

### Ubuntu root filesystem

The Ubuntu root filesystem is a pre-built copy of `/` for the Ubuntu Touch system. Discussion about this method of installing and upgrading Ubuntu can be found at [the Ubuntu Wiki](https://wiki.ubuntu.com/ImageBasedUpgrades/).

The vivid rootfs is built by creating an Ubuntu image with the following repositories, listed by priority (most important first):

1. [UBports Overlay](https://launchpad.net/~ubports-developers/+archive/ubuntu/overlay)
2. [Stable Phone Overlay](https://launchpad.net/~ci-train-ppa-service/+archive/ubuntu/stable-phone-overlay)
3. Ubuntu 15.04 Vivid repositores Actually these packages are the normal ones that are also used for the desktop distro ARE THEY STAYING HOSTED AT CANONICAL? OR DO WE HAVE TO MIRROR THEM?

All of this work is done by [rootstock-ng](https://github.com/ubports/rootstock-ng) on [our CI server](http://ci.ubports.com/job/vivid-rootfs-armhf/).

Maybe add short note about how the images are signed, and that the phone does only accept signed updates.

You can find the source of a package by selecting "View Package Details", then your desired package, and then clicking on a build. Launchpad will tell you the source package that it used to build.