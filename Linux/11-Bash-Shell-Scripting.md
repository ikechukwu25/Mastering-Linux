# BASIC SCRIPTING

A shell script is a file containing a series of commands that are executed in sequence by the shell interpreter. It is a file of executable commands that has been stored in a text file. When the file is run, each command is executed. Shell scripts are written in scripting languages supported by the shell, such as Bash, sh, or zsh.

Bash shell scripting involves writing scripts in the Bash (Bourne Again Shell) language, which is a command-line interpreter widely used on Unix-like operating systems.


#### SHELL SCRIPTING BASICS

- File Format: The `.sh` file extension commonly signifies a shell script, serving as a human-readable hint rather than influencing system behavior. Linux disregards file extensions.
- Execution: After creating a shell script, you need to make it executable using the `chmod` command:
  -  `chmod +x script.sh`: This command grants the user execute permission for the script named script.sh. Without execute permission, the script cannot be run as an executable file.
  -  `./script.sh`: This command executes the script named script.sh. The ./ prefix indicates that the script is located in the current directory. If the script is located in a different directory, you would need to specify the path to the script instead of just ./.


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


### PROGRAM CONTROL FLOW

Program control flow constructs can be categorized into two main types:

- Conditional Constructs: These constructs enable the execution of different blocks of code based on whether specific conditions are true or false. In Bash scripting, conditional constructs include the if statement and the case statement.

- Iterative Constructs (Loops): These constructs allow the repetition of a block of code multiple times until a certain condition is met or until all iterations have been completed. In Bash scripting, iterative constructs include for loops and while loops.

Both conditions and loops play crucial roles in controlling the flow of execution in scripts and programs, allowing for more dynamic and responsive behavior based on various factors and inputs.

### IF, ELIF AND ELSE STATEMENTS

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

**Example; **

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

