# Powershell scripting

## Variables

Variables are declared like this

```powershell
$test = "something"
```

## Execute scripts

So for security reasons the default policy for executing scripts is **Restricted**. Here are the different script-policies.

**Restricted**: PowerShell won't run any scripts. This is PowerShell's default execution policy.

**AllSigned**: PowerShell will only run scripts that are signed with a digital signature. If you run a script signed by a publisher PowerShell hasn't seen before, PowerShell will ask whether you trust the script's publisher.

**RemoteSigned**: PowerShell won't run scripts downloaded from the Internet unless they have a digital signature, but scripts not downloaded from the Internet will run without prompting. If a script has a digital signature, PowerShell will prompt you before it runs a script from a publisher it hasn't seen before.

**Unrestricted**: PowerShell ignores digital signatures but will still prompt you before running a script downloaded from the Internet.

Source: [http://windowsitpro.com/powershell/running-powershell-scripts-easy-1-2-3](http://windowsitpro.com/powershell/running-powershell-scripts-easy-1-2-3)

So if we want to run script `myscript.ps1` we have to set the execution-policy.  
First let's check what execution-policy we currently have:

```powershell
Get-ExecutionPolicy
```

Then we can set the execution policy like this

```powershell
set-ExecutionPolicy unrestricted

or

Set-ExecutionPolicy Bypass
```

## Generate Multiple Lines to print to Screen

Use Here-Strings

You can use here-strings to declare blocks of text. They’re declared just like regular strings except they have an **@** on each end. Instead of being limited to one line, you can declare an entire block or a multiple line string. Here-strings are also useful for making a string composed of the text to execute a command. Examples:

```
$String1 = @" 
Get-ChildItem c:\temp 
"@
```



```
$String2 = @" 
This is some
multiple line 
text! 
"@
```



```
Write-Host @"
I am writing cool
things to the screen
Arent I cool
"@
```

## 

## References

[https://github.com/samratashok/nishang](https://github.com/samratashok/nishang)

[https://www.youtube.com/watch?v=czJrXiLs0wM](https://www.youtube.com/watch?v=czJrXiLs0wM)

