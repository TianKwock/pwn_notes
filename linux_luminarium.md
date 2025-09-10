
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

 

