# BASIC SCRIPTING

A shell script is a file containing a series of commands that are executed in sequence by the shell interpreter. It is a file of executable commands that has been stored in a text file. When the file is run, each command is executed. Shell scripts are written in scripting languages supported by the shell, such as Bash, sh, or zsh.

Bash shell scripting involves writing scripts in the Bash (Bourne Again Shell) language, which is a command-line interpreter widely used on Unix-like operating systems.


#### SHELL SCRIPTING BASICS

- File Format: The `.sh` file extension commonly signifies a shell script, serving as a human-readable hint rather than influencing system behavior. Linux disregards file extensions.
- Execution: After creating a shell script, you need to make it executable using the `chmod` command:
  -  `chmod +x script.sh`: This command grants the user execute permission for the script named script.sh. Without execute permission, the script cannot be run as an executable file.
  -  `./script.sh`: This command executes the script named script.sh. The `./` prefix indicates that the script is located in the current directory. If the script is located in a different directory, you would need to specify the path to the script instead of just ./.


## BASH SHELL SCRIPTING

A shell is a programme that takes commands from the user through the keyboard and gives them to the OS kernel to get executed. 
The shell gets started when the user logs in to the terminal. 

These are fundamental commands used in shell environments to retrieve information about the shell environment and user configurations:

`echo $0`: This command reveals the shell that was launched upon login.
`cat /etc/shells`: Displays a catalog of all installed shells.
`cat /etc/passwd`: Reveals user account information, including default shells, like `pr2:x:1004:1006:Back-End:/home/pr2:/bin/bash`.

A shell script, an executable text file, encompasses shell commands along with structures like variables and functions, executed sequentially. It serves as a potent tool for automating repetitive tasks, and enhancing productivity. Whenever you find yourself running a task over and over, you should use shell scripting. 

Practical examples of shell script applications include system monitoring, data backup and restoration, and the establishment of email-based alert systems for event notifications. Additionally, shell scripts are invaluable for user administration and security auditing.

For organizational efficiency and user convenience, establishing a "bin" directory within the home directory provides a structured approach to managing custom scripts. This directory offers users a dedicated space for executable files, streamlining their utilization within the Unix shell environment.


#### THE BASH SHEBANG AND COMMENTS

- Shebang line: A shebang is a special line of text at the beginning of a script or executable file in Unix-like operating systems. It is also known as a hashbang, pound-bang, or hash-pling. The shebang is used to indicate the interpreter that should be used to execute the script.
  - `which -a bash`: Used to identify the location of an executable file.
  - `#!/path/to/interpreter` (e.g., `#!/bin/bash`): The shebang line is used to specify the path to the interpreter that should be used to execute the script.
-  Comments: Start lines with #. They provide context, explanations, or disable code. Inline comments are also supported.


#### RUNNING BASH SCRIPT

Below are the ways to run the bash scripts.

1. Absolute File Path: Run the script using its absolute file path, for example:
  - `/home/ikechukwu/scripts/first_script.sh`
2. Relative Path: Navigate to the directory where the script is located and run it using its relative path.
  - `./first_script.sh`: Make sure you are in the directory where the script is located.
3. Using Bash or Python Interpreter: Execute the script by invoking the Bash or Python interpreter, for example:
  - `bash first_script.sh` or `python3 first_script`: Make sure you are in the directory where the script is located. In this pattern, the user does not need the execute permission to run the script and it. This way will also overwrite the shebang directive. 
4. Using source or . Command: Execute the script using the source command or its shorthand, for example;
  - `source first_script.sh` or `. first_script`: It does not require execution permission and the source command reads and executes the command from the file specified as its argument in the current shell environment.

These methods provide flexibility in running Bash scripts, catering to various use cases and requirements.


## SHELL CUSTOMIZATION

Shell customization refers to the process of tailoring the shell environment to suit individual preferences and optimize workflow efficiency. It involves configuring various aspects of the shell, such as aliases, variables, etc to enhance usability and productivity.

They allow users to personalize their shell environment by creating shortcuts (aliases) for frequently used commands and storing data or values (variables) for easy reference and manipulation within scripts.

### BASH ALIASES

Bash aliases are a feature that allows a user to create a shortcut or alternative name for a command. It provides a convenient way to create shortcuts or alternative names for frequently used commands. Below are essential commands for customizing your shell environment:

- To create an alias, use the `alias` command followed by the alias name and the command it represents. For example:
  - `alias c="clear"`: This alias makes c a shortcut for the clear command.
  - `alias server1=“ssh -p 22 ikechukwu@192.168.64.2”`: This alias, named server1, is used to create a shortcut for connecting to a remote server via SSH (Secure Shell) using a specific port and user.

- To make it permanent, inscribe the command in the bash shell. 
  - To make aliases permanent, add them to your shell's configuration file, such as `~/.bashrc` or `~/.bash_profile`. Open the file in a text editor and add your aliases there. After saving the file, either restart your terminal or run source `~/.bashrc` to apply the changes.
  
- To remove an alias, use the `unalias` command followed by the name of the alias. For example:
  - `unalias c`: This command removes the c alias.

- If you want to bypass an alias and run the original command, precede the command with a backslash \. For example:
  - `\ls`: 

These utilities empower you to tailor your shell experience, streamlining common tasks and optimizing your workflow.


### VARIABLES IN BASH

In Bash scripting, variables serve as containers to store data or values, enabling easy reference and manipulation within scripts. Variables are assigned using the format `variable=value`. For example: `os=Linux` 

It is important to note that there are no spaces allowed in variables, but strings containing spaces should be enclosed in double quotes, for example: `variable=“strings and blings”`

**Variable Naming Rules**: Variable naming rules in Bash are as follows;

- Start with an Alphabet or Underscore: Variable names must begin with either an alphabet (uppercase or lowercase) or an underscore (_). They cannot start with a number.
- Can Contain Alphanumeric Characters and Underscore: After the initial character, variable names can contain alphanumeric characters (letters and numbers) as well as underscores (_). Special characters are not allowed in variable names.
- Case-Sensitive: Variable names are case-sensitive, meaning uppercase and lowercase letters are distinct. For example, var and VAR would be treated as different variables.
- Cannot be Reserved Keywords: Variable names cannot be the same as reserved keywords or commands in Bash. For example, you cannot use if, while, for, etc., as variable names.
- Avoid Using Bash Special Variables: It's recommended to avoid using names that coincide with Bash's special variables (e.g., PATH, HOME, PWD, etc.) to prevent unintentional conflicts.


Below is a typical example of how to use Variables; 

`ikechukwu@ubuntu-22-04-3:~/scripts$ age=30`</br>
`ikechukwu@ubuntu-22-04-3:~/scripts$ echo $age`</br>
`30`</br>
`ikechukwu@ubuntu-22-04-3:~/scripts$ os=Linux`</br>
`ikechukwu@ubuntu-22-04-3:~/scripts$ echo $os`</br>
`Linux`</br>
`ikechukwu@ubuntu-22-04-3:~/scripts$ echo "I am learning $os and I am $age years old"` </br>
`I am learning Linux and I am 30 years old`

In the above, I successfully assigned a value of 30 to the variable age and then echoed its value. This is a simple demonstration of how to use variables in a Bash shell. The last command echoes the concatenated string with the variable values.</br></br>

**Read-only Variables** </br>
To prevent changes to a variable's content, use the declare builtin command with the `-r` option. For instance:

`declare -r logdir="/var/"`: This makes the variable `logdir` read-only and immutable.</br></br>

**Viewing Variables**:</br>
To display all defined variables, use the `set` command. For better readability, pipe the output to less:

`set | less`


#### ENVIRONMENT VARIABLES

Environment variables play a crucial role in configuring and customizing the behavior of the shell and various processes running within it. They are essential elements of the environment in which a process operates, providing dynamic values and information to programs and scripts.

Each time we launch a terminal window a collection of predefined variables are set with some dynamic values and are used to customise the way the system works. 

- Environment Variables: Environment variables are variables that are defined for the current shell environment and inherited by any child shells or processes. They are typically written in uppercase letters by convention and are used to pass information to processes spawned from the current shell. For example, `echo $PATH` displays the value of the PATH environment variable, which contains a colon-separated list of directories where executable files are located.

- Shell Variables: Shell variables, on the other hand, are contained within the shell in which they are defined or set. They are specific to the shell session and are not inherited by child processes.

To manage environment variables and shell variables, various commands and techniques are available:

- `env`: Displays all the environment variables currently set in the shell.
- `printenv`: Displays the values of specific environment variables. For example, `printenv USER` shows the value of the USER environment variable.
- `set`: Shows all variables, including both environment variables and shell variables.
- `set -o posix`: Cleans up the output of set by operating in POSIX mode, which excludes shell functions from the output.


**Customizing the Shell Environment**

The .bashrc file is a vital component of shell customization in Unix-like operating systems, particularly for the Bash shell. It is read and executed by interactive, non-login Bash shells and allows users to configure their shell environment according to their preferences. See the steps below; 

- `vi ~/.bashrc`: This command opens the .bashrc file in the Vi text editor for editing. The .bashrc file contains shell commands and configurations that are executed whenever a new terminal session is initiated. It is primarily used for setting environment variables, defining aliases, and other customizations specific to the user's environment.
- `export PATH=$PATH:~/scripts`: This line adds the ~/scripts directory to the PATH environment variable. Breaking down the command:
  - `export`: This keyword is used to make the variable (PATH in this case) available to subprocesses of the shell.
  - `PATH=$PATH:~/scripts`: This command appends the ~/scripts directory to the existing PATH variable. The PATH variable specifies a colon-separated list of directories in which the shell looks for executable files. By adding ~/scripts to PATH, any executable files located in the ~/scripts directory can be executed directly from the command line without specifying the full path.
- `source ~/.bashrc` or `. ~/.bashrc`: This command reloads the .bashrc file, applying any changes made to it without needing to restart the shell. It ensures that the modifications made to the shell environment, such as adding directories to the PATH, take effect immediately.

To create a new environment variable in a Unix/Linux shell, the `export` command is used followed by the variable name and its value, as shown below:

`export VARIABLE_NAME=value`

To make environment variables available systemwide, they can be declared in system-level configuration files such as /etc/profile or /etc/bash.bashrc. Alternatively, the /etc/environment file can be used to specify systemwide environment variables.


### GETTING USER INPUT

The `read` command in Unix/Linux is used to read a line from the standard input (usually from the keyboard) and assign the words to one or more variables. It halts the program execution until the user provides input and presses the enter key.

`ikechukwu@ubuntu-22-04-3:~$ read name` </br>
`ikechukwu` ---input </br>
`ikechukwu@ubuntu-22-04-3:~$ echo $name`</br>
`ikechukwu`

In the above example, the read command prompts the user to enter their name, and the input is stored in the variable $name. The subsequent `echo` command then displays the value of $name.

The examples below demonstrate how to incorporate user input into Bash scripts and perform actions based on that input, making scripts more interactive and flexible:

1. **Script that drops all packets**</br></br>
Let us create a script that drops all packets from a specific IP address. Below are the steps;</br></br>
- `vi block_ip.sh`: creates a new bash script file. 
- `#!/bin/bash`: Shebang line: Specifies the path to the Bash interpreter
- `read -p "Enter IP address to block: " IP`: The `-p` "Prompt message:": This option allows you to specify a prompt message that will be displayed to the user before they enter input. This command prompts the user to enter an IP address and assigns it to the variable 'ip'. 
- `iptables -I INPUT -s "$IP" -j DROP`: Uses `iptables` to insert a rule into the INPUT chain, blocking traffic from the specified IP address
- `echo "This packet from $ip will be dropped"`: Displays a message indicating that packets from the specified IP address will be dropped.</br></br>
In this script named block_ip.sh, the user is prompted to enter an IP address to block. The entered IP address is stored in the variable `$ip`. Then, `iptables` is used to insert a rule into the INPUT chain, blocking traffic from the specified IP address. Finally, a message is displayed indicating that packets from the specified IP address will be dropped.


2. **Script to Fix Permissions Recursively**</br></br>
**For Files:** </br></br>
`#!/bin/bash`</br>
`read -p "Enter directory: " dir`: Prompt the user to enter a directory</br>
`echo -n "Changing files permissions to 644 recursively..."`</br>
`find $dir -type f -exec chmod 644 {} \;`: Uses `find` command to recursively search for files (-type f) within the specified directory and changes their permissions accordingly using `chmod`.</br>
`echo "Done"`</br></br>
**For Directories:**</br></br>
`echo -n "Changing subdirectories permissions to 755 recursively..."`</br>
`find $dir -type d -exec chmod 755 {} \;`: Uses `find` command to recursively search for files (-type d) within the specified directory and changes their permissions accordingly using `chmod`.</br>
`echo "Done"`</br></br>
In this script named fix_permissions.sh, the user is prompted to enter a directory. Then, the script uses `find` command to recursively search and change the permissions of files to 644 (-type f) and subdirectories to 755 (-type d) within the specified directory using `chmod`. Finally, messages are displayed to indicate the completion of the operations.


### SPECIAL VARIABLES AND POSITIONAL ARGUMENTS

In shell scripting, positional arguments refer to the arguments passed to a script or a function when it is executed. These arguments are provided on the command line and are referenced by position or order within the script. The first positional argument is represented by $1, the second by $2, and so on. For example:

`script.sh filename1 dir1 10.0.0.1`

- $0 is the name of the script itself (script.sh).
- $1 is the first positional argument (filename1).
- $2 is the second positional argument (dir1).
- $3 is the last argument of the script (10.0.0.1).
- ${10} would be the tenth argument.
- $# is the number of positional arguments.
- "$*" is a string representation of all positional arguments: $1, $2, $3, and so on.
- $? holds the exit status of the last executed command or function.

**Example Script to Handle Positional Arguments**

`ikechukwu@ubuntu-22-04-3:~/scripts$ vi pos_arguments.sh`</br>
`#!/bin/bash`</br>
`echo "First argument: $1"`</br>
`echo "Second argument: $2"`</br>
`echo "third argument: $3"`</br>
`echo "Fourth argument: $4"`</br>
`echo "Total number of arguments: $#"`</br>
`echo "All arguments: $*"`

`ikechukwu@ubuntu-22-04-3:~/scripts$ ./pos_arguments.sh Linux is really good `</br>
First argument: `$1`=Linux</br>
Second argument: `$2` = is</br>
third argument: `$3` = really</br>
Fourth argument: `$4` = good</br>
Total number of arguments: `$5` </br>
All arguments: `$*` Linux is really good though.


The script below, when executed with `./display_and_compress.sh scripts.txt`, will display the content of the file scripts.txt and then compress it into a .tar.gz archive with the same name.

- `ikechukwu@ubuntu-22-04-3:~$ cd scripts/`
- `ikechukwu@ubuntu-22-04-3:~/scripts$ vi display_and_compress.sh`

  - `#!/bin/bash`: shebang line which specifies the path to the Bash interpreter.
  - `echo "Displaying the content of $1"`: Displays a message indicating that the content of the file specified as the first argument ($1) will be displayed
  - `sleep 2`: Pauses the script execution for 2 seconds.
  - `cat $1`:  Displays the content of the file specified as the first argument ($1).
  - `echo`: Prints a new line for better formatting.
  - `echo "Compressing $1"`: Displays a message indicating that the specified file will be compressed.
  - `sleep 2`: Pauses the script execution for another 2 seconds.
  - `tar -czvf "$1.tar.gz" $1`: Creates a compressed .tar.gz archive of the specified file. The archive will be named after the original file with a .tar.gz extension.
- `ikechukwu@ubuntu-22-04-3:~/scripts$ chmod 755 display_and_compress.sh`
- `ikechukwu@ubuntu-22-04-3:~/scripts$ ./display_and_compress.sh scripts.txt`


## PROGRAM CONTROL FLOW

Program control flow constructs can be categorized into two main types:

- Conditional Constructs: These constructs enable the execution of different blocks of code based on whether specific conditions are true or false. In Bash scripting, conditional constructs include the if statement and the case statement.

- Iterative Constructs (Loops): These constructs allow the repetition of a block of code multiple times until a certain condition is met or until all iterations have been completed. In Bash scripting, iterative constructs include for loops and while loops.

Both conditions and loops play crucial roles in controlling the flow of execution in scripts and programs, allowing for more dynamic and responsive behavior based on various factors and inputs.

## IF, ELIF AND ELSE STATEMENTS

They are used for decision-making. This is program flow control in general and allows us to have logic in our scripts and execute a section of code only when some criteria are met. 

`if [ condition ]; </br>
then</br>
    # Code to execute if the condition is true</br>
elif [ another_condition ]; </br>
then</br>
    # Code to execute if the previous condition is false, and this condition is true</br>
else</br>
    # Code to execute if none of the previous conditions are true</br>
fi</br>

NOTES: 

- The conditions are enclosed in square brackets ( [ and ] ), and spaces are important around the square brackets.
- The `elif` statement allows you to test an additional condition if the previous if statement's condition is false.
- You can have multiple `elif` statements to test multiple conditions sequentially.
- The `elif` and `else` statements are optional.

The `test` command in Linux is used to evaluate conditional expressions. It is commonly used in various shell scripts and commands. The test command can also be used with square brackets `[ ]` as a synonym for the test command. (`man test` provides detailed information about the various options and usage of the `test` command. Additionally, since `[ ]` is a synonym for test, you can also check the manual page for [ ] - `man [ ]` )

The test command gives you easy access to comparison and file test operators. For example:

| Command |	Description |
|-----|-----|
| test –f /dev/ttyS0	| 0 if the file exists| 
| test ! –f /dev/ttyS0	| 0 if the file doesn’t exist| 
| test –d /tmp	| 0 if the directory exists| 
| test –x `which ls`	| substitute the location of ls then test if the user can execute| 
| test 1 –eq 1	0 | if numeric comparison succeeds| 
| test ! 1 –eq 1 | NOT – 0 if the comparison fails| 
| test 1 –ne 1	| Easier, test for numeric inequality| 
| test “a” = “a”	| 0 if the string comparison succeeds| 
| test “a” != “a”	| 0 if the strings are different| 
| test 1 –eq 1 –o 2 –eq 2	| -o is OR: | either can be the same| 
| test 1 –eq 1 –a 2 –eq 2	| -a is AND: both must be the same| 

**USE CASES**

The script below will show the content of a file (`cat $1`) as in if and the content of a directory as in the elif (`ls -l $1`), the else statement gives the response for any other argument that’s not in the script. 

`#!/bin/bash`</br>
`if [ -f $1 ];`</br>
\# if statement</br>
`then`</br>
`        echo "Displaying the content of $1.."`</br>
`        sleep 2`</br>
`        cat $1`</br>
\# main command</br>
`elif [ -d $1 ];` </br>
\# elif statement</br>
`then`</br>
`        echo "Listing content of the directory ($1)"`</br>
`        sleep 2`</br>
`        ls -l $1`</br>
\# main command</br>
`else` </br>
\# else statement </br>
`        echo "Get serious, this is neither a file nor a directory in the current directory"`</br>
`fi`

DO NOT FORGET TO ENABLE PERMISSION AFTER CREATING A BASH SCRIPT - `chmod 700 filename` or `chmod +x filename`


In Bash scripting, [ ] (single square brackets) and [[ ]] (double square brackets) are both used for conditional expressions, but they have some notable differences in functionality and use cases:

- Syntax and Punctuation:
  - [ ]: Requires spaces around the operators and operands inside the brackets.
  - [[ ]]: Does not require spaces around the operators and operands inside the double brackets.
- Logical Operators:
  - [ ]: Uses -a for logical AND and -o for logical OR.
  - [[ ]]: Uses && for logical AND and || for logical OR, which are more intuitive.
- String Comparisons:
  - [ ]: String comparisons use = for equality.
  - [[ ]]: Allows = for equality and == for pattern matching.
- Quoting:
  - [ ]: Requires variable references to be quoted to handle cases with spaces.
  - [[ ]]: Variable references inside double brackets don't require quotes in most cases.
 

### TESTING CONDITIONS FOR NUMBERS

When dealing with integer operands in conditional statements (if and elif), several comparison operators can be used to determine the relationship between values:

-eq: equals (=)
-ge: greater than or equal to (>=)
-gt: greater than (>)
-le: less than or equal to (<=)
-lt: less than (<)
-ne: not equal to (!=)

Below is an example Bash script named age.sh that prompts the user to input their age and then categorizes it based on the specified conditions:

`ikechukwu@ubuntu-22-04-3:~/scripts$ vim age.sh` </br>

`#!/bin/bash`</br>
\# Prompt the user to enter their age</br>
`read -p "Enter your age: " age`</br>
\# Check if the age is less than 18</br>
`if [[ $age -lt 18 ]];` </br>
`then`</br>
`    sleep 2`</br>
`    echo "You are a minor"`</br>
\# Check if the age is exactly 18</br>
`elif [[ $age -eq 18 ]];` </br>
`then`</br>
`    sleep 2`</br>
`    echo "You just became a minor"`</br>
\# Execute if none of the previous conditions are true</br>
`else`</br>
`    sleep 2`</br>
`    echo "You are an adult"`</br>
`fi`</br>

`ikechukwu@ubuntu-22-04-3:~/scripts$ chmod +x age.sh`</br>
`ikechukwu@ubuntu-22-04-3:~/scripts$ ./age.sh`

This script efficiently categorizes the user's age into different groups based on the provided conditions, providing a clear and concise output message.


### MULTIPLE CONDITIONS AND NESTED IF STATEMENTS

In Bash scripting, you can handle multiple conditions using logical operators and nested if statements which have been mentioned above. Logical operators such as && (AND) and || (OR) help combine conditions. For example;

This is a simple Bash script that takes user input for age and then categorizes the input into different age groups.

`#!/bin/bash`</br>
\# Prompt the user to enter their age</br>
`read -p "Enter your age: " age`</br>
\# Check if the age is between 0 and 18 (exclusive)</br>
`if [[ $age -lt 18 && $age -ge 0 ]];`</br>
`then`</br>
`    sleep 2`</br>
`    echo "You are a minor"`</br>
\# Check if the age is exactly 18</br>
`elif [[ $age -eq 18 ]];` </br>
`then`</br>
`    sleep 2`</br>
`    echo "You just became an adult"`</br>
\# Check if the age is between 18 and 100 (inclusive)</br>
`elif [[ $age -gt 18 && $age -le 100 ]];` </br>
`then`</br>
`    echo "You are a major"`</br>
\# Execute if none of the previous conditions are true</br>
`else`</br>
`    sleep 2`</br>
`    echo "Invalid input"`</br>
`fi`</br></br>

Using an if statement inside another if statement. For example, this script is designed to check whether an argument passed to it is a file, a directory, or neither. </br></br>


`#!/bin/bash`</br>
\# Check if the script is called with exactly one argument</br>
`if [[ $# -eq 1 ]]; `</br>
`then`</br>
    \# Check if the argument is a file</br>
`    if [ -f $1 ]; then`</br>
`        echo "The argument is a file, displaying its contents..."`</br>
`        sleep 2`</br>
        # Check if the file is not empty</br>
`        if [[ -s $1 ]]; then`</br>
`            cat $1`</br>
`        else`</br>
`            echo "The file is empty"`</br>
`        fi`</br>
    # Check if the argument is a directory </br>
`    elif [ -d $1 ]; then`</br>
`        echo "The argument is a directory, displaying its contents..."`</br>
`        sleep 2`</br>
`        ls -l $1`</br>
    # Execute if the argument is neither a file nor a directory</br>
`    else`</br>
`        echo "Be serious, the file ($1) is neither an existing file nor directory"`</br>
`    fi`</br>
\# Execute if the script is not called with exactly one argument</br>
`else`</br>
`    echo "This script should be run with exactly one argument"`</br>
`fi`

This script is useful for performing different actions based on whether the argument passed to it is a file, a directory, or something else. It provides informative messages to the user depending on the type of argument passed.


### COMMAND SUBSTITUTION 

Command Substitution simply means running a shell command and storing its output in a variable for later use. There are two syntaxes for command substitution:

Using backticks: result=\`command` </br>
Using $() syntax: result=$(command) </br>

`now=$(date)` </br>
`echo $now` </br>

Examples: 

`output=$(ps -ef | grep ls)`: creating a variable. </br>
`echo $output`: view the content of the variable </br>
`set | less`: To view all the creates variables and their value

**USE CASES**

**USING COMMAND SUBSTITUTION IN CREATING COMPRESSED ARCHIVES**

You can embed the current date and time in the filename of a compressed archive using command substitution with the `date` command.

`sudo tar -czvf etc-$(date +%F_%H%M).tar.gz /etc/`: This command will give the file - etc-2023-12-14_0824.tar.gz which has the date and time of the new backup file. In this case, it won’t overwrite the previous file. 
  - `date +%F_%H%M`: Changes the display format of the date command output. 
  - `sudo tar -czvf "etc.tar.gz" /etc/`: To compress the etc directory into a compressed file - etc.tar.gz, but when the command is being run again, it overwrites the previously compressed file.

For arithmetic operations, you use double parentheses ((...)) syntax. This allows you to perform arithmetic calculations and assign the result to a variable. For example:

`ikechukwu@ubuntu-22-04-3:~$ c=$((a+b))` </br>
`ikechukwu@ubuntu-22-04-3: ~$` </br>
`echo $c` </br>
`11` </br>
`ikechukwu@ubuntu-22-04-3:~$` </br>
`ikechukwu@ubuntu-22-04-3:~$ let d=$a+$b` </br>
`ikechukwu@ubuntu-22-04-3:~$ echo $d` </br>
`11`

The `let` command is often used for arithmetic operations in Bash scripts.

**USE OF DOUBLE BRACKET FOR ARITHMETIC IN COMMAND SUBSTITUTION**

This script below allows the user to specify a file and two positive integers n and m. It then displays a portion of the content of the file, starting from line n and ending at line m, inclusively.

`#!/bin/bash` </br>
`read -p "Enter the filename: " filename`</br>
`if [[ -f $filename ]];`</br>
`then`</br>
`    read -p "Enter a positive integer n: " n`</br>
`    read -p "Enter a positive integer m: " m`</br>
`    q=$((m - n + 1))` # Calculates the number of lines to display</br>
`    tail -n "+$n" $filename | head -n $q`</br>
`else`</br>
`    echo "$filename is not a file."`</br>
`fi`

In Bash, the expression `q=$((m+n+1))` is used to perform arithmetic operations and assign the result to the variable q. Below is an explanation of this script:
* $((...)): This is the arithmetic expansion syntax in Bash. Anything inside the double parentheses is treated as an arithmetic expression.
* m+n+1: This is the arithmetic expression in your case. It adds the values of variables m and n and then adds 1 to the result.
* q=: This is the assignment operator, assigning the result of the arithmetic expression to the variable q.


### COMPARING STRINGS IN 'IF STATEMENTS'.

N/B: Two strings are equal if they have the same length and contain the same sequence. 

`#!/bin/bash` </br>
`read -p "String1: " str1`</br>
`read -p "String2: " str2`</br>
`if [[ "$str1" == "$str2" ]];`</br>
`then`</br>
`        echo "They are equal"`</br>
`elif [[ "$str1" != "$str2" ]];`</br>
`then`</br>
`        echo "They are not equal"`</br>
`else`</br>
`        echo "What are you inputting, this man?"`</br>
`fi`

**Important Notes**:

- Do not forget to quote string variables in testing conditions to avoid word splitting or global issues.
- A blank space must be used between the operator and the operand.
- '=' is the operator; 'str1' and 'str2' are the operands.


### TO CHECK FOR SUBSTRINGS

`#!/bin/bash`</br>
`str1="Nowadays, Linux powers the servers of the internet"`</br>
`if [[ "$str1" == *"Linux"* ]]`</br>
`then`</br>
`        echo "The substring Linux is there"`</br>
`else`</br>
`        echo "The substring Linux is not there"`</br>
`fi`

The above script is a good example of how to check if a substring exists within a larger string in a Bash script. The [[ "$str1" == \*"Linux"* ]] condition uses the == operator for string comparison, and the * wildcard before and after "Linux" checks if "Linux" is a substring of the variable str1. If the substring is found, it prints a message indicating its presence; otherwise, it prints a message stating its absence.


### CHECKING STRING LENGTH IN BASH SCRIPTING

The script below will attempt to check whether a string is zero length or not using the `-z` (zero length) and `-n` (non-zero length) tests in a Bash script.

`#!/bin/bash`</br>
`mystr="abcd"`  # Assigns the string "abcd" to the variable mystr</br>
`if [[ -z "$mystr" ]];` # Checks if the length of the string in mystr is zero</br>
`then`</br>
`    echo "String is zero length"`  # Prints a message indicating that the string is zero length if the condition is true</br>
`else`</br>
`    echo "String is NOT zero length"`  # Prints a message indicating that the string is not zero length if the condition is false</br>
`fi`</br>
</br>
`if [[ -n "mystr" ]];` # Checks if the length of the string "mystr" is non-zero (incorrectly references a string literal instead of the variable)</br>
`then`  </br>
`    echo "String is NOT zero length"`  # Prints a message indicating that the string is not zero length if the condition is true</br>
`else`</br>
`    echo "String is zero length"`  # Prints a message indicating that the string is zero length if the condition is false</br>
`fi`


## FOR LOOPS

For statement is used to execute a block of codes repeatedly. The for loop in Bash is used to iterate over a sequence of values, such as a range of numbers, a list of items, or the contents of an array. 

**SYNTAX:**

`for item in LIST`</br>
`do`</br>
`COMMANDS`</br>
`done`</br>

`Item` becomes the variable. 

**EXAMPLES:**

1. `#!/bin/bash`</br>
\# Loop 1: iterating over a list of strings</br>
`for os in Ubuntu CentOS "Mx Linux" Kali`</br>
`do`</br>
`    echo "os is $os"`</br>
`done`

2. `#!/bin/bash`</br>
\# Loop 2: Iterate over a range of numbers</br>
`for num in {10..15}`</br>
`do`</br>
`    echo "num is $num"`</br>
`done`


3. `#!/bin/bash`</br>
\# Loop 3: iterating over a list of files</br>
`for item in ./* `       # files in the current dir</br>
`do`</br>
`    if [[ -f $item ]];` # using the if statement to confirm if the variable is a file. </br>
`    then`</br>
`        echo "Displaying the contents of $item"`</br>
`        sleep 1`</br>
`        cat $item`</br>
`        echo "#######################"`</br>
`    fi`</br>
`done`


4. `#!/bin/bash`</br>
\# Loop 4:  iterating over a list of numbers in increments</br>
`for x in {10..100..5} `</br>
`do`</br>
`        echo $x`</br>
`done`

These scripts demonstrate various uses of the for loop in Bash, including iterating over lists of strings, numbers, and files, as well as iterating with specified increments. 

**USE CASES**

**Dropping a List of IP addresses Using a For Loop**

`#!/bin/bash`</br>
`DROPPED_IPs="192.168.1.1 192.168.1.2 192.168.1.4”`    #The values for the variables are separated with spaces </br>
`for ip in $DROPPED_IPs`  #Second variable</br>
`do`</br>
`        echo "Dropped packets from $ip"`</br>
`        iptables -I INPUT -s $ip -j DROP`</br>
`done`
~           

OR 

You can create a file containing the list of IPs to be dropped line by line. 

`vim IPs`</br>
Input the IP addresses line by line;</br>
192.168.1.1</br>
192.168.1.2

In the script file, run;

`#!/bin/bash`</br>
`for ip in $(cat ip.txt)`  #This is a command substitution running the command to display the content of the just created file containing the IPs..</br>
`do`</br>
`        echo "Dropped packets from $ip"`</br>
`        iptables -I INPUT -s $ip -j DROP`</br>
`done`


### WHILE LOOPS

While loops are another way to execute code repeatedly in Bash scripting. They continue to execute a block of code as long as a specified condition is true. In while loops, the semicolon ; is not necessary because the newline character serves as the command separator.

**SYNTAX:**

`While CONDITION`</br>
`do`</br>
`	COMMANDS`</br>
`done`

The set of commands are executed as long as the given condition evaluates to true.

**INFINTE LOOP**

`#!/bin/bash`</br>
`while [ 1 -eq 1 ]`</br>
`do`</br>
`	echo “This is an infinite loop that can be stopped with CTRL + C”`</br>
`	sleep 2`</br>
`done`

This script creates an infinite loop because the condition [ 1 -eq 1 ] always evaluates to true (1 is indeed equal to 1). As a result, the code block within the loop will continue to execute indefinitely until it's interrupted, typically by pressing Ctrl + C. This type of loop is useful for situations where you want a process to run continuously until manually stopped. However, it's important to use infinite loops judiciously to avoid consuming excessive system resources.

`#!/bin/bash`</br>
`while :`</br>
`do`</br>
`    echo "This is an infinite loop that can be stopped with CTRL + C"`</br>
`    sleep 2`</br>
`done`

This script creates an infinite loop using the while : syntax, where : represents a shell built-in command that always returns true. As a result, the loop continues indefinitely until it's interrupted, typically by pressing Ctrl + C. This type of loop is useful for situations where you want a process to run continuously until manually stopped, such as monitoring or background tasks."

**USE CASES**

If I want to continuously check every 3 seconds if a particular process is running, imagine having a sever application that should be continuously monitored,. It can’t be done with cronjob because the minute is the minimum time period available. Hence, it can be done by running the below script. 

`#!/bin/bash` </br>
`while :` # Infinite loop to continuously monitor the specified process </br>
`do`</br>
`        output="$(pgrep -l $1)"`</br>
`        if [[ -n "$output" ]]` # Check if the output is not empty, indicating the process is running </br>
`                then`</br>
`                echo "The process "$1" is running"`</br>
`        else`</br>
`                echo "The process "$1" is NOT running"` # If the process is not found, print a message and exit the loop </br>
`                break`
`        fi`</br>
`done`
~

The `break` statement is a control flow statement used in many programming languages to terminate the execution of a loop (such as for or while) or switch statement prematurely. When the `break` statement is encountered, the program exits the loop or switch statement immediately, and the control is transferred to the next statement after the loop or switch. </br></br>

The `let` command is often used for arithmetic operations in Bash scripts. This Bash script below demonstrates the use of a while loop to iterate over a sequence of numbers from 1 to 50, incrementing by 2 in each iteration. The loop continues as long as the value of the counter variable i is less than or equal to 50. Inside the loop, the current value of i is echoed to the console, and then i is incremented by 2 using the let command.

`#!/bin/bash` </br>
`i=1` # Initialize the counter variable </br>
`while [[ $i -le 50 ]]` # Loop while the value of i is less than or equal to 50 </br>
`do`</br>
`    echo $i` # Output the current value of i </br>
`    let "i += 2"`  # Increment i by 2 for the next iteration </br>
`done`

* let "i ≤ 50": The `let` command is used to evaluate the condition inside the double quotes. If the result is true (i.e., i is less than 50), the loop will continue; otherwise, it will exit.
* let "i += 2": This effectively increments the value of i by 2 in each iteration of the loop.
  - let: The let command is used for evaluating arithmetic expressions in Bash.
  - "i += 2": This is the arithmetic expression that adds 2 to the value of the variable i.
  - i: Represents the variable i.
  - +=: Is the assignment operator for addition. It adds the value on the right side of the operator to the variable on the left side.
  - 2: Is the value to be added to the variable i.


The below script prompts the user to enter a number specifying how many files they want to create. Then, it uses a `while` loop to create the specified number of files, naming each file with a numeric suffix (e.g., 0.txt, 1.txt, etc.). Finally, it prints a message confirming the number of files created.

`#!/bin/bash`
`read -p "Enter the number of files to create: " n`  # Prompt the user to enter the number of files to create and store the input in the variable 'n'
`i=0`  # Initialize a variable 'i' to 0 to serve as a counter
`while [[ $i -lt $n ]]`  # Start a while loop that continues as long as 'i' is less than 'n'
`do`
    `touch "$i.txt"`  # Inside the loop, create a file with the name '$i.txt' using the 'touch' command
    `((i++))`  # Increment the value of 'i' by 1 using the '((i++))' expression
`done`
`echo "$n files were created!"` # After the loop completes, print a message indicating the number of files created

The expression ((i++)) is a shorthand notation for incrementing the value of a variable by 1. Let's break down what each part of this expression does:

- `((...))`: This is an arithmetic expansion in Bash. It allows you to perform arithmetic operations.
- `i++`: This is the post-increment operator. It increments the value of the variable i by 1 after the current value of i has been used in the expression where it appears.

So, ((i++)) effectively increments the value of i by 1. In the context of the script you provided, this operation is used inside the while loop to increment the loop control variable i after each iteration of the loop. This ensures that the loop will eventually terminate after creating the specified number of files.

## CASE STATEMENT

Case statement allows us to test strings and numbers and is a simpler form of the bash if, elif, else statement. It is not a loop as it does not execute a block of code for n number of times. The case statement on Bash is similar to switch statement in C, C++ or Java.


**SYNTAX**

`case` </br>
` EXPRESSION` </br> 
`in` </br>
`  PATTERN_1)` </br>
`    STATEMENTS` </br>
`    ;;` </br>
`  PATTERN_2)` </br>
`    STATEMENTS` </br>
`    ;;` </br>
`  PATTERN_N)` </br>
`    STATEMENTS`</br>
`    ;;` </br>
`  *)` </br>
`    STATEMENTS` </br>
`    ;;` </br>
`esac`


**USE CASE**

`#!/bin/bash` </br>
`read -p "Enter a day of the week: " day` </br>
`case $day in` </br>  # Start of the case statement, evaluating the value of 'day'
`    "Monday")` </br>
`        echo "It's the start of the week."` </br>
`        ;;` </br> # End of the case block
`    "Tuesday" | "Wednesday" | "Thursday")` </br> # If 'day' equals "Tuesday", "Wednesday", or "Thursday"
`        echo "It's a weekday."` </br>
`        ;;` </br> # End of the case block
`    "Friday")` </br>
`        echo "TGIF! It's Friday."` </br>
`        ;;` </br> # End of the case block
`    "Saturday" | "Sunday")` </br>
`        echo "It's the weekend."` </br>
`        ;;`</br> # End of the case block
`    *)`</br>
`        echo "Invalid day entered."`</br>
`        ;;` </br> # End of the case block
`esac` 

This Bash script prompts the user to enter a day of the week. Based on the input provided by the user, it uses a case statement to determine the day of the week and then prints out a corresponding message.

* The user is prompted to enter a day of the week (`read -p "Enter a day of the week: " day`).
* The `case` statement evaluates the value of the variable $day against various patterns specified after each ).
* The `;;` syntax is used to terminate each pattern block. While the `*)` pattern serves as a catch-all or default case, similar to the default case in other languages. </br></br>


`#!/bin/bash`</br>
`if [[ $# -ne 2 ]]` # Code to execute if the number of arguments is not equal to 2 </br>
`then`</br>
`         echo "Run the script with two arguments: Signal and PID"`</br>
`         exit` # Exit the script if arguments are incorrect</br> 
`fi`</br></br>
`case "$1" in`  # Start of the case statement to determine signal based on argument 1 </br>
`         1)`</br>
`                echo "Sending the SIGHUP signal to $2"`</br>
`                 kill -SIGHUP $2` # Send SIGHUP signal to process specified by argument 2 </br>
`                 ;;`</br>
`         2)`</br>
`                 echo "Sending the SIGINT signal to $2"`</br>
`                 kill -SIGINT $2` # Send SIGINT signal to process specified by argument 2 </br>
`                 ;;`</br>
`         15)`</br>
`                 echo "Sending the SIGTERM signal to $2"`</br>
`                 kill -SIGTERM $2` # Send SIGTERM signal to process specified by argument 2</br>
`                 ;;`</br>
`         *)`</br>
`                 echo "The signal number $1 will not be delivered"`</br>
`esac`

The script is designed to be run with two command-line arguments: a signal number and a process ID. It then uses a case statement to determine the corresponding signal to send to the specified process. If the number of arguments is not exactly two, it provides a usage message and exits.


### FUNCTIONS IN BASH

We use functions to organise our codes in blocks that can be later reused without the need to rewrites copy and paste that block of code. 
Functions are useful for organizing code, improving reusability, and making scripts more modular.

`#!/bin/bash` </br>
\# Function definition </br>
`function my_function() {` </br>
    # Commands to be executed </br>
`    echo "Hello from the function!"` </br>
`}` </br>
\# Function invocation </br>
`my_function`

**DO NOT INPUT ANY DATA INSIDE THE PARENTHESIS IN FUNCTIONS.**

If you want the functions to process some data, then you send it to the function in a similar way to passing command line arguments to a script. 
Use $1 for the first argument of the function, and $2 for the second.

`#!/bin/bash` </br>
`function create_file () {  # Function to create two files and set permissions` </br>
`        echo "Creating $1"` </br>
`        touch $1` </br>
`        chmod 700 $1` </br>
`        echo "Creating $2"` </br>
`        touch $2` </br>
`        chmod 700 $2` </br>
`        return 10` </br>
`}`</br>
`function lines_in_file () {`  # Function to count lines containing a pattern in a file </br>
`        grep -c "$1" "$2"` </br>
`}` </br>
</br>
`create_file new_me.txt life.txt`  # Create files and set permissions</br>
`n=$(lines_in_file "usb" "/var/log/dmesg")`  # Count lines containing "usb" in /var/log/dmesg and store the result in n</br>
`echo $n`  # Print the result

**EXPLANATIONS:**

* Function Definition (create_file):
    * Declares a Bash function named create_file.
    * Takes two arguments, $1 and $2, representing filenames.
    * Prints messages indicating the creation of each file using echo.
    * Uses touch to create the files.
    * Sets the file permissions to read, write, and execute only for the owner using chmod 700.
* Function Invocation (create_file new_me.txt life.txt):
    * Calls the create_file function with two arguments: "new_me.txt" and "life.txt."
* It then calls lines_in_file with the pattern "usb" and the file "/var/log/dmesg" and stores the result in the variable n.
* Finally, it echoes the value of n, which represents the number of lines containing "usb" in the specified log file.

When you run this script, it will create two files, "new_me.txt" and "life.txt," in the current directory, and set their permissions to allow only the owner to read, write, and execute. It also prints the number of lines in "/var/log/dmesg" that contain the pattern "USB."


### VARIABLE SCOPE IN FUNCTIONS

Scope refers to each part of a script where a variable is visible. Variable scope determines where a variable is accessible and modifiable within a script or function. There are two primary types of variable scope: Global scope and Local scope.

* Variables declared with the local keyword inside a function have local scope.
* Local variables are accessible and modifiable only within the function where they are declared.
* They do not affect global variables with the same name.

`#!/bin/bash` </br>
`var1="AA" - - - - global var` </br>
`var2="BB" - - - - global var` </br>
</br>
`function func1 () {`</br>
`        var1="CC" - - - - global var`</br>
`        local var2="DD" - - - - local var`</br>
`        echo "Inside func1: var1= $var1 var2=$var2"`</br>
`}`</br>
</br>
`func1`</br>
`echo "After calling func1: var1: $var1 var2: $var2"`

* var1 and var2 are defined in the global scope with values "AA" and "BB," respectively.
    * The func1 function is defined, and within the function:
    * var1 is reassigned to a new value "CC" in the global scope.
    * var2 is defined as a local variable within the function with the value "DD."
    * The function prints the values of var1 and var2 within its local scope.
* The function func1 is called.
* After calling the function, the script prints the values of var1 and var2 in the global scope.

The script defines a function func1 and demonstrates variable scoping in Bash. It initializes two global variables (var1 and var2), modifies var1 within the function's scope, and declares a local variable var2. After calling the function, it prints the values of var1 and var2 to illustrate their scope and any changes made within the function.


### MENUS IN BASH (THE SELECT STATEMENT)

The select statement in Bash allows you to create interactive menus for users to make choices from predefined options. 

**SYNTAX:** The select statement follows this syntax:

`select VARIABLE in OPTION1 OPTION2 OPTION3 ...;` </br>
`do`</br> 
    # Commands to execute for each selected option </br>
`done`

**USE CASE:**

`#!/bin/bash` # Set the prompt for the select command </br>
`PS3="Select your Bank name: "` </br>
`select BANKS in UBA GTB "Zenith Bank" "Optimus Bank"` # Use select to generate a menu </br>
`do`  # $BANKS contains the selected value </br> 
`    echo "Bank is $BANKS"` </br>
`    echo "Reply is $REPLY"`  # $REPLY contains the number corresponding to the user's choice </br> 
`done`

* PS3 Variable (Line 2):
    * PS3 is a variable that determines the prompt used by the select statement.
* select Statement (Lines 4-8):
    * select is used to generate a menu for the user to choose from.
    * The user can select a bank name from the list (UBA, GTB, Zenith Bank, Optimus Bank).
    * The selected value is stored in the variable $BANKS.
    * The variable $REPLY contains the number corresponding to the user's choice.
    * The statements within the do and done block are executed for each iteration of the select loop.
* echo Statements (Lines 6-7):
    * Print the selected bank name ($BANKS) and the corresponding number ($REPLY).
 
This script demonstrates the use of the select statement in Bash to generate a menu for the user to choose from. The user can select a bank name from the list (UBA, GTB, Zenith Bank, Optimus Bank), and the selected value is stored in the variable $BANKS. The variable $REPLY contains the number corresponding to the user's choice. The script continuously prompts the user to select a bank name until the user decides to exit the loop.

**ANOTHER USE CASE BELOW:**

`#!/bin/bash` </br>
`PS3="Select your language: "` # Set the prompt for the select command</br>
`select COUNTRY in USA France Germany "United Kingdom" Quit` # Use select to generate a menu</br>
`do`</br>
`    # Use a case statement to handle different choices`</br>
`    case $REPLY in`</br>
`        1)`</br>
`            echo "You speak American English"`</br>
`            ;;`</br>
`        2)`</br>
`            echo "You speak French"`</br>
`            ;;`</br>
`        3)`</br>
`            echo "You speak German"`</br>
`            ;;`</br>
`        4)`</br>
`            echo "You speak British English"`</br>
`            ;;`</br>
`        5)`</br>
`            echo "Ending session"`</br>
`            sleep 1`</br>
`            break`</br>
`            ;;`</br>
`        *)`</br>
`            echo "Invalid input $REPLY"`</br>
`    esac`</br>
`done`

This Bash script uses the select statement along with a case statement to create a menu for selecting a language or ending the session. 

* PS3 Variable (Line 2):
    * PS3 is a variable that determines the prompt used by the select statement.
* select Statement (Lines 3-21):
    * select is used to generate a menu for the user to choose from (USA, France, Germany, United Kingdom, Quit).
    * The selected value is stored in the variable $COUNTRY.
* case Statement (Lines 5-25):
    * A case statement is used to handle different choices based on the value of $REPLY.
    * Each case corresponds to a different language based on the country chosen.
    * The case with value 5 corresponds to Quit, and it ends the session with a break statement.
* sleep Statement (Line 20):
    * Introduces a 1-second delay before breaking out of the loop.
* * Case (Line 23):
    * Handles any other input that doesn't match the specified cases.
   

`#!/bin/bash`</br>
`PS3="Your choice: "` # Set the prompt for the select command</br>
`select ITEM in "Add User" "List All Processes" "Kill Process" "Install Program" "Quit" # Use select to generate a menu`</br>
`do`</br>
`    if [[ $REPLY -eq 1 ]]; then` # Check the user's choice using a series of if-elif-else statements</br>
        # Option: Add User</br>
`        echo -n "Enter your username: "`</br>
`        read username`</br>
`        output=$(grep -w $username /etc/passwd)`</br>
`        if [[ -n $output ]]; then`</br>
`            echo "The username $username already exists"`</br>
`            grep -w $username /etc/passwd`</br>
`        else`</br>
`            read -p "Input new username: " newusername`</br>
`            sudo useradd -m -s /bin/bash "$newusername"`</br>
`            if [[ $? -eq 0 ]]; then`</br>
`                echo "The username $newusername has been created"`</br>
`                tail -n 1 /etc/passwd`</br>
`            else`</br>
`                echo "There was an error"`</br>
`            fi`</br>
`        fi`</br>
`    elif [[ $REPLY -eq 2 ]]; then`</br>
        # Option: List All Processes</br>
`        echo "Listing all processes...."`</br>
`        sleep 2`</br>
`        ps -ef`</br>
`    elif [[ $REPLY -eq 3 ]]; then`</br>
        # Option: Kill Process</br>
`        read -p "Enter the process name to kill: " name`</br>
`        pkill $name`</br>
`    elif [[ $REPLY -eq 4 ]]; then`</br>
        # Option: Install Program</br>
`        read -p "Enter the program to install: " program`</br>
`        sudo apt update && sudo apt install $program`</br>
`    elif [[ $REPLY -eq 5 ]]; then`</br>
        # Option: Quit</br>
`        echo "Quitting..."`</br>
`        sleep 2`</br>
`        break`</br>
`    else`</br>
`        echo "Invalid input $REPLY"`</br>
`    fi`</br>
`done`

* PS3 Variable (Line 2):
    * PS3 is a variable that determines the prompt used by the select statement.
* select Statement (Lines 3-46):
    * select is used to generate a menu for the user to choose from ("Add User," "List All Processes," "Kill Process," "Install Program," "Quit").
* If-Elif-Else Statements (Lines 5-44):
    * The script checks the value of $REPLY (the user's choice) using a series of if-elif-else statements.
        * Each option corresponds to a different action:
        * If the user chooses "Add User," it prompts for a username, checks if it already exists, and adds a new user if it doesn't.
        * If the user chooses "List All Processes," it lists all processes using `ps -ef`.
        * If the user chooses "Kill Process," it prompts for a process name and uses `pkill` to kill the specified process.
        * If the user chooses "Install Program," it prompts for a program name and installs it using sudo apt install.
        * If the user chooses "Quit," it prints a message and exits the loop with `break`.
        * If the user provides an invalid input, it prints an error message.

This script provides a menu-driven interface for system administration tasks. It allows the user to choose from various options such as adding a user, listing all processes, killing a process, installing a program, or quitting. Each option corresponds to different actions implemented using if-elif-else statements. The script guides the user through the chosen task, interacts with system utilities like `useradd`, `ps`, `pkill`, and `apt`, and provides feedback based on the user's input.
