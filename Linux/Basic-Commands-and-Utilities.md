# WHY USE THE TERMINAL?

Linux users prefer the terminal over GUI for its efficiency, flexibility, and power. Unlike other operating systems, Linux offers a vast array of command-line utilities for advanced system administration, scripting, and automation. Knowing these commands is essential for managing Linux systems effectively, enabling tasks such as remote access, resource-efficient operations, and a deeper understanding of the operating system's internals. The terminal fosters a culture of learning and understanding, encouraging users to interact directly with the system and develop proficiency in command-line operations. This preference reflects Linux's heritage as a system designed for experienced users and administrators who value control, customization, and the ability to work efficiently at the command line.


# BASIC COMMANDS AND THEIR UTILITIES. 

Basic commands in a terminal environment serve as fundamental tools for users to interact with their operating systems efficiently. From listing files with 'ls' to navigating directories with 'cd,' manipulating files with 'cp' and 'rm,' and performing system tasks with 'pwd' and 'mkdir,' these commands empower users to accomplish various tasks seamlessly. Understanding these commands and their utilities is fundamental for effective system administration and development workflows.

## COPYING FILES

To copy files in Linux, users commonly employ the `cp` command. It's simple yet versatile, allowing for the duplication of files and directories within the file system. For instance, `cp file1.txt directory/` copies `file1.txt` into the specified directory.

Two options can be used to safeguard against accidental overwrites. With the `-i` interactive option, the cp command prompts the user before overwriting a file. The following example demonstrates this option, first restoring the content of the original file:

`ikechukwu@ubuntu:~$ cp -i /etc/hosts example.txt`                  
`cp: overwrite '/home/sysadmin/example.txt'?`

NB: Also, users should use the `-i` option when deleting multiple files: eg: `rm -i /etc/ssh/ssdh_config`

## MONITORING

The `watch` command in Linux is used to execute a command periodically and display its output in real time. It continuously runs the specified command at regular intervals (usually every 2 seconds by default) and updates the terminal with the latest output. This is particularly useful for monitoring system changes, observing the progress of long-running processes, or keeping track of dynamic data. For example;

`watch -n 1 -d ifconfig`:  is used to continuously monitor and display the output of the `ifconfig` command with a 1-second refresh rate (-n 1) and with differences highlighted (-d)

`watch -n 1 -d ls`: is used to continuously monitor and display the output of the current directory with a 1-second refresh rate (-n 1) and with differences highlighted (-d)

## REDIRECTION

In Linux, the ">" symbol is used for output redirection, allowing users to redirect the output of a command to a file. This simple yet powerful feature enables efficient file creation and manipulation. For example;

`ls -l > ls.txt` =  a new file is created and the `ls -l` command is now seen when the ls.txt file is opened. 

To redirect another command to the same file and not overwrite = `ls -l > ls.txt`

'>' = overwrite </br>
'>>' = append

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

For example: 
`ls /etc/ssh | nl | tail -5`
* The `ls /etc/ssh` command lists the contents of the /etc/ssh directory.
* nl numbers the lines of the output.
* tail -5 displays the last 5 lines of the numbered output.
  

Live file changes can be viewed by using the `-f` option to the tail command—useful when you want to see changes to a file as they are happening. 

## LOCATING FILES

- Locate:
To locate files efficiently, you can utilize the `locate` and `find` commands. Begin by installing `locate` if not already available on your system `sudo apt install locate`. "Locate" efficiently finds strings within absolute path names by searching its own database. Remember to update the database with `sudo updatedb` before searching for newly created files. For example
  - `locate -b string` : searches for files with the strings in their name. 
  - `locate -b "\string"` :  does not use the default *name* searches system but searches for the exact string. 

- Which: 
The `which` command helps find the location of an executable command. For example;
  - `which ls` : will display the location of the ls command.
  - `which cd` : won't display anything since cd is a shell built-in command, not an executable.
  - `which -a locate` : will display all instances of the locate command found in the PATH.

- Find: 
The find command in Linux is a powerful utility for searching files and directories based on various criteria within a directory hierarchy. It allows users to locate files by specifying conditions such as filenames, modification times, ownership, and more. For example; </br>

  - `find . -name linux.txt` : This command searches for files named "linux.txt" starting from the current directory (.) and displays the path to each file found.
  - `find -iname "*Pub*"` : This command searches for files with names containing "Pub" (ignoring case due to -i). The asterisks (*) are wildcards, allowing for matches with any characters before and after "Pub".
  - `find -name "*txt*"`: This command finds files with names containing the string "txt" (case-sensitive). Again, the asterisks act as wildcards, matching any characters before and after "txt".
  - Find and Exec : 
When the `find` command is combined with the -exec option, it allows users to perform actions on the files or directories found. For example:</br>
  `sudo find /etc/ -type f -mtime 0 -exec cp {} /root/backup \;`: This copies the files that have been generated by the `find`
  command which is being put in the curly brackets before being executed by the exec command to copy (cp) </br>
  `sudo find /etc/ -type f -mtime 0 -ok cp {} /root/backup \;` : Similar to the previous command, this one also finds files modified within the last 24 hours in the /etc/ directory. However, instead of directly executing the cp command, the ok option prompts the user for confirmation before executing the cp command for each found file. </br>
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

## FILE PATHS

Paths in the Linux file system are indeed divided into two categories: Absolute paths and Relative paths.

- Absolute Path:
An absolute path specifies the exact location of a file or directory in the file system hierarchy.
It begins from the root directory (/) and includes all directories leading to the target file or directory.
Example: `/var/log` is an absolute path that specifies the location of the log directory within the var directory.

- Relative Path:
A relative path specifies the location of a file or directory relative to the current working directory.
It does not begin with the root directory (/).
Example: If the current working directory is `/home/user`, then `./Documents/file.txt` is a relative path that specifies the location of the `file.txt` within the Documents directory relative to the current directory.

Special Directory References: These symbols provide convenient ways to reference specific directories in relation to the current working directory or the user's home directory, particularly while using a relative path.

- .  = the current working directory
- .. = the parent directory
- ~  = the user's home directory
- /  = the root directory 

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
- `mkdir` : 

Listed below are the commands utilized for accessing a file:

cat, less, more, head, tail, vim, nano

- `cat`: The `cat` command is a simple utility for viewing the content of a file. It's often used to display the entire contents of a file.
    - e.g. `cat ./filename` = This displays the contents of the file named "filename" which is located in the current directory
- `less`: The `less` command is a pager that allows you to view files one page at a time. It provides navigation and search capabilities for larger files. To navigate in `less`, you can use the arrow keys, Page Up, Page Down, and the / or ? key to search.
    - e.g. `less ../filename` = allows you to view the contents of the file named "filename" which is located in the parent directory (one level up) relative to your current directory
- `more`: Similar to `less`, the `more` command also allows viewing files one page at a time. While it has fewer features than the `less` command, however, the `less` command isn't included with all Linux distributions. The `more` command is always available.
    - e.g. `more filename`
- `head`: The `head` command as mentioned earlier displays the beginning (or top) of a file. By default, it shows the first 10 lines of a file.
    - e.g. `head filename`
- `tail` : The tail command displays the end (or bottom) of a file. By default, it shows the last 10 lines of a file. However, you can specify a different number of lines to display using the -n option followed by the desired number of lines.
    - e.g. `tail -n 2 /etc/syslog` = Shows the last two lines.
    - `tail -n +20 /etc/syslog` = shows the lines from the 20th to the last.

## COMPARING FILES

- cmp: Compares the contents of two files byte by byte. If the files are identical, no output is displayed. For example;</br>
    `cmp /usr/bin/ls ./ls` = Compares the ls file in the bin directory with a file created names ls. When similar, does not give any output. 
- sha256: Calculates the SHA-256 hash of each file and displays the difference if they are not identical. For example;</br>
    `sha256 /usr/bin/ls ./ls` = shows the difference in the hash
- diff: Used primarily for comparing text files. It shows the actual differences between two files line by line. For example;</br>
    `diff linux.txt ours.txt` = The output e.g. `1c1,17` means that the first line in the initial file should be replaced with the 1 - 17th
    lines in the latter file to make them similar.  </br>
    `diff -y /etc/ssh/sshd_config ./sshd_config` = The `-y` option juxtaposes the selected files and shows the contents side by side.

## HISTORY

The bash shell keeps track of the command history for each user in a file, typically located at .bash_history. The number of commands stored in this file is controlled by the `HISTFILESIZE` (case sensitive) environment variable, while `HISTSIZE` (case sensitive) controls the number of commands stored in memory.

To manipulate history, various commands and techniques are available:

`!ping`: selects the last occurrence of the ping command in the history list.
`!10`: selects the 10th command in the history list.
`!ping:p`: prints the last ping command without executing it.
`history -d <line number>`: deletes a particular command from the history.
`history -c`: clears the entire history.

Additionally, the $HISTCONTROL environment variable allows control over history list behavior, with options like ignorespace, ignoredups, ignoreboth, and erasedup.

* ignorespace: lines that begin with a space are not saved.
* ignoredups: lines that match the previous line are not saved.
* ignoreboth: shorthand for ignorespace and ignoredups.
* erasedups: all previous lines matching the current line are removed from the history.

`echo “HISTCONTROL=ignoreboth” >> .bashrc`: This command appends the command to the shell.

## TIME STAMPS

Every file on Linux has three timestamps:

1. The access timestamp or `atime` is the last time the file was read (`Is -lu`)
2. The modified timestamp or `mtime` is the last time the contents of the file was modified
(`Is -1`, `ls -It`)
3. The changed timestamp `ctime` is the last time when some metadata related to the file
was changed (`Is -Ic`)

The `stat` command shows the access, modification, and change information. 

The `touch` command is used to alter some of the `stat` information. 

`touch -m filename` = modifies the modification and the change time to the current system time. 
`touch -t file name` = always followed by a date format which modifies the date for the specified date selection. 
`touch -d “date format” file name` = This changes both the access and modification time to a specified date. 
`touch -a` = change only access time
`touch filename` = changes access time, modification time, change time. 

The -d and -t options in commands like `touch` or `date` indeed allow for specifying different date/time formats: 

-d = “year-month-day hour:minute:second” For example; </br> 
`touch -d "2023-07-15 14:30:00" filename`
-t = "yearmonthdayhourminute.second" For example; </br> 
`touch -t 202307151430.00 filename`
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

A symbolic link has an l as the file type lrwxrwxrwx, while a hard link doesn’t. 

## SORT

Sorting in Linux refers to arranging data in a specified order, typically alphabetically or numerically, using the `sort` command. This command is versatile and allows for various sorting options and configurations.

`sort -k3 -t ”:” -r -n /etc/passwd`

* -k3: Specifies that sorting should be based on the third field.
* -t ":": Specifies : as the field delimiter.
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

- Last Line Mode: Accessed by typing : in Command mode, Last Line mode is used for commands that apply to the entire file or for performing actions like searching and replacing. Common Last Line mode commands include:</br></br>
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

Additionally, you can customize Vim settings by creating a .vimrc configuration file in your home directory.

Different command line options can be used to open multiple files simultaneously or to display files in split windows for comparison, such as -o or -d for `vimdiff` mode.

To practice Vim, you can run `vimtutor` in your terminal.

