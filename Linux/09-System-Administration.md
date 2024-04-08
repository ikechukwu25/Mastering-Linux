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
- * in the day or the week means every day or every week 
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


 # MOUNTING AND UNMOUNTING FILE SYSTEMS (df, mount, umount, fdisk, gparted)

If you want to access a file system that’s on another partition or disk, you need to mount it or logically attach it to an existing directory of the unique filesystem. Only root can mount partitions using the mount command.

In Linux, mounting is the process of making the contents of a storage device (like a USB drive or a hard disk) accessible at a specific location in your computer's directory structure. This location is called the "mount point," and it's like assigning a specific drawer in the filing cabinet for that storage device.

Sometimes the usb stick that has been attach is not mounted automatically like in the case of a disk partition or you want to mount it in another place or with other options, in linux a storage device is logically represented as a special char device in /dev. In Linux, storage devices, including USB sticks, are logically represented as special character devices in the /dev directory. Each device is assigned a specific file in the /dev directory. For example, a USB stick might be represented as /dev/sdb or a similar name. 
/dev/sdb: This is the device identifier for the storage device you want to mount. In Linux, storage devices are represented as block devices under the /dev directory.
