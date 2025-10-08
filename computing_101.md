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



