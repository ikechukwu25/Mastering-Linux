# PROCESSES

A process is an executing instance of a program. When you run a program, the operating system creates a process for that program to execute. Each process has its own memory space, system resources, and state. In simple terms, a program in execution is considered a "process" while the elements of activity inside a process are called "threads". Threads are lightweight, independently scheduled processes that share the same resources, such as memory space, file descriptors, and other process-related attributes. Multiple threads can exist within the same process. Threads within the same process can run concurrently, providing a way to perform multiple tasks simultaneously.

A running instance of a program is called a process and it runs in its own memory space. Each time you execute a command, a new process starts. Each instance of a running command is a process, but not all commands create a process. Each background process has two IDs the Job ID and the Process ID.


In Unix-like operating systems, processes can be categorized into foreground, which interact directly with the user through the terminal, and background, which operate independently of the terminal.

- Foreground = These processes run in the foreground and interact with the user through the terminal. They may require user input and typically hold the terminal until they complete. Example:
  - `sleep 10` = This command executes a process that waits for 10 seconds before completing its task, effectively holding the terminal for that duration in a foreground process.

- Background = Background processes run independently of the terminal and do not require user interaction. They can be started from the command line with an ampersand (&) at the end of the command to run in the background. Example:
    - `sleep 10&` = This command initiates the "sleep" command as a background process, allowing other commands to be executed in the foreground without waiting for it to finish.
    - `ping -c 1 www.google.com > /dev/null 2>&1 &` =  runs the "ping" command in the background, sending one ICMP echo request to www.google.com and discarding both the output and errors, thus allowing the terminal to remain available for other tasks. /dev/null is a special file that serves as a bit-bucket or a null device.


## PROCESSES AND PSEUDO FILESYSTEMS

The kernel provides access to information about active processes through a pseudo filesystem that is visible under the /proc directory. Hardware devices are made available through special files under the /dev directory, while information about those devices can be found in another pseudo filesystem under the /sys directory.

Pseudo filesystems appear to be real files on disk but exist only in memory. Most pseudo file systems such as /proc are designed to appear to be a hierarchical tree off the root of the system of directories, files, and subdirectories, but in reality, only exist in the system's memory, and only appear to be resident on the storage device that the root file system is on.

A pseudo filesystem, also known as a virtual filesystem, is a special type of filesystem in Unix-like operating systems that presents information and resources in a hierarchical structure similar to traditional filesystems but does not correspond directly to physical storage devices. It is a type of filesystem that exists only in memory and is not backed by physical storage like traditional filesystems. 


They are stored in the system's RAM (Random Access Memory), whereas traditional filesystems are stored on physical storage devices such as hard disk drives (HDDs) or solid-state drives (SSDs).

The /proc directory not only contains information about running processes, as its name would suggest, but it also contains information about the system hardware and the current kernel configuration.

The /proc directory is read, and its information is utilized by many different commands on the system, including but not limited to `top`, `free`, `mount`, `umount`, and many many others. It is rarely necessary for a user to mine the /proc directory directly but it’s easier to use the commands that utilize its information.

The output shows a variety of named and numbered directories. There is a numbered directory for each running process on the system, where the name of the directory matches the process ID (PID) for the running process.

The /proc directory also contains information about the operating system and its hardware in files like /proc/cpuinfo, /proc/meminfo, and /proc/devices.

N/B: The /proc/sys subdirectory contains pseudo files that can be used to alter the settings of the running kernel. Since these files are not "real" files, an editor should not be used to change them; instead, you should use either the `echo` or the `sysctl` command to overwrite the contents of these files. For the same reason, do not attempt to view these files in an editor, but use the `cat` or `sysctl` command instead.
For permanent configuration changes, the kernel uses the /etc/sysctl.conf file. Typically, this file is used by the kernel to make changes to the /proc files when the system is starting up.

There are also some regular files in the /proc directory that provide information about the running kernel:

| File | Contents |
|-----|-----|
|/proc/cmdline |	Information that was passed to the kernel when it was first started, such as command line parameters and special instructions |
|/proc/meminfo |	Information about the use of memory by the kernel |
|/proc/modules |	A list of modules currently loaded into the kernel to add extra functionality |


## PROCESS HIERARCHY

When a Linux system boots up, the kernel initializes and starts the init process, which is assigned a Process ID (PID) of 1. The init process is responsible for initializing the system and starting other system processes. In System V-based systems, the init process is represented by the /sbin/init program, while in systemd-based systems, it's typically represented by /lib/systemd/systemd, although often symbolically linked to /bin/systemd.

Regardless of the type of init system used, information about the init process can be found in the /proc/1 directory. This directory provides details about the init process and allows system administrators and utilities to gather information about the system's initialization and process hierarchy.

As a Linux system runs, it assigns unique Process IDs (PIDs) to running processes. The maximum PID value that the system can assign is defined in the file /proc/sys/kernel/pid_max. When the system reaches this maximum value, it rolls over and starts assigning PIDs from the beginning of the range again. This ensures that the system can continue running without interruption, even after reaching the maximum PID value.

### PROCESS MANAGEMENT

fork() is a system call in Unix-like operating systems, including Linux. It's used for process creation, allowing a running process (referred to as the parent process) to create a new process (referred to as the child process).

The fork() system call generates a child process identical to the parent process. Subsequent to the fork() invocation, both parent and child processes resume execution from the forked point, albeit with distinct process IDs (PIDs).

**Types of processes.**

- Parent - "This is a program that uses the fork() system call to create a child process. It can create one or more child processes depending on how many times fork() is called within the program. </br>
- Child - This is the process created after the fork system call from the parent. 
- Daemon - Daemons are background processes that provide specific system services. They often start at boot time and run continuously. They are not interactive Eg: sshd (OpenSSH server), httpd (Apache web server).
- Zombie (defunct) - A terminated process whose data has not been collected. They don’t use any of the system resources. A process that has completed execution but has not been cleaned up by its parent.
- Orphan - Opposite of the zombie process. Orphan processes are those whose parent processes have terminated or no longer exist. They are adopted by the init process (PID 1).


## LINUX PROCESS MANAGEMENT COMMANDS

In Linux, process management commands are essential for monitoring, analyzing, and controlling processes running on the system. Here are some commonly used commands used to check if a specific process is running and it’s properties: `ps`, `pgrep`, `pstree`, and `top`. Any user can see this information.

**`ps` command**

The `ps` command in Linux is used to display information about active processes on the system. It allows users to view a snapshot of the currently running processes and their attributes which means that it provides a static view of the processes.

`ps -e` = Lists all processes </br>
`ps -f` = Displays detailed information about processes, including UID, PID, PPID, CPU utilization, start time, terminal type, CPU time, and command.</br>
`ps -ef` = Displays detailed information about all currently running processes. See output titles below;</br>
* UID: The numeric User ID (UID) of the user who owns the process.
* PID: Process ID, a unique identifier for each process.
* PPID: Parent Process ID, the PID of the parent process that spawned this process.
* C: CPU utilization as a percentage of total CPU time.
* STIME: Start time of the process.
* TTY: Terminal type associated with the process.
* TIME: Cumulative CPU time used by the process.
* CMD: The command or program that initiated the process.

`ps aux` = is commonly used in Linux to display a detailed list of information about all currently running processes. See output titles below;</br>
* USER: The user who owns the process.
* PID: Process ID, a unique identifier for each process.
* %CPU: CPU usage as a percentage of total CPU time.
* %MEM: Memory usage as a percentage of total physical memory.
* VSZ: Virtual memory size in kilobytes (KB).
* RSS: Resident set size, the portion of the process's memory held in RAM, in kilobytes (KB).
* TTY: Terminal type associated with the process.
* STAT: Process status, indicating whether the process is running, sleeping, stopped, etc.
* START: Start time of the process.
* TIME: Cumulative CPU time used by the process.
* COMMAND: The command or program that initiated the process.

`pgrep` = The `pgrep` command is used to search for processes by name and print their IDs. Examples:</br>
`pgrep sshd` OR `ps -ef | grep sshd` = pulls out the process information on sshd.</br>
`pgrep -l sshd` = This command shows the name and the PID of processes with the specified name.</br>

`pstree` = This command displays a hierarchical tie structure of the running processes. It visually represents the hierarchy and relationships between parent and child processes in a tree-like structure.</br>

`ps -axjf` = The command is used to display a hierarchical (tree) view of processes. </br>
* PPID: Parent Process ID, the PID of the parent process.
* PID: Process ID, a unique identifier for each process.
* PGID: Process Group ID, a unique identifier for each process group.
* SID: Session ID, a unique identifier for each session.
* TTY: Terminal type associated with the process.
* TPGID: Terminal Process Group ID.
* STAT: Process status, indicating whether the process is running, sleeping, stopped, etc.
* UID: User ID, the numeric user ID of the process owner.
* TIME: Cumulative CPU time used by the process.
* COMMAND: The command or program that initiated the process.


1. **`top` command**

The renice command allows users to adjust the priority of running processes by modifying their niceness values. The R key in the `top` command provides a convenient interface for users to interactively adjust process priorities based on their needs and system requirements. However, it's important to note the limitations and permissions associated with adjusting process priorities, especially with respect to root privileges.

When you're running the `top` or `htop` command, you can see the niceness value of processes listed in the process list. The niceness value is usually displayed in one of the columns, often labeled as "NI" or "Nice".

* Niceness Values: Niceness values range from -20 to 19 in Unix-like operating systems. A lower niceness value indicates a higher priority for the process, while a higher niceness value indicates a lower priority. The default niceness value for most processes is 0.
* Adjusting Process Priority with renice: The renice command is used to change the priority (niceness value) of running processes. It requires the PID (Process ID) of the process and the desired niceness value.

Examples: Let's say we have a  and we want to  We would use the following command:

`renice -10 1234` = This command increases the priority of process with PID 1234 by setting its niceness value to -10.

`renice -n -5 -p 1234` = This would decrease the niceness value (increase the priority) of the process with PID 1234 by 5.

It's important to note that adjusting process priorities with renice typically requires appropriate permissions. Modifying the priority of processes owned by other users usually requires root privileges. Additionally, changing process priorities can impact system performance and should be done carefully.


The `top` command provides a dynamic real-time view of the running system, displaying summary information and a list of processes or threads managed by the Linux kernel.

Commonly Used Options includes:

- -h: See help summary.
- -q: Exit the top screen.
- -1: View individual statistics for each CPU.
- -t: Change the CPU display to simple graphs and show the percentage of use for each CPU.
- -m: Change the memory and swap lines to different display options.
- -d: Change the delay value of the output refreshing time.
- Space key: Manually refresh the display.
- -e: Change the measurement units.
- -P: Sort processes by processor.
- -M: Sort processes by memory.
- -u: View process info for a particular user.
- -F: Customize which columns are displayed in the process list.
- -x and y: Toggle highlighting of the current sort column and running tasks.
- -W: Save changes made to settings.

Examples:

`top -d 1 -n 3 -b > filename.txt`: This command runs top in batch mode, refreshing every second for 3 iterations, and outputs the result to a file named filename.txt. This is useful for capturing the output for later analysis or processing.

-d 1: Sets the update interval of top to 1 second. This means that top will refresh its display every second. </br>
-n 3: Specifies that top will run for 3 iterations and then exit. In other words, it will collect information for 3 snapshots.</br>
-b: Runs top in batch mode. In batch mode, top outputs the result to standard output rather than to the terminal. This is useful when you want to capture the output in a file or process it further.</br>
\> processes.txt: Redirects the output of the top command to a file named processes.txt. This allows you to save the information for later analysis or review.

2. **`htop` command**

`htop` is indeed a more advanced and visually appealing version of the top command. It provides a dynamic, real-time view of system processes and resource usage, similar to top, but with additional features and improved usability. 

3. **`kill` command**

In Unix-like operating systems, process termination and signal management are crucial aspects of system administration. The `kill` command is a fundamental tool for terminating processes and managing their behavior through signal delivery. 

The primary function of the kill command is to terminate processes. It sends signals to processes, instructing them to terminate gracefully or immediately, depending on the signal sent. The `kill` command allows users to send various signals to processes. Each signal has a specific purpose, such as requesting termination (SIGTERM), forcing termination (SIGKILL), or initiating a reload of configuration files (SIGHUP).

`kill -l` = By running this command, it provides a list of signal names and their corresponding numbers, enabling users to choose appropriate signals for terminating or manipulating processes.

`pidof firefox` = This command allows users to retrieve the Process IDs (PIDs) associated with Firefox, facilitating targeted signal delivery.

Various forms of the kill command, such as `kill -2 $(pidof firefox)`, `kill -INT PIDs`, or `kill -2 PIDs`, effectively terminate processes by sending the SIGINT signal (interrupt).

`kill -2 $(pidof firefox)` = This command retrieves the PID of the Firefox process using pidof and sends the SIGINT signal (interrupt) to terminate it.

`kill -INT PIDs` = This command explicitly specifies the signal SIGINT by its name (INT) and terminates the processes with the given PIDs.

`kill -2 PIDs` = Similarly, this command sends the SIGINT signal to the processes specified by their PIDs, effectively terminating them.

All the three commands below achieve the same result of sending the SIGINT signal to the specified processes, resulting in their termination. It's essential to note that the signal number 2 corresponds to the SIGINT signal, making these commands functionally equivalent.

`kill -1` OR `kill -HUP` = These commands are equivalent and both send the SIGHUP (hangup) signal to the specified process. This signal is commonly used to instruct a process to reload its configuration files or to restart gracefully.

The /var/run directory serves as a repository for temporary runtime files, including PID files and other pertinent information related to active processes.

The `pkill` and `killall` commands provide alternative methods of sending signals to processes. `killall` terminates all processes with a specific name, while `pkill` offers partial name matching for more flexible process targeting.

`pkill firefox` = This command terminates all processes with the name "firefox". It matches the process name exactly.

`killall firefox` = This command terminates all processes with the name "firefox". It matches the process name exactly and does not accept partial names.

`killall -r "firefox.*"` = This command terminates all processes whose command line matches the regular expression "firefox.*". It allows for more flexible process targeting using regular expressions.


4. **`jobs` command**

Job control refers to the management and manipulation of processes in a Unix-like operating system. The jobs command is used to display a list of jobs that are running in the background or suspended in the current shell session. Jobs are processes that are started from the current shell session and can be either running in the background or suspended (stopped). 

`fg% job ID` = This command is used to bring a background process to the foreground. By specifying the job ID, you can specify which background job to bring to the foreground.

Ctrl + Z: Pressing Ctrl + Z suspends a process running in the foreground, pausing its execution and placing it in a suspended state.

`jobs`: The jobs command lists the current jobs along with their job IDs. It provides information about both background and suspended processes.

`bg % job ID` : The bg command is used to resume a suspended foreground process and move it to the background, allowing it to continue executing without user interaction.

`nohup`: The nohup command stands for "no hang up" and is used to run a command in a way that it ignores the hangup (HUP) signal. This ensures that the command persists even if the terminal session from which it was started is closed. For example, running `nohup sleep 344 &` will keep the sleep command running even after closing the terminal.

Job control provides users with flexibility and control over running processes, allowing for efficient management of tasks and resources in Unix-like systems.
