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
    
and finally, install it. The `dpkg-buildpackage` command will print out the list of generated packages, and it's those filenames you will need to pass to the next command:

    sudo dpkg -i ../<package>.deb [../<package2>.deb ...]
    
Note, however, that you might not need to install all the packages: generally, you can skip all packages whose name ends with `-doc` or `dev`, since they don't contain code used by the device.

## Cross-building with crossbuilder

This is the recommended way to develop non trivial changes, and it's suitable for all devices since the build happens on your desktop PC (will call it "host" from now on) and not on the target device. It's also extremely fast and easy to use.

Start with installing `crossbuilder` in your host:

    git clone git@github.com:ubports/crossbuilder.git
    
It's a shell script, so you don't need to build it. Instead, you will need to add its directory to your `PATH` environment variable, so that you can execute it from any directory:

    echo "export PATH=$HOME/crossbuilder:$PATH" >> ~/.bashrc
    # and add it to your own session:
    export PATH="$HOME/crossbuilder:$PATH"

Then, you need to setup LXD; luckily, crossbuilder has a command which does everything for you; you just need to carefully follow its instructions:

    crossbuilder setup-lxd
    
If this is the first time you used LXD, you might need to reboot your host once everything has completed.
After LXD has been setup, using crossbuilder is as easy as it can get: just move to the directory where the source code of your project is (for example, `~/src/git/address-book-app`) and launch it like this:

    cd ~/src/git/address-book-app
    crossbuilder --ubuntu=15.04
    
*Note: if your device is connected to the PC, you don't need to specify the `--ubuntu=15.04` parameter because crossbuilder will figure out the proper Ubuntu version by itself. If you don't specify any parameter and have no device connected to your PC, crossbuilder will assume `16.04` (Xenial).*

Crossbuilder will do everything for you: it will create the LXD container, download the development image, install all your package build dependencies, perform the build and finally, if your device is connected to your host, it will copy the packages over to the target and install them. The first two steps (creating the LXD image and getting the dependencies) can take a few minutes, but will be executed only the first time you launch crossbuilder for a new package.

Now, whenever you change the source code in your git repository, the same changes will be available inside the container, and the next time you'll type the `crossbuilder` command, only the changed files will be rebuilt. This makes iterative development blazing fast.

### Unit tests

By default crossbuilder does not run unit tests; that's both for speed reasons, and because the container created by crossbuilder is not meant to run native (target) executables: the development tools (qmake/cmake, make, gcc, etc.) are all run in the host architecture, with no emulation (again, for speed reasons). However, qemu emulation is available inside the container, so it should be possible to run unit tests inside the container. You can do that by getting a shell inside the container with

    crossbuilder --ubuntu=15.04 shell
    
and then find the unit tests and execute them. Be aware that the emulation is not perfect, so there's a very good chance that the tests will fail even when they'd otherwise succeed, when run into a proper environment. For that reason, it's probably wiser not to worry about unit tests when working with crossbuilder, and run them only when not cross-compiling.