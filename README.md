# EK-7688AMx.OW1407


## How to build the firmware for EK-7688AMx?

* 1) [Install prerequisite packages](http://labs.mediatek.com/fileMedia/download/87c801b5-d1e6-4227-9a29-b5421f2955ac#page=97&zoom=auto,70,239)

* 2) Update the feed information for all packages and install all packages
```
     ./scripts/feeds update -a
     ./scripts/feeds install -a
```	 

* 3) Choose default config
```
make defconfig
```

* 4) Select options for EK-7688AMx
```
make menuconfig
```

* 5) Make a new firmware 
```
make V=s
```

* 6) Get a new firmware under bin/ramips/XXX-sysupgrade.bin

