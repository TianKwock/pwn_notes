
# Linux Luminarium

### Globbing

'*' is a wildcard, and '?' is a wildcard but only for one character, and '[]' is a limited form of '?' in which it will match specified characters within the brackets. 

If the first character in the brackets is a '!' or '^' (in newer versions of bash), it is an exclusionary glob.

### Piping

'>' to redirect output, '>>' to append output

``` [command] > output.log 2> errors.log ``` will redirect standard output and error to their respective files

'<' redirects input

'|' will pipe std output from left to std input of right

'>&' redirects a file descriptor to another file descriptor. Therefore, '2>& 1' can be used to redirect std error to std output, so that it can be piped, since '|' only redirects std output.

'grep -v' is inverse grep

'tee' duplicates data flowing through pipes to any number of files 

``` <(command) ``` is process substitution that runs the command and hooks up its output to a temp file. This is called a named pipe. 

- Example: ``` diff <(ls dir1) <(ls dir2) ```

``` >(command) ``` is output process substitution

- Example: ``` /challenge/hack | tee >(/challenge/the) >(/challenge/planet) ```

``` mkfifo ``` is to create a FIFO, which is a persiting pipe.

### Variables 

Prepending a variable name with '$' will let you print out its value using ``` echo ```

VAR=VALUE or VAL="VALUE 123" to set variables. ``` export VAR ``` to export the variable, else other commands won't inherit variables

``` env ``` will print out all exported variables set in shell 

Command substitution format is VAR=$(command)

``` read VAR ``` reads input into a variable

``` read VAR < file ``` will read the file and store the contents in the variable

### Data Manipulation

``` tr ``` will translate the character(s) provided in the first argument to the character(s) provided in the second arguemnt

- Example showing how to swap case of all characters: ``` tr [:upper:][:lower:] [:lower:][:upper:] ```

- ``` tr -d ``` can be used to delete characters 

- ``` tr -d "\n" ``` can be used to delete newlines

- ``` head -n 2 ``` will display first 2 lines of its input

- ``` cut -d " " -f 2 file.txt ``` will extract the second column, using a space as a delimiter, from file.txt

- ``` sort ``` orders lines from input/files alphabetically by default 

### Processes and Jobs 

``` ps ``` lists processes running in terminal 

``` ps aux ``` will list processes for all users, processes that aren't running in terminal, and in a user-readable output

``` kill [pid] ``` will terminate the process 

crtl+c interrupts processes, crtl+z suspends them, and ```fg``` resumes them in the foreground, ```bg``` resumes them in the background 

``` [command] & ``` will start a backgrounded process 

The '?' variable has the exit code of the most recently-terminated command, and can be read by running ``` echo $? ```

### Untangling Users

When you input a password into ```su```, it hashes it and compares it to the value in /etc/shadow 

### Perceiving Permissions

```chown [new owner] [file]``` will change the owner of the file

```chgrp``` will change group. Requires write access to file and membership in new group to do without root 

```chmod [options] mode file``` to change file permissions

- format is who+/-what, for example ug+wx is to add write and execute privs for user and group

- doing ```u=rw```, for example, will simply set these permissions and overwrite the old ones

- you can chain chmod modes with ',', for example ```chmod u=rw,g=r file.txt```

- ```chmod u+s [program]``` will set SUID bit (you must be owner)

### Chaining Commands

Easy way to chain commands is with a ';'

```command1 && command2``` runs command2 only if command1 exits with code 0 (succeeds)

```command1 || command2``` means to run command1, and if it fails, run command2

Scripts are treated as commands, therefore you can redirect its input and output

If a program file starts with '#!' (shebang), Linux treats the file as an interpreted program, and the contents of the rest of the line as the path to the interpreter

Common shebangs: #!/bin/bash, #!/usr/bin/python3, #!/bin/sh 

Scripts can access arguments using special variables '$1', '$2', etc.

### Terminal Multiplexing



 

