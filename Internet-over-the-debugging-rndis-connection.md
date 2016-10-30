If you're porting to a device using the rndis debugging connection but haven't gotten Wi-Fi figured out yet, you can use the Internet connection of your computer on the phone. Read on to find out how.

I assume you're running Ubuntu >=16.04 for these instructions. Earlier versions of Ubuntu or other distros will probably work if iptables is installed.

First, find the name of the interface you're using for your internet connection using `ifconfig`. You'll need it for the following commands. Run them in order on your host machine, replacing `[if]` with your interface's name.

```
sudo sysctl net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o [if] -j MASQUERADE
sudo iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i net0 -o [if] -j ACCEPT
```