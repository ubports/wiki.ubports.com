## Introduction

Libertine is a command line tool to easily install and manage standard desktop applications in Ubuntu Touch using containers.

## Background explaination

A display server is what it's used to coordinate input and output of an operative system. Most Linux distributions today use the X server while Ubuntu Touch uses a new generation server called Mir. This cause an incompatibility of standard X applications with Ubuntu Touch, this issue is solved with a compatibility layer called XMir. Application installed with Libertine will use XMir to work. Another issue is that Ubuntu Touch system updates are released as OTA images, this cause the root filesystem to be read only. To install standard programs Libertine uses containers: basic Ubuntu installations where you can install any package you want.

## Useful commands

### Note

To display and launch the application you will install with Libertine you have to install the Desktop Apps Scope, available in the Canonical Store.

The commands listed below cannot be run directly on the terminal app, due apparmor restrictions. You have to either run them from another device using either adb or ssh, or from your device you can use a loopback ssh connection running this command:

"ssh localhost"

### Create a container

First step is to create a new container where applications can be installed:

"libertine-container-manager create -i <container-identifier>"

You can add extra options such as:

"-n <name>" name is a more user friendly name of the container

"-t <type>" type can be either chroot or lxc. Default is chroot and is compatible with every device. If the kernel of your devices support lxc, is suggested to use it

The creating process can take some time, due to the size of the container (some hunded of megabytes)

To list all containers created run:
"libertine-container-manager list"

### Destroy a container
"libertine-container-manager destroy -i <container-identifier>"

### Manage applications

Once a container is set up, you can manage applications:

"libertine-container-manager list-apps -i <container-id>" Lists installed launchable applications

"libertine-container-manage install-package -i <container-id> -p "package-name"" install a package

"libertine-container-manager remove-package -i <container-id> -p "package-name"" remove a package

### others

To execute any arbitrary command inside the container run:

"libertine-container-manager exec -i <container-id> -c "command you want to execute"

To have a shell you can use /bin/bash as a command.