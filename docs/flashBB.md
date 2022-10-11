# Flashing Beaglebone

Run on production machine
```bash
./skyzeroconf 
```

Insert the SD card with image to the Beaglebone (BB), connect etherent and with the machine hosting skyzeroconf.
All blue beaglebone LEDs should 'walking' back and forth. Once the flashing is complete the leds go off.
Connect flashed BB to the source board. The board should be connected to the 12V board PS and also to the Meanwell PS. Power up and connect with ssh to the BB.

Run
```bash
skymux-flash --hw-version <get the number written on the board, it should be 1.2, so specify 1.2.0>
```






