In case you want to connect your phone manually, maybe because you don't have GUI or RNDIS does not work over USB or simply for test via the commandline, you can still use Network-Manager.

Since Network Manager is driven by config files, first step is to create a new config file, probably for a WiFi connection:


Call this file after the SSID of the network, lets say xxx.

We will place this config file in the folder /etc/NetworkManager/system-connections/ and change the permissions to 0600 - this is important, files with other modes will not be accepted.

Now we use the cmdline tool nmcli to tell Network-Manager what we want:

1. nmcli con reload

this will re-read the config directories

2. nmcli con up id 'xxx'

This should bring up the interface, attach wpa_supplicant to it and handle the association and key-excha nge, and get dhclient informed. Pretty neat!