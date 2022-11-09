# Preparing Skycharge System

This document is about preparing brand new Skycharge source board with brand new Beaglebone when building a charging system.

## Starting config server
Run on production machine skyzeroconf server. The server is genrating UUID, name, generate sticker etc. The server script is located at: /devel/skycharge/skyzeroconf and can be run with command:
```bash
./skyzeroconf 
```

Make sure that the server machine and label printer is turned on and connected to ethernet.

## Flashing BB
Insert the SD card with image to the Beaglebone (BB), connect it with etherent with acces to internet and to the machine hosting skyzeroconf.
Power the BB up, after a minute or so all blue LEDs on BB should start 'walking' back and forth - flashing. The flashing proces takes about 15mins or so. Once the flashing is complete the leds go off. ==At the moment there is a bug and the flashing process sometimes run twice.== During the flashing a label should be automaticly printed. Once the flashing process is completed, the BB LEDs are off and the BB is ready and can be disconnected from power and ethernet.

!!! Note
        Remeber to remove the SD card from the flashed Beaglebone after flashing.

## First power up 
Mounf the flasshed BB on the source board. 
Connect the source board to the 12V board PS and also the Meanwell PS - (essential for calibration process). Power up.
Power up the BB, after a minute ish, once it is booted, acces the BB remotly via ssh [^1].

```bash
ssh -i <path to ssh keys> root@skydevice.local
```

## Flashing MCU on source board
Flashed BB consists debian system with all skycharge deamons and packages pre-installed. On the source board there is STM microcontroller which need to be flashed with Skycharge firmware when it comes from PCB manufacture. 
To do so, we can use preinstalled cli tool from BB and run:
```shel
skymux-flash --hw-version <get the number written on the PCB i.e 1.3 at the moment, so specify 1.3.0>
```
This will flash the STM microcontrller on the source board. The board may need power cycle (down and up) to be fully functional.

## System calibration
The system calibration scripts are located @ /devel/skycharge/skyautotests and have two steps:

1) source PCB board calibration
```shell
./skyautotests.py root@skydevice.local sense-calibration
```
2)  Meanwell Power Supply (PS) calibration
```shell
./skyautotests.py root@skydevice.local ps-calibration
```
To run both, source followed by PS calibration sequences run:
```shell
./skyautotests.py root@skydevice.local full-calibration
```

For the development kit PCB boards without PS, the PS calibration can be achived mannually with the PS potentiometer. The procedure is as follow:
 
- ssh to BB
```shell
  ssh root@skydevice.local
```
- set a voltage i.e 20V at config file
```bash
sink-batt-max-voltage-mv = 20000
```
- restart skycharge deamon
```shell
systemctl restart skycharged
```

and adjust the PS pot so the skycharge-cli monitor voltage is as close as 20V. The setup voltage point is arbitrary and it schould be choosen in the middle of the range or close to the battery charging voltage to minimise the error.

Errors are calculated as follows:  

$$
\varepsilon _{absolutle} = U _{config} - U _{measured}
$$

Measured voltage is taken from skycharge-cli not from load. (verify cli vs load)

$$
\varepsilon _{relative} = \frac{\varepsilon _{absolutle}}{U _{measured}}
$$

$$
accuracy \rightarrow \varepsilon _{relative}
$$

Estimated accuracy:

- manually calibrated board is about 1.5%
- calibrated PS is about 0.5%

!!! note

        the error values are estimated and need to be verified with more measurments with more PSs



## System test

Run 

```bash
./skyautotests.py root@skydevice.local full-test
```

[^1]: Every BB use the same mDNS name skycharge.local, there will be confilict if two or more devices connected.
<!-- TODO format as warning note?  -->


