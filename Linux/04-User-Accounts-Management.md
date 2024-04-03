# USER ACCOUNTS MANAGEMENT

User management in Linux involves the creation, modification, and removal of user accounts, as well as the management of associated permissions and privileges. It is a crucial aspect of system administration, ensuring secure and efficient access to resources on the system.
The two main folders involved in user management are `/etc/passwd` and `/etc/shadow`. Here are some key notes on user management in Linux:

`/etc/passwd`:

This file contains essential information about each user account on the system.
Each line represents a user account and is composed of several fields separated by colons (:).
Fields include username, password placeholder (actual password hash stored in /etc/shadow), UID, GID, user's full name or description, home directory, and login shell.

Example: backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
Username: backup
Password placeholder: x (actual password hash stored in /etc/shadow)
UID: 34
GID: 34
Full name/description: backup
Home directory: /var/backups
Login shell: /usr/sbin/nologin

`/etc/shadow`:

This file stores user account passwords in an encrypted format, enhancing security by protecting password information.
Each line represents a user account and is composed of several fields separated by colons (:).
Fields include username, encrypted password, password change and expiration information, and other account-related settings.
The password field typically contains a hash generated using a hashing algorithm, along with a salt for added security.
Example: $type$salt$hash
$6$ indicates the type of hashing algorithm used (e.g., SHA-512).
