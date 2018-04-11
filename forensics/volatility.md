

# Volatility Usage {#yui_3_17_2_1_1523459228961_493}



## MEMORY ACQUSITION

WINPMEM/LINPMEM

**1.  Windows**

  a.       C:\&gt; winpmem\_&lt;version&gt;.exe -o F:\mem.aff4

  b.       C:\&gt; winpmem\_&lt;version&gt;.exe F:\mem.aff4 -e PhysicalMemory -o mem.raw

**2.  Linux**

  a.       ./linpmem\_&lt;version&gt;.post4 -o F:\mem.aff4

  b.       ./linpmem\_&lt;version&gt;.post4 F:\mem.aff4 -e PhysicalMemory -o mem.raw

**3. Linux Alt**

  a. sudo dd if=/dev/fmem of=/tmp/memory.raw bs=1MB

## VOLATILITY USAGE

      Example usage: ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt;&lt;command&gt; -f &lt;memory file name&gt;

## LISTING AVAILABLE PROFILES

1.  info - Displays a list of profiles

  a.  ./volatility\_&lt;version&gt;\_lin64\_standalone --info

## ROGUE PROCESS IDENTIFICATION

1.  pslist - High level view of running processes

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; pslist -f &lt;memory file name&gt;

2.  psscan - Scan memory for EPROCESS blocks

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; psscan -f &lt;memory file name&gt;

3.  pstree - Display parent-process relationships

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; pstree -f &lt;memory file name&gt;

## ROOTKIT IDENTIFICATION

1.  psxview - Find hidden processes using cross-view

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; psxview -f &lt;memory file name&gt;

2.  modscan - Scan memory for loaded, unloaded, and

  a.  unlinked drivers

    i.   \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; modscan -f &lt;memory file name&gt;

3.  apihooks - Find API/DLL function hooks

  a.  -p Operate only on specific PIDs

  b.  -Q Only scan critical processes and DLLS

     i.   \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; apihooks -f &lt;memory file name&gt;

4.  ssdt - Hooks in System Service Descriptor Table

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; ssdt \| egrep –v ‘\(ntoskrnl\|win32k\)’ -f &lt;memory file name&gt;

5.  driverirp - Identify I/O Request Packet \(IRP\) hooks

  a.  -r Analyze drivers matching REGEX name pattern

     i.   \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; driverirp –r tcpip -f &lt;memory file name&gt;

6.  idt - Display Interrupt Descriptor Table

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; idt -f &lt;memory file name&gt;

## NETWORK ARTIFACTS

1.  Connections - List of open TCP connections

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; connections -f &lt;memory file name&gt;

2.  connscan - ID TCP connections, including closed

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; connscan -f &lt;memory file name&gt;

3.  sockets - Print listening sockets \(any protocol\)

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; sockets -f &lt;memory file name&gt;

4.  sockscan - ID sockets, including closed/unlinked

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone  --profile=&lt;profile name&gt; sockscan -f &lt;memory file name&gt;

5.  netscan - Scan for connections and sockets

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; netscan -f &lt;memory file name&gt;

## CODE INJECTION IDENTIFICATION

1.  malfind - Find injected code and dump sections

  a.  -p Show information only for specific PIDs

  b.  -o Provide physical offset of single process to scan

  c.  --dump-dir Directory to save memory sections

      i.      \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; malfind -f &lt;memory file name&gt; --dump-dir ./output\_dir

2.  ldrmodules - Detect unlinked DLLs

  a.  -p Show information only for specific PIDs

  b.  -v Verbose: show full paths from three

     i.      \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; ldrmodules –p 4 –v -f &lt;memory file name&gt;

## REGISTRY KEY ANALYSIS

1.  printkey - Output a registry key, subkeys, and values

  a.  -K “Registry key path”

     i.   \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; printkey –K “Software\Microsoft\Windows\CurrentVersion\Run” -f &lt;memory file name&gt;

## HASH DUMP

1.  hivelist - Find and list available registry hives

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; hivelist -f &lt;memory file name&gt;

2.  hashdump - Dump user NTLM and Lanman hashes

  a.  -y Virtual offset of SYSTEM registry hive \(from hivelist\)

  b.  -s Virtual offset of SAM registry hive \(from hivelist\) 

    i.      \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; hashdump -f &lt;memory file name&gt; –y 0x8781c008 –s 0x87f6b9c8

## PROCESSES

1.  procdump - Dump process to executable sample

  a.  -p Dump only specific PIDs

  b.  -o Specify process by physical memory offset

  c.  --dump-dir Directory to save extracted files

     i.   \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; procmemdump -p 4 -f &lt;memory file name&gt; --dump-dir ./output

2.  memdump - Dump every memory section into a file

  a.  -p Dump memory sections from these PIDs

  b.  --dump-dir Directory to save extracted files

    i.   \# ./volatility\_&lt;version&gt;\_lin64\_standalone --profile=&lt;profile name&gt; memdump -p 4 –dump-dir ./output -f &lt;memory file name&gt;

##  FILES

1.  Filescan - Scan memory for FILE\_OBJECT handles

  a.  \# ./volatility\_&lt;version&gt;\_lin64\_standalone filescan -f &lt;memory file name&gt;

2.  Dumpfiles - Extract FILE\_OBJECTs from memory

  a.  -Q Dump using physical offset of FILE\_OBJECT

  b.  -r Extract using a REGEX \(add -i for case insensitive\)

  c.  -n Add original file name to output name

  d.  --dump-dir Directory to save extracted files

3.  Example: \# v./volatility\_&lt;version&gt;\_lin64\_standalone dumpfiles -n -i -r \\.exe -f &lt;memory file name&gt; –dump-dir=./





References

http://www.cydefe.com/podcast/2018/1/30/tools-101-volatility-usage

