# LINUX FILE SYSTEM

The Linux file system is a hierarchical structure that organizes and stores data on a Linux-based operating system. It provides a unified way to manage files, directories, devices, and other resources.


### DIRECTORY STRUCTURE

On a Windows system, the top level of the directory structure is called My Computer. Physical devices, such as hard drives, USB drives, and network drives, show up under My Computer and are each assigned a drive letter, such as C: or D:

Like Windows, the Linux directory structure, typically called a filesystem, also has a top level. However instead of My Computer, it is called the root directory, and it is symbolized by the slash (/) character. Additionally, there are no drives in Linux; each physical device is accessible under a directory, as opposed to a drive letter.

Most of the hidden files are customization files, designed to customize how Linux, your shell, or programs work. For example, the .bashrc file in the home directory customizes features of the shell, such as creating or modifying variables and aliases.


### FILESYSTEM HIERARCHY STANDARD

The FHS standard categorizes each system directory in a couple of ways:

* A directory can be categorized as either shareable or not, referring to whether the directory can be shared on a network and used by multiple machines.
* The directory is put into a category of having either static files (file contents won't change) or variable files (file contents can change).

The FHS standard defines four hierarchies of directories used in organizing the files of the filesystem. The top-level or root hierarchy follows:

| Directory	| Contents |
|--------|--------|
| /	| The base of the structure, or root of the filesystem, this directory unifies all directories regardless of whether they are local partitions, removable devices, or network shares |
| /bin |	Essential binaries like the ls, cp, and rm commands, and be a part of the root filesystem |
| /boot |	Files necessary to boot the system, such as the Linux kernel and associated configuration files |
| /dev |	Files that represent hardware devices and other special files, such as the /dev/null and /dev/zero files |
| /etc |	Essential host configurations files such as the /etc/hosts or /etc/passwd files |
| /home |	User home directories |
| /lib |	Essential libraries to support the executable files in the /bin and /sbin directories |
| /lib64 |	Essential libraries built for a specific architecture. For example, the /lib64 directory for 64-bit AMD/Intel x86 compatible processors |
| /media |	Mount point for removable media mounted automatically |
| /mnt |	Mount point for temporarily mounting filesystems manually |
| /opt |	Optional third-party software installation location |
| /proc |	Virtual filesystem for the kernel to report process information, as well as other information |
| /root |	Home directory of the root user |
| /sbin |	Essential system binaries primarily used by the root user |
| /sys |	Virtual filesystem for information about hardware devices connected to the system |
| /srv |	Location where site-specific services may be hosted |
| /tmp |	Directory where all users are allowed to create temporary files and that is supposed to be cleared at boot time (but often is not) |
| /usr |	**Second hierarchy**. Non-essential files for multi-user use |
| /usr/local |	**Third hierarchy**. Files for software not originating from distribution |
| /var |	**Fourth hierarchy**. Files that change over time |
| /var/cache |	Files used for caching application data |
| /var/log |	Most log files |
| /var/lock |	Lock files for shared resources |
| /var/spool |	Spool files for printing and mail |
| /var/tmp |	Temporary files to be preserved between reboots |

The second and third hierarchies, located under the /usr and /usr/local directories, repeat the pattern of many of the key directories found under the first hierarchy or root filesystem. The fourth hierarchy, the /var directory, also repeats some of the top-level directories such as lib, opt and tmp.

While the root filesystem and its contents are considered essential or necessary to boot the system, the /var, /usr and /usr/local directories are deemed non-essential for the boot process. 

The /usr/local hierarchy is for installation of software that does not originate with the distribution. Often this directory is used for software that is compiled from the source code.


#### **Software Application Directories**

Unlike the Windows operating system, where applications may have all of their files installed in a single subdirectory under the C:\ Program Files directory, applications in Linux may have their files in multiple directories spread out throughout the Linux filesystem. For Debian-derived distributions, you can execute the `dpkg -L packagename` command to get the list of file locations. In Red Hat-derived distributions, you can run the `rpm -ql packagename` command for the list of the locations of the files that belong to that application.

The executable program binary files may go in the /usr/bin directory if they are included with the operating system, or else they may go into the /usr/local/bin or /opt/application/bin directories if they came from a third party.

The data for the application may be stored in one of the following subdirectories:
* /usr/share
* /usr/lib
* /opt/application
* /var/lib
The file related to documentation may be stored in one of the following subdirectories:
* /usr/share/doc
* /usr/share/man
* /usr/share/info
The global configuration files for an application are most likely to be stored in a subdirectory under the /etc directory, while the personalized configuration files (specific for a user) for the application are probably in a hidden subdirectory of the user's home directory.


#### **Library Directories**

Libraries are files that contain code that is shared between multiple programs. Most library file names end in a file extension of `.so`, which means "shared object".

The libraries that support the essential binary programs found in the /bin and /sbin directories are typically located in either /lib or /lib64.

To support the /usr/bin and /usr/sbin executables, the /usr/lib and /usr/lib64 library directories are typically used.

For supporting applications that are not distributed with the operating system, the /usr/local/lib and /opt/application/lib library directories are frequently used.


# FILE PATHS IN LINUX

Paths in the Linux file system are indeed divided into two categories: Absolute paths and Relative paths.

- **Absolute Path**:
An absolute path specifies the exact location of a file or directory in the file system hierarchy.
It begins from the root directory (/) and includes all directories leading to the target file or directory.
Example: `/var/log` is an absolute path that specifies the location of the log directory within the var directory.

- Begins from the root directory (/).
- Specifies the location of the syslog file within the log directory, which is within the var directory.

- **Relative Path**:
A relative path specifies the location of a file or directory relative to the current working directory.
It does not begin with the root directory (/).
Example: If the current working directory is `/home/user`, then `./Documents/file.txt` is a relative path that specifies the location of the `file.txt` within the Documents directory relative to the current directory.

- Starts with ./, indicating the current working directory.
- Specifies the location of the file.txt within the Documents directory relative to the current directory.

**Special Directory References**: These symbols provide convenient ways to reference specific directories in relation to the current working directory or the user's home directory, particularly while using a relative path.

- .  = the current working directory
- .. = the parent directory
- ~  = the user's home directory
- /  = the root directory


# FILE TYPES IN LINUX

In the Linux ecosystem, files serve as the building blocks of the operating system, storing data, configurations, programs, and more. Each file type has its own unique attributes and behaviors, crucial for understanding and effectively managing the system. Knowing the various file types in a Linux system is crucial for understanding their features and functions. 

#### **File Type Indicators**: These symbols are often referred to as file type indicators or file mode indicators. They provide information about the type of file or special file in a Unix-like operating system such as Linux. 

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


#### **Useful Commands**: Commands like `ls` and `file` are instrumental in providing detailed information about file types and attributes. They empower users and system administrators to efficiently manage and interact with the file system. Examples:

`ls -lF /etc/`: This command lists the contents of the /etc/ directory with detailed information about each entry. </br>
The `-l` option provides a long listing format, showing file permissions, ownership, size, modification time, and name.</br>
The `-F` option appends special characters to entries to indicate their file types:</br>

Directories are marked with a trailing slash (/).</br>
Executable files are marked with an asterisk (*).</br>
Symbolic links are marked with an at sign (@).</br>
Socket files are marked with an equal sign (=).</br>
Named pipes (FIFOs) are marked with a vertical bar (|).

`file /etc/*`: This command displays information about the file types of all entries within the /etc/ directory.</br>
The file command examines the contents of each file and attempts to determine its type based on magic numbers, file signatures, and other characteristics.</br>
By specifying /etc/*, the command examines all files within the /etc/ directory.</br>
The output includes descriptive information about each file's type, such as ASCII text, directory, symbolic link, shell script, etc.


# VIEWING FILES

Viewing files in Linux can be accomplished using various commands, these commands offer flexibility and convenience in viewing files of different sizes and formats, catering to the diverse needs of Linux users. Listed below are the primary commands utilized for accessing a file:

`cat, less, more, head, tail, vim`

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


# FILE AND DIRECTORY MANAGEMENT COMMANDS

Creating files and directories is fundamental in managing a Linux system, allowing users to organize data and store information efficiently. Here are some essential commands used for these tasks:

- `touch`: This command is used to create a file. If the file already exists, touch updates the file's access and modification timestamps to the current time.
    - `touch file1.txt file2.txt file3.txt` = This command creates three new empty files named file1.txt, file2.txt, and file3.txt in the current directory.

- `mkdir`: This command is used to create a directory.  
    - `mkdir -p /ikechukwu/solidity` = It creates the directory Ikechukwu with a directory solidity. The `-p` option ensures that if the parent directories (ikechukwu) do not exist, they will be created recursively.
    - `mkdir -v /ikechukwu/solidity` = The `-v` option is used to make the `mkdir` command operate in "verbose" mode, which means it will display a message for each directory it creates, showing the name of the directory.

- `mv`: The mv command in Linux is used to move or rename files and directories.
    - `mv ./Odoemenam/us.txt ./Ikechukwu` = This command moves the file us.txt from the directory Odoemenam to the directory Ikechukwu.
    - `mv ./Odoemenam ./Ikechukwu` = This command renames the directory Odoemenam to Ikechukwu.
    - `mv -i source destination` = The -i option activates interactive mode, prompting the user for confirmation before overwriting existing files or performing any other action.
 

# FILE TIME STAMPS

Every file on Linux has three timestamps:

1. The access timestamp or `atime` is the last time the file was read (`Is -lu`)
2. The modified timestamp or `mtime` is the last time the contents of the file were modified
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


# OUTPUT REDIRECTION

In Linux, the ">" symbol is used for output redirection, allowing users to redirect the output of a command to a file. This simple yet powerful feature enables efficient file creation and manipulation. For example;

`ls -l > ls.txt` =  a new file is created and the `ls -l` command is now seen when the ls.txt file is opened. 

To redirect another command to the same file and not overwrite = `ls -l > ls.txt`

`>` = overwrite </br>
`>>` = append


## ADVANCED CONSTRUCTS FOR STREAM MANAGEMENT:

In Linux command-line operations, managing standard output (stdout) and standard error (stderr) streams is crucial for effective error handling and data processing. Two constructs, `2>&1` and `|&`, provide advanced functionality for handling both the standard output (stdout) and standard error (stderr) streams.

`2>&1`: When the 2>&1 construct is used, it redirects the stderr stream to the stdout stream. This means that error messages generated on stderr are combined with regular output, allowing for unified stream processing.

Example 1: `ls -l /nonexistent 2>&1 > error.log` </br>
In this example, the `ls -l /nonexistent` command generates an error because the directory /nonexistent does not exist. The `2>&1` construct redirects the stderr output to stdout, and > error.log redirects the combined output (stdout and stderr) to a file named error.log.

Example 2: Redirect stderr to stdout and display both on the terminal: `ls -l /nonexistent 2>&1` </br>

`|&`: The `|&` construct is used to combine the stdout and stderr streams using a pipe (|). This enables simultaneous processing of both streams, which is particularly useful for operations where both types of output need to be analyzed or redirected together.

Example: `ls -l /nonexistent |& wc -l`
In this example, the ls -l /nonexistent command generates an error because the directory /nonexistent does not exist. The |& construct combines the stdout and stderr streams and passes them as input to wc -l, which counts the number of lines in the combined output.

These advanced constructs enhance command-line operations by providing flexibility in managing and processing both stdout and stderr streams effectively. They are invaluable tools for error handling, debugging, and data analysis tasks in Linux environments.


## EDITING TEXT FILES: UNDERSTANDING VIM

Most Linux systems provide a choice of text editors which are commonly used at the console to edit configuration files. The two main applications are Vi (or the more modern Vim) and Emacs. Both Vi and Emacs are complex and have a steep learning curve, which is not helpful for simple editing of a small text file. Therefore, Pico and Nano are available on most systems and provide very basic text editing.

However, Vim, or Vi Improved, is a preferred text editor for many users due to its ubiquity across Unix-like systems, efficiency in navigating and editing text with modal editing, high customizability, powerful features such as syntax highlighting and search functionality

Here's an overview of Vim's modes and commands to aid navigation and editing:

The mode of operation in Vim can be categorized into Command mode, Insert mode, and Last Line mode.

- Command Mode: Upon opening Vim, you're in Command mode. Here, characters are interpreted as commands. Common commands include: </br></br>
  - `X`: Deletes characters under the cursor.</br>
  - `R`: Replaces the character under the cursor.</br>
  - `:`: Moves the cursor to the Last Line mode.</br>
  - `:w!`: Saves the file without closing Vim.</br>
  - `:q!`: Closes Vim without saving.</br>
  - `:wq!` or `Shift + zz`: Saves the file and closes Vim.</br>
  - Pressing the Esc button takes you back to Command mode.

- Insert Mode: Press i, I, a, A, o, or O to enter Insert mode. Common insert commands include:</br></br>
  - `i:` Inserts text before the cursor.</br>
  - `I`: Insert text at the beginning of the current line.</br>
  - `o`: Insert text on a new line below the current line.</br>
  - `O`: Inserts text on a new line above the current line.</br>
  - `a`: Inserts text after the cursor.</br>
  - `A`: Appends text at the end of the line.

- Last Line Mode: Accessed by typing: in Command mode, Last Line mode is used for commands that apply to the entire file or for performing actions like searching and replacing. Common Last Line mode commands include:</br></br>
  - `:%s/string/replacement/g`: Search for a pattern and replace all occurrences.</br>
  - `:e!`: Undo everything done since the last save.</br>
  - `u`: Undo the last event.</br>
  - `Ctrl + R`: Redo.</br>
  - `dd`: Cut. </br>
  - `p`: Paste.</br>
  - `10 + dd`: Cut 10 lines from the cursor.</br>
  - `V`: Highlight text for copying.</br>
  - `y`: Copy.</br>
  - `G`: Moves to the bottom of the file.</br>
  - `gg`: Moves to the first line of the file.</br>
  - `:set nu`: Enables line numbering.</br>
  - `:set nonu`: Disables line numbering.</br>
  - `:syntax off`: Disables syntax coloring.</br>
  - `:syntax on`: Enables syntax coloring.</br>
  - `:number`: Jumps to a specific line number.
 
Press each of the following keys once or twice and observe how the cursor moves. Remember that you are in command mode:

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

Different command line options can be used to open multiple files simultaneously or to display files in split windows for comparison, such as `-o` or `-d` for `vimdiff` mode.

To practice Vim, you can run `vimtutor` in your terminal. Here's an example of how to use Vim; 

Open the example.txt file in Vim by typing: `vim example.txt`

You can use the aforementioned insert commands to input text. 


# LINKS

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

Like users and groups, what defines a file is not its name, but rather the number it has been assigned.　For each file, there is also an entry that is stored in a directory's data area (data block) that links the file's name with its inode number. Eg.

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
`278772 -rw-rw-r--. 2 ikechukwu ikechukwu 5 Oct 25 15:53 file.hard.1`</br> 
`278772 -rw-rw-r--. 2 ikechukwu ikechukwu 5 Oct 25 15:53 file.original`

To find the other linked files with the inode number, run the command;
`find . -inum 3151382`


#### **CREATING SYMBOLIC LINKS**

A symbolic link, also called a soft link, is simply a file that points to another file.

To create a symbolic link, use the `-s` option with the `ln` command:

`ln -s target link_name`

`ikechukwu@ubuntu-22-04-3:~$  ln -s /etc/passwd mypasswd`</br>
`ikechukwu@ubuntu-22-04-3:~$  ls -l mypasswd`</br>
`lrwxrwxrwx. 1 ikechukwu ikechukwu 11 Oct 31 13:17 mypasswd -> /etc/passwd`

N/B: A symbolic link has an l as the file type "lrwxrwxrwx", while a hard link doesn’t. 

**DIFFERENCE**

1. Using hard links offers the advantage that every file name pointing to the same file content is equal. If you have multiple files hard linked together, deleting any of them won't delete the actual file contents, as long as at least one hard link remains. This is because each hard link refers to the same unique inode number, ensuring the file data persists as long as at least one hard link exists. In symlink,  if the original file is deleted in a symbol link is deleted as well. 

2. Soft links are much more visual, not requiring any extra commands beyond the ls command to determine the link. If you encounter a regular file with a link count greater than one and need to find its hard links, you can use the find command with the -inum search criteria. First, you would use the `ls -i` command to find the inode number of the file in question. Then, you can use `find` to locate other files with the same inode number.
   
3. Hard links cannot be created between files that reside on different filesystems or partitions because each filesystem or partition has its own set of inodes. </br></br>
`ikechukwu@ubuntu-22-04-3:~$ ln /boot/vmlinuz-2.6.32-358.6.1.el6.i686 Linux.Kernel` </br>
`ln: creating hard link 'Linux.Kernel' => '/boot/vmlinuz-2.6.32-358.6.1.el6.i686': Invalid cross-device link` </br> </br>
In the previous example, a hard link was attempted to be created between a file in the /boot file system and the / file system; it failed because each of these file systems has a unique set of inode numbers that can't be used outside of the filesystem.
However, because a symbolic link points to another file using a pathname, you can create a soft link to a file in another filesystem.

5. Another limitation of hard links is that they cannot be created on directories. The reason for this limitation is that the operating system itself uses hard links to define the hierarchy of the directory structure. While Linking to directories using a symbolic link is permitted: </br></br>
`ikechukwu@ubuntu-22-04-3:~$ ln -s /bin binary`</br> 
`ikechukwu@ubuntu-22-04-3:~$ ls -l binary`</br> 
`lrwxrwxrwx. 1 ikechukwu ikechukwu 11 Oct 31 13:17 binary -> /bin`</br> </br>
Symbolic links do not increase the link count of files with which they are linked. Symbolic link files have their own inode and type of file. Instead of linking and sharing an inode, they link to the file name.


# CREATING A FILE SYSTEM

In computing, a filesystem governs the storage and retrieval of data, organizing files on storage media. Without a filesystem, stored information would be an undifferentiated mass, making it impossible to discern individual pieces. The filesystem assigns names to files, storing data and maintaining a directory of files and directories, including their locations, sizes, and other attributes on the storage medium. The below steps are to be followed to create a filesystem:

1. **Identify the Disk or Partition**: The first you have to do while creating a filesystem is to identify volumes using the command `lsblk`. </br>
The `lsblk` command in Linux is used to list information about all available block devices, including hard drives, USB drives, CD/DVD drives, and partitions.</br></br>
`root@ubuntu-22-04-3:/home/ikechukwu# lsblk` </br>
`NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS` </br>
`sda       8:0    0  465.8G  0 disk ` </br>
`├─sda1    8:1    0   1000M  0 part /boot` </br>
`├─sda2    8:2    0    256M  0 part /boot/efi` </br>
`└─sda3    8:3    0 464.6G  0 part ` </br>
`  ├─vg-root  253:0    0    50G  0 lvm  /` </br>
`  └─vg-home  253:1    0   414G  0 lvm  /home` </br>
`sdb       8:16   0   1.8T  0 disk ` </br>
`sr0     11:0    1   4.7G  0 rom  /media/ikechukwu/Ubuntu 22.04.3 LTS amd641`</br></br>
We will see the main volumes - `sda` which has multiple partitions, `sdb` with one partition and `sr0` with no partition, it represents the first SCSI CD/DVD-ROM device in the system. 

2. **Partition the Disk** - `sudo fdisk /dev/sdb`: When you run sudo fdisk `/dev/sdb`, fdisk will display information about the existing partitions on `/dev/sdb`, if any, and allow you to create, delete, or modify partitions as needed. You can use fdisk commands to interactively manage the disk's partition table.
        - `fdisk`: This is a command-line utility used for disk partitioning. It allows users to create, delete, and manipulate disk partitions on a storage device.
        - `/dev/sdb`: This is the block device representing the entire disk. It could be a physical disk (e.g., a hard drive or SSD) or a virtual disk (e.g., a virtual disk in a virtual machine). The device name is followed by a letter indicating the drive and a number indicating the partition. </br></br>
A prompt pops up when you input the above command - `Command (m for help)`, select `n` to create a new partition, and select 'p' for primary or 'e' for entended. You can choose the default option for the rest. Lastly, you select the size of the partition with a "+" prefix `+40G`. See screenshot below:</br></br>
![image](https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/e9b8c7dc-3c79-4352-8d82-81d431407d65)</br></br>
Press 'p' when the command prompt pops up to make sure the details of the newly created partition are accurate. </br>
Afterwards, press 'w' to save the newly created partition. </br>
To validate the recently created partition, run the `lsblk` command. </br></br>
`root@ubuntu-22-04-3:/home/ikechukwu# lsblk` </br>
`NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS` </br>
`sda       8:0    0  465.8G  0 disk ` </br>
`├─sda1    8:1    0   1000M  0 part /boot` </br>
`├─sda2    8:2    0    256M  0 part /boot/efi` </br>
`└─sda3    8:3    0 464.6G  0 part ` </br>
`  ├─vg-root  253:0    0    50G  0 lvm  /` </br>
`  └─vg-home  253:1    0   414G  0 lvm  /home` </br>
`sdb       8:16   0   1.8T  0 disk ` </br>
` └─sdb1    8:17   0   1.8T  0 part /mnt/data` </br>
`sr0     11:0    1   4.7G  0 rom  /media/ikechukwu/Ubuntu 22.04.3 LTS amd641`</br></br>

3. **Create the Mount Point Directory** - `mkdir testfile`: This command creates a new directory named testfile in the current directory. The `-p` option can be used to create parent directories if they don't already exist.
4. **Create the Filesystem** - `mkfs.ext4 /dev/sdb1`: This command creates an ext4 filesystem on the partition `/dev/sdb1`. It formats the partition, making it ready for use as a filesystem. After running this command, `/dev/sdb1` will contain the ext4 filesystem.
5. **Mount the Filesystem** - `mount /dev/sdb1 testfile/`: This command mounts the filesystem located on `/dev/sdb1` to the directory `testfile/`. After mounting, any files or directories within the filesystem on /dev/sdb1 will be accessible via the `testfile/` directory.
6. **Configure Auto-Mount (Optional)**: To ensure that the filesystem is automatically mounted during system boot, you can add an entry to the `/etc/fstab` file. This file contains information about filesystems and their associated mount points, options, and other parameters.
7. **Unmount the Filesystem (Optional)** - `umount testfile/`: This command unmounts the filesystem previously mounted on the `testfile/` directory. After running this command, the filesystem on `/dev/sdb1` will no longer be accessible via the testfile/ directory.




