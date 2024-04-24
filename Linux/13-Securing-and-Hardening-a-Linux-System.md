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

Visit the website - [have i been pwned?](https://haveibeenpwned.com/), to check if your account has been compromised in a data breach. If your email is on the list, it means that the hackles have the hash of your password and they could try to hack it offline. 
