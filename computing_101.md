# Computing 101 

### Your First Program

```rax``` is a general purpose register 

```mov``` is used to move data 

syscall number of ```exit``` is 60

programs exit with an exit code by passing a parameter to the ```exit``` system call 

- this is done through the ```rdi``` register

To let the assembler know which syntax you are using, prepend a directive to the beginning of the code

- ```.intel_syntax noprefix``` is for the Intel assembly syntax

To assemble code: ```as -o program.o program.s``` assembles program.s into binary code and outputs an object file called program.o 

To link the object file(s) into an executable: ```ld -o program program.o```

To tell ```ld``` where program execution should begin, add ```.global _start``` near the top of the .s file  and then the ```_start:``` label where you want it to start

### Software Introspection

Syscall tracer ```strace``` uses the Linux OS to introspect and record every system call that the program invokes

- Syntax is ```system_call(parameter, parameter, ...)``` 

- The ```execve``` system call starts a new program

- ```alarm``` system call will set a timer in the OS, and terminate the program when that many seconds pass

GDB (GNU Debugger) is used to hunt down and understand bugs 

### Computer Memory

Accessing memory example: ```mov rdi, [31337]```, stores value stored at address 31337 in rdi

Example: if ```rax``` holds a memory address, it is a pointer. To dereference the pointer, we can do ```mov rdi, [rax]```, which will tell the CPU to use the value in ```rax``` as a memory address to dereference, and not just as a value

Offset example: ```mov rax, [rdi+1]```

### Hello Hackers

```write``` syscall is 1

```write``` first parameter is file descriptor in ```rdi```, second is memory address in ```rsi```, third is number of characters to write in ```rdx``` 

```read``` syscall number is 0

```read``` parameters are same as ```write```'s parameters, but will read the specified number of bytes into memory starting from the provided address

### Assembly Crash Course 

```add reg1, reg2``` means reg1 += reg2 ; ```sub reg1, reg2``` means reg1 -= reg2 ; ```imul reg1, reg2``` means reg1 *= reg2

- ```mul``` is unsigned multiply, ```imul``` is signed multiply

```div``` results in an integer, and works by dividing a 128-bit dividend by a 64-bit divisor

- When doing ```div reg```, this happens behind the scenes: ```rax = rdx:rax / reg``` and then ```rdx = remainder``` ; note that rdx:rax means that rdx will be the upper 64-bits and rax will be the lower 64-bits of the 128-bit dividend

- Modulo is done by looking at ```rax``` after, since it holds the remainder

Registers in x86_64 are 64 bits in size, ```eax``` accesses lower 32 bits of ```rax```, ```ax``` accesses lower 16 bits, ```al``` accesses lower 8 bits, ```ah``` is upper 8 bits of the ```ax``` register 

- Example: ```mov al, [address]``` moves least significant byte from address to ```rax```, and ```mov ax``` moves least significant word 

If you do ```x % y```, and 'y' is a power of 2 (2^n), the result will be in the lower 'n' bits of 'x' <-- much more efficient than using ```div``` for modulo

```shl reg1, reg2``` shifts reg1 left by the amount in reg2, ```shr reg1, reg2``` works similarly but to the right

- reg2 can be replaced by a constant, but note that it will be in bits

```and reg1, reg2``` will AND each bit pair one by one, saving the result in ```reg1```, same goes for ```or``` and ```xor```

Declaring operand size example: ```add qword ptr [0x404000], 0x1337```







