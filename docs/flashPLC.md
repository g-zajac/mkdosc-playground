# Flashing PLC

## Connecting programmer

Connect the ST-link USB dongle (programmer) to a USB port and clip the PLC board.

!!! failure

        The clip pin order works ONLY with the sink PLC ver 1.0.3 older version have diferent order and need to be wire manually without the clip.

4 wires need to be connected from programmer to PLC:
- 3V3
- GND
- CLK
- DIO
  
![PLC programmer](assets/flashing-plc.jpg)

## Flashing the firmware 

To flash the connected sink PLC run from /devel/skycharge/hw2/skysink/firmware:
```bash
make flash-hw-version HW_VERSION=1.2.0
```

## Other usefull commands
```bash
st-info —probe
```
