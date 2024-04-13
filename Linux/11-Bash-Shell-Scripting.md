# BASIC SCRIPTING

A shell script is a file containing a series of commands that are executed in sequence by the shell interpreter. It is a file of executable commands that has been stored in a text file. When the file is run, each command is executed. Shell scripts are written in scripting languages supported by the shell, such as Bash, sh, or zsh.

Bash shell scripting involves writing scripts in the Bash (Bourne Again Shell) language, which is a command-line interpreter widely used on Unix-like operating systems.


#### SHELL SCRIPTING BASICS

- File Format: The `.sh` file extension commonly signifies a shell script, serving as a human-readable hint rather than influencing system behavior. Linux disregards file extensions.
- Execution: After creating a shell script, you need to make it executable using the `chmod` command:.
  -  `chmod +x script.sh`:
  -  `./script.sh`: 


## BASH SHELL SCRIPTING

A shell is a programme that takes commands from the user through the keyboard and gives them to the OS kernel to get executed. 
The shell gets started when the user logs in to the terminal. 

These are fundamental commands used in shell environments to retrieve information about the shell environment and user configurations:

`echo $0`: This command reveals the shell that was launched upon login.
`cat /etc/shells`: Displays a catalog of all installed shells.
`cat /etc/passwd`: Reveals user account information, including default shells, like `pr2:x:1004:1006:Back-End:/home/pr2:/bin/bash`.

A shell script, an executable text file, encompasses shell commands along with structures like variables and functions, executed sequentially. It serves as a potent tool for automating repetitive tasks, enhancing productivity. Whenever you find yourself running a task over and over, you should use shell scripting. 

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
  - `bash first_script.sh` or `python3 first_script`: Make sure you are in the directory where the script is located. This pattern, the user does not need the execute permission to run the script and it. This way will also overwrite the shebang directive. 
4. Using source or . Command: Execute the script using the source command or its shorthand, fornexample;
  - `source first_script.sh` or `. first_script`: It does not require the execution permission and the source command reads and executes command from the file specified as it’s argument in the current shell environment.

These methods provide flexibility in running Bash scripts, catering to various use cases and requirements.


## SHELL CUSTOMIZATION

Shell customization refers to the process of tailoring the shell environment to suit individual preferences and optimize workflow efficiency. It involves configuring various aspects of the shell, such as aliases, variables etc to enhance usability and productivity.

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


Below is a typic example of how to use Varibales; 

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

