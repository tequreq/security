### Assembly \(x86\)

remember Syntax:

`operation <destination>, <source>`

Move value from ESP to EBP **then** subtract 8 from ESP and store the value in ESP

`mov    ebp,esp`

`sub    esp,0x8`

`cmp`compares values

anything staring with a j is a jump \(depending on the result of a comparison\), unless an unconditional jump`jmp`

`lea` instruction is an acronym for Load Effective Address,

Below will load the familiar address of EBP minus 4 into the EAX register.

`lea      eax,[ebp-4]`

Use often before an increment instruction to increment a variable for a loop

use `gcc -g program.c -o whatever`

the -g option gives the debugger the source code. Only useful if you have it obviously.

gdb -q whatever        \#starts gdb on the whatever file and starts in quiet mode, gets rid of intro messages

\(gdb\) break main   \#sets a breakpoint on the main function

\(gdb\) run                \#starts the program which stops at the breakpoint

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

**Note**

gets & strcpy functions are vulnerable

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

### 

### 

### 

### 

### 

### 

### References

[https://killyp.com/2018/02/25/ctf-tamuctf-2018-pwn1/](https://killyp.com/2018/02/25/ctf-tamuctf-2018-pwn1/)

hacking the art of exploitation

