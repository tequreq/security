# Log Analysis



##### Find how many different IP addresses in the log

```
cat squid_access.log | awk '{print $3}' | sort | uniq -c
```



##### Fun with apache logs

https://www.the-art-of-web.com/system/logs/

