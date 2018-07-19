# PowerShell

PowerShell is Windows new shell. It comes by default from Windows 7. But can be downloaded and installed in earlier versions.

* PowerShell provides access to almost everything an attacker might want.
* It is based on the .NET framework.
* It is basically bash for windows

## Basics

So a command in PowerShell is called **cmdlet**. To get help on how to use a **cmdlet** while in PowerShell, the man-page, you do:

```
Get-Help    <cmdlet    name    |    topic    name>
```

Example

```
get-help echo
get-help get-command
```

### Format Output

```
 get-process | Format-Table ProcessName
```

### Grep Equivalent

Select-String

```
cat .\filelist.txt | Select-String Music
```

Find Juicy Stiff in the File System \(From SANS\)

```
ls -r C:\PATH\TO\DIRECTORY -file | % {Select String -path $_ -patten STRING}
```

Searches C:\PATH\TO\DIRECTORY for files that contain the "STRING", displaying the file name and the line containing the STRING.

