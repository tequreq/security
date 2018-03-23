## Reverse \(WIP\)

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

set disassembly-flavor intrl

disass main
```

review the calls and any cmp and jne functions. May lead to potential passwords which are used in the compare function or jump if not equal.





Links

[http://bitvijays.github.io/LFC-BinaryExploitation.html](http://bitvijays.github.io/LFC-BinaryExploitation.html)

[https://writeups.easyctf.com/binary-exploitation/doubly-dangerous-110-points.html](https://writeups.easyctf.com/binary-exploitation/doubly-dangerous-110-points.html)

[https://samsclass.info/127/127\_S18.shtml\#lecture](https://samsclass.info/127/127_S18.shtml#lecture)

