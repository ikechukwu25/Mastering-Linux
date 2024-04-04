# LINUX FILE PERMISSIONS

Users typically own the files they create by default. Changing ownership requires admin privileges. Commands display the user's name as the owner, but the OS associates ownership with the user's UID.

Each file has a group owner. By default, when a user creates a file, it belongs to their primary group. Users can change the group owner of their files to any group they're part of. The operating system identifies group ownership using the Group ID (GID) rather than the group's name.

Since ownership is determined by the UID and GID associated with a file, changing the UID of a user (or deleting the user) has the effect of making a file that was originally owned by that user have no real user owner. 

### CHANGING GROUPS

If you know that the file you are about to create should belong to a group different from your current primary group, then you can use the  `newgrp` command to change your current primary group. When using the `newgrp` command to change your current primary group, the new primary group must be among the secondary groups associated with your user account.

Administrative privileges are required to change the primary group of the user permanently. The root user would execute the following command:

`usermod -g groupname username`

### CHANGING GROUP OWNERSHIP

To change the group owner of an existing file the `chgrp` command can be used.

`chgrp group_name file`

`ikechukwu@ubuntu-22-04-3:~$ ls -l sample`                                    
`-rw-rw-r-- 1 sysadmin sysadmin 0 Oct 23 22:12 sample‌⁠​​⁠​`                         
`ikechukwu@ubuntu-22-04-3:~$ chgrp research sample`
`ikechukwu@ubuntu-22-04-3:~$ ls -l sample`
`-rw-rw-r--. 1 sysadmin research 0 Oct 23 22:12 sample‌⁠​​⁠​`

To change the group ownership of all of the files of a directory structure, use the recursive `-R` option to the `chgrp` command. 

While you can view the ownership of a file with the `-l` option to the `ls` command, the system provides another command that is useful when viewing ownership and file permissions: the `stat` command. The `stat` command displays more detailed information about a file, including providing the group ownership both by group name and GID number.

One big advantage of the stat command is that it shows permissions using both the symbolic and numeric methods, as highlighted below;

`$ stat testfile`
 ` File: testfile`
`  Size: 0               Blocks: 0          IO Block: 4096   regular empty file`
`Device: 801h/2049d      Inode: 9496506     Links: 1`
`Access: (0644/-rw-r--r--)  Uid: ( 1000/   user)   Gid: ( 1000/   user)`
`Access: 2024-04-02 12:00:00.000000000 +0000`
`Modify: 2024-04-02 12:00:00.000000000 +0000`
`Change: 2024-04-02 12:00:00.000000000 +0000`
`Birth: -`

### CHANGING GROUP OWNERSHIP

The `chown` command enables the root user to modify the user ownership of files and directories. Regular users lack the privilege to utilize this command for altering the user owner of a file, even to transfer ownership of their own files to another user. However, both the root and the file owner can use `chown` to change group ownership. For example:

`chown user:group /path/to/file`

`root@ubuntu-22-04-3:~# chown jane:users /tmp/filetest2`
`root@ubuntu-22-04-3:~# ls -l /tmp/filetest2`
`-rw-r--r-- 1 jane users 0 Dec 19 18:53 /tmp/filetest2`

To use `chown` only to change the group ownership of the file, use a colon or a period as a prefix to the group name. For example:
`chown :group /path/to/file`

chgrp
chown
useradd
groupadd
usermod
groupmod
userdel
groupdel 

The permissions of all parent directories must be considered before considering the permissions on a specific file.

The `w` permission allows a user to delete files from a directory, but only if the user also has x permission on the directory.

All that is required to be able to view a directory's contents is `r` permission on the directory (and the ability to access the parent directories).

The `x` permission is required to "get into" a directory, but the r permission on the directory is not necessary unless you want to list the directory's contents.

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

| Operator	| Meaning |
|---|---|
| r	| read |
| w	| write |
| x	| execute |
