## Reverse \(WIP\)

Determine type of file

```
file filename
```

High Level Overview of process

```
strings
```

To view plaintext \(potentially passwords and text printing to screen\)

Try simple buffers to input functions:

```
python -c 'print "A"*2000'
```

to view library calls

```
ltrace
```

to view system calls

```
strace
```

Break down and disassemble

```
gdb

set disassembly-flavor intel

disass main
```

review the calls and any cmp and jne functions. May lead to potential passwords which are used in the compare function or jump if not equal.

view functions may be an easy win

```
gdb

info fucntions

call <name of interesting function>
```

## **Radare2**

to start

```
r2 -d filename
```

start code analysis

```
> aaa
```

to print all functions

```
>afl
```

to move location to main function \(seek to location of function main\)

```
>s [name of main function from previous command]
```

to view the dissassembyl of current function

```
>pdf
```

To enter visual mode helpful for stepping thorugh and debugging

```
V
then 
pp
```

to see visual mode like IDA

```
>VV

# you can hit ? to view all options within this mode
```

to see visual mode that also shows registers, stack and dissassembly

```
>V!
```

to enter command mode

```
:     #colon enters the command mode
```

to exit command mode

```
[enter key]   #enter key exits command mode
```

to run the application with parameters in debug

```
>:ood [parameter]  #initiate
>:dc #execute
```

set a breakpoint

```
>:db 0x00460649

then above two commands to rerun
```

to view registers

```
:dr
```

to view hex dump of bytes

```
:pxq    #how hexadecimal quad-words dump (64bit)

:pxw    #show hexadecimal words dump (32bit)
```

to step once

```
s
```

to enter cursoe mode \(to manuall set break points

```
c

use arrows to move around and tab to switch panes

to set breakpoint in cursor mode use

b
```

Remember to view help at anytime in radare it's simply "?". Also when in visual mode, use ":" to enter cmd mode and &lt;enter&gt; to exit cmd mode.

## GDB

to start

```
gdb filename
```

disassemble main function

```
disassemble main
```

start with inspecting functions \(**note: gets and strcpy** are vulnerable to buffer overflows\)

```
> info functions
```

to find the value of the vulnerable buffer in the instance of a gets or strcpy:

```
Look for a something similarly to right before the call

lea eax,[esp+0x1e]

in the preceding case the buffer is 30 bytes (decimal version of the hex value 1e)
```

if looking for a flag and find a flag type function

```
(gdb) break main

(gdb) r

(gdb) call <nameofflagfunction)

#If the program required input and thus the call function you can input with the following syntax
#in this case 1234

(gdb) call <nameofflagfunction)(1234)
```

## Ghidra

```
download ghidra from website (ghidra-sre.org)

./ghirdaRun

create new project
click dragon(code browser)
file->import file-> target app
analyze it->select all->go
To start off looking at main function: functions->main (on the left hand side under symbol tree)
```

Links

[http://bitvijays.github.io/LFC-BinaryExploitation.html](http://bitvijays.github.io/LFC-BinaryExploitation.html)

[https://writeups.easyctf.com/binary-exploitation/doubly-dangerous-110-points.html](https://writeups.easyctf.com/binary-exploitation/doubly-dangerous-110-points.html)

[https://samsclass.info/127/127\_S18.shtml\#lecture](https://samsclass.info/127/127_S18.shtml#lecture)

