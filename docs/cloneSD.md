# Cloning SD card

Instruction to clone a SD card, used for backup of the Skycharge installation image.
The process run on Mac in terminal.
Inser the SD card, make sure it is the same siye or bigger then the source SD card.
Attach and identify the source disk
```bash
diskutil list
```

Unmount the source disk
```bash
diskutil unmountDisk /dev/disk2
```

The DD tool is used for cloning. 

Copy the source disk to the desktop
```bash
sudo dd if=/dev/rdisk2 of=/Users/production/diskimage.img bs=16M
```

!!! info

    if (input file) and of (output file)

Warning
There is no progress indicator while the dd is cloning the card and it can be very long.

To sovle the lack of progres the pv tool can be installed and added.
pv - Pipe Viewer - is a terminal-based tool for monitoring the progress of data through a pipeline
```bash
brew install pv
```
now the dd can be run with progress indication
```bash
dd if=/dev/rdisk2 | pv | of=/Users/production/skycharge_sd_backup.img bs=16M
```
if the size of image is now it can be applied
```bash
dd if=/dev/rdisk2 | pv -s 16G | of=/Users/production/skycharge_sd_backup.img bs=16M
```
expected oustcome:
```bash
1.61GiB 0:12:19 [2.82MiB/s] [===>                 ] 10% ETA 1:50:25
```

Remove the card after finished process. Attach and identify the destination disk
```bash
diskutil list
```
Unmount the destination disk
```bash
diskutil unmountDisk /dev/disk2
```
Copy the image to the destination disk
```bash
sudo dd if=/Users/production/sd_backup.dmg | pv -s 16G | sudo dd of=/dev/disk2
```
