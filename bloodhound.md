### BloodHound \(SharpHound\)

Great for quickly enumurating a domain to determine an attack path

```
Set-ExecutionPolicy RemoteSigned
Powershell -Exec Bypass (from cmd)
Import-Module .\SharpHound.ps1
Invoke-BloodHound -CollectionMethod Session -Stealth -Verbose
or
Invoke-BloodHound -CollectionMethod All -CompressData

or

powershell-import /usr/lib/bloodhound/resources/app/Ingestors/SharpHound.ps1
powershell Invoke-BloodHound -CollectionMethod All -CompressData -RemoveCSV
    
        Runs ACL, ObjectProps, Container, and Default collection methods sequentially, compressed the data to a zip file,
        and then removes the CSV files from disk


GUI side
/usr/bin/neo4j console
defaults neoj4 bloodhound

Note:
In cobalt can use powerpick or powershell-import and in meterpreter use "load powershell" and can run items in memory but still needs to save to disk

Note: Default Location
/usr/lib/bloodhound/resources/app/Ingestors/SharpHound.exe
/usr/lib/bloodhound/resources/app/Ingestors/SharpHound.ps1
```

if running into to powershell issues then try running straight from SysWOW if not located there use the "where" command to determine location. "where" is equivalent to "which" on linux.

```
 where explorer

 C:\Windows\explorer.exe
```

References:

[https://posts.specterops.io/sharphound-evolution-of-the-bloodhound-ingestor-3b46643ccbd8](https://posts.specterops.io/sharphound-evolution-of-the-bloodhound-ingestor-3b46643ccbd8)

[https://www.slideshare.net/AndyRobbins3/here-be-dragons-the-unexplored-land-of-active-directory-acls](https://www.slideshare.net/AndyRobbins3/here-be-dragons-the-unexplored-land-of-active-directory-acls)

