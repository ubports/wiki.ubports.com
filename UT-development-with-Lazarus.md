[Lazarus IDE](https://www.lazarus-ide.org) is a cross-platform open source and free IDE based on Delphi, that also supports ARM Linux natively. It uses [Free Pascal compiler](https://www.freepascal.org), and you can use it to compile once written code to a plethora of targets, including (but not limited to): Windows, OSX, Linux, and plethora of architectures, including Intel, ARM and many others. Both Free Pascal compiler and Lazarus IDE can be compiled, or installed from precompiled binaries/packages on Ubuntu Touch, using a default ARM Linux releases. In fact both **fpc** and **lazarus** packages are available in the default Ubuntu repositories, but most likely these are not the most recent versions, so on your Ubuntu Touch you could just run:
     
    sudo apt-get install fpc lazarus
     
Just that in reality there are few problems with this:
* on UT devices by default the system partition is read-only (can be easilyremounted to rw though)
* on UT devices by default the free space on system partition is quite low and might not be enough for installing both packages along with all dependencies (on Meizu MX4 phone with original UT only fpc package was possible to install, but not lazarus due to insufficient space). The resizing of the filesystem is not a very easy task.
* by default Lazarus IDE, which is a GTK app starts in multi-window mode, which does not work well when running gtk on the UT device via XMir. Lazarus can be configured into single window mode, which solves the problem. 

Laso Lazarus comes in QT mode, but built with an older QT than the version supported by UT. Also using Lazarus with OSK (on screen keyboard) is not convenient, but when using BT keyboard/mouse dongle over phones OTG/USB port, it works greatm, and UT will even show up a mouse pointer like on Ubuntu Desktop. Finally, one great way to use Lazarus is via ssh with X forwarding. in that scenario, although Lazarus IDE is installed and running off your UT device (phone/tablet) but it is forwarded via ssh onto your Ubuntu Desktop's monitor, and you also can use your desktop's keyboard and mouse to interact with it.

Before this wiki page gets full update, please check some external articles talking about all this:
* [Free Pascal development for Ubuntu Phone](http://kriscode.blogspot.tw/2016/09/freepascal-development-for-ubuntu-phone.html)
* [Lazarus development for Ubuntu Phone](http://kriscode.blogspot.tw/2016/10/lazarus-development-for-ubuntu-phone.html)

Benefits of using Lazarus are:
* Lazarus IDE is one of the best. see: [What is the best IDE on Linux](https://www.quora.com/What-is-the-best-IDE-for-Linux/answer/Krzysztof-Kamil-Jacewicz?srid=uKbMW)
* You kill multiple birds with one stone, because whatever you write for UT, you can also compile for Linux Desktop, Windows, OSX and other OSes
* you can actually create apps for UT device on the UT device itself!

GTK vs QT
When compiling Lazarus app, it gets built against a widgetset. By default the widgetset is GTK (unless you are using QT Lazarus version), but you can change a widgetset in the Lazarus configuration. Even if you do, the version of QT that Lazarus uses is 4, whereas UT devices use newer QT5. There are QT5 bindings for Lazarus available, but reportedly they are not very recent.
The simplest way between design and production is to build standard GTK apps. Currently the [GTK port for Mir](http://www.omgubuntu.co.uk/2014/06/ubuntu-devs-demo-gtk-apps-running-mir-unity-8) display server is only experimental and it is not sure if it will continue. But UT comes with XMir by default, which will run GTK apps on the phone itself: [X applications on Ubuntu Phone](http://kriscode.blogspot.tw/2016/09/x-applications-on-ubuntu-phone.html)