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
python -c 'print "A"*2000"
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

## **Radare2**

to start

```
r2 -d filename
```

start code analysis

```
> aaa
```

to print all fucntions

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

to run the application with parameters in debug

```
>ood [parameter]  #initiate
>dc #execute
```

set a breakpoint

```
>db 0x00460649

then above two commands to rerun
```

to view registers

```
dr
```

to step once

```
s
```

Remember to view help at anytime in radare it's simply "?". Also when in visual mode, use ":" to enter cmd mode and &lt;enter&gt; to exit cmd mode.

Links

[http://bitvijays.github.io/LFC-BinaryExploitation.html](http://bitvijays.github.io/LFC-BinaryExploitation.html)

[https://writeups.easyctf.com/binary-exploitation/doubly-dangerous-110-points.html](https://writeups.easyctf.com/binary-exploitation/doubly-dangerous-110-points.html)

[https://samsclass.info/127/127\_S18.shtml\#lecture](https://samsclass.info/127/127_S18.shtml#lecture)

