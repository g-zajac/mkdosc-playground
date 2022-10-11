# Flashing PLC

Connect to USB the ST-link and wire it to a sink PLC with 4 wires:
- 3V3
- GND
- CLK
- DIO

Run: 

```bash
cd /devel/skycharge/hw2/skysink/firmware
make flash-hw-version HW_VERSION=1.2.0
st-info —probe
st-flash
make flash
```

