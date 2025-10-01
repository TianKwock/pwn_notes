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

 
