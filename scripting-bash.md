## Bash scripting

### Running a script

- `#!/bin/bash`  
The shebang (#!) must be on the very first line of the file, with no spaces before the # or between the ! and the path to the interpreter.
- `chmod 755 script.sh`  
The shorthand 755 is often used for scripts as it allows you the owner to write or modify the script and for everyone to execute the script.

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

__Special Variables:__

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

  ```bash
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

### If Statements

```bash
if [ <test> ]
then
  <commands>
elif [ <test> ]
then
  <commands>
else
  <commands>
fi
```

Operator | Description
:---: | :---
! EXPRESSION | The EXPRESSION is false
-n STRING | The length of STRING is greater than zero
-z STRING | The length of STRING is zero (i.e. it is empty)
STRING1 = STRING2 | STRING1 is equal to STRING2
STRING1 != STRING2  | STRING1 is not equal to STRING2
INTEGER1 -eq INTEGER2 | INTEGER1 is numerically equal to INTEGER2
INTEGER1 -gt INTEGER2 | INTEGER1 is numerically greater than INTEGER2
INTEGER1 -lt INTEGER2 | INTEGER1 is numerically less than INTEGER2
-d FILE | FILE exists and is a directory
-e FILE | FILE exists
-r FILE | FILE exists and the read permission is granted
-s FILE | FILE exists and it's size is greater than zero (i.e. it is not empty)
-w FILE | FILE exists and the write permission is granted
-x FILE | FILE exists and the execute permission is granted

- A string based vs numerical comparison:

	```bash
	$ test 001 = 1
	$ echo $?
	1
	```

	```bash
	$ test 001 -eq 1
	$ echo $?
	0
	```

- Single vs. double square brackets:  
  - Single `[ … ]` is POSIX shell compliant, equivalent to `test`.  
  - Double `[[ … ]]` is a Bash extension that supports extra operations, for example: `&&` and `||` instead of `-a` and `-o`, lexicographical comparison with `<`, regex matching with `=~`.


- Case Statements:

	```bash
	case <variable> in
	  <pattern>)
	    <commands>
	    ;;
	  <pattern>)
	    <commands>
	    ;;
	  *)
	    <catch all commands>
	    ;;
	esac
	```

### Loops

- While Loops:

  ```bash
  while [ <test> ]
  do
    <commands>
  done
  ```

- Until Loops:

  ```bash
  until [ <test> ]
  do
    <commands>
  done
  ```

- For Loops:

  ```bash
  for var in <list>
  do
    <commands>
  done
  ```

  - The list is a series of strings, separated by spaces: `'a b c'`.  
  - The range is a series of numbers, with no spaces between the curly brackets: `{1..5}` or `{$startingValue..$endingValue..$valueToStepBy}`.

- `break`: exit the currently running loop.

- `continue`: stop this iteration of the loop and begin the next iteration.

- `select`: display a simple menu system for selecting items from a list.

  ```bash
  select var in <list>
  do
    <commands>
  done
  ```

  Example:

  ```bash
  options='start stop restart quit'
  PS3='Select: '
  select option in $options
  do
          if [ $option == 'quit' ]
          then
                  break
          fi
          echo $option
  done
  ```

### Functions

- Creating a function:

  ```bash
  function function_name {
    <commands>
  }
  ```

  or

	```bash
	function_name () {
		<commands>
	}
	```

