### Assembly \(x86\)

remember Intel Syntax:

`operation <destination>, <source>`

Move value from ESP \(stack pointer\) to EBP\(base pointer\) **then** subtract 8 from ESP and store the value in ESP

`mov    ebp,esp`

`sub    esp,0x8`

`cmp`compares values

anything staring with a j is a jump \(depending on the result of a comparison\), unless an unconditional jump`jmp`

`lea` instruction is an acronym for Load Effective Address,

Below will load the familiar address of EBP minus 4 into the EAX register. Unlike mov which moves the content to the location lea moves the address to the location

`lea      eax,[ebp-4]`

Use often before an increment instruction to increment a variable for a loop

use `gcc -g program.c -o whatever`

the -g option gives the debugger the source code. Only useful if you have it obviously.

gdb -q whatever        \#starts gdb on the whatever file and starts in quiet mode, gets rid of intro messages

\(gdb\) break main   \#sets a breakpoint on the main function

\(gdb\) run                \#starts the program which stops at the breakpoint

\(gdb\) info variables  \#shows all variables and their address

\(gdb\) x/xb &&lt;variable name&gt;    \#shows value of the address to the named variable

\(gdb\) x/xb &lt;variable address&gt;   \#show the value of the variable

\(gdb\) info register eip    \#provides the eip value

\(gdb\) x/10i $eip      \#examins the value of the next 10 instructions after EIP, useful for seeinng how a program starts

\(gdb\) x/i $eip      \#examines the value of eip as hexadecimal

\(gdb\) x/32x $esp \#examines the next 32 after esp

\(gdb\) x/x $ebp   \#examines the ebp location

\(gdb\) nexti        \#steps through the program to the next instruction

\(gdb\) info register eip    \#doing this again shows us the new value after step

\(gdb\) x/i $eip      \#doing this again examines the new value of eip as hexadecimal after step

\(gdb\) b \*0x0804861A   \#puts a breakpoint at address 0x0804861A

\(gdb\) checksec   \#determines what security is enabled

\(gdb\) disassemble main   \#disassembles the main function

\(gdb\) del    \#removes all previously created breakpoints

**Note**

**gets & strcpy** functions are vulnerable to overflows

check if ASLR is enabled on the host, execute \#ldd /bin/executable \| grep libc   \(if address stays the same then not enabled\)

### Change values within executable

```
if already in gdb and you see a test eax, eax 
we can modify the value to make this true

set a breakpoint at the test instruction

(gdb)b * 0x0804861A
(gdb) continue
(gdb) i r #to verify that eax is not zero
(gdb) set $eax=0
(gdb) i r #to verify that eax is now changed to zero
(gdb) ni  #to continue now
```

### View function calls \(useful when asking for passwords\)

ltrace to view library function calls

or

strace to view system function calls \(stack trace\)

or

radare

### Notes

The values between ebp \(bottom of stack frame\) and esp \(top of stack frame\) is the stack

#### **More Random Notes**

Typically DWORD PTR is setting a variable

For example:

```
mov DWORD PTR [esp+0x5c], 0x0   #this is setting a variable to 0
```

**Function Prologue**

`push ebp`

`mov ebp, esp`

`sub ebp, 0x20`

these sets of instructions are preparing the stack

**Function Epilogue**

leave:

* Combines:
  * `mov esp, ebp`
  * `pop ebp`

ret:

* Same as "`pop eip`"

### Determine the entry point address when unknown

i.e. Don't know the name of the "main" / starting function

```
within gdb

(gdb) shell readelf -h <name of the program>

:this will indicate the entry point address, so you can now setup a break point from that address
```

### References

[https://killyp.com/2018/02/25/ctf-tamuctf-2018-pwn1/](https://killyp.com/2018/02/25/ctf-tamuctf-2018-pwn1/)

[https://www.youtube.com/watch?v=T03idxny9jE](https://www.youtube.com/watch?v=T03idxny9jE)

hacking the art of exploitation

