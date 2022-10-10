# Updateing Debian on Beaglebone

The Skycharge card image used to flash new Beaglebone is based on Debian 9 Stretch which has reached the end of life but it is still supported.
More info about Debian verisions [here](https://wiki.debian.org/DebianReleases) 

!!! Warning

This procedure was carried for Fortem in Septebmeber 2022. Works but it has not been fully tested.


## Prepare Beaglebone
Flash brand new Beaglebone with Skycharge SD card as usual.
Restart and log in and follow steps below.

## Upgrading Linux v9 Stretch to Linux v10 Buster
The upgrade is done via apt upgrade on existing and running system with preinstalled Skychage packages.
The upgrade steps:

To check current linux version run:
```bash
cat /etc/*release
```
optional:
```bash
lsb_release -a
cat /etc/debian_version
```

You should receive:
PRETTY_NAME="Debian GNU/Linux 9 (stretch)"
NAME="Debian GNU/Linux"
VERSION_ID="9"
VERSION="9 (stretch)"
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"

## Preparing space on flash disk
To run update some space on flash is needed.
To check available space on Beaglebone run
```bash
df -h
```
should have about 77% on /

To update Debian 9 to debian 10 please edit the file /etc/apt/sources.list using a text editor (i.e: vim, nano) and replace each instance of stretch with buster.
Before updating please run ´apt install dirmngr´ explanation in next paragraph.
```bash
apt update 
```

If you got missing GPG signatures then install missing network certificate management service (this should be done before apt update as it is stretch package).
```bash
apt install dirmngr
```

And add missing keys (listed in error message) with:
```bash
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <missing_key>
```
Then run update again, this time should run without any errors:
```bash
apt update
```


## Minimal system upgrade
The minimal system upgrade can be useful when the system is tight on space and a full upgrade cannot be run due to space constraints.
Detailed information [here](https://www.debian.org/releases/buster/amd64/release-notes/ch-upgrading.en.html#minimal-upgrade)
_4.4.3. Make sure you have sufficient space for the upgrade_

```bash
apt upgrade --without-new-pkgs
```
There will be an error: …run out of space
The Beagle bone does not have enough flash to run the system upgrade, workaround:
```bash
apt autoremove
apt clean
```
To save space, there are still some files which can be removed:
```bash
rm -fR /var/lib/cloud9
rm -fR /var/lib/cloud9_backup_examples/
rm -fR /usr/local/lib/node_modules/
rm -fR /lib/firmware/iwlwifi*
rm -fR /usr/share/bone101/examples/extras/bacon_cape
rm -fR /opt/scripts/device/bbai
```
Checking available space:
```bash
df -h
```
If it is still not enough, you can add external usb drive or card for /var/cache/apt/archives/
any package needed for installation that is fetched from the network is stored in /var/cache/apt/archives (and the partial/ subdirectory, during download), so you must make sure you have enough space on the file system partition that holds /var/ to temporarily download the packages that will be installed in your system

## Adding temporary external drive (SD card) to extend flash
To add external USB drive or SD card, list external drives and find the name, in my case mmcblk0
```bash
fdisk -l
```
A SD card formatted to EXT4 has been used.
To prepare the SD card:
```bash
mkfs.ext4 /dev/mmcblk0
```

To mount the SD card:
```bash
mkdir /mnt/external
mount -t ext4 /dev/mmcblk0 /mnt/external/
```
Copy the directory /var/cache/apt/archives to the card
```bash
cp -ax /var/cache/apt/archives /mnt/external/
```
Mount the temporary cache directory on the current one:
```bash
mount --bind /mnt/external/archives /var/cache/apt/archives
```
After the upgrade, restore the original /var/cache/apt/archives directory:
```bash
umount /var/cache/apt/archives
```
The command df -h should show the external drive with mounted filesystem

## Upgrade
Now run the upgrade:
```bash
apt upgrade --without-new-pkgs
```

Once the update finishes you can check linux version:
```bash
cat /etc/*release
```
PRETTY_NAME="Debian GNU/Linux 10 (buster)"
NAME="Debian GNU/Linux"
VERSION_ID="10"
VERSION="10 (buster)"
VERSION_CODENAME=buster
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"

```bash
reboot
```
