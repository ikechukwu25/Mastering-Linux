# WHY USE THE TERMINAL?

Linux users prefer the terminal over GUI for its efficiency, flexibility, and power. Unlike other operating systems, Linux offers a vast array of command-line utilities for advanced system administration, scripting, and automation. Knowing these commands is essential for managing Linux systems effectively, enabling tasks such as remote access, resource-efficient operations, and a deeper understanding of the operating system's internals. The terminal fosters a culture of learning and understanding, encouraging users to interact directly with the system and develop proficiency in command-line operations. This preference reflects Linux's heritage as a system designed for experienced users and administrators who value control, customization, and the ability to work efficiently at the command line.


# BASIC COMMANDS AND THEIR UTILITIES. 

Basic commands in a terminal environment serve as fundamental tools for users to interact with their operating systems efficiently. From listing files with 'ls' to navigating directories with 'cd,' manipulating files with 'cp' and 'rm,' and performing system tasks with 'pwd' and 'mkdir,' these commands empower users to accomplish various tasks seamlessly. Understanding these commands and their utilities is fundamental for effective system administration and development workflows.

## COPYING FILES

To copy files in Linux, users commonly employ the `cp` command. It's simple yet versatile, allowing for the duplication of files and directories within the file system. For instance, `cp file1.txt directory/` copies `file1.txt` into the specified directory.

Two options can be used to safeguard against accidental overwrites. With the `-i` interactive option, the cp command prompts the user before overwriting a file. The following example demonstrates this option, first restoring the content of the original file:

ikechukwu@ubuntu:~$ `cp -i /etc/hosts example.txt`                  
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

> = overwrite </br>
>> = append

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
`ikechukwu@ubuntu-22-04-3:~/Documents$ ls -l longfile*`</br>
`-rw-r--r-- 1 ikechukwu ikechukwu 66540 Dec 20  2017 longfile.txt`</br>

The `tar` command has three modes that are helpful to become familiar with:

* Create: Make a new archive out of a series of files.
* Extract: Pull one or more files out of an archive.
* List: Show the contents of the archive without extracting.

The `tar` command has variety of functions depending on the option being utilized in a command. For example; 

- You can archive without compressing, the main compressing options for the `tar` command are -z and -j gz and bz2 respectively. 

`tar -cvf archive.tar source` = ARCHIVE ONLY </br>
`tar -czvf archive.tar.gz source` = ARCHIVE AND COMPRESS

The `tar` command is primarily used to archive files only. However, you can compress a file using the `-z` option. For example;

`tar -czvf archive.tar.gz /etc/` = creates a file where the compressed directory -etc is located. 
`-c` = create an archive
`-z` = tells tar to compress the archive using gz (file has to be filename.tar.gz)
`-v` = verbose
`-f` = file. 

While, 

`tar -cjvf archive.tar.bz2 /etc/` 
`-j` = tells tar to compress the archive using bz2 (file has to be `filename.tar.bz2`)

- To exclude specific files using a suffix. This command will exclude the .txt and .config files from the archive. 

`tar --exclude='*.txt' --exclude='*.config' -czf filename.tar.gz /etc/` 

- To display the date the compressed file was created when listed. 

`tar -czvf etc-$(date +%F).tar.gz /etc/`

- To add a file to an existing archive, use the -r option to the tar command. Execute the following commands to perform this action and verify the existence of the new file in the tar archive:

`tar -rvf udev.tar /etc/hosts` = To add to an existing archived file.
`tar –tvf udev.tar` = To list an existing archived file. 

`tar -rzvf udev.tar /etc/hosts` = To add to an existing archived file. The z tells tar to compress the archive using gzip.
`tar –tzvf udev.tar` = To list an existing archived file.  The z tells tar to compress the archive using gzip.


It should be noted that tar requires the –f option to indicate a filename is being passed, while zip and unzip require a filename and therefore don’t need you to inform the command a filename is being passed.

Here's how you would use each command:

For tar, you would typically use:

`tar -cf archive.tar file1 file2`</br>
where -c creates a new archive and -f specifies the filename.

For zip, you would use:

`zip archive.zip file1 file2` </br>
where `archive.zip` is the filename of the archive being created.

For unzip:

`unzip archive.zip` </br>
where `archive.zip` is the filename of the archive being extracted.

Furthermore, the zip command will not recurse into subdirectories by default, which is a different behavior than the `tar` command. If you want tar-like behavior, you must use the `–r` option to indicate recursion is to be used. For example ;

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



