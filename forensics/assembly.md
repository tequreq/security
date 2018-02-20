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

\(gdb\) nexti        \#steps through the program to the next instruction

\(gdb\) info register eip    \#doing this again shows us the new value after step

\(gdb\) x/i $eip      \#doing this again examines the new value of eip as hexadecimal after step

### 

### 

### 

### 

### 

### 

### 

### 

### References

hacking the art of exploitation

