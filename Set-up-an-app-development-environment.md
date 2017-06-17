[Clickable](https://github.com/bhdouglass/clickable) is a program to support you with developing apps for the Ubuntu Touch platform. It is written by Brian Douglass and helps you to build, manage, install and test your app without the need of the whole Ubuntu SDK.

This guide assumes you are using Ubuntu Xenial on your development machine. Other host systems might work just fine as well. If you cannot set up Clickable as described here you might want to try the alternative instructions to setup [Clickable inside a container](https://wiki.ubports.com/wiki/Set-up-a-Clickable-working-environment-inside-an-LXC-container), or the [Clickable website](https://github.com/bhdouglass/clickable) for other alternatives like snap. 

# Install 

Download clickable 
`cd ~`
`git clone https://github.com/bhdouglass/clickable.git`

Add this repository on your PATH by adding the following line at the end of your `~/.bashrc` file:
`export PATH=$PATH:~/clickable`


# Configure

Run 
`clickable setup-lxd` 
to create a container which will be used for building your app.


# First app
Now you are setup to build and run your first app:

`git clone https://github.com/bhdouglass/ut-app-template`
`cd ut-app-template/`
`clickable`

This should build and start an app on your Ubuntu Touch device displaying "Hello World!"

# Final thoughts

Clickable is a wonderful tool to develop app for Ubuntu Touch. Thanks to Brian Douglass and all the devs for maintaining it and for all the help they gave :D
Good coding everyone!!!