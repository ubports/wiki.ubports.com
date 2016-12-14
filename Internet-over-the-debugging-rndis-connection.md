If you're porting to a device using the rndis debugging connection but haven't gotten Wi-Fi figured out yet, you can use the Internet connection of your computer on the phone. Read on to find out how.

I assume you're running Ubuntu >=16.04 for these instructions. Earlier versions of Ubuntu or other distros will probably work if iptables is installed.

First, find the name of the interface you're using for your internet connection using `ifconfig`. We'll call this `[if]` from here. Also note your PC's IP on the rndis network, `192.168.2.*`. Finally, note the interface name for the rndis network. We'll call that `[pf]`. You'll need them for the following commands. 

```
sudo sysctl net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o [if] -j MASQUERADE
sudo iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i net0 -o [if] -j ACCEPT
```

Then, using your telnet connection to your phone, run the following command:

`route add default gw [host ip on 192.168.2.* network]`

Then try pinging 8.8.8.8 on the phone. The pings should go through.

To temporarily add a DNS server on your phone, edit `/etc/resolv.conf` and add the line `nameserver 8.8.8.8`. This is NOT the recommended way to add a nameserver on Debian, but it works reliably when you can't depend on other options. Your changes will be overwritten on reboot, so you will need to perform them again.