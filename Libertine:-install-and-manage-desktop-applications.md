## Introduction

Libertine is a tool to install and manage standard desktop applications in Ubuntu Touch.

## Background 

A display server coordinates input and output of an operating system. Most Linux distributions today use the X server. Ubuntu Touch does not use X, but  a new display server called Mir. This means that standard X applications are not directly compatible with Ubuntu Touch. A compatibility layer called XMir resolves this. Libertine relies on XMir to display desktop applications. 

Another challenge is that Ubuntu Touch system updates are released as OTA images. Therefore the root filesystem is read only. Libertine provides a container with a read-write filesystem to allow the installation of regular Linux desktop applications.

## Desktop Apps Scope

To display and launch applications with Libertine you need the Desktop Apps Scope which is available in the Canonical App Store.

## Manage containers

### Create a container

The first step is to create a new container where applications can be installed:

<code> libertine-container-manager create -i container-identifier </code>

You can add extra options such as:

<code> -n name</code> name is a more user friendly name of the container

<code>-t type</code> type can be either chroot or lxc. Default is chroot and is compatible with every device. If the kernel of your device supports it then lxc is suggested.

The creating process can take some time, due to the size of the container (some hunded of megabytes).

#### Note

The create command shown above cannot be run directly in the terminal app, due apparmor restrictions. You can run it from another device using either adb or ssh connection. Alternatively, you can run it from the terminal app using a loopback ssh connection running this command:

<code> ssh localhost </code>

### List containers
To list all containers created run:
<code> libertine-container-manager list </code>

### Destroy a container
<code> libertine-container-manager destroy -i container-identifier </code>

## Manage applications

Once a container is set up, you can manage applications:

<code> libertine-container-manager list-apps -i container-identifier </code>Lists installed applications

<code> libertine-container-manage install-package -i container-identifier -p package-name</code> install a package

<code> libertine-container-manager remove-package -i container-identifier -p package-name</code> remove a package

## Other useful commands

To execute any arbitrary command inside the container run:

<code>libertine-container-manager exec -i container-identifier -c "command you want to execute" </code>

To have a shell you can use /bin/bash as command.