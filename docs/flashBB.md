# Flashing Beaglebone

This document is about preparing brand new Skycharge source board with brand new Beaglebone when building a charging system.

Run on production machine
```bash
./skyzeroconf 
```
Make sure that the label printer is on and connected to ethernet.
<!-- TODO add more info about the script, why, what for, what does it do -->

Insert the SD card with image to the Beaglebone (BB), connect it with etherent with acces to internet and to the machine hosting skyzeroconf.
Power the BB up, after a minute or so all blue LEDs on BB should start 'walking' back and forth - flashing. The flashing proces takes about 15mins or so. Once the flashing is complete the leds go off. At the moment there is a bug, the process run twice. During the flashing a label should be automaticly printed. Once the flashing process is completed, the BB LEDs are off, disconnect from power and ethernet and install the BB to the source board. Connect the source board to the 12V board PS and also the Meanwell PS - (essential for calibration process). Power up.

!!! Note

  Remeber to remove the SD card after flashing.

Power up the BB, after a minute ish, once it is booted, acces the BB remotly via ssh.

```bash
ssh -i <path to ssh keys> root@skydevice.local
```

# (1)

Flashed BB consists debian system with all skycharge deamons and packages pre-installed. On the source board there is STM microcontroller which need to be flashed with Skycharge firmware when it comes from PCB manufacture. 
To do so, we can use preinstalled cli tool from BB and run:
```bash
skymux-flash --hw-version <get the number written on the board, it should be 1.3, so specify 1.3.0>
```
This will flash the STM microcontrller on the source board. The board may need power cycle (down and up) to be fully functional.

(1) - every BB use the mDNS name skycharge.local and if there will be two or more in the same LAN there will be confilict.
<!-- TODO format as warning note?  -->


