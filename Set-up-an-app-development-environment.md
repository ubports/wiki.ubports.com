# Alternative: on-device software development

When it comes to app development, there is the default approach, and some alternative ones. One such alternative approach is the [[UT on-device software development]] wiki, which gathers various methods of native software development on the UT device itself, using tools that run on the phone/tablet itself. Listed alternatives propose a few different tools and programming languages, some more simple, some more sophisticated.

# Clickable

[Clickable](https://github.com/bhdouglass/clickable) is a program to support you with developing apps for the Ubuntu Touch platform. It is written by Brian Douglass and helps you to build, manage, install and test your app without the need of the whole Ubuntu SDK.

This guide assumes you are using Ubuntu 16.04 on your development machine. Other host systems might work just fine as well. If you cannot set up Clickable as described here you might want to try the alternative instructions to setup [[Clickable inside a container|Set-up-a-Clickable-working-environment-inside-an-LXC-container]], or the [Clickable website](https://github.com/bhdouglass/clickable) for other alternatives like snap. 

## Prerequisites
Ubuntu 16.04

```
sudo apt-get install lxd android-tools-adb
sudo lxd init
```
If you have the Ubuntu SDK IDE install, you will already have the necessary prerequisites. If you don't already have the IDE installed you will need to install adb and lxd. After installing lxd you will need to run `lxd init` to get everything setup with lxd.

## Install

```
cd ~
git clone https://github.com/bhdouglass/clickable.git
echo "export PATH=\$PATH:~/clickable" >> ~/.bashrc
. ~/.bashrc
clickable setup-lxd
```

## First app

Now you are set up to build and run your first app:

```
git clone https://github.com/bhdouglass/ut-app-template
cd ut-app-template/ 
clickable
```

This should build and start an app on your Ubuntu Touch device displaying "Hello World!"

Look [here](https://github.com/bhdouglass/clickable#usage) for further instructions.

# Ubuntu SDK IDE (unsupported)

The [Ubuntu SDK IDE](https://docs.ubuntu.com/phone/en/platform/sdk) is no longer supported by Canonical, and UBports does not currently have the the time and manpower to get it to a working state.

It can still be installed, but issues are expected.

```
sudo add-apt-repository ppa:ubuntu-sdk-team/ppa
sudo apt update && sudo apt dist-upgrade
sudo apt install ubuntu-sdk
sudo reboot # or logout/login 
```