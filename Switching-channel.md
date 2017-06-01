### Method 1 (system-image-cli):

1. ssh/adb or use the terminal app to access command line
2. run
`system-image-cli --switch [channel]`

### Method 2 (udf from ubuntu):

1. Connect device to an PC
2. Run from the connected PC
`ubuntu-device-flash --server=http://system-image.ubports.com touch --channel=[channel]`

### Method 3 (udf from recovery):

1. Connect device to an PC
2. Reboot to recovery (you can use adb to do this `adb reboot recovery`)
3.  Run from the connected PC
`ubuntu-device-flash --server=http://system-image.ubports.com touch --channel=[channel]`