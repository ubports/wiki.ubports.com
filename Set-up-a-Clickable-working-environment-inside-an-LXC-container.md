[Clickable](https://github.com/bhdouglass/clickable) is a program to support you with developing apps for the Ubuntu Touch platform. It is written by Brian Douglass and helps you to build, manage, install and test your app without the need of the whole Ubuntu SDK.

If you use a recent version of Ubuntu or of any other GNU/Linux flavour you can probably install Clickable without any problem directly on your system as described [[here|Set up an app development environment]]. However, if you encouter any problems setting this up it in your favourite distro, then this guide is for you. 

This guide is for setting up Clickable in a LXC container. That way you can run Clickable in virtually any Linux environment (differently from the ubuntu SDK). No need to change distro or run an expensive virtual machine. You can use Clickable almost like a native set up.
In this guide I consider using the apt package manager. Adapt the 'apt-get' commands to your circustances.

## Set up LXD

We are going to use an ubuntu 16.04 LTS container. To use it we have to install lxd, the lxc container hypervisor deamon. Install it.
`sudo apt-get install lxd`
You could be on a distro which doesn't have LXD in the repository. Don't worry, if your distro supports snap packages you can install the snap version of LXD.
I used the snap package to achieve the final result, but I suggest you to use your distro LXD package if you can. So first install snapd, then install the LXD snap:
`sudo apt-get install snapd`
`sudo snap install lxd`
Here is a deeper guide about the LXD snap package: https://stgraber.org/2016/10/17/lxd-snap-available/. If you are going to use the snap package, take a look there.
Configure LXD:
`sudo lxd init`
Just press enter until the end for a standard set up.

### Troubleshooting:
If you stumble upon any strange error when running lxd commands or lxc commands below, check if your user is in the lxd group, if not add yourself there:
`sudo usermod -a -G lxd username`
You might have to log out and log back in afterwards for this to take effect.

Another common issue could be to not have the lxd daemon running; if so just run:
`sudo systemctl start lxd.service`

## Set up the container

Now create the ubuntu container:
`lxc launch ubuntu:16.04 clickablecontainer`
and lxc will automatically download and set up our new container.

Before enter the new environment, we need to change some container policy options to enable nested lxc containers creation:
`lxc config set clickablecontainer security.privileged true`
`lxc config set clickablecontainer security.nesting true`
now you are ready to enter the matr...emm shell of our ubuntu container:
`lxc exec clickablecontainer -- /bin/bash`

### Troubleshooting
If you get an error about apparmor (aa_allow_incomplete) change this setting and start the container again:
`lxc config set clickablecontainer raw.lxc 'lxc.aa_allow_incomplete = 1'`
`lxc start clickablecontainer`


## Inside the container

First of all we need some basic utility:
`apt-get update`
`apt-get install nano sudo git python`
These packages may be already installed, but who know?
Next step is to configure a not root user:
`adduser mr_nice_guy`
Enable him to run sudo
`usermod -a -G sudo mr_nice_guy` // (Maybe this is not the most clean way to do it?)
Now we are ready to being the nice guy.
`su mr_nice_guy`
Install and configure LXD. See the previous 'SET UP LXD' section, here is the same story.

## Configure Clickable inside the container

Now you can set up Clickable like in a normal system, following the guide [[here|Set up an app development environment]].

## First app
Once the container is setup you can build and run your first app:

`git clone https://github.com/bhdouglass/ut-app-template`
`cd ut-app-template/`
`clickable`

This should build and start an app on your Ubuntu Touch device displaying "Hello World!"

## Final thoughts

Clickable is a wonderful tool to develop app for ubuntu touch, thanks to Brian Douglass and all the devs for manteining it and for all the help they gave me :D
Good coding everyone!!!