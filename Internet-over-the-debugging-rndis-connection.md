If you're porting to a device using the rndis debugging connection but haven't gotten Wi-Fi figured out yet, you can use the Internet connection of your computer on the phone. Read on to find out how.

I assume you're running Ubuntu >=16.04 for these instructions. Earlier versions of Ubuntu or other distros will probably work if iptables is installed.

First, find the name of the interface you're using for your internet connection using `ifconfig`.