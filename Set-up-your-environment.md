Setting up you environment is necessary before starting poring to any device.

## Using Ubuntu:
### Step 1, Add the phablet-toos:
```
sudo add-apt-repository ppa:phablet-team/tools
sudo apt-get update
sudo apt-get install phablet-tools
```

### Step 2, Installing building tools:
```
sudo apt-get install git gnupg flex bison gperf build-essential \
  zip bzr curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
  libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
  libgl1-mesa-dev g++-multilib mingw32 tofrodos \
  python-markdown libxml2-utils xsltproc zlib1g-dev:i386 schedtool \
  g++-4.8-multilib
```

### Step 3, Create a new directory and download the AOSP tree
```
mkdir phablet
phablet-dev-bootstrap phablet
```