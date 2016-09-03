# EK-7688AMx.OW1407


## How to build the firmware for EK-7688AMx?

0. [Install prerequisite packages](http://labs.mediatek.com/fileMedia/download/87c801b5-d1e6-4227-9a29-b5421f2955ac#page=97&zoom=auto,70,239)

0. Update the feed information for all packages and install all packages
   ```
     ./scripts/feeds update -a
     ./scripts/feeds install -a
   ```	 

0. Choose default config -- `make defconfig`

0. Select options for EK-7688AMx -- `cp EK-7688AMx.OW1407 .config`

0. Make a new firmware -- `make V=s`

0. Get a new firmware under bin/ramips/xxx-sysupgrade.bin

## How to setup AP-Client mode?

0. Rewrite /etc/config/network -- `vi /etc/config/network` (ps:look for the apcli0's mac `ifconfig apcli0 up` `ifconfig`)

	```
	config interface 'lan'
   		option ifname 'eth0.1'
		option force_link '1'
		option type 'bridge'
		option proto 'static'
		option ipaddr '192.168.1.1'
		option netmask '255.255.255.0'
		option ip6assign '60'
		option macaddr '9C:65:F9:1D:80:AF'

	config interface 'wan'
		+++option ifname 'apcli0'
		option proto 'dhcp'
		+++option macaddr '9E:65:F9:0D:81:28'
	```

0. Rewrite /etc/config/wireless -- `vi /etc/cnfig/wireless`

	```
    	+++option channel  3  （ps: the same as RootAP's)
    	option auotch   2

	config wifi-iface
		option device   mt7628
		option ifname   ra0
		option network  lan
		option mode     ap
		option ssid     mt7628-80AF  
		option encryption psk2
		option key      12345678
		+++option ApCliEnable '1'                        
		+++option ApCliSsid 'RootAP_SSID' (RootAP's SSID)
    	+++option ApCliBssid 'xx:xx:xx:xx:xx:xx'  (RootAP's BSSID)
		+++option ApCliAuthMode 'WPA2PSK'  (RootAP's Auth.)
    	+++option ApCliEncrypType 'AES'  (RootAP's Encryp.)
		+++option ApCliWPAPSK 'RootAP_PW' (RootAP's password)
	```

0. restart network -- `/etc/init.d/network restart` 
