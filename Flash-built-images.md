This is the exiting part, trying out your built images

Using portcraft:
1. Install portcraft 

2. Flash
```

```

Using rootstock installer

1. Download latest vivid (it need to be vivid, never images does not yet work!) 

ARM (32 and 64 bit): http://cdimage.ubuntu.com/ubuntu-touch/vivid/daily-preinstalled/current/vivid-preinstalled-touch-armhf.tar.gz
i386: http://cdimage.ubuntu.com/ubuntu-touch/vivid/daily-preinstalled/current/vivid-preinstalled-touch-i386.tar.gz

2. Download the rootstock tool 
```
bzr branch lp:~mariogrip/project-rootstock-ng/project-rootstock-ng
```

3. Flash
```
./rootstock-touch-install [path to vivid-preinstalled-touch] [path to your built system.img]
```