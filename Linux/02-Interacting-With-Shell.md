# WHY USE THE TERMINAL?

Linux users prefer the terminal over GUI for its efficiency, flexibility, and power. Unlike other operating systems, Linux offers a vast array of command-line utilities for advanced system administration, scripting, and automation. Knowing these commands is essential for managing Linux systems effectively, enabling tasks such as remote access, resource-efficient operations, and a deeper understanding of the operating system's internals. The terminal fosters a culture of learning and understanding, encouraging users to interact directly with the system and develop proficiency in command-line operations. This preference reflects Linux's heritage as a system designed for experienced users and administrators who value control, customization, and the ability to work efficiently at the command line.


# SHELL EXPLAINED

Once a user has entered a command the terminal then accepts what the user has typed and passes it to a shell. The shell is the command line interpreter that translates commands entered by a user into actions to be performed by the operating system.

In Bash, commands can generally be categorized into various types based on how they are executed and interpreted:

* **Internal commands**: These commands are built into the shell itself and are interpreted directly by the shell without invoking external programs. A good example is the `cd` (change directory) command as it is part of the Bash shell. When a user types the `cd` command, the Bash shell is already executing and knows how to interpret it, requiring no additional programs to be started.
* **External commands**: These are binary executables stored in directories that are searched by the shell. If a user types the `ls` command, the shell searches through the directories that are listed in the PATH variable to try to find a file named ls that it can execute. 
* **Scripting**: The ability to place commands in a file and then interpret (effectively use Bash to execute the contents of) the file, resulting in all of the commands being executed. This feature also has some programming features, such as conditional statements and the ability to create functions (AKA subroutines).
* **Aliases**: Aliases are user-defined shortcuts or nicknames for longer commands or command sequences. They are used to simplify frequently used commands or customize the command-line experience. Aliases are typically defined in configuration files like `.bashrc`.
* **Variables**: These are used to store information for the Bash shell and for the user. These variables can be used to modify how commands and features work as well as provide vital system information.
* **Executable programs**: These are standalone programs installed on the system that can be executed directly from the command line. Examples include text editors like `vi` or `nano`, compilers like `gcc`, and utilities like `tar` or `curl`.

Here are representations of command line prompts in a Unix/Linux environment. 

* User Name: `ikechukwu`@ubuntu-22-04-3:~$ 
* System Name: ikechukwu@`ubuntu-22-04-3`:~$
* Current Directory: ikechukwu@ubuntu-22-04-3:`~`$

### VARIABLES

A variable is a feature that allows the user or the shell to store data. his data can be used to provide critical system information or to change the behavior of how the Bash shell (or other commands) works. Variables are given names and stored temporarily in memory. There are two types of variables used in the Bash shell: Local and Environment.

##### LOCAL VARIABLES
Local or shell variables exist only in the current shell, and cannot affect other commands or applications. When the user closes a terminal window or shell, all of the variables are lost. 

`ikechukwu@ubuntu-22-04-3:~$ variable1='Something'` </br>
`ikechukwu@ubuntu-22-04-3:~$ echo $variable1`</br>
`Something`

##### ENVIRONMENT VARIABLES
Environment variables, also called global variables, are available system-wide, in all shells used by Bash when interpreting commands and performing tasks.

The **HISTSIZE** variable defines how many previous commands to store in the history list. 

When run without arguments, the `env` command outputs a list of the environment variables. The `export` command is used to turn a local variable into an environment variable.

`export MY_VARIABLE="World"`

After executing this command, whenever you reference $MY_VARIABLE in your shell session or in scripts, it will have the value "World" until you either change it again or unset it.

To concatenate the value of two environment variables, use the assignment expression:

`ikechukwu@ubuntu-22-04-3:~$ variable1="Something"` </br>
`ikechukwu@ubuntu-22-04-3:~$ variable2="Else"`</br>
`ikechukwu@ubuntu-22-04-3:~$ variable1=$"variable1 $variable2"`</br>
`ikechukwu@ubuntu-22-04-3:~$ echo $variable1`</br>
`Something Else`

So, if variable1 had the value "Something" and variable2 had the value "Else", after executing these commands, variable1 will have the value "Something Else".

##### PATH VARIABLE
One of the most important Bash shell variables to understand is the PATH variable. It contains a list that defines which directories the shell looks in to find commands. If a valid command is entered and the shell returns a "command not found" error, it is because the Bash shell was unable to locate a command by that name in any of the directories included in the path.

By default, the PATH variable often includes directories like /usr/bin, /bin, /usr/sbin, and /sbin, among others.

For instance, if you type `ls` in the shell, it will search for the `ls` command in these directories specified in the PATH.

### EXTERNAL COMMANDS
External commands are binary executables stored in directories that are searched by the shell. If a user types the ls command, then the shell searches through the directories that are listed in the PATH variable to try to find a file named ls that it can execute.

If a command does not behave as expected or if a command is not accessible that should be, it can be beneficial to know where the shell is finding the command or which version it is using. It would be tedious to have to manually look in each directory that is listed in the PATH variable. Instead, use the `which` command to display the full path to the command in question.

### FUNCTIONS
Functions can also be built using existing commands to either create new commands or to override commands built-in to the shell or commands stored in files.

function_name () </br>
{ </br>
    commands </br>
} </br>

# FILE PATHS

Paths in the Linux file system are indeed divided into two categories: Absolute paths and Relative paths.

- **Absolute Path**:
An absolute path specifies the exact location of a file or directory in the file system hierarchy.
It begins from the root directory (/) and includes all directories leading to the target file or directory.
Example: `/var/log` is an absolute path that specifies the location of the log directory within the var directory.

- **Relative Path**:
A relative path specifies the location of a file or directory relative to the current working directory.
It does not begin with the root directory (/).
Example: If the current working directory is `/home/user`, then `./Documents/file.txt` is a relative path that specifies the location of the `file.txt` within the Documents directory relative to the current directory.

**Special Directory References**: These symbols provide convenient ways to reference specific directories in relation to the current working directory or the user's home directory, particularly while using a relative path.

- .  = the current working directory
- .. = the parent directory
- ~  = the user's home directory
- /  = the root directory

**File Type Indicators**: These symbols are often referred to as file type indicators or file mode indicators. They provide information about the type of file or special file in a Unix-like operating system such as Linux. 

* -: Regular file.
* d: Directory. Represented as /.
* l: Symbolic link. Similar to a shortcut in Windows. Represented as @.
* b: Block device.
* c: Character device.
* s: Socket. Used by processes to communicate. Represented as (symbol).
* p: Named pipe. Used by processes to communicate through pipes. Represented as |.

For example, if you execute the command ls -l in a directory, you may see output like: 

`lrwxrwxrwx 1 user group   10 Jan 1 00:00 link -> targetfile` (symbolic link) </br>
`drwxr-xr-x 2 user group 4096 Jan 1 00:00 directory/` (directory)</br>
`-rw-r--r-- 1 user group 1024 Jan 1 00:00 example.txt` (regular file)

These indicators are typically displayed in the leftmost column of the output and indicate the file type. Understanding these symbols aids in navigating and comprehending the structure and content of the Linux file system. 


# GLOBBING

Globbing refers to the process of using wildcards or special characters, such as '*' and '?', in a command-line interface to match files or directories based on patterns.

### ASTERISK (*) CHARACTER
  
The asterisk * character is used to represent zero or more of any character in a filename. For example, to display all of the files in the /etc directory that begin with the letter t:

`ikechukwu@ubuntu-22-04-3:~$ echo /etc/t*`                              
`/etc/terminfo /etc/timezone /etc/tmpfiles.d`

The following matches any filename in the /etc directory that ends with .d:

`ikechukwu@ubuntu-22-04-3:~$ echo /etc/*.d`                                 
`/etc/apparmor.d /etc/binfmt.d /etc/cron.d` 

All of the files in the /etc directory that begin with the letter r and end with .conf are displayed:

`ikechukwu@ubuntu-22-04-3:~$ echo /etc/r*.conf`                             
`/etc/resolv.conf /etc/rsyslog.conf`

### QUESTION MARK (?) CHARACTER
  
The question mark character represents any single character. Each question mark character matches exactly one character, no more and no less.
Suppose you want to display all of the files in the /etc directory that begin with the letter t and have exactly 7 characters after the t character:

`ikechukwu@ubuntu-22-04-3:~$ echo /etc/t???????`      
`/etc/terminfo /etc/timezone`

The ? character can be used to match exactly 1 character in a file name. Execute the following command to display all of the files in the /etc directory that are exactly four characters long:

`ikechukwu@ubuntu-22-04-3:~$ ls -d /etc/????`

Glob characters can be used together to find even more complex patterns. The pattern /etc/*???????????????????? only matches files in the /etc directory with twenty or more characters in the filename:

`ikechukwu@ubuntu-22-04-3:~$ echo /etc/*????????????????????`            
`/etc/bindresvport.blacklist /etc/ca-certificates.conf`

The asterisk and question mark could also be used together to look for files with three-letter extensions by using the /etc/*.??? pattern:

`ikechukwu@ubuntu-22-04-3:~$ echo /etc/*.???`              
`/etc/issue.net /etc/locale.gen`


### BRACKET [ ] CHARACTERS

The bracket [ ] characters are used to match a single character by representing a range of characters that are possible match characters. For example, the `/etc/[gu]*` pattern matches any file that begins with either a "g" or "u" character and contains zero or more additional characters:

`ikechukwu@ubuntu-22-04-3:~$ echo /etc/[gu]*`                            
`/etc/gai.conf /etc/groff /etc/group /etc/group- /etc/gshadow /etc/gshadow- /etc/
gss /etc/ucf.conf /etc/udev /etc/ufw /etc/update-motd.d /etc/updatedb.conf`           

By using square brackets [ ] you can specify a single character to match from a set of characters. Execute the following command to display all of the files in the /etc directory that begin with the letters a, b, c, or d:

`ikechukwu@ubuntu:~$ ls –d /etc/[abcd]*`

Brackets can also be used to represent a range of characters. For example, the `/etc/[a-d]*` pattern matches all files that begin with any letter between and including a and d. 

The `/etc/*[0-9]*` pattern displays any file that contains at least one number:

Exclamation Point (!) Character
The exclamation point character is used in conjunction with the square brackets to negate a range. For example, the pattern `/etc/[!DP]*` matches any file that does not begin with a D or P.

`ikechukwu@ubuntu-22-04-3:~$ echo /etc/[!a-t]*`
`/etc/X11 /etc/ucf.conf /etc/udev /etc/ufw /etc/update-motd.d /etc/updatedb.conf 
/etc/vim /etc/vtrgb /etc/wgetrc /etc/xdg`


# KEYBOARD SHORTCUTS

* TAB - autocompletes the command or the filename if it's unique

* TAB TAB (press twice) - displays all commands or filenames that start with those letters

* Clearing the terminal - CTRL + L

* Closing the shell (exit) - CTRL + D

* Cutting (removing) the current line  - CTRL + U

* Moving the cursor to the start of the line - CTRL + A

* Moving the cursor to the end of the line - Ctrl + E

* Stopping the current command - CTRL + C

* Sleeping a running program - CTRL + Z

* Opening a terminal  - CTRL + ALT + T

* Search for commands in history. - CTRL + R

* Previous command in history - Ctrl + P

* Leave the history search mode without running a command. - Ctrl + G

* Leave the root environment - Ctrl + D


# REGULAR EXPRESSIONS (REGEX)

Regular expressions are extensively employed in text processing, searching, and data extraction tasks across various programming languages and command-line utilities. There are both Basic Regular Expressions (available to a wide variety of Linux commands) and Extended Regular Expressions (available to more advanced Linux commands). Basic Regular Expressions include the following:

### BASIC REGULAR EXPRESSIONS

Regular expressions also referred to as regex, are a collection of normal and special characters that are used to find simple or complex patterns, respectively, in files. 

| Character | Matches |
|----------|----------|
| . | Any single character | 
| [ ] | A list or range of characters to match one character. If the first character within the brackets is the caret ^, it means any character not in the list |
| * | The previous character repeated zero or more times | 
| ^ | If the first character is in the pattern, the pattern must be at the beginning of the line to match, otherwise, it is just a literal ^ character | 
| $ | If the last character in the pattern, the pattern must be at the end of the line to match, otherwise just a literal $ character | 

The `grep` command is just one of the many commands that support regular expressions. Some other commands include the `more` and `less` commands.

1. The Period (.) Character : 
One of the most useful expressions is the period character. It matches any character except for the new line character.
The pattern r..f would find any line that contained the letter r followed by exactly two characters and then the letter f: </br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep 'r..f' red.txt`</br></br>
`reef`</br>
`roof`</br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep '....' red.txt`</br>
`reef`</br>
`reeed`

2. The Bracket [ ] Characters : 
The square brackets [ ] match a single character from the list or range of possible characters contained within the brackets. 
Note that each possible character can be listed out [abcd] or provided as a range [a-d], as long as the range is in the correct order. </br>
The range is specified by a standard called the ASCII table. This table is a collection of all printable characters in a specific order. You can see the ASCII table with the ASCII command. E.g. </br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep '[0-9]' profile.txt`</br>
`I am 37 years old.`</br>
`3121991`</br>
`I have 2 dogs.` </br></br>
Character classes allow you to specify sets of characters that can match at a particular point in the pattern. For example, [aeiou] matches any vowel, [0-9] matches any digit, and [^a-z] matches any character that is not a lowercase letter. [^0-9] is a character class that matches any single character except for digits from 0 to 9.</br></br>
Suppose you want to search for a pattern containing a sequence of three digits. You can use { } characters with a number to express that you want to repeat a pattern a specific number of times; for example: {3}. The use of the numeric qualifier requires the extended mode of grep. For example; </br></br>
`grep -E '[0-9]{3}' passwd`

3. The Asterisk (\*) Character : 
The asterisk * character is used to match zero or more occurrences of a character or pattern preceding it. E.g. </br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep 'e*' red.txt`</br>
`red`</br>
`reef`</br>
`rot`</br></br>
To make the asterisk character useful, it is necessary to create a pattern that includes more than just the one character preceding it. For example, the results above can be refined by adding another "e" to make the pattern "ee*" effectively match every line that contains at least one E.g. </br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep 'ee*' red.txt`</br>
`red`</br>
`reef`</br>
`reeed`

4. Anchor (^) Characters : 
When performing a pattern match, the match could occur anywhere on the line. Anchor characters are one of the ways regular expressions can be used to narrow down search results. They specify whether the match occurs at the beginning of the line or the end of the line.

The caret (circumflex) ^ character is used to ensure that a pattern appears at the beginning of the line. Eg. </br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep '^root' /etc/passwd`</br>
`root:x:0:0:root:/root:/bin/bash`</br></br>
The second anchor character $ can be used to ensure a pattern appears at the end of the line, thereby effectively reducing the search results. Eg. </br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep 'r$' alpha-first.txt`</br>
`B is for Bear`</br>
`F is for Flower`

6. The Backslash (\\) Character : 
In some cases, you may want to match a character that happens to be a special regular expression character. E.g </br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep 're*' newhome.txt` </br>
`Thanks for purchasing your new home!!` </br>
`**Warning** it may be haunted.` </br>
`There are three bathrooms.`</br></br>
In the output of the grep command above, the search for re* matched every line that contained an "r" followed by zero or more of the letter e. To look for an actual asterisk * character, place a backslash \ character before the asterisk * character: </br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep 're\*' newhome.txt` </br>
`**Beware** of the ghost in the bedroom.`

### EXTENDED REGULAR EXPRESSIONS

The use of extended regular expressions often requires a special option be provided to the command to recognize them. Historically, there is a command called `egrep`, which is similar to `grep`, but can understand extended regular expressions. Now, the `egrep` command is deprecated in favor of using grep with the -E option.

| Character | Meaning |
|----------|----------|
| ? | Matches previous character zero or one time, so it is an optional character |
| + | Matches previous character repeated one or more times |
| \| | Alternation or like a logical "or" operator |

1. To match color followed by zero or one u character followed by an r character: </br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep -E 'colou?r' spelling.txt`</br>
`American English: Do you consider gray to be a color or a shade?`</br>
`British English: Do you consider grey to be a colour or a shade?`

2. To match one or more e characters:</br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep -E 'e+' red.txt` </br>
`red`</br>
`reef`</br>
`reeed`

3. To match either gray or grey:</br></br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ grep -E 'gray|grey' spelling.txt` </br>
`American English: Do you consider gray to be a color or a shade?`</br>
`British English: Do you consider grey to be a colour or a shade?`


# BASIC COMMANDS AND THEIR UTILITIES. 

Basic commands in a terminal environment serve as fundamental tools for users to interact with their operating systems efficiently. From listing files with `ls` to navigating directories with `cd`, manipulating files with `cp` and `rm`, and performing system tasks with `pwd` and `mkdir` these commands empower users to accomplish various tasks seamlessly. Understanding these commands and their utilities is fundamental for effective system administration and development workflows.

## GETTING HELP IN LINUX

In Linux, getting help is essential for mastering the operating system and its various commands. Here are some common methods to get help:

#### MAN PAGES

The Manual Pages (man pages) in Linux systems provide documentation for various commands, functions, system calls, and configurations. By default, there are nine sections in the man pages, each covering different aspects of the system:

- General Commands (Section 1): Documentation for general user commands and utilities typically used on the command line.
- System Calls (Section 2): Describes system calls, which are functions provided by the kernel for programmatic interaction with the operating system.
- Library Calls (Section 3): Covers library functions provided by the C library and other libraries, often used by developers when writing programs in C.
- Special Files (Section 4): Information about special files representing devices or interfaces in the system, found in the /dev directory.
- File Formats and Conventions (Section 5): Documents file formats, conventions, and specific configuration files used by the system.
- Games (Section 6): Documentation for games available on the system.
- Miscellaneous (Section 7): Includes miscellaneous documentation on topics like macro packages and conventions.
- System Administration Commands (Section 8): Documentation for commands primarily used by system administrators to manage and configure the system.
- Kernel Routines (Section 9): Provides documentation for kernel routines, often of interest to kernel developers.

On most Linux distributions:

The `whatis` command and `man -f` command are functionally equivalent, providing a brief description of commands.

The `apropos` command and `man -k` command are functionally equivalent, searching for keywords in man page names and descriptions.

To search for man pages by name, use the `-f` option with the man command to display man pages matching a specific name and provide their section number and a brief description.

To search for the location of a command or its man pages, use the `whereis` command, which searches for commands, source files, and man pages in typical locations where these files are stored. 

NB: The man page is displayed with the less command

##### SHORTCUTS:
- h         => getting help
- q         => quit
- enter     => show next line
- space     => show next screen
- /string   => search forward for a string
- ?string   => search backward for a string
- n / N     => next/previous appearance

#### HELP

When dealing with shell built-in commands in Linux, you can use the `help` command followed by the built-in command name to get information about its usage and options. For example:

help command    => Ex: `help cd` </br>
command --help  => Ex: `rm --help`

On most systems, there is a directory where additional documentation (such as documentation files stored by third-party software vendors) is found.
‌⁠
These documentation files are often called readme files since the files typically have names such as README or readme.txt. The location of these files can vary depending on the distribution that you are using. Typical locations include `/usr/share/doc` and `/usr/doc`.
Typically, this directory is where system administrators go to learn how to set up more complex software services. However, sometimes regular users also find this documentation to be useful.

## COPYING FILES

To copy files in Linux, users commonly employ the `cp` command. It's simple yet versatile, allowing for the duplication of files and directories within the file system. For instance, `cp file1.txt directory/` copies `file1.txt` into the specified directory.

Two options can be used to safeguard against accidental overwrites. With the `-i` interactive option, the cp command prompts the user before overwriting a file. The following example demonstrates this option, first restoring the content of the original file:

`ikechukwu@ubuntu:~$ cp -i /etc/hosts example.txt`                  
`cp: overwrite '/home/sysadmin/example.txt'?`

NB: Also, users should use the `-i` option when deleting multiple files: eg: `rm -i /etc/ssh/ssdh_config`

## REAL-TIME MONITORING WITH WATCH

The `watch` command in Linux is used to execute a command periodically and display its output in real time. It continuously runs the specified command at regular intervals (usually every 2 seconds by default) and updates the terminal with the latest output. This is particularly useful for monitoring system changes, observing the progress of long-running processes, or keeping track of dynamic data. For example;

`watch -n 1 -d ifconfig`:  is used to continuously monitor and display the output of the `ifconfig` command with a 1-second refresh rate (-n 1) and with differences highlighted (-d)

`watch -n 1 -d ls`: is used to continuously monitor and display the output of the current directory with a 1-second refresh rate (-n 1) and with differences highlighted (-d)

## OUTPUT REDIRECTION

In Linux, the ">" symbol is used for output redirection, allowing users to redirect the output of a command to a file. This simple yet powerful feature enables efficient file creation and manipulation. For example;

`ls -l > ls.txt` =  a new file is created and the `ls -l` command is now seen when the ls.txt file is opened. 

To redirect another command to the same file and not overwrite = `ls -l > ls.txt`

'>' = overwrite </br>
'>>' = append

## ADVANCED CONSTRUCTS FOR STREAM MANAGEMENT:

Two constructs, `2>&1` and `|&`, provide advanced functionality for handling both the standard output (stdout) and standard error (stderr) streams.

`2>&1`: Redirects stderr to stdout. It combines error messages with regular output, facilitating unified stream processing.

Example 1: Redirect stderr to stdout and then to a file: `ls -l /nonexistent 2>&1 > error.log` </br>
Example 2: Redirect stderr to stdout and display both on the terminal: `ls -l /nonexistent 2>&1` </br>

`|&`: Combines stdout and stderr using a pipe. It's useful for the simultaneous processing of both streams.

Example: Combine stdout and stderr and count the lines using wc: `ls -l /nonexistent |& wc -l`

These constructs enhance command-line operations by enabling efficient management and processing of both stdout and stderr streams.

## VIEWING FILES USING A PAGER

While viewing small files with the cat command poses no problems, it is not an ideal choice for large files. The cat command doesn't provide any easy ways to pause and restart the display, so the entire file contents are dumped onto the screen.

For larger files, use a pager command to view the contents. Pager commands display one page of data at a time, allowing you to move forward and backward in the file by using movement keys.

There are two commonly used pager commands:
* The command provides a very advanced paging capability. It is usually the default pager used by commands like the `man` command.
* The `more` command has been around since the early days of UNIX. While it has fewer features than the `less` command, however, the `less` command isn't included with all Linux distributions. The `more` command is always available.

## FILE PREVIEWING AND TAILING.

The head and tail commands are used to display only the first few or last few lines of a file, respectively (or, when used with a pipe, the output of a previous command). By default, the head and tail commands display ten lines of the file that is provided as an argument.

- Negative Value Option: 
Traditionally in UNIX, the number of lines to output would be specified as an option with either command, so -3 is meant to show three lines. For the tail command, either -3 or -n -3 still means show three lines.

However, the GNU version of the head command recognises -n -3 as showing all but the last three lines, and yet the head command still recognizes the option -3 as show the first three lines.

- Positive Value Option: 
The GNU version of the tail command allows for a variation of how to specify the number of lines to be printed. If the `-n` option is used with a number prefixed by the plus sign, then the tail command recognizes this to mean to display the contents starting at the specified line and continuing all the way to the end.

Examples: </br>
`ls /etc/ssh | nl | head -5`</br>
* The `ls /etc/ssh` command lists the contents of the `/etc/ssh` directory.
* nl numbers the lines of the output.
* `head -5` displays the first 5 lines of the numbered output.


`ls /etc/ssh | tail -5 | nl` </br>
* The `ls /etc/ssh` command lists the contents of the `/etc/ssh` directory.
* `tail -5` selects the last 5 lines of the output.
* nl numbers the lines of the selected output.
  
Live file changes can be viewed by using the `-f` option to the tail command—useful when you want to see changes to a file as they are happening. 

## LOCATING FILES

- Locate:
To locate files efficiently, you can utilize the `locate` and `find` commands. Begin by installing `locate` if not already available on your system `sudo apt install locate`. "Locate" efficiently finds strings within absolute path names by searching its own database. Remember to update the database with `sudo updatedb` before searching for newly created files. For example
  - `locate -b string`: searches for files with the strings in their name. 
  - `locate -b "\string"`:  does not use the default *name* searches system but searches for the exact string. 

- Which: 
The `which` command helps find the location of an executable command. For example;
  - `which ls`: will display the location of the ls command.
  - `which cd`: won't display anything since cd is a shell built-in command, not an executable.
  - `which -a locate`: will display all instances of the locate command found in the PATH.

- Find: 
The find command in Linux is a powerful utility for searching files and directories based on various criteria within a directory hierarchy. It allows users to locate files by specifying conditions such as filenames, modification times, ownership, and more. For example; </br>

  - `find . -name linux.txt`: This command searches for files named "linux.txt" starting from the current directory (.) and displays the path to each file found.
  - `find -iname "*Pub*"`: This command searches for files with names containing "Pub" (ignoring case due to -i). The asterisks (*) are wildcards, allowing for matches with any characters before and after "Pub".
  - `find -name "*txt*"`: This command finds files with names containing the string "txt" (case-sensitive). Again, the asterisks act as wildcards, matching any characters before and after "txt".
  - Find and Exec : 
When the `find` command is combined with the -exec option, it allows users to perform actions on the files or directories found. For example:</br>
  `sudo find /etc/ -type f -mtime 0 -exec cp {} /root/backup \;`: This copies the files that have been generated by the `find`
  command which is put in the curly brackets before being executed by the exec command to copy (cp) </br>
  `sudo find /etc/ -type f -mtime 0 -ok cp {} /root/backup \;`: Similar to the previous command, this one also finds files modified within the last 24 hours in the /etc/ directory. However, instead of directly executing the cp command, the ok option prompts the user for confirmation before executing the cp command for each found file. </br>
  `find /etc/ -type f -no -user root` = shows all var files that are not under root. 

## ARCHIVING AND COMPRESSING

* Archiving: Combines multiple files into one, which eliminates the overhead in individual files and makes the files easier to transmit.
* Compression: Makes the files smaller by removing redundant information.

Files can be compressed individually, or multiple files can be combined into a single archive and then subsequently compressed. The latter is still referred to as archiving.

Even though disk space is relatively cheap, archiving and compression still have value:
* When making a large number of files available, such as the source code to an application or a collection of documents, it is easier for people to download a compressed archive than it is to download files individually.
* Log files have a habit of filling disks, so it is helpful to split them by date and compress older versions.
* When backing up directories, it is easier to keep them all in one archive than it is to version (update) each file.
* Some streaming devices such as tapes perform better if you’re sending a stream of data rather than individual files.
* It can often be faster to compress a file before sending it to a tape drive or over a slower network and decompress it at the other end than it would be to send it uncompressed.

#### COMPRESSING FILES 

Compression reduces the amount of data needed to store or transmit a file while storing it in such a way that the file can be restored.

When talking about compression, there are two types:
* Lossless: No information is removed from the file. Compressing a file and decompressing it leaves something identical to the original.
* Lossy: Information might be removed from the file. It is compressed in such a way that uncompressing a file will result in a file that is slightly different from the original. For instance, an image with two subtly different shades of green might be made smaller by treating those two shades as the same. Often, the eye can’t pick out the difference anyway.

Linux provides several tools to compress files; the most common is gzip.

`ikechukwu@ubuntu-22-04-3:~/Documents$ ls -l longfile*` </br>
`-rw-r--r-- 1 ikechukwu ikechukwu 66540 Dec 20  2017 longfile.txt` </br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ gzip longfile.txt` </br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ ls -l longfile*` </br>
`-rw-r--r-- 1 ikechukwu ikechukwu 341 Dec 20  2017 longfile.txt.gz`

Compressed files can be restored to their original form using either the gunzip command or the gzip –d command. This process is called decompression.

`ikechukwu@ubuntu-22-04-3:~/Documents$ gunzip longfile.txt.gz` </br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ ls -l longfile*` </br>
`-rw-r--r-- 1 ikechukwu ikechukwu 66540 Dec 20  2017 longfile.txt` </br>

The `tar` command has three modes that are helpful to become familiar with:

* Create: Make a new archive out of a series of files.
* Extract: Pull one or more files out of an archive.
* List: Show the contents of the archive without extracting.

The `tar` command has variety of functions depending on the option being utilized in a command. For example; 

- You can archive without compressing, the main compressing options for the `tar` command are -z and -j gz and bz2 respectively. </br>
`tar -cvf archive.tar source` = ARCHIVE ONLY </br>
`tar -czvf archive.tar.gz source` = ARCHIVE AND COMPRESS

- The `tar` command is primarily used to archive files only. However, you can compress a file using the `-z` option. For example; </br>
`tar -czvf archive.tar.gz /etc/` = creates a file where the compressed directory -etc is located. 
`-c` = create an archive.
`-z` = tells tar to compress the archive using gz (file has to be filename.tar.gz)
`-v` = verbose
`-f` = file. </br>
While, </br>
`tar -cjvf archive.tar.bz2 /etc/` </br>
`-j` = tells tar to compress the archive using bz2 (file has to be `filename.tar.bz2`)

- To exclude specific files using a suffix. This command will exclude the .txt and .config files from the archive. </br>
`tar --exclude='*.txt' --exclude='*.config' -czf filename.tar.gz /etc/` 

- To display the date the compressed file was created when listed. </br>
`tar -czvf etc-$(date +%F).tar.gz /etc/`

- To add a file to an existing archive, use the -r option to the tar command. Execute the following commands to perform this action and verify the existence of the new file in the tar archive: </br>
`tar -rvf udev.tar /etc/hosts` = To add to an existing archived file.</br>
`tar -rzvf udev.tar /etc/hosts` = To add to an existing archived file. The z tells tar to compress the archive using gzip.</br>
`tar –tvf udev.tar` = To list an existing archived file. </br>
`tar –tzvf udev.tar` = To list an existing archived file. The z tells tar to compress the archive using gzip.

- To extract a compressed file, use the `-x` option. For example; </br>
  `tar -xzvf archive.tar.gz /etc/` </br>
  `-x` = extract a file. </br>
  `tar -xzvf etc.tar.gz -C my.backup/` </br>
  `-C` = helps extract a file to a specific directory. </br>
  `-t` = to see the content of an archive </br>
  
It should be noted that tar requires the `–f` option to indicate a filename is being passed, while zip and unzip require a filename and therefore don’t need you to inform the command a filename is being passed.

Here's how you would use each command:

For tar, you would typically use:

`tar -cf archive.tar file1 file2`</br>
where `-c` creates a new archive and `-f` specifies the filename.

For zip, you would use:

`zip archive.zip file1 file2` </br>
where `archive.zip` is the filename of the archive being created.

For unzip:

`unzip archive.zip` </br>
where `archive.zip` is the filename of the archive being extracted.

The `zip` command will not recurse into subdirectories by default, which is a different behavior than the `tar` command. If you want tar-like behavior, you must use the `–r` option to indicate recursion is to be used. For example ;

`zip -r archive.zip directory/` 

When extracting files using the `unzip` command, it operates similarly to creating an archive, as its default behavior is to extract files. If the extraction process encounters files with the same names as existing files in the target directory, it provides several options to handle potential conflicts. 

`ikechukwu@ubuntu-22-04-3:~/Documents$ unzip School.zip`  </br>
`Archive:  School.zip`  </br>
  `replace School/Engineering/hello.sh? [y]es, [n]o, [A]ll, [N]one, [r]ename: n`  </br>
  `replace School/Art/linux.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: n`  </br>

This can be avoided by copying the zip file into a new directory:

`ikechukwu@ubuntu-22-04-3:~/Documents$ mkdir tmp` </br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ cp School.zip tmp/School.zip` </br>
`ikechukwu@ubuntu-22-04-3:~/Documents$ cd tmp` </br>
`ikechukwu@ubuntu-22-04-3:~/Documents/tmp$ unzip School.zip` </br>
`Archive:  School.zip` </br>
   `creating: School/` </br>
   `creating: School/Engineering/` </br>
  `inflating: School/Engineering/hello.sh`

Using bzip2 and bunzip2 to compress and uncompress a file is very similar to using gzip and gunzip. The compressed file is created with a .bz2 extension.
`gzip` and `gunzip` = are used to compress and extract a file or directory respectively. (.gz files) </br>
`bzip2` and `bunzip2` = are used to compress and extract a file or directory respectively. (.bz2 files)


## NAVIGATION COMMANDS

Navigation in a Linux system primarily involves moving between directories and exploring the file system. It is important to note these paths in a Linux system; 

Here are some common commands for navigating between directories:

- `cd`: (Change directory) Use this command followed by the name of the directory you want to navigate to. For example:
    - `cd /home/ikechukwu` = This will change the current directory to the directory named "ikechukwu" within the "/home" directory
    - `cd .` = change to the current directory.
    - `cd ..` = change to the parent directory.
    - `cd -` = changing the current directory to the last directory
- `pwd`: Printing the current working directory. This command shows you the full path of the current directory you are in.
- `ls`: List directory contents. This command lists the files and directories in the current directory. For example:
    - `ls /home/ikechukwu` = lists the contents of the directory named "ikechukwu".
    - `ls -l /home/ikechukwu` = lists the contents of the directory named "ikechukwu" in a long listing format.
    - `ls -lhS /etc/` = Shows the content of the etc dir in a human-readable format (-h) and sorted by file size in descending order (-S).
    - `ls -ld` = This command lists information about the current working directory without recursively listing its contents.
- `mkdir`: This command is used to create a directory.  
    - `mkdir -p /ikechukwu/solidity` = It creates the directory Ikechukwu with a directory solidity. The `-p` option ensures that if the parent directories (ikechukwu) do not exist, they will be created recursively.
    - `mkdir -v /ikechukwu/solidity` = The `-v` option is used to make the `mkdir` command operate in "verbose" mode, which means it will display a message for each directory it creates, showing the name of the directory.
- `mv`: The mv command in Linux is used to move or rename files and directories.
    - `mv ./Odoemenam/us.txt ./Ikechukwu` = This command moves the file us.txt from the directory Odoemenam to the directory Ikechukwu.
    - `mv ./Odoemenam ./Ikechukwu` = This command renames the directory Odoemenam to Ikechukwu.
    - `mv -i source destination` = The -i option activates interactive mode, prompting the user for confirmation before overwriting existing files or performing any other action.

Listed below are the commands utilized for accessing a file:

`cat, less, more, head, tail, vim, nano`

- `cat`: The `cat` command is a simple utility for viewing the content of a file. It's often used to display the entire contents of a file.
    - e.g. `cat ./filename` = This displays the contents of the file named "filename" which is located in the current directory
- `less`: The `less` command is a pager that allows you to view files one page at a time. It provides navigation and search capabilities for larger files. To navigate in `less`, you can use the arrow keys, Page Up, Page Down, and the / or ? key to search.
    - e.g. `less ../filename` = allows you to view the contents of the file named "filename" which is located in the parent directory (one level up) relative to your current directory
- `more`: Similar to `less`, the `more` command also allows viewing files one page at a time. While it has fewer features than the `less` command, however, the `less` command isn't included with all Linux distributions. The `more` command is always available.
    - e.g. `more filename`
- `head`: The `head` command as mentioned earlier displays the beginning (or top) of a file. By default, it shows the first 10 lines of a file.
    - e.g. `head filename`
- `tail`: The tail command displays the end (or bottom) of a file. By default, it shows the last 10 lines of a file. However, you can specify a different number of lines to display using the -n option followed by the desired number of lines.
    - e.g. `tail -n 2 /etc/syslog` = Shows the last two lines.
    - `tail -n +20 /etc/syslog` = shows the lines from the 20th to the last.
- `touch`: This command is used to create a file. If the file already exists, touch updates the file's access and modification timestamps to the current time.
    - `touch file1.txt file2.txt file3.txt` = This command creates three new empty files named file1.txt, file2.txt, and file3.txt in the current directory.

## COMPARING FILES

- `cmp`: Compares the contents of two files byte by byte. If the files are identical, no output is displayed. For example;</br>
    `cmp /usr/bin/ls ./ls` = Compares the ls file in the bin directory with a file created names ls. When similar, does not give any output. 
- `sha256`: Calculates the SHA-256 hash of each file and displays the difference if they are not identical. For example;</br>
    `sha256 /usr/bin/ls ./ls` = shows the difference in the hash
- `diff`: Used primarily for comparing text files. It shows the actual differences between two files line by line. For example;</br>
    `diff linux.txt ours.txt` = The output e.g. `1c1,17` means that the first line in the initial file should be replaced with the 1 - 17th
    lines in the latter file to make them similar.  </br>
    `diff -y /etc/ssh/sshd_config ./sshd_config` = The `-y` option juxtaposes the selected files and shows the contents side by side.

## HISTORY

To view a limited number of commands, the history command can take a number as a parameter to display exactly that many recent entries. 

The bash shell keeps track of the command history for each user in a file, typically located at .bash_history. The number of commands stored in this file is controlled by the `HISTFILESIZE` (case sensitive) environment variable, while `HISTSIZE` (case sensitive) controls the number of commands stored in memory.

To manipulate history, various commands and techniques are available:

`!ping`: selects the last occurrence of the ping command in the history list. </br>
`!10`: selects the 10th command in the history list.</br>
`!ping:p`: prints the last ping command without executing it.</br>
`history -d <line number>`: deletes a particular command from the history.</br>
`history -c`: clears the entire history.

Additionally, the `$HISTCONTROL` environment variable allows control over history list behavior, with options like ignorespace, ignoredups, ignoreboth, and erasedup.

* ignorespace: lines that begin with a space are not saved.
* ignoredups: lines that match the previous line are not saved.
* ignoreboth: shorthand for ignorespace and ignoredups.
* erasedups: all previous lines matching the current line are removed from the history.

`echo “HISTCONTROL=ignoreboth” >> .bashrc`: This command appends the command to the shell instructing the shell to ignore duplicate commands and commands preceded by spaces when recording command history.

## TIME STAMPS

Every file on Linux has three timestamps:

1. The access timestamp or `atime` is the last time the file was read (`Is -lu`)
2. The modified timestamp or `mtime` is the last time the contents of the file was modified
(`Is -1`, `ls -It`)
3. The changed timestamp `ctime` is the last time when some metadata related to the file
was changed (`Is -Ic`)

The `stat` command shows the access, modification, and change information. 

The `touch` command is used to alter some of the `stat` information. 

`touch -m filename` = modifies the modification and the change time to the current system time.  </br>
`touch -t file name` = always followed by a date format which modifies the date for the specified date selection. </br>
`touch -d “date format” file name` = This changes both the access and modification time to a specified date. </br>
`touch -a` = change only access time </br>
`touch filename` = changes access time, modification time, change time. 

The -d and -t options in commands like `touch` or `date` indeed allow for specifying different date/time formats: 

-d = “year-month-day hour:minute:second” For example; </br> 
`touch -d "2023-07-15 14:30:00" filename` </br>
-t = "yearmonthdayhourminute.second" For example; </br> 
`touch -t 202307151430.00 filename`</br>
-r = to make two files share the same timestamps. For example; </br> 
`touch -r file1.txt file2.txt`

## LINKS

Consider a scenario where there is a file deeply buried in the file system called:

`/usr/share/doc/superbigsoftwarepackage/data/2013/october/tenth/valuable-information.txt`

Another user routinely updates this file, and you need to access it regularly. The long file name is not an ideal choice for you to type, but the file must reside in this location. It is also updated frequently, so you can't simply make a copy of the file.
In a situation like this, links come in handy. You can create a file that is linked to the one that is deeply buried. This new file could be placed in the home directory or any other convenient location. When you access the linked file, it accesses the contents of the valuable-information.txt file.
Each linking method, hard and symbolic, results in the same overall access, but uses different techniques. There are pros and cons to each method, so knowing both techniques and when to use them is important.

#### **CREATING HARD LINKS**

For every file created, there is a block of data on the file system that stores the metadata of the file. Metadata includes information about the file like the permissions, ownership, and timestamps. Metadata does not include the file name or the contents of the file, but it does include just about all other information about the file. This metadata is called the file's **inode table**.

Every file on a partition has a unique identification number called an inode number. The ls -i command displays the inode number of a file.

`ikechukwu@ubuntu-22-04-3:~$ ls -i /tmp/file.txt`                                    
`215220874 /tmp/file.txt`  

Like users and groups, what defines a file is not its name, but rather the number it has been assigned.　For each file, there is also an entry that is stored in a directory's data area (data block) that links the file's name with its inode number. Eg

| File Name | Inode Number |
|----------|----------|
| passwd | 123 |
| group | 144 |

Hard links are two file names that point to the same inode. For example, consider the following directory entries:

| File Name | Inode Number |
|----------|----------|
| passwd | 123 |
| mypasswd | 123 |
| group | 144 |

Because both the passwd and mypasswd files have the same inode number, they essentially are the same file. You can access the file data using either file name.

To create hard links, the ln command is used with two arguments. The first argument is an existing file name to link to, called a target, and the second argument is the new file name to link to the target.

When the ln command is used to create a hard link, the link count number increases by one for each additional filename:

`ikechukwu@ubuntu-22-04-3:~$ ln file.original file.hard.1`</br> 
`ikechukwu@ubuntu-22-04-3:~$ ls -li file.*`</br> 
`278772 -rw-rw-r--. 2 sysadmin sysadmin 5 Oct 25 15:53 file.hard.1`</br> 
`278772 -rw-rw-r--. 2 sysadmin sysadmin 5 Oct 25 15:53 file.original`

To find the other linked files with the inode number, run the command;
`find . -inum 3151382`

#### **CREATING SYMBOLIC LINKS**

A symbolic link, also called a soft link, is simply a file that points to another file.

To create a symbolic link, use the `-s` option with the `ln` command:

`ln -s target link_name`

`ikechukwu@ubuntu-22-04-3:~$  ln -s /etc/passwd mypasswd`</br>
`ikechukwu@ubuntu-22-04-3:~$  ls -l mypasswd`</br>
`lrwxrwxrwx. 1 sysadmin sysadmin 11 Oct 31 13:17 mypasswd -> /etc/passwd`

N/B: A symbolic link has an l as the file type lrwxrwxrwx, while a hard link doesn’t. 

## SORT

Sorting in Linux refers to arranging data in a specified order, typically alphabetically or numerically, using the `sort` command. This command is versatile and allows for various sorting options and configurations.

`sort -k3 -t ”:” -r -n /etc/passwd`

* -k3: Specifies that sorting should be based on the third field.
* -t ":": Specifies: as the field delimiter.
* -r: Specifies that sorting should be done in reverse order.
* -n: Specifies that sorting should be done numerically.

To sort first by the operating system (field #2) and then by year (field #1) and then by last name (field #3), use the following command:

`ikechukwu@ubuntu-22-04-3:~/Documents$ sort -t, -k2 -k1n -k3 os.csv` </br>
`1991,Linux,Torvalds`</br>
`1987,Minix,Tanenbaum`</br>
`1970,Unix,Richie`


| Option | Function |
|----------|----------|
| -t |	Specifies the comma character as the field delimiter |
| -k2 |	Sort by field #2 |
| -k1n |	Numerically sort by field #1 |
| -k3 |	Sort by field #3 |

## TEXT EDITORS

Most Linux systems provide a choice of text editors which are commonly used at the console to edit configuration files. The two main applications are Vi (or the more modern Vim) and Emacs. Both Vi and Emacs are complex and have a steep learning curve, which is not helpful for simple editing of a small text file. Therefore, Pico and Nano are available on most systems and provide very basic text editing.

The mode of operation in Vim can be categorized into Command mode, Insert mode, and Last Line mode.

- Command Mode: Upon opening Vim, you're in Command mode. Here, characters are interpreted as commands. Common commands include: </br></br>
  -  X: Deletes characters under the cursor.</br>
  -  R: Replaces the character under the cursor.</br>
  -  :: Moves the cursor to the Last Line mode.</br>
  -  :w!: Saves the file without closing Vim.</br>
  -  :q!: Closes Vim without saving.</br>
  -  :wq! or Shift + zz: Saves the file and closes Vim.</br>
  -  Pressing the Esc button takes you back to Command mode.

- Insert Mode: Press i, I, a, A, o, or O to enter Insert mode. Common insert commands include:</br></br>
  - i: Inserts text before the cursor.</br>
  - I: Insert text at the beginning of the current line.</br>
  - o: Insert text on a new line below the current line.</br>
  - O: Inserts text on a new line above the current line.</br>
  - a: Inserts text after the cursor.</br>
  - A: Appends text at the end of the line.

- Last Line Mode: Accessed by typing: in Command mode, Last Line mode is used for commands that apply to the entire file or for performing actions like searching and replacing. Common Last Line mode commands include:</br></br>
  -  :%s/string/replacement/g: Search for a pattern and replace all occurrences.</br>
  -  :e!: Undo everything done since the last save.</br>
  -  u: Undo the last event.</br>
  -  Ctrl + R: Redo.</br>
  -  dd: Cut. </br>
  -  p: Paste.</br>
  -  10 + dd: Cut 10 lines from the cursor.</br>
  -  V: Highlight text for copying.</br>
  -  y: Copy.</br>
  -  G: Moves to the bottom of the file.</br>
  -  gg: Moves to the first line of the file.</br>
  -  :set nu: Enables line numbering.</br>
  -  :set nonu: Disables line numbering.</br>
  -  :syntax off: Disables syntax coloring.</br>
  -  :syntax on: Enables syntax coloring.</br>
  -  :number: Jumps to a specific line number.
 

Press each of the following keys once or twice and observe how the cursor moves. Remember that you are in command mode:+wq!+

 | Key | Function |
 |-------|-------|
| j |	Moves cursor down one line (same as down arrow) |
| k |	Moves cursor up line (same as up arrow) |
| l |	Moves cursor to the right one character (same as right arrow) |
| h |	Moves the cursor to the left one character (same as a left arrow) |
| w |	Moves cursor to the beginning of next word |
| e |	Moves cursor to end of word |
| b |	Moves cursor to the beginning of the previous word |


| Keys | Function |
|-------|-------|
| $ |	Moves cursor to end of the current line (same as End key) |
| 0 (zero) | Moves the cursor to the beginning of the current line (same as the Home key) |
| 3G |	Jumps to the third line (nG jumps to the nth line) |
| 1G |	Jumps to the first-line |
| Shift+G |	Jumps to the last line |


Additionally, you can customize Vim settings by creating a `.vimrc` configuration file in your home directory.

Different command line options can be used to open multiple files simultaneously or to display files in split windows for comparison, such as -o or -d for `vimdiff` mode.

To practice Vim, you can run `vimtutor` in your terminal.

