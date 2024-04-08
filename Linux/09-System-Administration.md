# TASK AUTOMATION AND SCHEDULING USING CRON (crontab)

Cron is a time-based job scheduler in Unix-like operating systems, enabling users to schedule commands or scripts to run periodically at fixed times, dates, or intervals. It runs as a daemon and is commonly used for automating repetitive tasks such as backups, disk space monitoring, and system updates. The scheduling information is stored in a file called the "crontab."

Key Components:

`crontab` command: Users interact with cron through the crontab command, which allows them to create, edit, and manage their cron jobs. Each user can have their own crontab, stored in the /var/spool/cron/crontabs/ directory.

System-wide Configuration: The /etc/crontab file serves as the system-wide crontab file, containing cron jobs that are not associated with a specific user. These jobs are executed under the system's context.

