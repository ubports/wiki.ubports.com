In this page you'll find information on how to develop system software, including how to build it, cross-compile it and make it available to other users. Most of the software preinstalled in your Ubports device is shipped in the device image in the form of a Debian package. This format is used by several Linux distributions (such as Debian, Ubuntu, Mint) and [plenty of documentation](https://www.debian.org/doc/manuals/maint-guide/index.en.html) is available out there on how to work with it, so we won't be covering it here. Besides, in most cases you'll find yourself in need of modifying existing software, rather than developing new packages from scratch; for this reason, this guide is mostly about recompiling an existing Ubports package.

There are essentially three ways of developing Ubports system software: building it directly on device, cross-compiling it or uploading the source code to a Launchpad PPA and have it built by Launchpad. We'll examine all of the three methods, and use [address-book-app](https://github.com/ubports/address-book-app) (the Contacts application) as an example.

## Building on the device itself

This is the fastest and simplest method to develop small changes and test them in nearly real-time. Depending on your device resources, however, it might not be possible to follow this path: if you don't have enough free space in your root filesystem you won't be able to install all the package build dependencies; or, your device's RAM might not be enough for the compiler. Assuming that you are lucky enough not to run into these restrictions, and that you don't mind reflashing your device afterwards (to clear it from all the development packages you installed), please read on.

You can ssh to the device (via `phablet-shell`, for example) and then install all the packages needed to rebuild the component you want to modify (the Contacts app, in this example):

    sudo apt-get build-dep address-book-app
    sudo apt-get install fakeroot

This will install a bunch of packages into your device's rootfs. Additionally, you probably want to install `git` in order to get your app's source code in the device and later push your changes back into the repository:

    sudo apt-get install git
    git clone git@github.com:ubports/address-book-app.git   # or your own clone
    cd address-book-app
    
Now, you are ready to build the package:

    DEB_BUILD_OPTIONS="parallel=2 debug" dpkg-buildpackage -rfakeroot -b