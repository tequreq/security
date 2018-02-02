If you have a valid cookie you can manipulate to switch login



1\) Take the get request from Burp \(try bdmin\)

2\) highlight cookie & Send to intruder

3\) Attempt the Bit flip \(hopefully it will flip bdmin to admin\) 

4\) payloads -&gt;payload type Bitflipper 

     options-&gt; literal value



Oracle Padding Attack

Noted by Invalid Padding Errors

1\) PadBuster.pl 

```
padbuster.pl URL EncryptedSample(randomcookiefromdummyaccount) BlockSize(choose 8 or 16) -cookies auth=(randomcookiefromdummyaccount)
```



