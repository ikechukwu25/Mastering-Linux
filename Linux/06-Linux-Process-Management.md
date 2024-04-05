# PROCESSES AND PSEUDO FILESYSTEMS

The kernel provides access to information about active processes through a pseudo filesystem that is visible under the /proc directory. Hardware devices are made available through special files under the /dev directory, while information about those devices can be found in another pseudo filesystem under the /sys directory.

Pseudo filesystems appear to be real files on disk but exist only in memory. Most pseudo file systems such as /proc are designed to appear to be a hierarchical tree off the root of the system of directories, files and subdirectories, but in reality only exist in the system's memory, and only appear to be resident on the storage device that the root file system is on.

A pseudo filesystem, also known as a virtual filesystem, is a special type of filesystem in Unix-like operating systems that presents information and resources in a hierarchical structure similar to traditional filesystems, but does not correspond directly to physical storage devices. 
A pseudo filesystem, also known as a virtual filesystem or pseudo file system, is a type of filesystem that exists only in memory and is not backed by physical storage like traditional filesystems. 


Pseudo filesystems, also known as virtual filesystems or pseudo files, are stored in the system's RAM (Random Access Memory), whereas traditional filesystems are stored on physical storage devices such as hard disk drives (HDDs) or solid-state drives (SSDs).

The /proc directory not only contains information about running processes, as its name would suggest, but it also contains information about the system hardware and the current kernel configuration.

The /proc directory is read, and its information utilized by many different commands on the system, including but not limited to top, free, mount, umount and many many others. It is rarely necessary for a user to mine the /proc directory directly—it’s easier to use the commands that utilize its information.

The output shows a variety of named and numbered directories. There is a numbered directory for each running process on the system, where the name of the directory matches the process ID (PID) for the running process.

The /proc directory also contains information about the operating system and its hardware in files like /proc/cpuinfo, /proc/meminfo and /proc/devices.

************. IMPORTANT

The /proc/sys subdirectory contains pseudo files that can be used to alter the settings of the running kernel. Since these files are not "real" files, an editor should not be used to change them; instead you should use either the echo or the sysctl command to overwrite the contents of these files. For the same reason, do not attempt to view these files in an editor, but use the cat or sysctl command instead.
For permanent configuration changes, the kernel uses the /etc/sysctl.conf file. Typically, this file is used by the kernel to make changes to the /proc files when the system is starting up.

*************

There are also a number of regular files in the /proc directory that provide information about the running kernel:

File	Contents
/proc/cmdline	Information that was passed to the kernel when it was first started, such as command line parameters and special instructions
/proc/meminfo	Information about the use of memory by the kernel
/proc/modules	A list of modules currently loaded into the kernel to add extra functionality
