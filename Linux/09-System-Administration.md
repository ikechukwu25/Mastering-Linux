# TASK AUTOMATION AND SCHEDULING USING CRON (crontab)

Cron is a time-based job scheduler in Unix-like operating systems. It allows users to schedule jobs (commands or scripts) to run periodically at fixed times, dates, or intervals. The scheduling information is stored in a file called the "crontab."

Cron runs as a daemon and is utilized for automating repetitive tasks such as backups, monitoring disk space usage, and updating the system with the latest app version.

**Key Components**:

- `crontab` Command: This command is used to create, edit, and manage cron jobs for a user. Each user can have their own crontab file, stored in /var/spool/cron/crontabs/.
- /var/spool/cron/crontab: Contains individual user crontab files, allowing users to schedule tasks specific to their needs.
- /etc/crontab: System-wide crontab file, intended for system-wide cron jobs not associated with a specific user.

**Common Commands**:

`crontab -l`: Displays the content of the current user's crontab file.
`crontab -e`: Edits the current user's crontab file.
`crontab -r`: Removes the current user's crontab file.
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

`0 6,8,10 * */3 1-5 /root/backup.sh`

* Minute Field (0): This field is for the “minute”. The cron job is scheduled to run at the 0th minute of the specified hours.
* Hour Field (6,8,10): This field means “hour” The cron job is scheduled to run at the 6th, 7th, and 8th hours of the day (6 AM, 8 AM, and 10 AM).
* Day of Month Field (\*): The asterisk (*) in this field means "every day of the month." It doesn't restrict the cron job based on the day of the month.
* Month Field (*/3): This field means "every month." It doesn't restrict the cron job based on the month. The job is scheduled to run every 3 months. The */3 means "every 3 months."
* Day of Week Field (*): 1-5: The day of the week field, meaning Monday through Friday (1 is Monday and 5 is Friday).
* Command (/root/backup.sh): The command to be executed is /root/backup.sh.

<img width="760" alt="Screenshot 2024-04-08 at 23 23 12" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/a7e3ba1b-6b04-48e1-bcd1-7d959409c780">


<img width="813" alt="image" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/fdb0ff83-6a90-47f6-a61c-1194fa98a407">

This cron job will append the current date and time to the file today.txt in the user's home directory every 3 minutes past 10:00 AM on the 1st day of December every year.

`*/3 10 1 12 *`: Specifies the timing for the command:

- */3: Indicates that the command will run every 3 minutes.
- 10: The hour (10:00 AM).
- 1: The day of the month (1st day).
- 12: The month (December).
- *: The day of the week (any day).
- `date >> ~/today.txt`: The command to be executed. It appends the output of the date command (current date and time) to the file today.txt in the user's home directory (~).

The @yearly directive in a cron job is equivalent to the cron expression 0 0 1 1 *. It specifies that the associated command should be executed once a year, specifically at midnight on January 1st.

The @monthly cron expression is a special string used in cron to specify a monthly schedule. In this case, it is equivalent to the more detailed cron expression 0 0 1 * *, which means "at midnight on the first day of every month."

The @reboot cron expression is a special string used in cron to specify a schedule that runs once when the system starts or is rebooted.

System Files:

/etc/crontab: System-wide cron configuration file.
/etc/cron.daily: Directory containing daily cron jobs.
/etc/cron.weekly: Directory containing weekly cron jobs.

Additional Information:

- tail -f /var/log/syslog: Command to view the cron log file in Ubuntu, useful for monitoring cron job execution and troubleshooting.

- Root Privileges: Root can edit a user's crontab using the -u option. To edit a user's crontab as root;
  - `sudo su` = became root
  - `crontab -e -u username` = This command allows root to edit a user’s crontab.


# SCHEDULING TASKS USING ANACRON (anacron)

Anacron serves a similar purpose to cron but is designed for systems that are not continuously powered on, such as desktops or laptops. It operates with root privileges and executes tasks with a frequency expressed in days rather than minutes, as in cron. The configuration file for Anacron is located at /etc/anacrontab.

Anacron Job layout includes Days Delay Identifier Command

Days: Specifies the interval in days at which the command should be executed.
Delay: Identifies the delay in minutes before the command execution. This helps prevent system overload by staggering the execution of multiple tasks.
Identifier: This is a unique identifier for the job, typically the name of the associated script or task.
Command: The command to be executed.

Example; 

- `vim /etc/anacron`
  - <img width="799" alt="image" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/159a5029-a111-4433-8fa3-91a3bb0136d5">

`7	10	cron.weekly 		run-parts --report /etc/cron.weekly` </br>
`@daily	15			cron.weekly 		run-parts --report /etc/cron.weekly`

- 7 (days) = This means the command should be run every 7 days - weekly	
- 10 (minutes) = This identifies the delay in minutes. This is intended to keep the system from being overloaded with the jobs. If `anacron` determines that it needs to run several commands when it starts up, it won’t run them simultaneously but with a delay. 
- cron.weekly = This is a job identifier. It is the name of the file that will be created under /var/spool/anacron. This is also called the job timestamp file that will contain a single line that indicates the last time this job was executed.  The identifier identifies the job in the messages or the log files. 

**Additional Anacron Commands**:

- `anacron -T` = Checks for syntax errors in the Anacron configuration file.
- `anacron -d` = When `anacron` is run with the `-d` option, it provides more detailed output and information about its activities, which can be helpful for troubleshooting and understanding how it is scheduling and executing jobs.
- `sudo cat /var/spool/anacron` = Displays the log file containing information about Anacron job executions.


UNDERTSTANDING COMPUTER HARDWARE

The motherboard, or system board, is the main hardware board in the computer through which the central processing unit (CPU), random-access memory (RAM) and other components are all connected. 

A central processing unit (CPU or processor) is one of the most critical hardware components of a computer. The processor is the brain of the computer, where the execution of code takes place and where most calculations are done. It is directly connected (soldered) to the motherboard, as motherboards are typically configured to work with specific types of processors.

Processors are electronic circuits that execute instructions and perform calculations in a computing device. The term "processor" generally refers to the central processing unit (CPU) of a computer, which is responsible for executing program instructions, performing arithmetic and logic operations, and managing data movement within the system.

If a hardware system has more than one processor, the system is referred to as a multiprocessor.  If more than one processor is combined into a single overall processor chip, then it is called multi-core.
In summary, a multiprocessor system comprises multiple independent processors working together, whereas a multi-core processor integrates multiple processing cores onto a single chip. Both architectures enable parallelism and improve overall system performance, but they differ in their implementation and organization of processing units.

Although support is available for more types of processors in Linux than any other operating system, there are primarily just two types of processors used on desktop and server computers: x86 and x86_64.

On an x86 system, the system processes data 32 bits at a time; on an x86_64 the system processes data 64 bits at a time. An x86_64 system is also capable of processing data 32 bits at a time in a backward compatible mode. One of the main advantages of a 64-bit system is the ability to work with more memory, while other advantages include increased efficiency of processing and increased security.

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
`Buses`

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
- `sudo fdisk -l` : used to list information about all the available disk drives and their partitions on your system.
  - `fdisk`: It is a command-line utility for disk partitioning. 
- `lsblk` : This command will provide a hierarchical view of the block devices attached to your system, along with information about their partitions and mount points. You can run the `dmesg` and `lsblk` (lists all block devices) commands to find the name of the device.

**Unmounting**

- `sudo umount /home/ikechukwu/file`: Unmounts the filesystem located at /home/ikechukwu/file.
- `sudo umount -l /home/ikechukwu/usb`: This command will unmount the filesystem located at /home/ikechukwu/usb. Make sure there are no active processes or open files on the mounted filesystem before attempting to unmount it.

N/B: When a USD drive or hard drive is connected, they can be located at the media directory. Also, make sure that no processes or applications are actively using the mounted filesystem before attempting to unmount it. If any processes are still accessing the filesystem, you may encounter an error.

**Tips for Mounting**

- Create a mount point.
- Use `mount -l` to check the initial mount point of the external device.
- Confirm the block device file using `lsblk`.
- Utilize graphical tools like `GParted` for disk partition management (`sudo apt install gparted` to install).




