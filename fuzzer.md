Quick Fuzzer



```
import socket
s = socket.socket()

s.connect(("172.16.1.249", 80))

n = int( raw_input("Number of A's:"))

req = "GET " + "A" * n
req += " HTTP/1.1\r\n"
req += "Host: 172.16.1.249\r\n\r\n"

s.send(req)
print s.recv(1024)
```



