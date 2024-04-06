# LINUX FILE PERMISSIONS

Users typically own the files they create by default. Changing ownership requires admin privileges. Commands display the user's name as the owner, but the OS associates ownership with the user's UID.

Each file has a group owner. By default, when a user creates a file, it belongs to their primary group. Users can change the group owner of their files to any group they're part of. The operating system identifies group ownership using the Group ID (GID) rather than the group's name.

Since ownership is determined by the UID and GID associated with a file, changing the UID of a user (or deleting the user) has the effect of making a file that was originally owned by that user have no real user owner. 

### CHANGING GROUPS

If you know that the file you are about to create should belong to a group different from your current primary group, then you can use the  `newgrp` command to change your current primary group. When using the `newgrp` command to change your current primary group, the new primary group must be among the secondary groups associated with your user account.

Administrative privileges are required to change the primary group of the user permanently. The root user would execute the following command:

`usermod -g developers john` : After running this command, the primary group of the user "john" would be changed to "developers". This means that any files created by "john" would now belong to the "developers" group by default.

### CHANGING GROUP AND FILE OWNERSHIP (chgrp and chown)

To change the group owner of an existing file the `chgrp` command can be used.

`chgrp group_name file`

`ikechukwu@ubuntu-22-04-3:~$ ls -l sample` </br>                                    
`-rw-rw-r-- 1 sysadmin sysadmin 0 Oct 23 22:12 sample‌⁠​​⁠​`</br>                    
`ikechukwu@ubuntu-22-04-3:~$ chgrp research sample`</br>
`ikechukwu@ubuntu-22-04-3:~$ ls -l sample`</br>
`-rw-rw-r--. 1 sysadmin research 0 Oct 23 22:12 sample‌⁠​​⁠​`

To change the group ownership of all of the files of a directory structure, use the recursive `-R` option to the `chgrp` command. 

While you can view the ownership of a file with the `-l` option to the `ls` command, the system provides another command that is useful when viewing ownership and file permissions: the `stat` command. The `stat` command displays more detailed information about a file, including providing the group ownership both by group name and GID number.

One big advantage of the stat command is that it shows permissions using both the symbolic and numeric methods, as highlighted below;

`$ stat testfile`</br>
 ` File: testfile`</br>
`  Size: 0               Blocks: 0          IO Block: 4096   regular empty file`</br>
`Device: 801h/2049d      Inode: 9496506     Links: 1`</br>
`Access: (0644/-rw-r--r--)  Uid: ( 1000/   user)   Gid: ( 1000/   user)`</br>
`Access: 2024-04-02 12:00:00.000000000 +0000`</br>
`Modify: 2024-04-02 12:00:00.000000000 +0000`</br>
`Change: 2024-04-02 12:00:00.000000000 +0000`</br>
`Birth: -`

The `chown` command enables the root user to modify the user ownership of files and directories. Regular users lack the privilege to utilize this command for altering the user owner of a file, even to transfer ownership of their own files to another user. However, both the root and the file owner can use `chown` to change group ownership. For example:

`chown user:group /path/to/file`

`root@ubuntu-22-04-3:~# chown jane:users /tmp/filetest2`</br>
`root@ubuntu-22-04-3:~# ls -l /tmp/filetest2`</br>
`-rw-r--r-- 1 jane users 0 Dec 19 18:53 /tmp/filetest2`

To use `chown` only to change the group ownership of the file, use a colon or a period as a prefix to the group name. For example:

`chown :group /path/to/file`

### UNDERSTANDING FILE DIRECTORY PERMISSIONS IN LINUX

The permissions of all parent directories must be considered before considering the permissions on a specific file.

The "w" permission allows a user to delete files from a directory, but only if the user also has "x" permission on the directory.

All that is required to be able to view a directory's contents is "r" permission on the directory (and the ability to access the parent directories).

The "x" permission is required to "get into" a directory, but the "r" permission on the directory is not necessary unless you want to list the directory's contents.

The command of the directory overwrites that of the file. In summary, the execute permission on a directory is necessary to view or interact with the files and subdirectories inside it. If the execute permission is missing, you won't be able to access the directory's contents.

The `chmod` (change mode) command is used to change permissions on files and directories.

When specifying the new_permission argument of the `chmod` command using the symbolic method three types of information are required.

Start by using one or more of the following characters to indicate which permission group(s) to apply the changes to:

| Operator	| Meaning |
|---|---|
| u	| user owner |
| g	| group owner |
| o	| others |
| a	| all (user owner, group owner, and others) |

Then choose one of the following operators to indicate how to modify the permissions:

| Operator | 	Meaning |
|---|---|
| + | 	add |
| -	| remove |
| =	| equals |

Lastly, use the following characters to specify the permissions type(s) to change:

| Operator	| Meaning | Digital Representation |
|---|---|---|
| r	| read | 4 |
| w	| write | 2 |
| x	| execute | 1 |

`chmod 777 filename` = This command assigns full permissions to the file specified (filename). The three digits represent permissions for the user, group, and others, respectively. Each digit corresponds to a combination of read (4), write (2), and execute (1) permissions.</br>
7 grants read (4), write (2), and execute (1) permissions.</br>
0 means no permissions.

`chmod u-r filename`: This command removes the read (r) permission for the user (u). The u stands for "user" and r stands for "read". This means the user will no longer be able to read the file.

`chmod u-w filename`: This command removes the write (w) permission for the user (u). The u stands for "user" and w stands for "write". This means the user will no longer be able to modify or write to the file.

`chmod -v u-r,g-rx,o+rwx filename`: This command combines multiple permission changes using the `-v` option for verbose output. It demonstrates how you can perform multiple permission changes in a single command.

u-r: Removes read permission for the user.</br>
g-rx: Removes read and execute permissions for the group.</br>
o+rwx: Adds read, write, and execute permissions for others.

`chmod a+r,a-wx user.txt`: This command sets permissions for all (a), including the user, group, and others.

a+r: Adds read permission for all. </br>
a-wx: Removes write and execute permissions for all.</br>
This command sets read permission for all and removes write and execute permissions for all, effectively making the file readable by everyone but not writable or executable by anyone.


### USING FIND AND CHMOD

When trying to effect a change on the permissions of the file in a directory and not the directory. You can use the find command and the chmod command. For example: 

`find directory name -type f -exec chmod 777 {} \;`

`find directory_name -type f`: This part of the command searches for files (-type f) within the specified directory (directory_name). It ensures that only regular files are selected, not directories or other types of files.

`-exec chmod 777 {} \;`: This part of the command executes the `chmod 777` command on each file found by find. `chmod 777` sets the permissions of the file to full permissions for the user, group, and others (equivalent to rwxrwxrwx). {} is a placeholder for the file name found by find, and \; terminates the -exec command.

`find ~ -type f -ls` : This command is used to search for all regular files (-type f) in your home directory (~) and display detailed information about them using the -ls option.


### SETUID (SUID)

When a binary file has the setuid permission enabled, it runs with the privileges of the owner of the file, not the user who executes it. This is used for certain system utilities, allowing regular users to run them with elevated permissions, typically those of the root user, granting access to system files beyond their usual reach.

The permissions on /etc/shadow do not allow normal users to view (or modify) the file. Since the file is owned by the root user, the administrator can temporarily modify the permissions to view or modify this file.

The `passwd` command can modify the /etc/shadow file even though other commands run by the user cannot. This is because the `passwd` command is setuid root, allowing it to run with root privileges, thus enabling it to access and modify the /etc/shadow file which is otherwise restricted to normal users. For example:

`ikechukwu@ubuntu-22-04-3:~$ ls -l /usr/bin/passwd` </br>
`-rwsr-xr-x 1 root root 31768 Jan 28 2010 /usr/bin/passwd`

Notice the output of the ls command above; the setuid permission is represented by the "s" in the owner permissions where the execute permission would normally be represented. 

A lowercase "s" means that both the setuid and execute permission are set, while an uppercase "S" means that only setuid and not the user execute permission is set.

To add the setuid permission symbolically, run:

`chmod u+s filename` : To add the setuid permission numerically, add 4000 to the file's existing permissions (assume the file originally had 775 for its permission in the following example):

`chmod 4775 file` : When using the octal method to set permissions with the `chmod` command, if you provide a three-digit code, `chmod` assumes that the first digit is 0. Only when you specify four digits is a special permission set.

`find /usr/bin/ -perm -4000 -ls` : This command not only finds files with the SUID permission but also lists detailed information about each file using the -ls option. This includes permissions, number of hard links, owner, group, size, modification date, and file name.

**SCENARIO**

When a user runs the `passwd` command, which is owned by root and has the setuid bit (4755 permissions), the process that is created will run with the effective user ID (EUID) of the owner of the executable, in this case, root.

The setuid bit (4 in the leftmost position of the permission bits) allows a user to execute a program with the permissions of its owner rather than the permissions of the user who runs the program. In this scenario, since the passwd command has the setuid bit set and is owned by root, any user who runs it will effectively have their process run with root privileges for the duration of the command's execution.

Therefore, the owner of the process that is created when a user runs the passwd command will be root. This allows the passwd command to modify the /etc/passwd and related files, which typically require elevated privileges. The setuid bit is a security feature that enables specific programs to perform privileged operations on behalf of users without granting them overall root access.


### SETGID

The setgid permission is similar to setuid, but it makes use of the group owner permissions. There are two forms of setgid permissions: setgid on a file and setgid on a directory. The behavior of setgid depends on whether it is set on a file or directory.

**SETGID ON FILES**

The setgid permission on a file is very similar to setuid; it allows a user to run an executable binary file in a manner that provides them additional (temporary) group access. The system allows the user running the command to effectively belong to the group that owns the file, but only in the setgid program.

A good example of the setgid permission on an executable file is the `/usr/bin/wall` command. Notice the permissions for this file as well as the group owner:

`ikechukwu@ubuntu-22-04-3:~$ ls -l /usr/bin/wall`</br>
`-rwxr-sr-x 1 root tty 30800 May 16  2018 /usr/bin/wall`

**SETGID ON DIRECTORIES**

When set on a directory, the setgid permission causes files created in the directory to be owned by the group that owns the directory automatically. This behavior is contrary to how new file group ownership would normally function, as by default new files are group owned by the primary group of the user who created the file.

If a directory has the setgid permission set, any directories created within it automatically inherit the setgid permission. This means that new directories within the setgid directory are owned by the same group and also have the setgid permission enabled.

A lowercase "s" means that both setgid and group execute permissions are set while An uppercase S means that only setgid and not group execute permission is set.

If you see an uppercase S in the group execute position of the permissions, then it indicates that although the setgid permission is set, it is not really in effect because the group lacks the execute permission to use it. For example:

`chmod g+s /directory/` : This command sets the setgid (SGID) bit for the specified directory /directory/. When the SGID bit is set on a directory, new files created within that directory inherit the group ownership of the directory, rather than the group ownership of the user who created the file. This command uses symbolic notation (g+s) to set the SGID bit for the group.

To add the setgid permission numerically, add 2000 to the file's existing permissions (assume in the following example that the directory originally had 775 for its permissions). For example:

`chmod 2770 /directory/`: This command sets both the setuid (SUID) bit and the setgid (SGID) bit for the specified directory /directory/. The "2" in the first position of the mode (2770) represents the SGID bit.

**SCENARIO**

Why would an administrator want to set up a setgid directory? First, consider the following user accounts:
* The user bob is a member of the payroll group.
* The user sue is a member of the staff group.
* The user tim is a member of the acct group.

In this scenario, these three users need to work on a joint project. They approach the administrator to ask for a shared directory in which they can work together, but that no one else can access their files. The administrator does the following: 

1. Creates a new group called team.
2. Adds bob, sue, and tim to the team group.
3. Makes a new directory called /home/team.
4. Makes the group owner of the /home/team directory be the team group.
5. Gives the /home/team directory the following permissions: rwxrwx---

As a result, bob, sue, and tim can access the /home/team directory and add files. However, there is a potential problem: when bob creates a file in the /home/team directory, the new file is owned by his primary group: 

`-rw-r-----. 1 bob payroll 100 Oct 30 23:21 /home/team/file.txt`

Unfortunately, while sue and tim can access the /home/team directory, they can't do anything with bob's file. Their permissions for that file are the others permissions (---).

If the administrator sets the setgid permission to the /home/team directory, then when bob creates a file, it is owned by the team group: 

`-rw-r-----. 1 bob team 100 Oct 30 23:21 /home/team/file.txt`

As a result, sue and tim would have access to the file through the group owner permissions (r--).

### STICKY BIT

The sticky bit permission is used to prevent other users from deleting files that they do not own in a shared directory. Recall that any user with write permission on a directory can create files in that directory, as well as delete any file in the directory, even if they do not own the file!

A good example of the use of sticky bit directories would be the /tmp and /var/tmp directories. These directories are designed as locations where any user can create a temporary file.

Because these directories are intended to be writable by all users, they are configured to use the sticky bit. Without this special permission, users would be able to delete any files in this directory, including those that belong to other users.

A lowercase "t" means that both the sticky bit and execute permissions are set for others. An uppercase "T" means that only the sticky bit permission is set. For examples:

To set the sticky bit permission symbolically, execute a command like the following:

`chmod o+t directory_name`

To set the sticky bit permission numerically, add 1000 to the directory's existing permissions (assume the directory in the following example originally had 775 for its permissions):

`chmod 1777 /directory_name/`

### UNDERSTANDING FILES ATTRIBUTES

File attributes, often managed through commands like lsattr and chattr in Linux systems, provide additional control over how files behave and interact with the file system. For examples: 

`sudo chattr -R +i directory_name` : This command makes the directory and its contents immutable, meaning no changes can be made to them. The -R option makes the operation recursive, applying the attribute change to all files and directories within the specified directory. The +i attribute sets the "immutable" attribute, preventing any modifications, deletions, or renames of files and directories within the specified directory.

`sudo chattr +a filename` : This command sets the attribute of the file to be "append-only." When this attribute is set, users can only append data to the file; they cannot modify or truncate it. This can be useful for log files or other types of data that you want to preserve without modification.

`lsattr filename` : This command lists the attributes of a file. It shows which attributes are currently set on the file.
