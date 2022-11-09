# Printing labels

To generate a label for a device
```bash
skyzeroconf/generate-label.py --label-printer Brother_QL_820NWB  --device-name <name> --device-uuid <uuid> --output-path <path>
```
Device name and device uuid can be copied from the config file.
To print a label:
```bash
lpr -P Brother_QL_820NWB  -o landscape path-to-the-label.pdf
```

all generated labels should be in customers folder