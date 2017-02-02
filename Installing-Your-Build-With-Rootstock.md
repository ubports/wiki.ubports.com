So, you've got your Ubuntu Touch image ready to go. Now what? Should you create a .ZIP file and sideload it with adb? Well, not quite, but installing Ubuntu Touch isn't very hard at all once you've got the tools. Let's begin!


# MAKE A BACKUP!
This is important. Don't skip it. Back up your phone, including the Boot/ and Recovery/ partitions. Don't enable compression. Also have images of your ROM of choice available so you can flash them if things go awry. Copy these backups to your computer and make sure you have images of boot and recovery that can be flashed with fastboot! This is easy with TWRP as it saves them as boot.emmc.win and recovery.emmc.win, respectively. YMMV with other Recoveries.

# Set up your environment

As always, the first thing we'll need to do is get you set up to follow the guide.

## Download your preinstalled image
The stuff that you've built is just the Android system that Ubuntu Touch runs on top of. The actual Ubuntu Touch system is packaged into what is known as a "Preinstalled Image" and you'll use that along with your Android build to run the operating system.
There are two options for the preinstalled image: The 15.04 and 16.04 versions of Ubuntu. They roughly follow the packages that were in Ubuntu in their release. This has the benefit of allowing you to use tools you recognize while debugging such as lsb_release and nano. 
You should try the 15.04 image as it's what stable Ubuntu Touch is currently running on. You can get it here: <http://cdimage.ubuntu.com/ubuntu-touch/vivid/daily-preinstalled/current/> . The links nearer the top of the page are the ones you want, likely the ARM EABI images unless you know you have an x86 phone.
You can also try the 16.04 or 16.10 images if you're feeling adventurous and willing to submit LOTS of bug reports.

## Downloading Rootstock-NG
In order to install the system, we need a script called rootstock-touch-install, which is included in Rootstock-NG. The version found on the public Launchpad is broken, so we'll use Mariogrip's version: <http://people.ubuntu.com/~mariogrip/Ubuntu-touch/project-rootstock-ng.tar.gz>
Download that, extract it into your out/target/product/[DEVICE]/ folder so that it's in project-rootstock-ng. Make sure that rootstock-touch-install is executable.
Copy your downloaded prebuilt image to your build directory, usually ~/phablet/out/target/product/[DEVICE]/

# Installing


## Preparing the phone
Before beginning, ensure that your phone is not encrypted. If you have a phone that encrypts itself by default (like the Nexus 5X and 6P), you will need to factory reset it and go straight into these instructions without setting up the phone again. It goes without saying that this will erase all of the data from your phone.

First, boot your phone into Fastboot mode. You probably do this by holding down the power and volume down buttons to boot the phone, but your manufacturer may have changed that.

Then, run 
```
fastboot devices
```
Make sure that your device shows up. If it does, we're good to go

cd into your build directory, for me it's usually ~/phablet/out/target/product/[devicename]

Then,
```	
	sudo fastboot flash boot boot.img
	sudo fastboot flash recovery recovery.img
```
And boot into your recovery using your phone's preferred method.

## Installing the system

Once you've appeared at the recovery (probably a black screen after your boot logo, or the boot logo hanging for more than 20 seconds), run 
```
adb devices
```
To make sure your device appears. If it does, we're good to go. If it doesn't, it's time to ask someone because we haven't written docs for that quite yet.

Next,
```
adb shell
```
to enter your phone's shell.

Once you're in, type these commands:
```
	mount -a
	mkdir recovery
	exit
```

To ensure that Rootstock doesn't fail. You will probably see a lot of errors when running mount -a. This is acceptable.

Finally, we'll need to run rootstock-touch-install

```
sudo [path/to/]rootstock-touch-install [path/to/]vivid-preinstalled-touch-armhf.tar.gz [path/to]/system.img 
```

Rootstock should finish up, then reboot your device. If it doesn't, you can get help at the UBPorts or Ubuntu Touch IRC.



Please note that these instructions come with no warranty and UBPorts is not responsible for any damage to life, liberty, or your phone.