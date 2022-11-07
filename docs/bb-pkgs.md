# Beaglebone Skycharge Packages

So the procedure is the following on BB:

Install public key
```shel
wget -O - -q http://install.skycharge.de/debian/pubkey.gpg | apt-key add -
```

Add skycharge repo to the repos list
```shel
echo "deb http://install.skycharge.de/debian stretch main" >
/etc/apt/sources.list.d/skycharge.list
```

Update BB repos cache
```shel
apt update
```

Now install all the packages from the web
```shel
apt install skysense-conf skysensed skysense-cli
```

## Helper commands
List available versions
```shel
apt-cache policy skysense*
```

Or install particular version
```shel
apt install skysensed=1.2.1
```


## Selfinstall script
Script for allowing flashed bbone to execute simple script and selfinstall. /usr/local/bin/selfinstall.sh launched in rc.local:

```bash
#!/bin/bash

FLAG="/var/log/firstboot.log"
if [ ! -f $FLAG ]; then
   #all commands here

   #the next line creates an empty file so it won't run the next boot
   touch $FLAG
else
   echo "Do nothing"
fi
```