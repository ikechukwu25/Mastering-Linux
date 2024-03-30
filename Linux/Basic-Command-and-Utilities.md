# WHY USE THE TERMINAL?

Linux users prefer the terminal over GUI for its efficiency, flexibility, and power. Unlike other operating systems, Linux offers a vast array of command-line utilities for advanced system administration, scripting, and automation. Knowing these commands is essential for managing Linux systems effectively, enabling tasks such as remote access, resource-efficient operations, and a deeper understanding of the operating system's internals. The terminal fosters a culture of learning and understanding, encouraging users to interact directly with the system and develop proficiency in command-line operations. This preference reflects Linux's heritage as a system designed for experienced users and administrators who value control, customization, and the ability to work efficiently at the command line.

Below are a list of the basic Linux commands and their utilities; 

### COPYING FILES

To copy files in Linux, users commonly employ the `cp` command. It's simple yet versatile, allowing for the duplication of files and directories within the file system. For instance, `cp file1.txt directory/` copies `file1.txt` into the specified directory.

Two options can be used to safeguard against accidental overwrites. With the -i interactive option, the cp command prompts the user before overwriting a file. The following example demonstrates this option, first restoring the content of the original file:

ikechukwu@ubuntu:~$ `cp -i /etc/hosts example.txt`                  
`cp: overwrite '/home/sysadmin/example.txt'?`

NB: Also, users should use the -i option when deleting multiple files: eg: `rm -i /etc/ssh/ssdh_config`

### MONITORING

The `watch` command in Linux is used to execute a command periodically and display its output in real time. It continuously runs the specified command at regular intervals (usually every 2 seconds by default) and updates the terminal with the latest output. This is particularly useful for monitoring system changes, observing the progress of long-running processes, or keeping track of dynamic data. For example;

`watch -n 1 -d ifconfig`:  is used to continuously monitor and display the output of the `ifconfig` command with a 1-second refresh rate (-n 1) and with differences highlighted (-d)

`watch -n 1 -d ls`: is used to continuously monitor and display the output of the current directory with a 1-second refresh rate (-n 1) and with differences highlighted (-d)

### REDIRECTION

In Linux, the ">" symbol is used for output redirection, allowing users to redirect the output of a command to a file. This simple yet powerful feature enables efficient file creation and manipulation. For example;

`ls -l > ls.txt` =  a new file is created and the ls -l command is now seen when the ls.txt file is opened. 

To redirect another command to the same file and not overwrite = `ls -l > ls.txt`

> = overwrite
>> = append

### VIEWING FILES USING A PAGER

While viewing small files with the cat command poses no problems, it is not an ideal choice for large files. The cat command doesn't provide any easy ways to pause and restart the display, so the entire file contents are dumped onto the screen.

For larger files, use a pager command to view the contents. Pager commands display one page of data at a time, allowing you to move forward and backward in the file by using movement keys.

There are two commonly used pager commands:
* The command provides a very advanced paging capability. It is usually the default pager used by commands like the `man` command.
* The `more` command has been around since the early days of UNIX. While it has fewer features than the `less` command, however, the `less` command isn't included with all Linux distributions. The `more` command is always available.

### FILE PREVIEWING AND TAILING.

The head and tail commands are used to display only the first few or last few lines of a file, respectively (or, when used with a pipe, the output of a previous command). By default, the head and tail commands display ten lines of the file that is provided as an argument.

- Negative Value Option: 
Traditionally in UNIX, the number of lines to output would be specified as an option with either command, so -3 is meant to show three lines. For the tail command, either -3 or -n -3 still means show three lines.

However, the GNU version of the head command recognises -n -3 as showing all but the last three lines, and yet the head command still recognizes the option -3 as show the first three lines.

- Positive Value Option: 
The GNU version of the tail command allows for a variation of how to specify the number of lines to be printed. If the -n option is used with a number prefixed by the plus sign, then the tail command recognizes this to mean to display the contents starting at the specified line and continuing all the way to the end.

For example: 
`ls /etc/ssh | nl | tail -5`
* The ls /etc/ssh command lists the contents of the /etc/ssh directory.
* nl numbers the lines of the output.
* tail -5 displays the last 5 lines of the numbered output.
  

Live file changes can be viewed by using the `-f` option to the tail command—useful when you want to see changes to a file as they are happening. 

### LOCATING FILES

- Locate:
To locate files efficiently, you can utilize the `locate` and `find` commands. Begin by installing `locate` if not already available on your system `sudo apt install locate`. "Locate" efficiently finds strings within absolute path names by searching its own database. Remember to update the database with `sudo updatedb` before searching for newly created files. For example
  - `locate -b string` = searches for files with the strings in their name. 
  - `locate -b "\string"` =  does not use the default *name* searches system but searches for the exact string. 

- Which: 
The `which` command helps find the location of an executable command. For example;
  - `which ls` will display the location of the ls command.
  - `which cd` won't display anything since cd is a shell built-in command, not an executable.
  - `which -a locate` will display all instances of the locate command found in the PATH.

- Find: 
The find command in Linux is a powerful utility for searching files and directories based on various criteria within a directory hierarchy. It allows users to locate files by specifying conditions such as filenames, modification times, ownership, and more. For example; </br>
  - `find . -name linux.txt` : This command searches for files named "linux.txt" starting from the current directory (.) and displays the path to each file found.
  - `find -iname "*Pub*"` : This command searches for files with names containing "Pub" (ignoring case due to -i). The asterisks (*) are wildcards, allowing for matches with any characters before and after "Pub".
  - `find -name "*txt*"`: This command finds files with names containing the string "txt" (case-sensitive). Again, the asterisks act as wildcards, matching any characters before and after "txt".

