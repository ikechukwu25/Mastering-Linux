# TASK AUTOMATION AND SCHEDULING USING CRON (crontab)

Cron is a time-based job scheduler in Unix-like operating systems. It allows users to schedule jobs (commands or scripts) to run periodically at fixed times, dates, or intervals. The scheduling information is stored in a file called the "crontab."

Cron runs as a daemon and is utilized for automating repetitive tasks such as backups, monitoring disk space usage, and updating the system with the latest app version.

**Key Components**:

- `crontab` Command: This command is used to create, edit, and manage cron jobs for a user. Each user can have their own crontab file, stored in /var/spool/cron/crontabs/.
- /var/spool/cron/crontab: Contains individual user crontab files, allowing users to schedule tasks specific to their needs.
- /etc/crontab: System-wide crontab file, intended for system-wide cron jobs not associated with a specific user.

**Common Commands**:

`crontab -l`: Displays the content of the current user's crontab file. </br>
`crontab -e`: Edits the current user's crontab file.</br>
`crontab -r`: Removes the current user's crontab file.</br>
crontab: Abbreviation for "crontable," synonymous with the crontab command.

Usage:

Cron is employed for automating various tasks, including:

- Regular backups of data.
- Monitoring disk space usage.
- Updating the system with the latest application versions.
- Performing routine maintenance tasks.
- By utilizing cron, users can streamline their workflows, reduce manual intervention, and ensure the timely execution of critical system tasks.

Below is a cron job schedule, specifying the time and frequency at which a particular command or script should be executed.

Remember that when you open the user crontab file using `crontab -e`, you get to see the crontab file and edit it. 

N/B: </br>
- \* in the day or the week means every day or every week 
- The minimum time limit used by cron is the minute as you cannot schedule a task to run by seconds using cron. You can create a bash script with a white loop and run the script instead.


1. `*/3 10 1 12 *`: Specifies the timing for the command:
- `*/3`: Indicates that the command will run every 3 minutes.
- `10`: The hour (10:00 AM).
- `1`: The day of the month (1st day).
- `12`: The month (December).
- `*`: The day of the week (any day).
- `date >> ~/today.txt`: The command to be executed. It appends the output of the date command (current date and time) to the file today.txt in the user's home directory (~).</br></br>

<img width="813" alt="image" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/fdb0ff83-6a90-47f6-a61c-1194fa98a407">
</br></br>


2. `0 6,8,10 * */3 1-5 /root/backup.sh`
* Minute Field (`0`): This field is for the “minute”. The cron job is scheduled to run at the 0th minute of the specified hours.
* Hour Field (`6,8,10`): This field means “hour” The cron job is scheduled to run at the 6th, 7th, and 8th hours of the day (6 AM, 8 AM, and 10 AM).
* Day of Month Field (`\*`): The asterisk (*) in this field means "every day of the month." It doesn't restrict the cron job based on the day of the month.
* Month Field (`*/3`): This field means "every month." It doesn't restrict the cron job based on the month. The job is scheduled to run every 3 months. The */3 means "every 3 months."
* Day of Week Field (`*`): 1-5: The day of the week field, meaning Monday through Friday (1 is Monday and 5 is Friday).
* Command (`/root/backup.sh`): The command to be executed is /root/backup.sh. </br></br>
This cron job will append the current date and time to the file today.txt in the user's home directory every 3 minutes past 10:00 AM on the 1st day of December every year.



The `@yearly` directive in a cron job is equivalent to the cron expression 0 0 1 1 *. It specifies that the associated command should be executed once a year, specifically at midnight on January 1st.

The `@monthly` cron expression is a special string used in cron to specify a monthly schedule. In this case, it is equivalent to the more detailed cron expression 0 0 1 * *, which means "at midnight on the first day of every month."

The `@reboot` cron expression is a special string used in cron to specify a schedule that runs once when the system starts or is rebooted.

System Files:

/etc/crontab: System-wide cron configuration file. </br>
/etc/cron.daily: Directory containing daily cron jobs.</br>
/etc/cron.weekly: Directory containing weekly cron jobs.

Additional Information:

- `tail -f /var/log/syslog`: Command to view the cron log file in Ubuntu, useful for monitoring cron job execution and troubleshooting.
- Root Privileges: Root can edit a user's crontab using the -u option. To edit a user's crontab as root;
  - `sudo su` = became root
  - `crontab -e -u username` = This command allows root to edit a user’s crontab.


# SCHEDULING TASKS USING ANACRON (anacron)

Anacron serves a similar purpose to cron but is designed for systems that are not continuously powered on, such as desktops or laptops. It operates with root privileges and executes tasks with a frequency expressed in days rather than minutes, as in cron. The configuration file for Anacron is located at /etc/anacrontab.

Anacron's job layout includes Days, Delay, Identifier, and Command.

Days: Specifies the interval in days at which the command should be executed. </br>
Delay: Identifies the delay in minutes before the command execution. This helps prevent system overload by staggering the execution of multiple tasks. </br>
Identifier: This is a unique identifier for the job, typically the name of the associated script or task. </br>
Command: The command to be executed.

Example; 

- `vim /etc/anacron`
  - <img width="799" alt="image" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/159a5029-a111-4433-8fa3-91a3bb0136d5">

`7	10	cron.weekly 		run-parts --report /etc/cron.weekly` </br>
`@daily	15			cron.weekly 		run-parts --report /etc/cron.weekly`

- `7` (days) = This means the command should be run every 7 days - weekly	
- `10` (minutes) = This identifies the delay in minutes. This is intended to keep the system from being overloaded with the jobs. If `anacron` determines that it needs to run several commands when it starts up, it won’t run them simultaneously but with a delay. 
- `cron.weekly` = This is a job identifier. It is the name of the file that will be created under /var/spool/anacron. This is also called the job timestamp file that will contain a single line that indicates the last time this job was executed.  The identifier identifies the job in the messages or the log files. 

**Additional Anacron Commands**:

- `anacron -T` = Checks for syntax errors in the Anacron configuration file.
- `anacron -d` = When `anacron` is run with the `-d` option, it provides more detailed output and information about its activities, which can be helpful for troubleshooting and understanding how it is scheduling and executing jobs.
- `sudo cat /var/spool/anacron` = Displays the log file containing information about Anacron job executions.


# UNDERTSTANDING COMPUTER HARDWARE

The motherboard, or system board, is the main hardware board in the computer through which the central processing unit (CPU), random-access memory (RAM) and other components are all connected. 

A central processing unit (CPU or processor) is one of the most critical hardware components of a computer. The processor is the brain of the computer, where the execution of code takes place and where most calculations are done. It is directly connected (soldered) to the motherboard, as motherboards are typically configured to work with specific types of processors.

Processors are electronic circuits that execute instructions and perform calculations in a computing device. The term "processor" generally refers to the central processing unit (CPU) of a computer, which is responsible for executing program instructions, performing arithmetic and logic operations, and managing data movement within the system.

If a hardware system has more than one processor, the system is referred to as a multiprocessor.  If more than one processor is combined into a single overall processor chip, then it is called multi-core.
In summary, a multiprocessor system comprises multiple independent processors working together, whereas a multi-core processor integrates multiple processing cores onto a single chip. Both architectures enable parallelism and improve overall system performance, but they differ in their implementation and organization of processing units.

Although support is available for more types of processors in Linux than any other operating system, there are primarily just two types of processors used on desktop and server computers: x86 and x86_64.

On an x86 system, the system processes data 32 bits at a time; on an x86_64 the system processes data 64 bits at a time. An x86_64 system is also capable of processing data 32 bits at a time in a backward-compatible mode. One of the main advantages of a 64-bit system is the ability to work with more memory, while other advantages include increased efficiency of processing and increased security.

Intel originated the x86 family of processors in 1978 with the release of the 8086 processor. Since that time, Intel has produced many other processors that are improvements to the original 8086; they are known generically as x86 processors. These processors include the 80386 (i386), 80486 (i486), the Pentium series (i586) and the Pentium Pro series (i686). 
While Linux is capable of supporting processors back to the i386 generation, many distributions (especially the ones that feature corporate support, such as SUSE, Red Hat and Canonical) limit their support to i686 or later.

The x86_64 family of processors, including the 64-bit processors from Intel and AMD, have been in production since around the year 2000. As a result, almost all of the modern processors shipped today are of the x86_64 type.
While the hardware has been available for over a decade now, the software to support this family of processors has been much slower to develop.

To see which family the CPU of the current system belongs to, use the `arch` command:

`ikechukwu@ubuntu-22-04-3:~$ arch` </br>
`x86_64`

For more information concerning the CPU, use the `lscpu` command:

`ikechukwu@ubuntu-22-04-3:~$ lscpu`</br>
`Architecture:          x86_64`</br>
`CPU op-mode(s):        32-bit, 64-bit`</br>
`Byte Order:            Little Endian`</br>
`CPU(s):                4`</br>
`On-line CPU(s) list:   0-3`</br>
`Thread(s) per core:    1`</br>
`Core(s) per socket:    4`</br>
`Socket(s):             1`</br>
`NUMA node(s):          1`</br>
`Vendor ID:             GenuineIntel`

For even more details about your CPU(s), you can examine the /proc/cpuinfo file, especially the "flags" that are listed which determine whether or not your CPU has certain features.


#### RANDOM ACCESS MEMORY (RAM)

The 32-bit architecture systems can use up to 4 gigabytes (GB) of RAM, while 64-bit architectures are capable of addressing and using far more RAM

When a computer system is running low on physical RAM (Random Access Memory), it may use a technique called "paging" or "swapping" to manage memory more effectively. Swapping involves temporarily moving data from RAM to a designated space on the hard drive, known as swap space or swap file, to free up RAM for currently active programs.
Here's how the process works:

* Low RAM Conditions: When the amount of available RAM becomes insufficient to accommodate all the data and programs currently in use, the operating system (OS) identifies this low-memory condition.
* Selection of Data to Swap: The OS identifies portions of data stored in RAM that have not been accessed or used recently. This data is considered less critical for immediate processing and is chosen for swapping to the swap space.
* Moving Data to Swap Space: The selected data is then transferred from RAM to the swap space on the hard drive. This action frees up space in RAM for use by currently active programs and processes.
* Managing Active Programs: The OS continues to monitor the system's memory usage and ensures that actively running programs have sufficient RAM available for optimal performance.
* Accessing Swapped Data: If an application needs access to data that has been swapped out to the swap space, the OS retrieves it from the swap space and moves it back into RAM. This process is known as swapping data back into memory.
* Automatic Management: The entire process of swapping data between RAM and the swap space is managed automatically by the operating system. Users typically do not need to intervene or manually manage the swap space.

It's important to note that while swapping can prevent system crashes and out-of-memory errors when RAM is low, accessing data from swap space is significantly slower than accessing data from RAM. Therefore, excessive swapping can lead to performance degradation and slowdowns in system responsiveness.

To optimize system performance, it's essential to ensure that the system has sufficient RAM to accommodate the workload without relying heavily on swap space. However, swap space serves as a valuable safety net, allowing the system to continue operating smoothly even under conditions of high memory demand.

To view the amount of RAM in your system, including the swap space, execute the free command. The `free` command has a `-m` option to force the output to be rounded to the nearest megabyte (MB) and a -g option to force the output to be rounded to the nearest gigabyte (GB):

`ikechukwu@ubuntu-22-04-3:~$ free -m`</br>
`             total       used       free     shared    buffers     cached`</br>
`Mem:          1894        356       1537          0          25       177`</br>
`-/+ buffers/cache:        153       1741`</br>
`Swap:         4063          0       4063`</br>
</br>


#### BUSES

A bus is a high-speed connection that allows communication between computers or the components inside a computer. The motherboard has buses that allow for multiple devices to connect to the system, including the Peripheral Component Interconnect (PCI) and Universal Serial Bus (USB). The motherboard also has connectors for monitors, keyboards and mice.

In a desktop or server computer, there is a motherboard with the processor, RAM, and other components directly attached, and then a high-speed bus that allows additional components to be attached via card slots, such as video, network and other peripheral devices.

Increasingly for laptop and light/thin/small form factor computers, the majority of the computer’s components may be directly connected to the motherboard, including the usual processor, RAM, as well as additional components like the network card. In this configuration, the bus still exists, but effectively one of the main convenience factors of being able to swap out or upgrade devices is no longer a possibility.

- Peripheral Devices
Peripheral devices are components connected to a computer that allow input, output or data storage. Keyboards, mice, monitors, printers and hard disks are all considered peripherals and are accessed by the system in order to perform functions outside of central processing. To view all of the devices connected by the PCI bus, the user can execute the lspci command.

- Universal Serial Bus Devices
While the PCI bus is used for many internal devices such as sound and network cards, an ever-increasing number of external devices (or peripherals) are connected to the computer via USB.</br>
Cold-plug refers to the ability to add or remove devices from a system while it's powered off or in standby mode. SB devices are hot-plug, meaning they can be connected or disconnected while the system is running.</br>
To display the devices connected to the system via USB, execute the lsusb command


#### HARD DRIVES

Hard drives, also called hard disks, disk devices, or storage devices, may be attached to the system in a number of ways; the controller may be integrated into the motherboard, on a PCI card, or as a USB device.
For the purposes of most Linux systems, a hard drive can generally be defined as any electromechanical or electronic storage device that holds data to be accessed by the system.

Hard drives are divided into one or more partitions. A partition is a logical division of a hard drive, designed to take a large amount of available storage space and break it up into smaller areas.
While it is common on Microsoft Windows to have a single partition for each hard drive, on Linux distributions, multiple partitions per hard drive is common.

Some hard drives make use of a partitioning technology called Master Boot Record (MBR) while others make use of a partitioning type called GUID Partitioning Table (GPT). The MBR type of partitioning has been used since the early days of the Personal Computer (PC), and the GPT type has been available since the year 2000.

An old term used to describe an internal hard disk is fixed disk, as the disk is fixed (not removable). This term gave rise to several command names: the `fdisk`, `cfdisk` and `sfdisk` commands, which are tools for working with the MBR partitioned disks.

The GPT disks use a newer type of partitioning, which allows the user to divide the disk into more partitions than what MBR supports. GPT also allows having partitions which can be larger than two terabytes (MBR does not). The tools for managing GPT disks are named similarly to their fdisk counterparts: gdisk, cgdisk, and sgdisk.

Hard drives are associated with file names (called device files) that are stored in the /dev directory. 

* File Type The file name is prefixed based on the different types of hard drives. IDE (Intelligent Drive Electronics) hard drives begin with hd, while USB, SATA (Serial Advanced Technology Attachment) and SCSI (Small Computer System Interface) hard drives begin with sd.
* Device Order Each hard drive is then assigned a letter which follows the prefix. For example, the first IDE hard drive would be named /dev/hda and the second would be /dev/hdb, and so on.
* Partition Finally, each partition on a disk is given a unique numeric indicator. For example, if a USB hard drive has two partitions, they could be associated with the /dev/sda1 and /dev/sda2 device files.


#### SOLID STATE DISKS

While the phrase hard disk is typically considered to encompass traditional spinning disk devices, it can also refer to the newer and very different solid state drives or disks.

A solid state disk is controlled by an embedded or onboard processor that makes the decisions as to where and how data is written and read back from the memory chips when requested.

Advantages of a solid state disk include lower power usage, time savings in system booting, faster program loads, and less heat and vibration from no moving parts. 
Disadvantages include higher costs in comparison to spinning hard disks, lower capacity due to the higher cost, and if soldered directly on the motherboard/mainboard, no ability to upgrade by swapping out the drive.

Where these removable disks are mounted in the file system is an important consideration for a Linux administrator. Modern distributions often mount the disks under the /media folder, while older distributions typically mount them under the /mnt folder. For example, a USB thumb drive might be mounted on the /media/usbthumb path.

With the popularity of USB devices, such as USB storage devices, cameras, and mobile phones, the number of available devices you would want to connect to a Linux system can number in the thousands.
The sheer number of different devices poses problems as these hardware devices typically need drivers, software that allows them to communicate with the installed operating system.

The process of enabling devices in Linux involves compiling drivers into the kernel, loading them as modules, or through user commands or applications. Unlike Windows, Linux often lacks vendor-provided drivers, especially for external devices like scanners and printers. Despite growing Linux popularity, vendor support remains limited, prompting community developers to create drivers. While not all hardware has Linux support, many do, requiring users to find compatible drivers or opt for Linux-certified hardware. Checking Linux distribution certifications and avoiding new or specialized devices can enhance device compatibility. Vendor support inquiries before purchase are advisable.

For monitors to work correctly with video display devices, they must be able to support the same resolution as the video display device. Normally, the software driving the video display device can automatically detect the maximum resolution that the video display and monitor can both support and set the screen resolution to that value.


**POWER SUPPLIES**: Convert alternating current (AC) into direct current (DC) for a computer's various voltage needs. They are critical for system function and often safeguard against voltage fluctuations, though not designed as surge suppressors. Quality power supplies are crucial, as failures can cause extensive system damage. Desktops, servers, racks, and standalone systems are more susceptible to power issues than laptops. Laptops, relying on internal batteries, are less affected by power fluctuations. Therefore, administrators should prioritize quality over price when selecting power supplies.

For hardware to function, the Linux kernel usually loads a driver or module. Use the `lsmod` command to view the currently loaded modules.

The `fdisk` command is useful for identifying and manipulating disk storage resources on a system. Since it can be used to create, format and delete partitions, as well as for getting information, it should be used with care in administrator mode to avoid data loss. The fdisk command can be used in two ways: interactively and non-interactively.


#### GETTING SYSTEM HARDWARE INFORMATION (lshw, lscpu, lsusb, lspci, dmidecode, hdparm) (must be run as root)

1. `lshw` is a command-line utility in Unix-like operating systems that provides detailed information about the hardware configuration of the system. The name "lshw" stands for "list hardware." It is a versatile tool that can display information about various hardware components, including the processor, memory, disk drives, network interfaces, and more. It’s always advisable to pipe it to less as the output is a lot. </br></br>
In virtualised environments, the info displayed by these commands (`lwhw`, `lscpu`, `lsusb`, `lspci`, `dmidecode`, `hdparm`) reflects the configuration of the guest operating system which is different from the physical host system. I.E when you run commands like `lwhw`, `lscpu`, etc., within a virtual machine, the information they provide reflects the virtualized hardware configuration of that specific virtual machine, and it may not accurately represent the physical hardware of the host machine running the virtualization software.</br></br>
Below are some common usage:
- `lshw -short`: This option provides a summary of the hardware configuration in a concise format.
- `lshw -html | less`
  * `lshw`: This is the command that lists hardware information on a Linux system.
  * `-html`: This option specifies the output format as HTML.
  * `|`: This is the pipe symbol, which is used to redirect the output of one command as input to another.
  * `less`: This is a pager program that allows you to view text files or command output one screen at a time.</br></br>


2. `inxi` is a command-line tool that provides a comprehensive and easily readable system information summary for Unix-like operating systems, particularly Linux. It displays details about the hardware, system, and network. Below are some common usage:
- `sudo apt install infix`: To install the command as it is not pre-installed in Linux.
- `inxi -Fx`: used to display a detailed output of your system's information, providing an extensive overview of both hardware and software configurations.
  * `inxi`: The main command for retrieving system information.
  * `-F`: This option specifies the level of information to be displayed. In this case, it stands for "Full," indicating a detailed output.
  * `-x`: This option adds extra details to the output, providing even more information.


3. The `lscpu` command is a useful tool for retrieving information about the CPU and its architecture on Unix-like operating systems, particularly Linux.</br></br>
N/B: `lscpu` = `lshw -C cpu` which means that you can also use the `lshw` command to show information about the CPU but running `lshw -C cpu` which provides almost the same information with the `lscpu` command.</br>
Below are some common usage:
- `lscpu`: Displays info about the CPU and its architecture. 
- `lscpu -J`: displays output in JSON format. 
- `lscpu | grep -i MHz`: search for the unit of the speed.


4. The `dmidecode` command shows all memory modules and their capacity. It provides information about the system's hardware as described in the System Management BIOS (SMBIOS) and Desktop Management Interface (DMI) specifications.
- `dmidecode -t memory`: Displays information about memory modules installed on the system.
- `dmidecode -t memory | grep -i size`: Shows the amount of RAM memory already installed on the system.
- `dmidecode -t memory | grep -i max`: Indicates the maximum RAM memory that can be installed on the system.
The `dmidecode` provides information about installed memory modules but does not directly report the amount of free or used memory in the system. To check the amount of free or used memory, you can use commands like `free -m` or monitor memory usage with tools like `top`. 
  - `free -m` = shows the amount of memory used or free.

5. PCI buses, or Peripheral Component Interconnect buses, are a type of computer bus (A computer bus is a communication system that transfers data between components inside a computer or between multiple computers) standard used for connecting various hardware devices to the motherboard of a computer. See below for an overview of several commands used to gather information about hardware components connected to a computer system.
- `lspci -v`: It is used to display information about the PCI buses and the devices connected to them. It provides detailed information about the hardware components connected to the PCI (Peripheral Component Interconnect) bus on your system.
- `lsusb -v`: The `lsusb` command is used in Linux to list USB devices connected to the system. It provides information about the USB buses and the devices attached to them.
- `lshw -C disk`: This command displays detailed information about disks or storage devices connected to the system. It provides information about the hardware configuration of disks.
- `lsblk`: This command displays information about all block devices, including hard disks and partitions. It provides a hierarchical view of block devices and their partitions.
- `fdisk -l`: The `fdisk` command with the `-l` option displays detailed information about disks and their partitions. It provides information such as size, filesystem type, and number of sectors for each disk and partition.

6. The `hdparm` command allows users to get or set SATA drive parameters and configure various aspects of a disk operation. It allows users to interact with and control the behavior of hard disk drives. For example:
  - `hdparm -i /dev/sda (drive)`:  
    * `hdparm: The command itself`.
    * `-i`: This option stands for "get information." It tells hdparm to display detailed information about the specified device.
    * `/dev/sda`: This is the device file for the first SATA hard disk drive. In Linux, devices are represented as files in the /dev directory.
N/B: Serial ATA (Serial Advanced Technology Attachment or SATA) is a command and transport protocol that defines how data is transferred between a computer's motherboard and mass storage devices, such as hard disk drives (HDDs), optical drives, and solid-state drives (SSDs).

7.  Other commands that are useful include:
  - The `iw list` This command provides detailed information about wireless devices, including their capabilities, supported modes, and available frequencies.
  - `uname -r`: This displays the version of the running kernel.
  - `uname -a`: This command provides more comprehensive information about the system, including the kernel version, hostname, architecture, and more.
  - `acpi -V`: This command shows detailed information about the system's Advanced Configuration and Power Interface (ACPI), including thermal zones, battery status, and power adapter information.
  - `acpi -b`: Specifically displays information about the battery, including its status, charge level, and capacity.
  - `lshw -C network` or `iw -l` or `lspci | grep wireless` : To display as much information as possible about the WiFi card, you can use any of these commands.


# MOUNTING AND UNMOUNTING FILE SYSTEMS (df, mount, umount, fdisk, gparted)

In Linux, mounting is the process of making the contents of a storage device (like a USB drive or a hard disk) accessible at a specific location in your computer's directory structure. This location is called the "mount point," and it's like assigning a specific drawer in the filing cabinet for that storage device.

To access a file system located on another partition or disk, it must be mounted or logically attached to an existing directory of the unique file system. This process is typically performed using the `mount` command. However, only the root user has the authority to mount partitions in Linux.

Sometimes the usb stick that has been attached is not mounted automatically like in the case of a disk partition or you want to mount it in another place or with other options, in linux a storage device is logically represented as a special character device in /dev. 

In Linux, storage devices, including USB sticks, are logically represented as special character devices in the /dev directory. Each device is assigned a specific file in the /dev directory. For example, a USB stick might be represented as /dev/sdb or a similar name. 

/dev/sdb: This is the device identifier for the storage device you want to mount. In Linux, storage devices are represented as block devices under the /dev directory.

**Mounting and Managing Filesystems in Linux**

- `mount -l -t ext4`: This command is used to display information about currently mounted ext4 filesystems.
  * mount: The command itself for mounting and displaying information about filesystems.
  * -l: Show labels instead of device names.
  * -t ext4: Filter the output to show only ext4 filesystems.
  * -a: Mounts all filesystems listed in /etc/fstab.
- `sudo mount /dev/sdb /home/ikechukwu/file` = this will mount the device located at /dev/sdb to the directory /home/ikechukwu/file.
In the above command, /home/ikechukwu/file. Is the mount point.
- `sudo mount -o ro /dev/sdb1 /home/ikechukwu/file`: The `-o ro` option is used to specify that the filesystem should be mounted as read-only. 
- `sudo mount -o rw,remount /dev/sr0 /home/ikechukwu/Desktop/usb`: This command will remount the previous command from read only to read and write. The `-o` loop option in Linux is used with the `mount` command to associate a regular file with a loop device. This is commonly used when mounting disk images, such as ISO files.
- `sudo fdisk -l`: used to list information about all the available disk drives and their partitions on your system.
  - `fdisk`: It is a command-line utility for disk partitioning. 
- `lsblk`: This command will provide a hierarchical view of the block devices attached to your system, along with information about their partitions and mount points. You can run the `dmesg` and `lsblk` (lists all block devices) commands to find the name of the device.

**Unmounting**

- `sudo umount /home/ikechukwu/file`: Unmounts the filesystem located at /home/ikechukwu/file.
- `sudo umount -l /home/ikechukwu/usb`: This command will unmount the filesystem located at /home/ikechukwu/usb. Make sure there are no active processes or open files on the mounted filesystem before attempting to unmount it.

N/B: When a USD drive or hard drive is connected, they can be located at the media directory. Also, make sure that no processes or applications are actively using the mounted filesystem before attempting to unmount it. If any processes are still accessing the filesystem, you may encounter an error.

**Tips for Mounting**

- Create a mount point.
- Use `mount -l` to check the initial mount point of the external device.
- Confirm the block device file using `lsblk`.
- Utilize graphical tools like `GParted` for disk partition management (`sudo apt install gparted` to install).

The `df` command displays information about total space and available space on a file system. It's particularly useful for monitoring disk space usage, providing insights into the available and used space on mounted file systems. The -h option enhances readability by presenting sizes in human-readable format.

On the other hand, du serves a different purpose. It's employed to determine the disk space utilized by directories and files. For example:

`du -sh /path/to/directory`: This command would display the disk space used by the specified directory in a human-readable format.

# WORKING WITH DEVICE FILES (dd)


The `dd` command in Linux is a versatile tool primarily used for copying and converting files, offering options to specify block size, input/output files, and other parameters. Despite its name standing for "data duplicator," it's often humorously referred to as "disk destroyer" due to its powerful and potentially destructive capabilities if used incorrectly.

It's crucial to note that dd has the potential to cause data loss, so it's necessary to back up files before using it.

In Linux, hard disks are represented as special device files. Unlike the `cp` command, `dd` directly reads from and writes to these device files.

`dd` can work directly with these device files and is commonly used for tasks such as backing up the boot sector of a hard drive, cloning a disk or partition to another one, or creating a bootable USB stick.

The command-line syntax for `dd` differs from other Linux commands, using the syntax `option=value` for its command-line options.

Cloning an entire partition to a file on another partition involves specifying the input file (source partition) and the output file (destination partition or backup file) using if and of options, respectively.

A "block" refers to a small unit of storage, and a "partition" is a section of a storage device used to organize and manage data. `dd` operates at the block level, providing precise control over data copying and manipulation.

Examples:

1. `sudo if=/dev/sdb of=/home/ikechukwu/backup-usb.img status=progress`: This command is used for cloning the device file you want to create an image of the entire /dev/sdb device and save it as backup-usb.img in the /home/ikechukwu/ directory. The `status=progress` option is included to show the progress of the `dd` command, which can be helpful for larger operations.</br></br>
After the command completes, you should have a file named backup-usb.img in the /home/ikechukwu/ directory, which is an image of your USB drive.</br></br>
The `dd` command works with blocks and cloning the device by copying everything including the empty and occupied space. If you have a partition of 10GB and 9 are free, the dd command will copy 10GB to the destination which makes it different from the `cp` command.</br></br>
Breakdown:
* `sudo`: Runs the command with superuser privileges, allowing it to access the specified device file and write to the specified output file.
* `dd`: The command for copying and converting data.
* `if=/dev/sdb`: Specifies the input file, which in this case is /dev/sdb, representing the USB drive you want to clone.
* `of=/home/ikechukwu/backup-usb.img`: Specifies the output file, which is the image file that will be created. It will be named backup-usb.img and will be saved in the /home/ikechukwu/ directory.
* `status=progress`: This option shows the progress of the `dd` command as it runs, indicating how much data has been copied and how much is remaining. This can be particularly helpful for larger operations to track the progress of the cloning process. </br>
It's important to note that the `status=progress` option requires the use of the GNU dd command from Coreutils version 8.24 or above to function properly.</br></br>


2. `sudo dd if=/home/ikechukwu/backup-usb.img of=/dev/sdb status=progress conv=sync`: This will write the contents of a disk image (backup.img) to a block device (/dev/sdb). Breakdown:
* `sudo`: This command is used to execute the subsequent command with elevated privileges.
* `dd`: This is a command used for copying and converting files. In this case, it's being used to copy the contents of a disk image to a block device.
* `if=/home/ikechukwu/backup.img`: This specifies the input file (source), which is the disk image located at /home/ikechukwu/backup.img.
* `of=/dev/sdb`: This specifies the output file (destination), which is the block device /dev/sdb.
* `status=progress`: This option shows the progress of the dd command, indicating how much data has been transferred.
* `conv=sync`: This option ensures that the data is synchronized after each write operation, making sure that all data is written to the destination before completing.</br></br>

3. To clone the partition where the root file system is mounted to a USB stick partition, follow these steps:</br></br>
- Confirm the name of the partition where the root file system is mounted using either `fdisk -l` or `df -h` command.
- Once you have identified the source partition (let's assume it's /dev/sda2) and the destination partition on the USB stick (let's assume it's /dev/sdb), use the following command to clone the partition:
  - `sudo dd if=/dev/sda2 of=/dev/sdb status=progress`
    - `sudo`: Execute the command with elevated privileges.
    - `dd`: Command for copying and converting data.
    - `if=/dev/sda2`: Specifies the input file, which is the source partition where the root file system is mounted (/dev/sda2 in this case).
    - `of=/dev/sdb`: Specifies the output file, which is the destination partition on the USB stick (/dev/sdb in this case).
    - `status=progress`: Option to display the progress of the `dd` command, showing how much data has been transferred.
- Wait for the cloning process to complete. Depending on the size of the partition and the speed of the devices involved, this process may take some time.
- Once the cloning process is finished, you can safely remove the USB stick and use it as needed. Make sure to eject it properly before removing it to avoid data corruption.
  

#### MBR

The Master Boot Record (MBR) is a special type of boot sector located at the very beginning of a storage device, such as a hard disk drive or solid-state drive. It contains the information necessary to boot the operating system.
The MBR holds the info on how the logical partition containing file systems are organised on that medium. It also contains executable codes which is referred to as the boot loader. 

The MBR itself is usually not represented as a partition. It is a small region at the very beginning of the disk that contains the partition table and the Master Boot Code. If you want to examine the MBR directly, you would typically use a tool like dd to copy the first sector of the disk to a file, as shown in the previous examples. The MBR doesn't have a specific partition designation like /dev/sda1. Instead, it resides in the initial sectors of the disk, before any partitions.


To create a backup of the MBR, you can use the dd command with specific options:

`sudo dd if=/dev/sda of=/root/mbr.dat bs=512 count=1`
Here's what each part of the command does:

- `dd`: Command for copying and converting data.
- `if=/dev/sda`: Specifies the input file, which is the entire storage device (/dev/sda in this case).
- `of=/root/mbr.dat`: Specifies the output file, where the MBR snapshot will be saved (/root/mbr.dat in this case).
- `bs=512`: Sets the block size to 512 bytes, which is the typical size of an MBR.
- `count=1`: Specifies that only one block (512 bytes) should be copied, containing the MBR.

This command essentially takes a snapshot of the MBR from /dev/sda and stores it in the file /root/mbr.dat. It's a common practice to create such backups before making changes to the disk or performing operations that might affect the MBR. The MBR is a critical component for booting the operating system, and having a backup can be useful for recovery purposes.

To restore the MBR from the backup file, you can use the following command:

`sudo dd if=/root/mbr.dat of=/dev/sda bs=512 count=1`
This command copies the contents of the backup file (/root/mbr.dat) back to the beginning of the storage device (/dev/sda), effectively restoring the MBR. Again, it's crucial to exercise caution when performing such operations, as improper manipulation of the MBR can lead to system boot failures and data loss.

#### CREATING A BOOTABLE USB STICK USING DD

Creating a bootable USB stick using `dd` involves transferring the contents of a disk image file directly onto a USB flash drive. 

To create a bootable USB stick using the `dd` command, follow these steps:

* Download an iso file: Obtain the ISO file of the operating system or software you want to make bootable.
* Identify the USB drive: Use the `lsblk` command to find the name of the device file for the USB drive. It's usually located under /media/username/...
* Unmount the USB drive: To make the USB drive bootable, it should be formatted with a file system: `umount /media/ikechukwu/……`
* Format the USB drive: Format using the shell command `mkfs -t vfat /dev/sdb` (unmount before formatting).
  * mkfs: Used to create a file system on a disk partition. It stands for "make file system." This command is used after creating a
  partition on a storage device (using tools like fdisk or parted) to prepare the partition for storing files by creating the necessary data structures for a specific file system type.
  * vfat: This is the filesystem 
* Write the ISO file to the USB drive: Now, use the dd command to write the contents of the ISO file to the USB drive. Specify the input file (if) as the path to the ISO file and the output file (of) as the device file of the USB drive. Set the block size (bs) for optimal performance and include status=progress to monitor the progress of the operation.
  * `sudo dd  if=/home/ikechukwu/Downloads/newbootablefile.iso of=/dev/sdb bs=4M status=progress`. Ensure to replace `/home/ikechukwu/Downloads/newbootablefile.iso` with the path to your downloaded ISO file, and /dev/sdb with the actual device file of your USB drive.
* After executing this command, you'll have a bootable USB stick ready for use with the contents of the ISO file written onto it.



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

2. **Partition the Disk** - `sudo fdisk /dev/sdb`: When you run the command, `fdisk` will display information about the existing partitions on `/dev/sdb`, if any, and allow you to create, delete, or modify partitions as needed. You can use `fdisk` commands to manage the disk's partition table interactively.
        - `fdisk`: This is a command-line utility used for disk partitioning. It allows users to create, delete, and manipulate disk partitions on a storage device.
        - `/dev/sdb`: This block device represents the entire disk. It could be a physical disk (e.g., a hard drive or SSD) or a virtual disk (e.g., a virtual disk in a virtual machine). The device name is followed by a letter indicating the drive and a number indicating the partition. </br></br>
A prompt pops up when you input the above command - `Command (m for help)`, select `n` to create a new partition, and select 'p' for primary or 'e' for entended. You can choose the default option for the rest. Lastly, you select the partition size with a "+" prefix `+40G`. See screenshot below:</br></br>
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



# INTRODUCTION TO SYSTEMD

systemd (system management daemon) is a system and service manager for Linux operating systems. It is designed to be a replacement for the traditional System V init system and the older init daemon. systemd provides a range of system management features, and it has become the default initialization system for many Linux distributions. It is the system initialization system responsible for managing the booting and startup process.

systemd is responsible for starting, stopping, and managing background services (daemons) on the system. The init process is the ancestor of all processes on a Unix or Unix-like operating system. It is the first process started by the kernel during system initialization. systemd starts with PID 1 as the first process, then takes over and continues to mount the host’s file systems and starts services.

systemd is a Linux initialisation system and service manager with many components, such as on-demand service management, logging, boot manager, etc. One of the key features of systemd, the system and service manager for Linux, is its ability to start services in parallel. Traditional init systems typically start services sequentially, one after the other, which can lead to increased boot times.

**systemd units**: These are defined by configuration files with specific file extensions, typically `.service` for services, although there are other types like `.socket`, `.target`, and `.timer`, among others. These unit files provide instructions to systemd on how to manage and interact with the corresponding resource, whether it's a service, socket, target, timer, or other component.

For example, a unit file named `nginx.service` would define how systemd should manage the Nginx web server service. Similarly, a unit file named `sshd.service` would provide instructions on managing the SSH server service.

Each unit file contains configuration directives specifying various parameters such as the service executable path, startup type, dependencies, permissions, and more. These directives allow systemd to control the lifecycle of the associated resource, including starting, stopping, restarting, and monitoring it.

By adhering to the systemd unit file format and naming conventions, administrators can effectively manage system resources and services using systemd's powerful management capabilities.

These are essential commands for managing and analyzing the systemd initialization system:

- `systemd --version`: This command displays the version of systemd installed on the system.
- `systemd-analyze`: Running this command without any arguments shows how long the boot process took, providing information on the time spent in the kernel as well as userspace.
- `systemd-analyze blame`: This command identifies the services or units that contribute the most to the overall system boot time. When executed, it provides a list of services along with the time each service takes to start during the boot process, helping administrators identify potential bottlenecks and optimize boot time by focusing on the services causing delays.


#### SERVICE MANAGEMENT (systemd and systemctl)

Service management is a critical aspect of system administration, ensuring that essential processes and applications run smoothly and reliably on a Linux system. 

Services are background processes or daemons that perform specific functions, such as web servers (e.g., Apache or Nginx), databases (e.g., MySQL or PostgreSQL), or networking services (e.g., SSH or DNS). Proper management of services is essential for system stability, security, and performance.

**systemctl**: `systemctl` is the primary command-line tool for managing services with systemd. It allows administrators to start, stop, enable, disable, restart, mask, and unmask services, among other tasks.

Key systemctl Commands include:

- `systemctl start nginx`: Start a nginx service.
- `systemctl stop nginx`: Stop a nginx service.
- `systemctl restart nginx`: Restart a nginx service.
- `systemctl status nginx`: View the status of a nginx service.

If you only use start after making changes, you might experience a brief interruption in service as the old instance of Nginx continues to handle requests until the new instance fully starts. In summary, restart is often preferred over start in situations where you've made configuration changes to a running service, as it helps maintain continuous service availability during the configuration update process.

- `systemctl enable nginx`: To configure a service to start at boot time, use the `enable` command.
- `systemctl disable nginx`: Prevents a service from starting automatically at boot time.
- `systemctl is-enabled nginx`: This command is used to confirm if a service will start automatically at boot time.
  
`enable`, `disable`, `is-enabled`: These options are used to manage whether a service starts automatically at boot time.
`start, stop, and restart`: actions that refer to the current session, affecting what's happening to the service at the time of input.

- `systemctl mask nginx`: The `systemctl mask` command is used to mask a service unit, effectively making it impossible to start the service through `systemctl`. When you mask a service, you are creating a symbolic link from the service's unit file to /dev/null, which prevents `systemctl` from managing the service. To unmask, run `systemctl unmask nginx`.

- `systemctl list-units`: This command is used to display information about active units on the system. Units can include services, sockets, devices, mounts, and more
- `systemctl list-units --all`: It is used to display a list of all loaded units in the system, including active and inactive units 


# GRUB (GNU GRand Unified Bootloader):

GRUB is a boot loader used on many Unix-like operating systems, including most Linux distributions. Its primary function is to load the operating system kernel into memory and transfer control to it. GRUB offers a flexible and configurable way to manage the boot process.

Linux boot process has the following phases;

- Power Up: The system is powered on, initiating the boot process.
- Bootloader (GRUB): The bootloader, often GRUB (GNU GRand Unified Bootloader), is loaded. Its primary function is to locate and load the kernel into memory. GRUB presents the user with a boot menu if multiple operating systems are installed.
- Kernel Initialization: The kernel is loaded into memory by the bootloader. It initializes essential system components and drivers necessary for the system to function. During this phase, the kernel also loads an initial RAM disk (initramfs or initrd) into memory. This RAM disk contains the necessary drivers and utilities required for the subsequent stages of the boot process.
- Initramfs Stage: The kernel mounts the initial RAM disk and extracts its contents. The initramfs contain essential modules and executables needed to bootstrap the system and locate the root file system. It may include device drivers, disk encryption tools, and filesystem utilities.
- Root File System Initialization: The kernel locates and mounts the root file system as specified in the bootloader configuration. It may be located on a local disk, network drive, or other storage devices. Once the root file system is mounted, the kernel transitions control to the init process.
- Systemd Initialization: On modern Linux distributions, systemd is the initialization system that takes control after the kernel initializes. systemd starts as the first process with PID 1. It manages system services, mounts additional file systems, sets up network interfaces, and performs other initialization tasks necessary for the system to become fully operational.
- Service Initialization: systemd continues the boot process by starting essential system services in parallel. This parallelization improves boot times by executing services concurrently rather than sequentially. Once all necessary services are started, the system is ready for user interaction.

