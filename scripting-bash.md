## Bash scripting

### Running a script

- `chmod 755 script.sh`  
The shorthand 755 is often used for scripts as it allows you the owner to write or modify the script and for everyone to execute the script.
- `#!/bin/bash`  
The shebang (#!) must be on the very first line of the file, with no spaces before the # or between the ! and the path to the interpreter.

### Variables

- `$1`, `$2`, ...  
The first, second, etc command line arguments to the script.
- `variable=value`  
To set a value for a variable. No spaces on either side of `=`.
- `$variable`    
To read the value of a variable.
- Quotes `"` `'`  
Double quotes will do variable substitution, single quotes will not.
- `variable=$( command )`  
Save the output of a command into a variable.
- `export var1`  
Make the variable var1 available to child processes.
- Formatting: the presence or absence of spaces is important.
- `env` command: to see a listing of the environment variables.

Special Variables:

- `$0` - The name of the Bash script.
- `$1` - `$9` - The first 9 arguments to the Bash script.
- `$#` - How many arguments were passed to the Bash script.
- `$@` - All the arguments supplied to the Bash script.
- `$?` - The exit status of the most recently run process.
- `$$` - The process ID of the current script.
- `$USER` - The username of the user running the script.
- `$HOSTNAME` - The hostname of the machine the script is running on.
- `$SECONDS` - The number of seconds since the script was started.
- `$RANDOM` - Returns a different random number each time is it referred to.
- `$LINENO` - Returns the current line number in the Bash script.

### User Input

- Command line arguments (accessed with `$1`, `$2`, ...)  
- Read input during script execution:  
	`read varName`  
	Read input from the user and store it in the variable `varName`.  
  Two commonly used options are `-p` to specify a prompt and `-s` to make the input silent.  
- Read from STDIN:    
  Bash accommodates piping and redirection by way of special files. Each process gets its own set of files (one for STDIN, STDOUT and STDERR respectively) and they are linked when piping or redirection is invoked.  
  `/dev/stdin` is a file you can read to get the STDIN for the Bash script.  
  Then accept data via piping: `command | ./script.sh` or redirection: `./script.sh < datafile`.
  
  ```
  #!/bin/bash
  cat /dev/stdin
  ```

### Arithmetic

Double parentheses `$(( expression ))` is the preferred method to do arithmetic in Bash scripts.

- `let expression`  
make a variable equal to an expression
- `expr expression`  
print out the result of the expression
- `$(( expression ))`  
return the result of the expression
- `${#var}`  
return the length of the variable var
- `${#variable}`  
length of a variable (how many characters)
