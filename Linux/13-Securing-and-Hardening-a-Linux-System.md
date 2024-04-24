# SECURING AND HARDENING A LINUX SYSTEM

Securing and hardening a Linux system involves implementing various measures to enhance the security posture of the system. This includes configuring security settings, restricting access, monitoring for suspicious activities, and implementing best practices to mitigate potential vulnerabilities.

## LINUX SECURITY CHECKLIST

The Linux Security Checklist provides a structured approach to enhancing the security of Linux systems. It covers a wide range of security measures, including physical security, software updates, user management, network security, and monitoring. Following this checklist helps ensure that Linux systems are adequately protected against potential threats and vulnerabilities.

INFOSEC: This stands for Information Security, encompassing fundamental principles guiding secure practices. It emphasizes skepticism, risk awareness, and the constant pursuit of enhancing security measures to safeguard digital assets effectively. Below are basic principles to be followed: </br>
- Do not assume anything.
- Nothing is secure.
- Trust no one, nothing.
- Security is a trade-off with usability.
- Paranoia is your friend.</br></br>

The following are comprehensive security checklists divided into three sections for securing Linux systems. These checklists cover various aspects of system security, including physical security, software protection, access control, network security, monitoring, and backup procedures.

- Security Checklist - 1
  - Ensure Physical Security.
  - BIOS Protection.
  - Disable Booting from external media devices.
  - Boot Loader Protection.
  - Keep the OS updated (only from trusted sources).
  - Check the installed packages and remove the unnecessary ones.
  - Check for Open Ports and stop unnecessary services.
  - Enforce Password Policy.
  - Audit Passwords using John the Ripper.
  - Eliminate unused and well-known accounts that are not needed.
  - Give users limited administrative access. 
  - Do not use the root account on a regular basis and do not allow direct root login.


- Security Checklist - 2
  - Set limits using the ulimit command to avoid DoS attacks such as launching a fork bomb.
  - Set proper file permissions.
    - Audit the Set User ID (SUID) and Set Group  ID (SGID) binaries on the system.
    - Do not mount remote filesystems with root read-write access. Read-only access would be enough.
    - Set the sticky bit on any world-writable directories.
    - Harden /tmp – mount it on a separate partition (not to fill all the disk space), mount it with noexec,nosuid bits set.
  - Implement File Monitoring (Host IDS - AIDE).
  - Scan for Rootkits, Viruses, and Malware (Rootkit Hunter, chkrootkit, ClamAV).
  - Use Disk Encryption to protect your data. Don’t forget to encrypt your Backups as well.
  - Secure every Network Service especially SSHd.



- Security Checklist - 3
  - Scan your Network and Hosts using Nmap.
  - Securing Your Linux System with a Firewall (Netfilter/Iptables).
  - Monitor the firewall and its logs.
  - Monitor your logs and search for suspicious activity (logwatch).
  - Scan your servers using a VAS such as Nessus or OpenVAS.
  - Make backups and test them


Stay up to date on security trends by receiving vulnerability alerts from pages like [Center for Internet Security](https://www.cisecurity.org/) and [CERT Coordination Center](https://kb.cert.org/vuls/report/)


## SECURING THE OPENSSH SERVER (sshd)

Securing the OpenSSH Server (sshd) focuses on enhancing the security of remote access to a Linux system by configuring the OpenSSH server. This involves adjusting settings in the `sshd_config` file, such as changing the default port, disabling direct root login, limiting user access, and implementing additional security measures. Properly securing OpenSSH helps mitigate potential security risks and unauthorized access to the system.

- `sudo vim  /etc/ssh/sshd_config`: This command is used to open  the configuration file for the OpenSSH server (sshd).
- `man sshd_config` -  This command is used to view the manual page for the `sshd_config` file.

Utilize the below options to secure the OpenSSH server (sshd) to enhance the security of remote access to the Linux system.

- Change from `port 22` to a random port to avoid being seen by casual scans but not by targeted attacks. After changing the port, you have to update the firewall rules to allow traffic on the new port.
  - `sudo ufw allow 2222/tcp` or `sudo iptables -A INPUT -p tcp --dport 2222 -j ACCEPT`: Both commands accomplish the same task of allowing incoming TCP traffic on port 2222.
- `PermitRootLogin no`: Disable direct root login.
- `AllowUsers ikechukwu`: Use `AllowUsers` directive in `sshd_config` to limit SSH access to specific users. However, if there are only a few admins that use SSH for remote management, then accept connections to the SSH only from a limited list of source IP addresses.
  - Allow SSH connections from the specified source IP addresses:
    - `iptables -A INPUT -p tcp --dport 2245 -s IP ADDRESS -j ACCEPT` 
    - `iptables -A INPUT -p tcp --dport 2245 -s IP ADDRESS 2 -j ACCEPT`
  - Drop SSH connections from all other source IP addresses:
    - `iptables -A INPUT -p tcp --dport 2245 -j DROP`
- `LoginGraceTime`: This parameter specifies the time window during which a user must authenticate after establishing an SSH connection. If the user fails to authenticate within this grace period, the connection is terminated.
- `ClientAliveIntervals`: This parameter specifies the interval at which the server sends keep-alive messages to connected SSH clients. These keep-alive messages help maintain the SSH connection by checking if the client is still responsive.
- `ClientAliveMaxCount`: This parameter determines the maximum number of client alive messages (keep-alive messages) that can be sent without any response from the client. If the client does not respond to the keep-alive messages within this count, the SSH server will terminate the connection.This helps improve resource utilization and security by closing inactive connections in a timely manner.
- `MaxAuthTries`: This determines the maximum number of authentication attempts permitted per connection. If a user exceeds this limit while attempting to authenticate (e.g., by entering incorrect passwords), the SSH server will terminate the connection.

N/B: DO NOT FORGET TO REMOVE COMMENTS AFTER EDITING

It's crucial to remove comments after editing configuration files, including `sshd_config`. Comments are helpful for documentation and understanding, but they don't have any impact on the server's behavior. Keeping unnecessary comments can clutter the file and make it harder to read, so it's a good practice to clean them up after making changes to ensure clarity and maintainability.


## SECURING THE BOOT LOADER (Grub)

Securing the Boot Loader (GRUB) involves implementing measures to protect the GRUB (Grand Unified Boot Loader) configuration from unauthorized access or tampering. This includes setting a password to restrict access to the GRUB menu, enabling secure boot options, and configuring other security features provided by GRUB to prevent unauthorized modification of the boot process. Securing the boot loader helps prevent unauthorized changes to the system's boot configuration, enhancing overall system security.

The boot sequence order outlines the steps involved in starting a computer system:

- BIOS Executes MBR (Master Boot Record): The Basic Input/Output System (BIOS) initializes hardware and executes the Master Boot Record (MBR) stored on the boot device.
- MBR Executes GRUB2: The MBR then loads and executes the GRUB2 (Grand Unified Boot Loader) bootloader, which is responsible for managing the boot process and loading the operating system.
- GRUB2 Loads the Kernel: GRUB2 loads the kernel of the operating system specified in its configuration. The kernel is the core component of the operating system responsible for managing system resources and executing user programs.
- Kernel Executes systemd: Once the kernel is loaded, it executes systemd, which initializes the system by starting essential system services and processes. systemd is a system and service manager for Linux operating systems.


The process of securing the GRUB bootloader involves several steps listed below:

- **Generate Hashed Password**: Use the command - `grub-mkpasswd-pbkdf2` in the GRUB bootloader to generate hashed passwords using the PBKDF2 algorithm.
- **Edit GRUB Configuration**: The next step is to edit the GRUB main config file and add the hash of the password so your actual password is not visible in the GRUB scripts and a possible hacker cannot see it. The config file is `/boot/grub/grub.cfg`. </br> However, this file can’t be modified directly by the user. It is overwritten by certain grub updates whenever a kernel is added or removed or when the user runs the `update-grub2` command. So, grub uses a series of scripts to build this configuration file which are located in `/etc/grub.d`. We need to change the files in this directory and run `update-grub2`. This command based on the content of the files in `/etc/grub.d` will generate `grub.cfg` the main configuration file. 
- **Edit 40_custom Script** (`sudo vim /etc/grub.d/40_custom`): Using the vim text editor to open and edit the file `40_custom` in the `/etc/grub.d/` directory. This file is part of the GRUB bootloader configuration and allows you to add custom menu entries.
- **Add Password Hash**: Add the following commands to input the hash for the password in the config file; `set superuser=“root”` and `password_pbkdf2 root HASH`
- **Update GRUB Configuration**:The command - `sudo update-grub2` will generate the new `grub.cfg` file - `/boot/grub/grub.cfg`. 
- **Reboot**: Reboot the system (`sudo reboot`) to confirm that it prompts for the password upon booting. Enter the username (root) and the password when prompted.


## ENFORCING PASSWORD POLICY

Enforcing a password policy is essential for maintaining strong security practices within a system. These are the set of rules that must be satisfied usually defining password aging, length and complexity, number of login failures, and if resting old password is allowed or denied. Below are important component;

- etc/login.defs: This is a configuration file used by the `login` and `passwd` commands on Linux systems. It contains various settings and parameters that influence user authentication, password aging, and other login-related behaviors. 
  - `PASS_MAX_DAYS`: Specifies the maximum number of days a password is valid. After this period, the user is required to change their password.
  - `PASS_MIN_DAYS`: Specifies the minimum number of days that must pass before a user can change their password again.
  - `PASS_WARN_AGE`: Specifies the number of days of warning before a password expires and a user is notified.
  - `PASS_MIN_LEN`: Sets the minimum acceptable password length.

- `man login.defs`: To view the manual page for the /etc/login.defs configuration file, you can use the man command followed by the path to the file. This command will display the manual page for the login.defs file, providing detailed information about its configuration options and parameters.

To adjust the password expiration settings for existing user accounts, you can use the `chage` command. Below are ways to utilise the command:
- `sudo chage -M MAX_DAYS USERNAME`: To set the maximum number of days between password changes (-M option). Replace MAX_DAYS with the desired maximum number of days between password changes, and USERNAME with the username of the user whose password expiration settings you want to modify.
- `sudo chage -l USERNAME`: To display the current password aging information (-l option). Replace USERNAME with the username of the user whose password aging information you want to view.


#### PAM

PAM, or Pluggable Authentication Modules, is a critical framework in Unix-like operating systems for providing a flexible and extensible authentication mechanism. By separating authentication processes from applications requiring authentication, PAM allows system administrators to centrally manage and configure authentication policies. 

One common use of PAM is enforcing password complexities in Linux distributions. The `/etc/pam.d/common-password` file (or `/etc/pam.d/system-auth` in Red Hat and CentOS) plays a vital role in this by defining PAM rules and modules related to password management shared across multiple services.

To implement password complexity rules using PAM in Ubuntu-based distributions, you can follow these steps:

- `sudo apt install libpam-pwquality`: Install the libpam-pwquality package, which provides PAM support for password quality checking.
- `sudo vim /etc/pam.d/common-password`: Open the /etc/pam.d/common-password file for editing.
- `password requisite pam_pwquality.so retry=3 minlen=8 difok=3 ucredit=-1 lcredit=-1 dcredit=-1 ocredit=-1`
  - password: This indicates that the line is related to password management.
  - requisite: This is a control flag, and it means that if this module fails, the authentication process is immediately aborted, and the user is denied access.
  - pam_pwquality.so: This is the PAM module responsible for checking password quality. It enforces rules related to password strength, including length, character composition, etc.
  - retry=3: If the password fails to meet the specified criteria, the user is given three attempts (retry=3) to set a valid password.
  - minlen=8: Specifies the minimum length for the password. In this case, the minimum length is set to 8 characters.
  - difok=3: Specifies the number of characters that must differ when changing a password. In this case, at least 3 characters must be different from the previous password.
  - ucredit=-1, lcredit=-1, dcredit=-1, ocredit=-1: These settings control the requirements for uppercase (ucredit), lowercase (lcredit), digit (dcredit), and 	other (ocredit) characters in the password. A value of -1 means that there is no requirement for that category.
    * ucredit=-1: implies that the password should have at least an uppercase character
    * lcredit=-1: implies that the password should have at least a lowercase characters
    * dcredit=-1: implies that the password should have at least a digital character - number
    * ocredit=-1: implies that the password should have at least another (special) character.

## LOCKING OR DISABLING USER ACCOUNTS

To lock or disable user accounts in Linux, you can use various commands to control access and ensure security as seen below:

- `sudo passwd - -lock/-l USERNAME`: This command is used to lock a specific user’s account. 
- `sudo passwd - -status/-S USERNAME`: This command is used to display the status of a user account.
  - Output: USERNAME LK 2023-01-01 0 99999 7 -1 (Password locked.)
    * USERNAME: The username for which you are checking the password status.
    * LK: Indicates that the password is locked.
    * 2023-01-01: Date of the last password change.
    * 0: Minimum number of days between password changes.
    * 99999: Maximum number of days the password is valid.
    * 7: Number of days before a password is set to expire that the user is warned.
    * -1: Number of days after a password has expired before the account is disabled.

N/B: There will be an exclamation mark in the hash password of the user in /etc/shadow, which denotes that the user is currently locked.

- `sudo usermod --expiredate 1 USERNAME`: To completely disable an account, use this command. The command `sudo usermod --expiredate` command in Linux is used to set the expiration date for a user account. The `--expiredate` option specifies the date when the user account should be disabled. In your command, you have set the expiration date to 1, which means the user account will be disabled starting from January 1, 1970 (the Unix epoch).

- `sudo usermod --expiredate "" iyke`: To reenable the account and change the expiry date to never, use this command.


## GIVING LIMITED ROOT PRIVILEGES (sudoers and visudo)

To manage users' access to administrative tasks using `sudo`, you can configure the sudoers file (/etc/sudoers) on Unix-like systems. `etc/sudoers` is a critical configuration file that defines the rules and permissions for allowing or denying users and groups the ability to execute commands as superusers (root) or other users through the sudo command. The file should only be edited using the `visudo` command, which provides syntax checking and prevents simultaneous edits by multiple users.

`visudo` command is used to edit the sudoers file (/etc/sudoers) on Unix-like systems. The reason for using visudo instead of directly editing the sudoers file with a regular text editor (such as nano or vim) is to ensure proper syntax and avoid potential errors.

`cat /etc/group | grep -i sudo`: This command is used to view the users that can run administrative tasks using `sudo`. 
`sudo update-alternatives --config editor`: This command on Linux is used to set the default text editor for system-wide use. When executed, it presents a menu that allows you to choose from the available text editors installed on your system. 

After giving the sudo password for the first time, it caches the credentials on the terminal for 15 minutes. After that, any other administrative sudo command will request a password. 

If a user is in the sudo group, he/she can run all administrative tasks. However, you can limit this access to allow the user to be able to update the system and not edit the configuration files. To do this, follow the steps below;

- `sudo visudo`: Open the configuration file of the users that can use the sudo command.
- `Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"`: Configure the secure path that will be used for the sudo commands. 
- In the "User privilege specification" section, specify the users and commands they're allowed to run as root.
  - \# User privilege specification
  - root                  ALL=(ALL:ALL) ALL
  - `USERNAME     ALL=(root)                    (path to the command it is allowed to run as root)
      - Replace USERNAME with the actual username and specify the path to the commands they can run with sudo.
- `which ls`: This command shows the path to the command `ls`, do the same for the command which you intend to give sudo access to the user. 
- `peter     ALL=(root)      PASSWD:/usr/bin/cat,/usr/bin/ls,NOPASSWD:/usr/bin/apt`: To set specific privileges like password requirements or exclusion. This example allows the user to run `ls` and `cat` commands with a password prompt, while `apt` can be run without a password.


The sudoers file can be organised easily by grouping things in aliases, here's how it works:

`User_Alias MYADMIN=peter,stephen`</br>
\# User alias specification: Defines a user alias named MYADMIN, including users like peter and stephen. This alias simplifies management by grouping multiple users.

`Cmnd_Alias FILE=/usr/bin/cp,/usr/bin/ls/,/usr/bin/touch,/usr/bin/rm`</br>
\# Cmnd alias specification: Specifies a command alias named FILE, containing commands related to file manipulation (cp, ls, touch, rm). This alias makes it easier to manage permissions for multiple commands.

`root    ALL=(ALL:ALL) ALL` </br>
`peter   ALL=(root)      PASSWD:/usr/bin/cat,/usr/bin/ls,NOPASSWD:/usr/bin/apt`</br>
`MYADMIN ALL=(root)      FILE`</br>
\# User privilege specification: Assigns privileges to users or user aliases. Here, root has full access. peter can run ls and cat with a password prompt, and apt without a password prompt. Members of the MYADMIN alias have access to commands specified in the FILE alias.


* MYADMIN: This is a user alias defined earlier in the file, including users like peter and stephen. The alias is used to group multiple users for the sake of brevity and easier management.
* ALL=(root): This part specifies that the members of the MYADMIN alias can run commands as the root user.
* FILE: This is a command alias defined earlier in the file, including commands related to file manipulation like /usr/bin/cp, /usr/bin/ls, /usr/bin/touch, and /usr/bin/rm.


## SETTING USERS’ LIMITS (Running a DoS Attack Without root Access)

Running a Denial of Service (DoS) attack without root access is possible through various means, such as resource-intensive scripts or network flooding. Below are steps on how to create a fork bomb script: 

- `vim bomb`: Create a new shell script
  - #!/bin/bash
  - `$0 && $0 &` - This command will hang/crash the system and hence result to force a reboot. This command can be run by the user without administrative access. This script performs a denial of service attack that makes use of the fork system call to create an infinite number of processes. $0 is a special variable that represents the script itself. So, the script is running itself recursively two times and is going in the background for another recursive call. & at the end puts the process in the background. So new child processes cannot die and start eating the system resources. 

### HOW TO PREVENT A FORK BOMB. 

A fork bomb is a type of denial-of-service (DoS) attack that exploits the fork() system call in Unix-like operating systems. The fork bomb's goal is to overwhelm the system by creating a large number of processes, causing resource exhaustion and making the system unresponsive. E.g `$0 && $0 &` as described above. 

- `ulimit -u` is used to display or set the user process resource limit, specifically the maximum number of processes a user can create.
  * When used without any arguments, `ulimit -u` displays the current maximum process limit for the user.
  * When used with an argument, such as `ulimit -u 100`, it sets the maximum process limit for the user to the specified value (100 in this case).

To prevent the fork bomb, we’ll reduce the number of processes the user can start. The processes cannot continue to replicate themselves. 

`/etc/security/limits.conf` file is used to set resource limits for user processes in Unix-like operating systems. It allows system administrators to define specific limits on resources such as CPU time, memory, file descriptors, and more for individual users or groups.

- `sudo vim /etc/security/limit.conf`: 
- `ikechukwu       hard    nproc           2000 @admin          hard    nproc           4000` # End of file
  * `User "ikechukwu"`:
    * `ikechukwu hard nproc 2000`: This sets a hard limit for the user "ikechukwu" to a maximum of 2000 processes.
  * Group "@admin":
    * `@admin hard nproc 4000`: This sets a hard limit for the group "@admin" to a maximum of 4000 processes.


DIFFERENCE
* Editing `/etc/security/limits.conf` is a way to set default resource limits for users globally on the system. Changes in this file affect all future logins for the specified users or groups.
* Using the `ulimit` command is a way for a user to adjust resource limits for the current session only. These changes are temporary and do not persist after the user logs out.


## INTRO TO CRACKING PASSWORDS

Cracking Passwords

1. Brute-force or dictionary attack: It means using automated software that systematically checks all possible passwords until the correct one is found. It's a trial-and-error process in which the hacker computes the hash of each word in a dictionary or a word list and then compares the resulting hash to the hash of the password.

2. Rainbow tables: These are precomputed tables used for reversing cryptographic hash functions, usually used for cracking password hashes.

DIFFERENCES

**Brute Force**
* Method: Brute force is a straightforward and exhaustive method where the attacker systematically tries every possible combination until the correct one is found.
* Efficiency: It is often time-consuming and resource-intensive, especially for complex and strong passwords.
* Applicability: Brute force attacks are applicable to any encryption or authentication system. They don't rely on precomputed data.

**Rainbow Table**
* Method: Rainbow table attacks involve using precomputed tables containing hashes of many possible passwords. These tables significantly reduce the time needed to crack a password.
* Efficiency: Rainbow tables are more efficient than brute force because they eliminate the need to compute the hash for each attempted password during the attack. Once the tables are generated, the attack becomes a simple lookup process.
* Applicability: Rainbow tables are effective against hashed passwords. They exploit the fact that many users use common passwords, and the precomputed tables store these hashes for quick retrieval.

Visit the website - [have i been pwned?](https://haveibeenpwned.com/), to check if your email address has been compromised in a data breach. If your email is on the list, it means that the hacker has the hash of your password and they could try to hack it offline. 

### CRACKING LINUX PASSWORDS USING JOHN THE RIPPER

JTR has three cracking modes: John the Ripper is a widely used open-source password-cracking software. It supports various cracking modes or attack methods to attempt to recover passwords. Some of the key cracking modes in John the Ripper include:

1. Single crack mode: It uses the login names together with other fields from the passwd file, also with a large set of mangling rules applied. This is the fastest cracking mode and is applicable to very simple passwords.
2. Dictionary Attack / Wordlist Attack: In this mode, you need to supply a dictionary file that contains one word per line and a password file. You can enable word mangling rules which are used to modify or "mangle" words producing other likely passwords.
3. "Incremental" mode: This is the most powerful cracking mode because it will try all possible character combinations as passwords. If you supply a random password with a length of more than 12-14 chars will never terminate and you’ll have to interrupt it manually.

**FOR SINGLE CRACK MODE**: 

`sudo apt install john`: Install the package for John the Ripper. 
`john -test`: This command is used to test if John the Ripper is working correctly on your system.
`unshadow /etc/passwd /etc/shadow > unshadow.txt`: Combine /etc/passwd and /etc/shadow into a file (e.g., unshadow.txt), which contains the necessary information for password cracking.
`cat unshadow.txt`: Displays the contents of the unshadow.txt file to verify that the combination was successful.
`john --single --format=crypt unshadow.txt`: Here, john is the command to execute John the Ripper. The `--single` flag indicates that we're using single crack mode. The `--format=crypt` flag specifies the hash format. unshadow.txt is the input file containing the combined password hashes.
`john --show unshadow.txt`: This command displays the cracked passwords found by John the Ripper.
`cat ~/.john/john.pot`: The file contains the cracked password hashes. This command displays the contents of that file.

The ~/.john/john.pot file in John the Ripper contains the cracked password hashes. It's essentially a "pot" where John stores the results of its successful password-cracking attempts. Each line in this file typically represents a cracked password and its corresponding hash.

**FOR DICTIONARY ATTACK**:

/usr/share/john directory typically contains various resources used by the tool, including wordlists, rules, and configuration files.

/usr/share/dict/american_english typically contains a list of words from the American English language. This file is often used as a wordlist in various applications, including password-cracking tools, spell checkers, and other linguistic applications.

`john --wordlist=/usr/share/john/password.lst --rules unshadowed.txt`: In this command, `--wordlist=/usr/share/john/password.lst` specifies the path to the wordlist file to be used for the dictionary attack. `--rules` option enables rule-based mangling of words. unshadowed.txt is the input file containing password hashes obtained using unshadow.


## SCANNING FOR ROOTKITS (rkhunter and chkrootkit)

A rootkit is a collection of malicious computer software designed to enable access to a computer that is not otherwise allowed. After a successful intrusion into a system, usually the intruder will install a so-called "rootkit" to secure further access. Rootkit detection is difficult because a rootkit may be able to subvert the software that is intended to find it (rootkit scanners, antivirus).  

Rootkit Scanners: 
- Rootkit Hunter (rkhunter) 
  - `rkhunter --check`
- chkrootkit 
  - `chkrootkit -q`

**Rootkit Hunter (rkhunter)**

One of the checks `rkhunter` performs is to compare various current file properties of various commands against those it has preciously stored. 

`sudo apt update && sudo apt install rkhunter`</br>
`sudo rkhunter --propupd`: used with Rootkit Hunter (rkhunter) to update its file properties database. When you run `rkhunter --propupd`, you are updating the baseline information about the system's file properties. This information includes checksums, file permissions, and other attributes that `rkhunter` uses to identify changes that might be indicative of a compromise.</br>
`sudo rkhunter --check`: This command performs various checks on the local system. The result of each test will be displayed on the terminal and if anything suspicious is found, then a warning will be displayed. A log file of the test and results will be automatically created in /var/log. </br>
`sudo rkhunter --check --report-warnings-only`: used to run a security scan with `rkhunter` while instructing it to report only warnings, not informational messages.

When `rkhunter` reports a warning that is a false positive, you can mute the warning by whitelisting the file in the `rkhunter` config file - `vim /etc/rkhunter.conf` and append - `SCRIPTWHITELIST=/usr/bin/lwp-request`.


**chkrootkit**

`sudo chkrootkit -q`: It is a security tool used to check for the presence of rootkits on a Linux system. Similar to `rkhunter`, it scans the system for signs of known rootkits, suspicious files, and other indicators of compromise. With the `-q` option, it runs in quiet mode.


## SCANNING FOR VIRUSES WITH ClamAV

Antivirus isn’t necessary in a Linux system but for the Windows systems which could carry a malicious virus from a file and can be transferred into another file in another Windows system. Hence, they are being installed to protect the Windows devices from other Windows devices. E.g ClamAV 

ClamAV is an open-source antivirus engine designed for detecting various types of malicious software, including viruses, malware, and phishing. It's primarily used for scanning files on Linux systems, but it can also be deployed on other platforms.

`clamd`: This is the ClamAV daemon, and it plays a crucial role in providing real-time antivirus scanning capabilities. The daemon runs in the background, continuously monitoring files, processes, and data streams for potential malware.

`clamdscan`: This is used as a client to communicate with the ClamAV daemon (clamd). The ClamAV daemon runs in the background and provides real-time scanning capabilities, making it more efficient for continuous monitoring of files for malware.

`clamscan`: It is used for scanning files and directories on a Linux system to detect and remove potential malware, viruses, or other malicious software. It's the on-demand scanner component of ClamAV, and it allows users to initiate manual scans as needed

`systemctl status clamav-freshclam.service`: Used to check the status of the ClamAV Freshclam service.

`systemctl status clamav-daemon.service`: Used to check the status of the ClamAV daemon service.


## FULL DISK ENCRYPTION USING DM-CRYPT AND LUKS

Encrypting disks and partitions in Linux which keeps data secured using dm-crypt and LUKS. It is recommended to backup the drive first before running the commands as the commands will Destroy all data on the disk. 

It is a full disk encryption solution for Linux based OS and if you want to access the encrypt disk, you must install another software. Below is a comprehensive guide to encrypting disks and partitions in Linux using dm-crypt and LUKS.

1. `sudo apt install cryptsetup`: Install the `cryptsetup` which is used for setting up encrypted filesystems and managing encrypted volumes. It provides a command-line interface for creating, accessing, and managing encrypted partitions or disk volumes. </br>
If you want to encrypt only the partition and not the entire disk, and a partition's name always ends in a digit. 

2. `dd if=/dev/urandom of=/dev/sdb status=progress`: This is a dangerous command that writes random data from /dev/urandom to the entire disk /dev/sdb. This operation effectively overwrites all existing data on the disk with random data, which makes the data irrecoverable.

3. `sudo cryptsetup -y -v luksFormat /dev/sdb`: The option `-y` is used to ask for a passphrase `-v` is for verbose. This command is used to format a block device (/dev/sdb in this case) with LUKS (Linux Unified Key Setup) encryption, which is commonly used to encrypt disk partitions on Linux systems. Let's break down the components of the command: </br>
    * `cryptsetup`: This is the command-line tool used to manage encrypted volumes on Linux.
    * `-v`: This option stands for "verbose" and instructs cryptsetup to provide more detailed output during the formatting process.
    * `-y`: This option prompts the user to confirm before overwriting existing data on the device. It's a safety measure to prevent accidental data loss.
    * `luksformat`: This sub-command tells cryptsetup to format the specified block device with LUKS encryption.
    * `/dev/sdb`: This is the path to the block device that will be formatted with LUKS encryption. It's important to ensure that you specify the correct device, as formatting will erase all data on it.

4. `cryptsetup luksOpen /dev/sdb secretdata`: This command is used to open a LUKS-encrypted partition/device (/dev/sdb in this case) and map it to a device mapper device named secretdata. Let's break down the components of the command: </br>
    * `cryptsetup`: This is the command-line utility used to manage encrypted volumes on Linux systems.
    * `luksOpen`: This sub-command is used to open a LUKS-encrypted device.
    * `/dev/sdb`: This is the path to the LUKS-encrypted block device you want to open. It could be a partition or an entire disk.
    * `secretdata`: This is the name you're assigning to the mapped device. After successfully running this command, you'll be able to access the decrypted data on /dev/mapper/secretdata.

5. `ls -l /dev/mapper/secretdata`: Lists information about the device mapper device secretdata, confirming that it has been successfully created.

6. `mkfs.ext4 /dev/mapper/secretdata`: Creates an Ext4 file system on the device mapper device /dev/mapper/secretdata, allowing the encrypted data to be stored in a usable file system format. Let's break down the components of the command: </br>
    * `mkfs.ext4`: This is the command used to create an Ext4 file system on a block device. Ext4 is a widely used file system type in Linux environments.
    * `/dev/mapper/secretdata`: This is the device mapper device representing the LUKS-encrypted device you previously opened. After unlocking the LUKS volume and mapping it, you can create a file system on it using `mkfs.ext4`.

7. `mount /dev/mapper/secretdata /mnt/`: Finally, we mount the encrypted file system to the file tree - `mount /dev/mapper/secretdata /mnt`. Data is protected when the disk is not mounted, but when it’s mounted, it is accessible by usually anyone. When you unmount the disk, data will be inaccessible.

8. `umount /mnt/`: Unmounts the encrypted file system from the mount point /mnt/, ensuring that the data is no longer accessible or you can mount to a new directory.

9. `mkdir /root/secretdata`: Creates a new directory named secretdata in the /root/ directory to mount the encrypted file system.

10. `mount /dev/mapper/secretdata /root/secretdata`: Mounts the encrypted file system represented by /dev/mapper/secretdata to the directory /root/secretdata, providing access to the decrypted data.

11. `cryptsetup luksClose /dev/mapper/secretdata`: Closes the LUKS volume represented by /dev/mapper/secretdata after unmounting the encrypted file system, ensuring that the encrypted data is no longer accessible.

These commands provide a step-by-step process for encrypting disks and partitions in Linux, ensuring data security while also allowing controlled access to decrypted data when needed.


### UNLOCKING LUKS ENCRYPTED DRIVES WITH A KEY FILE

1. `root@ubuntu-22-04-3:/home/ikechukwu# dd if=/dev/urandom of=/root/keyfile bs=1024 count=4`: This command generates a file named keyfile in the /root directory filled with random data sourced from /dev/urandom. Let's break down the components of the command: </br>
    * `dd`: This command is used for converting and copying files. It's commonly used for low-level operations like copying data between devices.
    * `if=/dev/urandom`: The if flag specifies the input file. In this case, `/dev/urandom` is a special file in Unix-like operating systems that provides an endless stream of pseudo-random bytes.
    * `of=/root/keyfile`: The of flag specifies the output file. In this case, it's `/root/keyfile`, meaning the generated random data will be written to a file named keyfile in the /root directory.
    * `bs=1024`: The bs flag sets the block size, which determines how much data is read and written at a time. In this case, it's set to 1024 bytes (1 KB).
    * `count=4`: The count flag sets the number of blocks to copy. In this case, it's set to 4, so the command will generate a file containing 4 KB of random data.

2. `chmod 400 /root/keyfile`: This command sets the permissions of the keyfile to read-only for the owner (root) and denies all permissions to others, ensuring that only the root user can read the keyfile.

3. `cryptsetup luksAddkey /dev/sdb /root/keyfile`: This command will prompt you to enter the passphrase for the LUKS-encrypted device `/dev/sdb`. After entering the passphrase, it will add the new key contained in the keyfile `/root/keyfile` to the LUKS key slot associated with the device. The key will be added as an additional authorisation method. 


## STEGANOGRAPHY EXPLAINED

Steganography is the practice of concealing a message, file, image, or video within another message, file, image, or video in such a way that the existence of the hidden content is not obvious to observers.

The Least Significant Bit (LSB) is the rightmost bit in a binary number, representing the smallest (least significant) value. In a binary number, each bit represents a power of 2, with the LSB representing  2 raised to the power of 0 (which equals 1). 

For example, in the binary number 1011, the LSB is 1, because it represents 2 raised to the power of 0 while the next bit to the left represents 2 raised to the power of 1, and so forth.

In the context of digital media and steganography, the concept of LSB refers to the technique of embedding information by manipulating the least significant bits of pixels in an image or samples in audio files. Since the changes in the LSB typically cause minimal alteration to the overall appearance or sound of the media, LSB steganography is often used to conceal data within images or audio without obvious distortion.

* Image LSB Steganography: In digital images, each pixel is represented by color channels (e.g., red, green, and blue for RGB images). By modifying the least significant bits of these channels, one can embed secret data. Since the LSBs represent the smallest value changes, they are less likely to be noticed by human observers.
* Audio LSB Steganography: In audio files, each sample typically consists of multiple bits representing the amplitude of the sound wave. By altering the LSBs of these samples, one can embed additional data into the audio file without significantly affecting its audible quality.

Steganography will allow you to embed much less information in order not to be detected. 

Color = RGB(255, 255, 0)</br>
Converted to Binary = (11111111, 11111111, 00000000)</br>
The last digit is the “Least Significant Bit - LSB”


When encrypting, at first, the secret data is compressed and encrypted then a sequence of position of pixels in the cover file is created based on a pseudo-random number generator initialised with the passphrase. The secret data will be embedded in the pixels at those positions.
If those positions do not need to be changed because they already contain the correct value by chance are sorted out. 

Audio samples are used in audio instead of pixels. 

By default, encryption algorithms is Advanced Encryption Standard which is an extremely strong encryption algorithm. 

- Download the image or audio to be embedded. 
- Copy the file since one will be embedded. 
- `sha256sum main_file.jpg copied_file.jpg`: Files will have the same hashes
- `ikechukwu@ubuntu-22-04-3:~/Desktop$ steghide embed -cf mona_lisa_steg.jpg -ef steg_file.txt`: This command is using `steghide`, a popular steganography tool, to embed a file (steg_file.txt) into another file (mona_lisa_steg.jpg), creating a steganographic image. 
Here's a breakdown of the command:
  * `steghide`: This is the command-line utility used for embedding and extracting data from digital media files using steganography techniques.
  * `embed`: This is the sub-command used to embed data into a cover file.
  * `-cf mona_lisa_steg.jpg`: This option specifies the cover file, which is the file that will contain the embedded data. In this case, it's mona_lisa_steg.jpg.
  * `-ef steg_file.txt`: This option specifies the file to embed, which is the data that will be hidden within the cover file. In this case, it's steg_file.txt. 
- `sha256sum main_file.jpg copied_file.jpg`: Files will have different hashes.
- `mv steg_file.txt steg_file_backup.txt`
- `steghide extract -sf mona_lisa_steg.jpg`: appears to be an attempt to extract hidden data from an image file named mona_lisa_steg.jpg using the steghide tool.  Here's a breakdown of the command:
  * `steghide`: This is a command-line tool used for hiding data within various types of image and audio files using steganography techniques.
  * `extract`: This sub-command is used to extract hidden data from a steganographic file.
  * `-sf mona_lisa_steg.jpg`: This option specifies the steganographic file from which you want to extract hidden data. In this case, it's mona_lisa_steg.jpg. 

N/B: It is always better to use a unique image for steganography e.g. an image taken with a digital camera.


## NMAP

Nmap (Network Mapper) is a free and open-source network scanning tool used to discover hosts and services on a computer network, thus creating a "map" of the network. NMAP is a network discovery and security auditing tool.

- TCP Scans: TCP SYN Scan (`-sS`):
  * Also known as half-open scanning, it sends SYN packets to target ports and analyzes responses to determine open (response), closed (reset), or filtered (no response) ports. It's fast and stealthy. Half-open cos it doesn’t open a full TCP connection. 
  * SYN Scan:`-sS` (root only)
  * Connect Scan: `-sT`

- UDP Scan: UDP Scan (`-sU`):
  * This scan type is used to identify open UDP ports on target systems. UDP scans can be more time-consuming and less reliable compared to TCP scans due to the stateless nature of UDP.

- ICMP Scan: `-sn` or `-sP`
  - Example:  `nmap -sS -p 22,100 -sV 192.168.0.1`

`sudo apt install nmap`: to install nmap for the terminal while The GUI is Zenmap - The official Nmap security scanner GUI. 

`sudo nmap 192.168.1.1` (must be root) - This command uses Nmap to perform a default scan on the target host 192.168.1.1.
Here's a breakdown of the command:
  * `nmap`: This is the command-line utility for network exploration and security auditing.
  * `192.168.1.1`: This is the target IP address on which the scan will be performed. In many home network setups, 192.168.1.1 is commonly used as the default gateway IP address, which is the IP address of the router.

`nmap -sS 192.168.1.1`: This command uses the TCP SYN scan (`-sS` option) to scan the target host.
`nmap -sT 192.168.1.1`: This command uses the TCP Connect scan (`-sT` option) to scan the target host.

By default, `nmap` scans the most common 1000 ports for each protocol TCP and UDP. But if a service has been moved to a non-standard port like SSH is listening to port 50005

`nmap -p 50005,80,22 192.168.1.1`: This command instructs Nmap to scan the target host 192.168.1.1 for specific TCP ports: 50005, 80, and 22.
Here's a breakdown of the command:
  * `nmap`: This is the command-line utility for network exploration and security auditing.
  * `-p 50005,80,22`: This option specifies the ports to scan. In this case, Nmap will scan ports 50005, 80 (HTTP), and 22 (SSH) on the target host.
  * `192.168.1.1`: This is the target IP address on which the scan will be performed.

However, in this case, it doesn’t show who’s listening we can run a version detection on the target port as seen below;

<img width="551" alt="STATE SERVICE" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/e4842a13-eba8-4641-9404-9a55c493f22e">

To display who’s listening, run;

`nmap -p 2266,80,22 -sV 192.168.64.2`: This command instructs Nmap to perform a TCP port scan with version detection (`-sV`) on the target host 192.168.64.2, specifically on ports 2266, 80 (HTTP), and 22 (SSH). Here's a breakdown of the command:
  * `nmap`: This is the command-line utility for network exploration and security auditing.
  * `-p 2266,80,22`: This option specifies the ports to scan. `nmap` will scan ports 2266, 80 (HTTP), and 22 (SSH) on the target host.
  * `-sV`: This option enables version detection. Nmap will attempt to determine the version and type of services running on the open ports.

The output is seen below:

<img width="822" alt="STATE SERVICE VERSION" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/9698f97e-ce07-45e1-9a21-342afece0c11">

`nmap -p- 192.168.64.2`: This command instructs `nmap` to perform a scan on all 65,535 TCP ports on the target host 192.168.64.2. Here's a breakdown of the command:
  * `nmap`: This is the command-line utility for network exploration and security auditing.
  * `-p-`: This option specifies scanning all ports in the range 1-65535. The hyphen - indicates that Nmap should scan all ports.
  * `192.168.64.2`: This is the target IP address on which the scan will be performed.
Press enter to see the percentage of the progress. 

Visit [Nmap Reference Guide](https://nmap.org/book/man.html) for more info.

### NMAP ADVANCED

To get around firewalls and routers that block ping packets we need to suppress nmaps default behaviour of sending out the initial ping. We can do this using the -Pn option. 

`nmap -Pn 192.168.64.2`: This command instructs Nmap to skip host discovery and treat the target host 192.168.64.2 as if it were online, regardless of whether it responds to ping probes or not. Here's a breakdown of the command:
  * `nmap`: This is the command-line utility for network exploration and security auditing.
  * `-Pn`: This option tells Nmap to skip host discovery and assume that the target host is online. It disables ping probes (-Pn stands for "No ping").
  * `192.168.64.2`: This is the target IP address on which the scan will be performed.

When scanning machines that aren’t yours, you often want to hide your real IP address. Obviously, every source must contain a source IP, otherwise, there will be no response from the target. The recommended solution to obfuscate your real IP is to use decoys.  This is generally an effective technique for hiding your IP addresses. 

`nmap -p 22 -sV 192.168.64.2 -D 192.168.0.1,192.168.64.33,192.168.64.290`: This command instructs Nmap to perform a TCP port scan with version detection (-sV) on port 22 of the target host 192.168.64.2. Additionally, it uses the -D option to specify decoy hosts as part of the scan. Here's a breakdown of the command:
  * `nmap`: This is the command-line utility for network exploration and security auditing.
  * `-p 22`: This option specifies that Nmap should scan port 22, which is commonly associated with the SSH service.
  * `-sV`: This option enables version detection. Nmap will attempt to determine the version and type of service running on port 22.
  * `192.168.64.2`: This is the target IP address on which the scan will be performed.
  * `-D 192.168.0.1,192.168.64.33,192.168.64.290`: This option specifies decoy hosts that Nmap will use to obfuscate the origin of the scan. In this case, Nmap will use the IP addresses 192.168.0.1, 192.168.64.33, and 192.168.64.290 as decoy hosts.

NOTE: The hosts you use as decoys should be up or you might accidentally confuse your target. It will be easy to determine which host is scanning if only one is actually up on the network. 

`vim hosts.txt`: “Input host names, IP addresses”
`nmap -p 80 -iL hosts.txt`: This command instructs Nmap to scan port 80 on the hosts listed in the file hosts.txt using the -iL option.
Here's a breakdown of the command:
  * `nmap`: This is the command-line utility for network exploration and security auditing.
  * `-p 80`: This option specifies that Nmap should scan port 80, which is commonly associated with the HTTP service.
  * `-iL hosts.txt`: This option tells Nmap to read the list of target hosts from the file hosts.txt. Each host should be listed on a separate line in the file.

To speed up this scan, you can deactivate the reverse DNS lookup which is done by default using the `-n` option: `nmap -p 80 -iL hosts.txt -n`

Reverse DNS (Domain Name System) is a process that maps an IP address to a domain name.

The `-T` option in Nmap specifies the timing template or timing options for the scan. It allows you to control the speed and aggressiveness of the scan. The `-T` option followed by a timing template can be used to set the timing parameters for the scan.

Here are the timing templates available with Nmap:

* -T0 (Paranoid): This timing template is the slowest and most stealthy option. It is designed to evade detection and minimize the impact on the target network.
* -T1 (Sneaky): This timing template is slightly faster than Paranoid but still conservative. It's suitable for network reconnaissance when you want to minimize the chance of detection.
* -T2 (Polite): This timing template is slower than the default and is intended to be considerate of network resources and avoid triggering alarms.
* -T3 (Normal): This timing template is the default setting for Nmap scans. It strikes a balance between speed and stealth and is suitable for most situations.
* -T4 (Aggressive): This timing template increases the speed of the scan and is more aggressive in probing the target network. It may be more likely to be detected by intrusion detection systems (IDS) or firewalls.
* -T5 (Insane): This timing template is the fastest and most aggressive option. It performs scans at maximum speed and may overwhelm the target network or trigger security measures. 

For example: `nmap -T4 scanme.nmap.org`, In this example, `nmap` is the command used to initiate the scan.
  - `-T4` specifies the timing template for the scan, which is set to "Aggressive". This means that the scan will be faster and more aggressive in probing the target network.
  - `scanme.nmap.org` is the target host or IP address that will be scanned.
