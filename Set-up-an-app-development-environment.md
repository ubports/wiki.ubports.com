# 1. GUI
[26.07.2017] Ubuntu SDK is a mirage, the fancy UI, the good documentation on ubuntu docs site, nice guides about it, the one commandline installer and you are good to go. It's all gone.
https://docs.ubuntu.com/phone/en/platform/sdk is still available
https://docs.ubuntu.com/phone/en/platform/installing-the-sdk is 404
I'm joking. Ubuntu SDK is still there just the link to installing the sdk on the docs page is wrong.
You probably know that there is a search in https://docs.ubuntu.com/phone/en/platform/sdk but just to mention it. If some link send you to 404 page, well search for it.
The correct link for Installing Ubuntu SDK is https://docs.ubuntu.com/phone/en/platform/sdk/installing-the-sdk
In terms of will it disappear, will it be supported, for how long, those are unknown variables depending on x^y variables.

# 2. Command Line gurus

[Clickable](https://github.com/bhdouglass/clickable) is a program to support you with developing apps for the Ubuntu Touch platform. It is written by Brian Douglass and helps you to build, manage, install and test your app without the need of the whole Ubuntu SDK.

This guide assumes you are using Ubuntu 16.04 on your development machine. Other host systems might work just fine as well. If you cannot set up Clickable as described here you might want to try the alternative instructions to setup [[Clickable inside a container|Set-up-a-Clickable-working-environment-inside-an-LXC-container]], or the [Clickable website](https://github.com/bhdouglass/clickable) for other alternatives like snap. 

# 2.1 Prerequisites
Ubuntu 16.04

```
sudo apt-get install lxd android-tools-adb
sudo lxd init
```
If you have the Ubuntu SDK IDE install, you will already have the needed prerequisites. If you don't already have the IDE installed you will need to install adb and lxd. After installing lxd you will need to run `lxd init` to get everything setup with lxd.

# 2.2 Install
```
cd ~
git clone https://github.com/bhdouglass/clickable.git
echo "export PATH=\$PATH:~/clickable" >> ~/.bashrc
clickable setup-lxd
```

# 2.3 First app

Now you are setup to build and run your first app:

```
git clone https://github.com/bhdouglass/ut-app-template
cd ut-app-template/ 
clickable
```

This should build and start an app on your Ubuntu Touch device displaying "Hello World!"

Read on [here](https://github.com/bhdouglass/clickable#usage) for further instructions.

# 3 Final thoughts
Clickable developer is not any different from me, he deploys code to his repository without testing it, so be aware! Do not trust me neither him blindly.