This is the original `xpad` kernel driver with support for Xbox One controllers removed. If you are running the `xone` driver (work in progress) you will have to replace your `xpad` binary with this one to retain the functionality of Xbox and Xbox 360 controllers.
# Using dkms
Best way to do that is probably by using `dkms` which will recompile this module for each new kernel version:
1. clone the repository
```
git clone https://github.com/medusalix/xpad-noone
```
2. then enter the folder and create a new file `dkms.conf` with this content:
```
PACKAGE_NAME="xpad-noone"
PACKAGE_VERSION="1.0"
BUILT_MODULE_NAME[0]="xpad"
DEST_MODULE_LOCATION[0]="/kernel/drivers/input/joystick"
AUTOINSTALL="yes"
```
3. finally copy the whole folder xpad-noone to `/usr/src/`:
```
sudo cp -R xpad-noone /usr/src/xpad-noone-1.0
```
4. Now you just need to install it through dkms: 
```
sudo dkms install xpad-noone/1.0
```
5. The last step is going to `/etc/modprobe.d/xone-blacklist.conf` and comment the line
```
# blacklist xpad
```
Then `sudo modprobe xpad` or reboot
(and a big thank you to NoXPhasma on Discord for helping with this procedure)
