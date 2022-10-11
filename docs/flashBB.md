# Flashing Beaglebone

This document is about preparing brand new source board with brand new Braglebone when building a charging system.


Run on production machine
```bash
./skyzeroconf 
```
Make sure that the label printer is on.
<!-- TODO add more info about the script, why, what for, what does it do -->

Insert the SD card with image to the Beaglebone (BB), connect it with etherent with acces to internet and to the machine hosting skyzeroconf.
Power up, after a minute or so all blue beaglebone LEDs should start 'walking' back and forth - flashing. The proces takes about 15mins or so. Once the flashing is complete the leds go off. At the moment there is a bug, the process run twice.
Install the BB to the source board. The souurce board should be powered with the 12V board PS and also the Meanwell PS should be connected (essential for calibration process).

!!! Note

  Remeber to remove the SD card after flashing

Power up the BB, after a minute ish, once it is booted, acces the BB remotly via ssh.

```bash
ssh -i <path to ssh keys> root@skydevice.local
```

# (1)

Flashed BB consists debian system with all skycharge deamons and packages pre-installed. On the source board there is STM microcontroller which need to be flashed when it is brand new. 
To do so, we can use preinstalled cli tool from BB and run:
```bash
skymux-flash --hw-version <get the number written on the board, it should be 1.2, so specify 1.2.0>
```
This will flash the STM microcontrller on the source board. The board may need power cycle down and up to be fully functional.


(1) - every BB use the mDNS name skycharge.local and if there will be two or more in the same LAN there will be confilict.
<!-- TODO format as warning note?  -->


