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
Command substitution: save the output of a command into a variable.
- `export var1`  
Make the variable var1 available to child processes.
- Formatting: the presence or absence of spaces is important.
- `env` command: to see a listing of the environment variables.

__Special Variables:__

- `$0` - The name of the Bash script.
- `$1` - `$9` - The first 9 arguments to the Bash script.
- `$#` - How many arguments were passed to the Bash script.
- `$@` - All the arguments supplied to the Bash script.
- `$?` - The exit status of the most recently run process (command or function).
- `$$` - The process ID of the current script.
- `$USER` - The username of the user running the script.
- `$HOSTNAME` - The hostname of the machine the script is running on.
- `$SECONDS` - The number of seconds since the script was started.
- `$RANDOM` - Returns a different random number each time is it referred to.
- `$LINENO` - Returns the current line number in the Bash script.

### User Input

- Command line arguments (accessed with `$1`, `$2`, ...)  
- Ask the user for input:  

  `read` command is used to read input from the user interactively during script execution.  
  Two commonly used options are `-p` to specify a prompt and `-s` to make the input silent.  

  ```bash
  # Ask the user for login details:
  read -p 'Username: ' uservar
  read -sp 'Password: ' passvar
	```

- Redirected from __STDIN__:    

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
return the length of the variable var (how many characters)

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

  The function definition must appear in the script before any calls to the function.

  ```bash
  function_name () {
    <commands>
  }
  ```

  or

  ```bash
  function function_name {
    <commands>
  }
  ```

- Passing Arguments:  

  Unlike other programming languages, in Bash the parenthesis () in a function declaration are there only for decoration and are never used to put arguments inside them. Instead the arguments are accessible within the function as $1, $2, etc:

  ```bash
  #!/bin/bash
  # Passing arguments to a function:
  test_function () {
    echo $1 $2
  }
  test_function arg1 arg2
  ```

- Return Values:  

  - Unlike other programming languages, Bash functions do not return a value, but a return status.  
  Use `return <value>` to exit the function with a return status of value:

    ```bash
    #!/bin/bash
    # Setting a return status for a function:
    test_function () {
      return 5
    }
    test_function
    echo The previous function has a return status of $?
    ```

  - Use command substitution to take what would normally be printed to the screen by a function and assign it to the variable:

    ```bash
    #!/bin/bash
    # Setting a return value to a function:
    lines_in_file () {
      wc -l < $1
    }
    num_lines=$( lines_in_file $1 )
    echo The file $1 has $num_lines lines in it.
    ```

- Variable Scope:

  - By default a variable is global.
  - Best practice is to create a local variable within a function:

    ```bash
    local var_name=<var_value>
    ```

- Overriding Commands:  

  `command <command>` is used to run the command with that name as opposed to the function with the same name in order not to end up in an endless loop when called from within a function:

  ```bash
  #!/bin/bash
  # Create a wrapper around the command ls:
  ls () {
    command ls -la
  }
  ls
  ```

### Parameter Expansion

- Good practice: always keep parameter expansions quoted: `"$parameter"`

- Good practice: use parameter expansions to modify strings instead of external applications that require an extra process to be started (sed, awk, cut, perl or others).

- To get the file name:

  ```bash
  "${file##*/}"
  ```

- To get the file directory:

  ```bash
  "${file%/*}"
  ```

- To get the file extension:

  ```bash
  "${file##*.}"
  ```

- To remove the file extension:

  ```bash
  "${file%.*}"
  ```

- To rename all files with a .JPG or a .jpeg extension to have a .jpg extension:

  ```bash
  for file in *.JPG *.jpeg
    do mv -- "$file" "${file%.*}.jpg"
  done
  ```

- To add a common prefix to all elements of an array:

  ```bash
  array=("${array[@]/#/$prefix}")
  printf '%s\n' "${array[@]}"
  ```

- To add a common suffix to all elements of an array:

  ```bash
  array=("${array[@]/%/$suffix}")
  ```

- Difference between `${parameter#pattern}` and `${parameter##pattern}`:  
The doubling of the `#` (match against the __beginning__ character) or the `%` (match against the __end__ character) means patterns will become greedy:

  ```bash
  version=1.5.9
  echo "major.minor.revision: $version"
  echo "major: ${version%%.*}"
  echo "minor.revision: ${version#*.}"
  echo "revision: ${version##*.}"
  ```

- Parameter expansion summary:

Syntax | Description
:-- | :--
${parameter:-word} | __Use Default Value__. If 'parameter' is unset or null, 'word' (which may be an expansion) is substituted. Otherwise, the value of 'parameter' is substituted.
${parameter:=word} | __Assign Default Value__. If 'parameter' is unset or null, 'word' (which may be an expansion) is assigned to 'parameter'. The value of 'parameter' is then substituted.
${parameter:+word} | __Use Alternate Value__. If 'parameter' is null or unset, nothing is substituted, otherwise 'word' (which may be an expansion) is substituted.
${parameter:offset:length} | __Substring Expansion__. Expands to up to 'length' characters of 'parameter' starting at the character specified by 'offset' (0-indexed). If ':length' is omitted, go all the way to the end. If 'offset' is negative (use parentheses!), count backward from the end of 'parameter' instead of forward from the beginning. If 'parameter' is @ or an indexed array name subscripted by @ or *, the result is 'length' positional parameters or members of the array, respectively, starting from 'offset'.
${#parameter} | The __length__ in characters of the value of 'parameter' is substituted. If 'parameter' is an array name subscripted by @ or *, return the number of elements.
${parameter#pattern} | The 'pattern' is matched against the __beginning__ of 'parameter'. The result is the expanded value of 'parameter' with the __shortest__ match __deleted__. If 'parameter' is an array name subscripted by @ or *, this will be done on each element. Same for all following items.
${parameter##pattern} | As above, but the __longest__ match is __deleted__.
${parameter%pattern} | The 'pattern' is matched against the __end__ of 'parameter'. The result is the expanded value of 'parameter' with the __shortest__ match __deleted__.
${parameter%%pattern} | As above, but the __longest__ match is __deleted__.
${parameter/pat/string} | Results in the expanded value of 'parameter' with the __first__ (unanchored) match of 'pat' __replaced__ by 'string'. Assume null string when the '/string' part is absent.
${parameter//pat/string} | As above, but __every__ match of 'pat' is __replaced__.
${parameter/#pat/string} | As above, but matched against the __beginning__. Useful for adding a common prefix with a null pattern: "${array[@]/#/prefix}".
${parameter/%pat/string} | As above, but matched against the __end__. Useful for adding a common suffix with a null pattern.
