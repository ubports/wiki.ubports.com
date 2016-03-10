This guide covers the basics of building certain portions of Android as they relate to Ubuntu Touch. The example device used in this guide is a OnePlus One.

# Setting up the environment

Setting up the environment is necessary before porting any device. Though it's not strictly necessary to use Ubuntu, you might run into problems by using different versions of software. This guide uses Ubuntu.

If you do not use Ubuntu as your host OS, you should look into virtualizing a Ubuntu environment via LXC or a VM.

## Using Ubuntu:
### Step 1, Add the phablet-tools repository:
```
sudo add-apt-repository ppa:phablet-team/tools
sudo apt-get update
sudo apt-get install phablet-tools
```

### Step 2, Installing build tools:
```
sudo apt-get install git gnupg flex bison gperf build-essential \
  zip bzr curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
  libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
  libgl1-mesa-dev g++-multilib mingw32 tofrodos \
  python-markdown libxml2-utils xsltproc zlib1g-dev:i386 schedtool \
  g++-4.8-multilib
```

### Step 3, Create a new directory and check out the ubp tree
```
mkdir phablet && cd phablet/
repo init -u https://github.com/ubports/android -b ubp-5.1
repo sync
```


# Build

### Initialize
First we need to Initialize the environment using the envsetup.sh tool:
```
. build/envsetup.sh
```
This will give you an output that looks like this:
```
including device/samsung/maguro/vendorsetup.sh
including device/samsung/toro/vendorsetup.sh
including device/samsung/tuna/vendorsetup.sh
including device/samsung/manta/vendorsetup.sh
including device/samsung/crespo4g/vendorsetup.sh
including device/samsung/torospr/vendorsetup.sh
including device/generic/armv7-a-neon/vendorsetup.sh
including device/generic/x86/vendorsetup.sh
including device/oneplus/bacon/vendorsetup.sh
including device/lge/hammerhead/vendorsetup.sh
including device/lge/mako/vendorsetup.sh
including device/asus/tilapia/vendorsetup.sh
including device/asus/deb/vendorsetup.sh
including device/asus/flo/vendorsetup.sh
including device/asus/grouper/vendorsetup.sh
```

### Choose you target
Now we need to choose the target to build using the lunch command;
```
lunch
```
The output of this command will look something like this:
```
You're building on Linux

Lunch menu... pick a combo:
 1. aosp_arm64-eng 	 4. aosp_mips-eng 	  7. cm_bacon-eng 
 2. aosp_arm-eng 	 5. aosp_x86_64-eng   8. cm_bacon-user 
 3. aosp_mips64-eng  6. aosp_x86-eng      9. cm_bacon-userdebug 

Which would you like? [aosp_arm-eng] 
```
Here you need to choose your device cm[your device]-userdebug, example if you were to build the oneplus one you would choose cm_bacon-eng or 7

### Building your device
Here comes the fun part, building the device it self using the command make
```
make
```
for building faster, you can use the -j[n] option for doing parallel operations. it's common to use a number of tasks N that's between 1 and 2 times the number of hardware threads on the computer being used for the build.
```
make -j4
```

The output will be in out/target/[device]