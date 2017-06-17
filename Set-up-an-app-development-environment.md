"Clickable" is a program to support you with developing apps for the Ubuntu Touch platform.
It is written by Brian Douglass and helps you to build, manage, install and test your app 
without the need of the whole Ubuntu SDK.

For information about using clickable, see here: https://github.com/bhdouglass/clickable


This guide assumes you are using Ubuntu Xenial on your development machine. Other host systems might work just fine as well. If you cannot set up Clickable as described here you might want to try our alternative instructions to setup Clickable inside a container. 

## Install 

`git clone https://github.com/bhdouglass/clickable.git`
Set the repo on your PATH

## Configure

Run clickable setup-lxd to create a container to build clicks an


## First app
Once the container is setup you can build and run your first app:

`git clone https://github.com/bhdouglass/ut-app-template`
`cd ut-app-template/`
`clickable`

This should build and start an app on your Ubuntu Touch device displaying "Hello World!"

## Final thoughts

Clickable is a wonderful tool to develop app for ubuntu touch, thanks to Brian Douglass and all the devs for manteining it and for all the help they gave me :D
Good coding everyone!!!