Libhybris is a library that translates between GCC syscalls and Bionic ones. This allows us to run gcc-based operating systems (like Ubuntu) on a Bionic-based system (any Android phone, ever).

Today I'll be discussing building Hybris for your device. You can use this to test fixes from other branches or hack on it yourself.

This guide focuses on building Hybris for a 32-bit arm environment. You'll need to change an autogen.sh argument in order to build for arm64 or another platform. Note that you'll need a newer version of Hybris than Ubuntu Touch provides to use arm64.

## Setting up your environment

If you're reading this, it probably means you have a build environment set up for your Android or Android-like port. In that case, you have everything you need to build Hybris. If you don't, though, here's a bunch of packages:

```
sudo apt-get install git-core gnupg flex bison gperf build-essential \
  zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 \
  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache \
  libgl1-mesa-dev libxml2-utils xsltproc unzip dh-autoreconf
```

You'll need a pre-existing device tree for your OS of choice. Since we at UBPorts are focused on Ubuntu Touch, that's what I'll be modeling.

## Extract your libraries

Hybris' repository includes two directories, hybris/ and utils/. The scrips in utils/ are essential to building Hybris. We'll be using one in particular, extract-headers.sh. This will take all of the important header files from your Android tree and place them in a folder of your choosing.

To run it, let's CD into your hybris directory first. For Ubuntu touch, this is at `ubuntu/libhybris` in your Android tree.

Then, make a directory in /tmp and use extract-headers.sh to extract your headers to it:

```
mkdir /tmp/android-headers/
extract-headers.sh "/path/to/android/tree" "/tmp/android-headers"
```

Where `/path/to/android/tree` is where your Android tree resides. For many Ubuntu Touch porters, this may be at `~/phablet`.

After this runs, you'll have what looks like a partial Android tree at /tmp/android-headers. Let's move it to the inside of the hybris/ folder.

```
mv /tmp/android-headers "/path/to/libhybris/hybris"
```

Where `/path/to/libhybris/hybris` is the hybris/ directory inside of your Libhybris repository. For Ubuntu Touch, this is at `ubuntu/libhybris/hybris`


## Generate and build

Now that we have the headers, we're ready to configure hybris and build it. Change into the hybris/ directory.

```
./autogen.sh --enable-wayland --enable-arch=arm --with-android-headers=./android-headers  --enable-property-cache --enable-debug --enable-trace
```

If you're compiling for a Mali GPU, you might consider adding `--enable-mali-quirks`. You may add ` --enable-experimental` if the regular build doesn't work.

This configures a hybris build with all debugging capabilities, turns on the Ubuntu Touch default egl platform, selects where the linked libraries shall be, tells it where your headers are, and cross-compiling for ARM.

Now, assuming autoconfig exited without errors, we're ready to build. Make sure that you're inside the hybris/ directory, then run

```
make
```

And that's about it! You should now have a ready-to-go install of libhybris. You can install it using `make install` but that's probably not what you want to do. You can install it to your phone by replacing the libraries that are currently there with the ones that you just created.