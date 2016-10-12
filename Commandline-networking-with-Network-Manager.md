In case you want to connect your phone manually, maybe because you don't have GUI or RNDIS does not work over USB or simply for test via the commandline, you can still use Network-Manager.

Since Network Manager is driven by config files, first step is to create a new config file, probably for a WiFi connection:

    [connection]
    id=Nerdbase
    uuid=<create_new_uuid_with_uuid_on_desktop>
    type=802-11-wireless
    autoconnect=true
    timestamp=0

    [ipv4]
    method=auto
    ignore-auto-routes=false
    ignore-auto-dns=false
    never-default=false

    [802-11-wireless]
    ssid=<use_python_script_on_desktop>
    mode=infrastructure
    channel=0
    rate=0
    tx-power=0
    mtu=0
    seen-bssids=
    security=802-11-wireless-security
    mac-address=<mac_from_wlan0_or_similar>

    [802-11-wireless-security]
    key-mgmt=wpa-psk
    wep-tx-keyidx=0
    psk=<psk_from_wpa_passphrase_output>

Call this file after the SSID of the network, lets say xxx.

We will place this config file in the folder /etc/NetworkManager/system-connections/ and change the permissions to 0600 - this is important, files with other modes will not be accepted.

Now we use the cmdline tool nmcli to tell Network-Manager what we want:

1. nmcli con reload

this will re-read the config directories

2. nmcli con up id 'xxx'

This should bring up the interface, attach wpa_supplicant to it and handle the association and key-excha nge, and get dhclient informed. Pretty neat!