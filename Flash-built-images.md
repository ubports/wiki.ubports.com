This is the exiting part, trying out your freshly built images!

<!--
## Using portcraft:
1. Install portcraft
```

```

2. cd to the root of your build (same folder as you would run repo sync)
```
cd [root of build path]
```

2. Flash
```
portcraft flash [device name]
```

3. (Optinal) enable adb at boot
```
portcraft enable-adb
```
-->

## Using rootstock installer

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

4. (optional) Enable adb at boot (for ARM)

Download these 3 files from http://people.ubuntu.com/~mariogrip/Ubuntu-touch/fp2/ and then run 
```
./adb-install
```