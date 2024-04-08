# DPKG (Debian and Ubuntu Based Distros)

Software management in Debian and Ubuntu-based distributions relies on DPKG, a package management system. DPKG operates at a low level, executing fundamental tasks for package management. At its core lies the concept of binary packages, which contain precompiled executables ready for deployment. These executables result from the compilation process, where source code, authored in languages like C, C++, or Rust, is translated into machine-executable binary code.

The binary package format, denoted by .deb extensions, serves as the installation package format across Debian-based distributions. These packages encapsulate various files, including executables, configuration files, documentation, and metadata. Thus, installation involves extracting these files onto the filesystem.

While source code represents the human-readable form of software, binaries embody its executable form. Compilation transforms source code into binaries, making them executable by hardware. The compilation process encompasses multiple stages such as preprocessing, compilation, assembly, and linking, culminating in the creation of binary executables.

Package management operations encompass tasks such as installing, updating, and removing software packages on a computer system. These operations can be performed using various tools, ranging from low-level command-line utilities like `dpkg` to more advanced tools like apt, and even graphical user interface (GUI) applications such as Synaptic. 

Unlike the Windows operating system, where applications may have all of their files installed in a single subdirectory under the C:\Program Files directory, applications in Linux may have their files in multiple directories spread out throughout the Linux filesystem. For Debian-derived distributions, you can execute the `dpkg -L packagename` command to get the list of file locations. In Red Hat-derived distributions, you can run the `rpm -ql packagename` command for the list of the locations of the files that belong to that application.

The executable program binary files may go in the /usr/bin directory if they are included with the operating system, or else they may go into the /usr/local/bin or /opt/application/bin directories if they came from a third party.

The data for the application may be stored in one of the following subdirectories:
* /usr/share
* /usr/lib
* /opt/application
* /var/lib
  
The file related to documentation may be stored in one of the following subdirectories:
* /usr/share/doc
* /usr/share/man
* /usr/share/info
  
The global configuration files for an application are most likely to be stored in a subdirectory under the /etc directory, while the personalized configuration files (specific for a user) for the application are probably in a hidden subdirectory of the user's home directory.

Installing software using dpkg involves the following steps:
- Download the .deb file. 
- Install using `dpkg -i filename`
- Open file on the system

To manage installed packages and gather information about them, you can use various `dpkg` commands:

- `dpkg --get-selections`: Obtain a list of installed packages.
- `dpkg-query -l`: List all installed packages along with their information, indicating their status.
  - "ii" stands for "installed" and "successfully installed."
  - Other possible statuses include "rc" (removed but still configured), "iU" (installed and unpacked but not configured), and others.
- `dpkg -L package`: List all files installed on the system from a specific package. For example:
-  `dpkg -L ssh`: This will list all files installed from the "ssh" package 
  - `which -a ls`: This command helps locate the ls command in the system. It displays all matching path names of the command.
  - `dpkg -S /path/to/file`: This command indicates the package containing the file specified by the path argument. It assists in finding the package associated with a particular file.
- `dpkg -r`: This command is used to remove (uninstall) a previously installed package from the system.
- `dpkg -P`: This command is used to purge (completely remove) a package and its configuration files from the system. Purging a package removes not only the package files but also its associated configuration files, essentially performing a more thorough removal than a regular uninstallation.


# APT - Advanced Package Tool

The recommended method for managing software packages on Ubuntu and other Debian-based distributions is using APT. Unlike dpkg, APT does not directly handle .deb files. Instead, it works with packages downloaded from repositories and calls dpkg directly after fetching the .deb archives.

An APT repository is a web server containing a collection of packages with metadata readable by the apt tool. Personal Package Archives (PPAs) are a special kind of repository hosted on servers like Launchpad.

Always provide the full path when installing a package from a .deb file using APT.

Common APT Commands include:

- `sudo apt update`: Refreshes the local package repository cache, pulling the latest changes from the APT repository.
- `sudo apt install package`: Installs a package.
- `sudo apt list --upgradable`: Lists upgradable packages.
- `sudo apt full-upgrade`: Upgrades the entire system, potentially removing some installed packages.
- `sudo apt remove packagename`: Removes an installed package, leaving configuration files behind.
- `sudo apt purge packagename`: Completely removes packages, including configuration files.
- `sudo apt autoremove`: Removes unneeded dependencies.
- `sudo apt clean`: Clears out the local repository of retrieved package files, leaving only the log file in the apt cache directory (/var/cache/apt/archives).
- `sudo apt list`: Lists all available packages.
- `sudo apt list | wc -l`: Shows the number of available packages.
- `sudo apt search "strings"`: Finds packages whose description contains a specific phrase.
- `sudo apt list --installed`: Lists only the installed packages.
- `sudo apt show packagename`: Shows information about a package.
- `sudo apt install synaptic`: Installs the Synaptic software manager with a GUI.


# COMPILING PROGRAMS FROM SOURCE CODE VS. PACKAGE MANAGER

Compiling executable files from source code and using package management tools like APT (Advanced Package Tool) and dpkg represent two different approaches to managing software on a Debian-based Linux system.

Developers write source code in a high-level programming language such as C or C++.	The source code needs to be compiled into machine-readable binary code. This process involves using a compiler (e.g., GCC is for C/C++ codes, G++, make ).	

The default Ubuntu repositories contain a meta package - build-essential. "Build-essential" is a meta-package in Debian-based Linux distributions that includes a set of packages commonly used for building software from source. It provides essential tools and libraries needed for compiling and linking applications. Installing "build-essential" is often one of the first steps when setting up a development environment or when compiling software from source code.

- GCC (GNU Compiler Collection): GCC is a widely used open-source compiler suite that supports several programming languages, including C and C++. It is the default compiler for many Unix-like operating systems, including Linux.
- G++: G++ is a specific component of GCC tailored for compiling C++ code. It is invoked in a similar manner to GCC but is optimized for C++ compilation.
- Make: Make is a build automation tool that manages the compilation process by determining which parts of the source code need to be recompiled and issuing the necessary commands to the compiler. It reads a file called a Makefile, which specifies dependencies between source files and instructions for compiling them.

`sudo apt update && sudo apt install build-essential`: This will install the GCC and G++ used to compile a program.

Compilation translates the human-readable source code into machine code specific to the target architecture. The compiled code is linked with the necessary libraries to create the final executable file. After compilation, the resulting executable needs to be installed on the system manually

![image](https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/fdeb3fbb-5bec-4926-9a6c-8ef006da6dca)

Compiling a single source file using gcc. 
- After installing build-essential: `sudo apt update && sudo apt install build-essential`
- Create a .c file: Create a source code file with a .c extension using a text editor.  
- `gcc file.c -o filename`: Open a terminal, navigate to the directory containing your .c file, and use the gcc compiler to compile it. Use the -o option to specify the name of the output executable file. 
- ./filename to open: After successful compilation, you can run the generated executable by executing the command.


### SOURCE COMPILATION GUIDE

1. Install the prerequisites: gcc, g++, make
  - Ubuntu: `sudo apt update && sudo apt install build-essential`
  - CentOS: `sudo dnf group install "Development Tools"`
2. Download the source files from the official Website
3. Check the integrity of the tarball (hash or digital signature)
4. Extract the archive and move it into the resulting directory
  - `tar -xvf filename.tar.gz`
  - `cd extracted_directory`
5. Check available configuration options - Run: /configure --help and set the required compilation options.
6. Run: `make` - To compile the source code
7. Run: `sudo make install` - If needed, run this command to install the compiled software system-wide.
8. Run `make clean` - Optionally, to clean up temporary build files.


### COMPILING SOFTWARE FROM SOURCE CODE (Lab ProFTPD)

FTP (File Transfer Protocol) is a standard network protocol used for transferring files between a client and a server on a computer network. It operates on a client-server model where the client initiates a connection to the server to perform file transfers.

- Visit the official website -  http://www.proftpd.org/ to download the source file using the wget link.
- Check the integrity of the file especially if you’re to install it on a production server.
  - Click on sha256 signatures to see the hash on the website.
  - Use sha256sum filename or md5sum filename to see the hash on the local host terminal.
- Extract the archive using `tar -xzvf filename` if it’s a .gz compressed file.
- The source code is in the src file when you go into the directory that has been extracted.
- The executable file called “configure” is important because it checks the requirements and dependency of the program you’re compiling are satisfied and configures how the program will be compiled - which options will be enabled and disabled. To learn about its options run `./configure --help`.
- Always use the  `--prefix` option to specify where the software will be installed else it will be installed in the standard directories like /bin /etc /usr /var. This could break your system.
- It is recommended that programmes that are compiled and are not controlled by the package manager are installed in dir. - /opt (optional software)
- Install using `./configure --prefix=/opt/proftpd`
- The next step is to run `make`, the GNU utility that builds your application by processing a collection of source files and transforming them into the final product. It does the real compilation process by invoking GCC multiple times as instructed by the makefile located in the project directory. This makefile, often named Makefile, contains rules and instructions for compiling the source code. After compilation, the necessary binaries are created, and ready for use.
- Run `make install` as root which is the final step `sudo make install` - This will create the dir. where the software will be installed.
  
N/B - The directory - /opt/proftpd, contains everything related to the server just compiled, so to remove the server, just remove the directory. 

The file name proftpd located in the sbin of the directory is actually the server. To start the server, `run`. 
