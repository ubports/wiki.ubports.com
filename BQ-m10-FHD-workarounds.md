This explains the 2 workarounds that was needed for the BQ m10 FHD to work without modifacations to the ubports rootfs. *NOTE: this does not effect the HD version*

### Woarkaround for low system partition space
The device do not have the space necessary in system to successfully run ubports rootfs, the workaround for this is to use the "image in data" method as we use on Oneplus one, fairphone 2 and Nexus 5. This means we place a image file in data that acts as the system partition.

To do this we removed `systempart=/dev/disk/by-partlabel/system` from boot.img cmdline and recovery.img cmdline


### Workaround for low cache partition space
The device do not have the space necessary in cache to successfully install ubports rootfs. Since the system partition is unused now, we swapped the cache partition with system.

To do this we removed /system and swapped the cache partition with system in fstab in android-ramdisk.img that exsists inside system.img (android system image)

For recovery we did the same as but insted we did this in /etc/recovery.fstab in the recovery. 

We also created a script that remounts /cache before it starts the recovery service