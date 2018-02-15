## Evading, Bypassing, and Disabling MS Advanced Threat Protection and Advanced Threat Analytics

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



