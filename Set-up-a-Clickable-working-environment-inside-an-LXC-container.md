Clickable is the Brian Douglass' program to build, manage, install and in general develop for the Ubuntu Touch platform without the need of the whole ubuntu SDK.
It can runs virtually in any linux environment (differently from the ubuntu SDK), but like me maybe also you encoutered problems setting up it in your favourite distro; here I am going to guide you throught setting up it in a LXC container.
In this way you aren't forced to change distro or run an expansive virtual machine, but you can use clickable almost like a native set up.
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

### Troubleshooting
If you get an error about apparmor (aa_allow_incomplete) change this setting and start the container again:
```
lxc config set clickablecontainer raw.lxc 'lxc.aa_allow_incomplete = 1'
lxc start clickablecontainer 
```

Before enter the new environment, we need to change some container policy options to enable nested lxc containers creation:
`lxc config set clickablecontainer security.privileged true`
`lxc config set clickablecontainer security.nesting true`
now you are ready to enter the matr...emm shell of our ubuntu container:
`lxc exec clickablecontainer -- /bin/bash`

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
Step in our home directory
`cd $HOME`
Install and configure LXD. See the previous 'SET UP LXD' section, here is the same story.

### Configure clickable inside the container

Here we are! Eventually you can download clickable:
`git clone https://github.com/bhdouglass/clickable.git`
Enter the master directory
`cd clickable-master`
We have to install the usdk-target executable (bundled with clickable) to be able to create sdk ubuntu LXC containers with clickable.
Inside the container we need to run sudo with the `-S` option, because without it will fail.
`sudo -S cp usdk-target /bin`
`sudo -S cp usdk-target /usr/bin`
`sudo -S cp usdk-target /usr/sbin`
`sudo -S cp usdk-target /sbin`
I copyied it into all the four directoryes because I don't know in which one I should copy it; it's a quick-and-dirt solution, but I am too lazy.
Now you need to patch the clickable executable. I said before that in this environment we have to run sudo with the `-S` option.
`nano clickable`
Look for the line:
`subprocess.check_call(shlex.split('sudo {} usdk-target create -n {} -p {}'.format(env, name, fingerprint)))`
And add the -S option. Here it is the result:
`subprocess.check_call(shlex.split('sudo -S {} usdk-target create -n {} -p {}'.format(env, name, fingerprint)))`
Save with `CTRL-o` and exit nano with `CTRL-x`.
You have succeffully set up clickable inside an lxd container!
Now you can run clickable inside the lxc container without problems.
For information about using clickable, see here: https://github.com/bhdouglass/clickable
Note that Canonical server might not work, you can tell clickable to use a different image server with the `USDK_TEST_REMOTE` environment variable.

## Final thoughts

Clickable is a wonderful tool to develop app for ubuntu touch, thanks to Brian Douglass and all the devs for manteining it and for all the help they gave me :D
Good coding everyone!!!