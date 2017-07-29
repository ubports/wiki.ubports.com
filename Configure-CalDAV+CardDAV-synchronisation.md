At the moment, there is no caldav/carddav implemention directly accessible from the Ubuntu Touch interface, so the only way to sync carddav & caldav is by using syncevolution + cron.
However, there is a simple way to do that with a script that you can run in the terminal or via phablet SSH connection.

1) Follow this [guide](https://wiki.ubports.com/wiki/How-to-use-adb-from-ubuntu-desktop) to activate Developer Mode and SSH connection

2) Download this [script](https://gist.github.com/bastos77/0c47a94dd0bf3e394f879c0ff42b7839) (let's call it dav.sh) and edit the following variables: 
- server side : CAL_URL, **CONTACTS_URL**, USERNAME, PASSWORD (of your ownCloud/nextCloud/baikal/SOGO/... server)
- CONTACT and CALENDAR _ NAME / VISUAL_NAME / CONFIG_NAME (it's more cosmetic)
- CRON_FREQUENCY (for the frequency of synchronisation)

3) Move the file to your UbuntuTouch device, either by file manager or with adb: 
```adb push dav.sh /home/phablet```

4) Connect with the phablet shell ( * ) or directly on the phone Terminal app and type the following:
```chmod +x dav.sh```
```./dav.sh```


( * ) One way among others to launch the phablet shell:
Install ubuntu-sdk (ppa:ubuntu-sdk-team/ppa), put your phone in developer mode, open ubuntu-sdk, connect your device to computer, go to devices in ubuntu-sdk and in control, exec open ssh session. 


Sources:
https://askubuntu.com/questions/616081/ubuntu-touch-add-contact-list-and-calendars/664834#664834
https://gist.github.com/boTux/069b53d8e06bdb9b9c97
https://gist.github.com/tcarrondo
https://gist.github.com/bastos77
https://askubuntu.com/questions/601910/ssh-ubuntu-touch