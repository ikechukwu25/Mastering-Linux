# ORIGIN OF LINUX

The journey of learning you are beginning today has no ending point. It can take you in a myriad of different directions, from cybersecurity to application and game development, system administration, networking, big data, and artificial intelligence; all of these fields are rooted in Linux.

GNU is the free software that provides open-source equivalents of many common UNIX commands. GNU, which stands for "GNU's Not Unix," is a free and open-source operating system. The project was initiated by Richard Stallman in 1983 to create a Unix-like operating system that is composed entirely of free software. Stallman and the Free Software Foundation (FSF) envisioned a system where users have the freedom to run, modify, and distribute the software.

The GNU Project aimed to develop a complete Unix-compatible software system, including the kernel, compilers, text editors, and other essential components. However, for many years, the project lacked a free kernel. In 1991, Linus Torvalds released the Linux kernel, which, when combined with the GNU userland tools, formed a complete, free, and open-source operating system. This combination of the Linux kernel and GNU software is often referred to as "GNU/Linux."

The GNU General Public License (GPL) is a widely used open-source license associated with GNU software. It ensures that the software remains free and open, and any modifications or improvements made to the code must also be released under the same license.

The development of Linux closely parallels the rise of open-source software. Open-source takes a source-centric view of software. The open source philosophy is that you have a right to obtain the software source code and to modify it for your own use. Take Linux and the GNU tools, add some user-facing applications like a web browser and an email client, and you have a full Linux system. 

The full-featured distributions also include tools to manage the system and a package manager to help you add and remove software after the installation is complete. Like UNIX, there are distributions suited to every imaginable purpose. Some distributions focus on running servers, desktops, or even industry-specific tools such as electronics design or statistical computing. 


# OPERATING SYSTEMS

An operating system is software that runs on a computing device and manages the hardware and software components that make up a functional computing system. Operating systems designed for desktops and servers inherently possess greater complexity compared to those tailored for single-purpose devices like firewalls or mobile phones.

Computer users today have a choice mainly between three major operating systems: Microsoft Windows, Apple macOS, and Linux.
Of the three major operating systems listed only Microsoft Windows is unique in its underlying code. Apple’s macOS is a fully-qualified UNIX distribution based on BSD Unix (an operating system distributed until 1995), complemented by a large amount of proprietary code. It runs on hardware specifically optimized to work with Apple software. Linux can be any one of hundreds of distribution packages designed or optimized for whatever task is required. Only Microsoft Windows is based on a proprietary code base that isn’t either UNIX- or Linux-based.

Users can seamlessly navigate everyday productivity tasks across different operating systems by using a graphical interface with point-and-click functionality. However, unlike Windows, where system administration primarily occurs through a graphical user interface (GUI), many other operating systems require administrators to perform tasks using typed commands in a terminal.

These are descriptions and considerations related to various aspects of operating systems;

- Role: 
Servers typically sit in a rack and share a keyboard and monitor with many other computers, since console access is generally only used for configuration and troubleshooting. Servers generally run as a CLI, which frees up resources for the real purpose of the computer: serving information to clients (any user or system that accesses resources remotely). Desktop systems primarily run a GUI for the ease of use of their users.

- Stability: 
When a software release has many new features that haven’t been tested, it’s typically referred to as beta. After being tested in the field, its designation changes to stable. Users who need the latest features can decide to use beta software. This is often done in the development phase of a new deployment and provides the ability to request features not available on the stable release. Software in the open source realm is often released for peer review very early on in its development process, and can very quickly be put into testing and even production environments, providing extremely useful feedback and code submissions to fix issues found or features needed.

- Compatibility: 
Another loosely related concept is backward compatibility which refers to the ability of later operating systems to be compatible with software made for earlier versions.

- Cost:
Cost is always a factor when specifying new systems. Microsoft has annual licensing fees that apply to users, servers, and other software, as do many other software companies. Ultimately, the choice of the operating system will be affected by available hardware, staff resources, and skills, cost of purchase, maintenance, and projected future requirements.

- Interface: 
The first electronic computer systems were controlled by employing switches and plugboards similar to those used by telephone operators at the time. Then came punch cards and finally a text-based terminal system similar to the Linux command line interface (CLI) in use today. The graphical user interface (GUI), with a mouse and buttons to click, was pioneered at Xerox PARC (Palo Alto Research Center) in the early 1970s and popularized by Apple Computer in the 1980s. Today, operating systems offer both GUI and CLI interfaces, however, most consumer operating systems (Windows, macOS) are designed to shield the user from the ins and outs of the CLI.

### WINDOWS
Backward compatibility is a priority for Microsoft. Windows Server currently (as of this writing) is at version 2019 to denote the release date. The server can run a GUI but recently Microsoft, largely as a competitive response to Linux, has made incredible strides in its command line scripting capabilities through PowerShell and Windows Subsystem for Linux (WSL).

### APPLE macOS
macOS is well known for being “easy to use”, and as such has continued to be favored by users with limited access to IT resources like schools and small businesses. On the server side, macOS Server is primarily aimed at smaller organisations. Some large corporate IT departments allow users to choose macOS since users often require less support than standard Microsoft productivity deployments.	

### LINUX
Linux users typically obtain an operating system by downloading a distribution. A Linux distribution is a bundle of software, typically comprised of the Linux kernel, utilities, management tools, and even some application software in a package which also includes the means to update core software and install additional applications. 


In Linux, The variety of distributions and accompanying software allows the operating system to be significantly more flexible and customizable. Distributions are available for a much wider variety of systems, from commercial offerings for the traditional server or desktop roles, to specialized distributions designed to turn an old computer into a network firewall; from distributions created to power a supercomputer, to those that enable embedded systems.

Linux distributions can be broadly classed into two main categories: enthusiast and enterprise. An enthusiast distribution such as OpenSUSE’s Tumbleweed has a fast update cycle, is not supported for enterprise, and may not contain (or drop) features or software in the next version that is in the current one. Red Hat’s Fedora project uses a similar method of development and release cycle, as does Ubuntu Desktop.
Enterprise distributions are almost the exact opposite, in that they take care to be stable and consistent, and offer enterprise-grade support for extended periods, anywhere from 5-13 years in the case of SUSE. Enterprise distributions are fewer by far, being offered mainly by Red Hat, Canonical, and SUSE.

In summary, while enthusiast distributions offer the latest features and rapid updates, they are not typically recommended for enterprise use due to potential stability concerns. Enterprise distributions prioritize stability, long-term support, and a predictable environment, making them suitable for mission-critical applications in business settings.

For example, some distributions offer stable, testing, and unstable releases. A business may value stability and want long release cycles, while a hobbyist or a startup may want the latest software and opt for a shorter release cycle. To satisfy the latter group, Red Hat sponsors the Fedora Project which makes a personal desktop comprising the latest software but is still built on the same foundations as the enterprise version.

Fedora = Enthusiast     WHILE    Red Hat Enterprise Linux = Enterprise. 

SUSE, originally derived from Slackware, was one of the first comprehensive Linux distributions, it has many similarities to Red Hat Enterprise Linux. While SUSE Linux Enterprise contains proprietary code and is sold as a server product, openSUSE is a completely open, free version with multiple desktop packages similar to CentOS and Linux Mint.

_Proprietary code, also known as closed-source or non-free code, refers to computer program code that is not freely available for the public to view, modify, or distribute._

# NAVIGATING THE LINUX DESKTOP

## Definition of various components of a Linux system: 

- **KERNEL**: refers to the core component of an operating system. It acts as an intermediary between the hardware and the software, managing system resources, providing essential services, and facilitating communication between various hardware components and software applications.
- **TERMINAL**: This is a program that opens a window and lets you interact with the shell. Most servers boot directly to a terminal, as a GUI can be resource-intensive and is generally not needed to perform server-based operations.
- **DAEMON**: is a background process that runs on a computer system, providing specific services or performing certain tasks independently of user interaction. Daemons are often started during the system boot process and continue to run in the background, waiting for specific events or conditions to occur.
- **SHELL**: Shell is a program that takes commands from the keyboard and gives them to the operating system to perform. The most common in Linux is Bash (Bourne Again Shell) - the "ps" command shows the shell being used.
- **CONSOLE**: A form of the terminal without a GUI. 

Most Linux distributions allow users to download a “desktop” installation package that can be loaded onto a USB key. This is one of the first things aspiring system administrators should do; download a major distribution and load it onto an old PC.


### KERNEL EXPLAINED

The kernel of the operating system is like an air traffic controller at an airport, and the applications are the airplanes under its control. 

Here are several functions performed by the Kernel:

- Helps execute systemd which then initializes the system. 
- Helps in starting and killing applications. 
- Decides which program gets which block of memory
- Handles displaying texts or graphics on a monitor

In addition to the above list, applications make requests to the kernel and in return receive resources, such as memory, CPU, and disk space. If two applications request the same resource, the kernel decides which one gets it, and in some cases, kills off another application to save the rest of the system and prevent a crash.

The kernel also handles the switching of applications, a process known as multitasking. A computer system has a small number of central processing units (CPUs) and a finite amount of memory. The kernel takes care of unloading one task and loading a new one if there is more demand than resources available. When one task has run for a specified amount of time, the CPU pauses it so that another may run. If the computer is doing several tasks at once, the kernel is deciding when to switch focus between tasks. With the tasks rapidly switching, it appears that the computer is doing many things at once.

The kernel also provides an API that applications can use to communicate with the underlying hardware and perform various operations.


# OVERVIEW OF LINUX SOFTWARE CATEGORIES

A computer can act as a server, which means it primarily handles data on others’ behalf, or as a desktop, which means a user interacts with it directly. 

Linux software generally falls into one of three categories:
* Server Applications: Software that has no direct interaction with the monitor and keyboard of the machine it runs on. Its purpose is to serve information to other computers, called clients. Sometimes server applications may not talk to other computers but only sit there and crunch data.
* Desktop Applications: Web browsers, text editors, music players, or other applications with which users interact directly. In many cases, such as a web browser, the application is talking to a server on the other end and interpreting the data. This is the “client” side of a client/server application.
* Tools: A loose category of software that exists to make it easier to manage computer systems. Tools can help configure displays, provide a Linux shell that users type commands into, or even more sophisticated tools, called compilers, that convert source code to application programs that the computer can execute.

The web page itself can either be static or dynamic. When the web browser requests a static page, the web server sends the file as it appears on disk. In the case of a dynamic site, the request is sent by the web server to an application, that generates the content.

Below are various types of Servers:

### PRIVATE CLOUD SERVERS

Private cloud servers such as ownCloud and Nextcloud offer software solutions for storing, syncing, and sharing data within private cloud environments.

ownCloud:
- Launch Date: 2010
- Founder: Frank Karlitschek
- Purpose: To provide software for storing, syncing, and sharing data from private cloud servers.
- License: Available in a standard open-source GNU AGPLv3 license.
- Enterprise Version: A commercial license is available for the enterprise version.

Nextcloud:
- Forked From ownCloud: 2016
- Founder: Frank Karlitschek (Nextcloud was initiated by the founder of ownCloud after he left the ownCloud project.)
- Purpose: Similar to ownCloud, providing a platform for self-hosted file synchronization and sharing.
- License: Provided under the GNU AGPLv3 license.
- Development Philosophy: Aims for an open and transparent development process.


### DATABASE SERVERS

Database server applications form the backbone of most online services. Dynamic web applications pull data from and write data to these applications. For example, a web program for tracking online students might consist of a front-end server that presents a web form. When data is entered into the form, it is written to a database application such as MariaDB. When instructors need to access student information, the web application queries the database and returns the results through the web application.
MariaDB is a community-developed fork of the MySQL relational database management system. Some other popular databases are Firebird and PostgreSQL. You might enter raw sales figures into the database and then use a language called Structured Query Language (SQL) to aggregate sales by product and date to produce a report.

### EMAIL SERVERS

When discussing email servers, it is always helpful to look at the 3 different tasks required to get email between people:

* Mail Transfer Agent (MTA): The most well-known MTA (software that is used to transfer electronic messages to other systems) is Sendmail. Postfix is another popular one and aims to be simpler and more secure than Sendmail.
* Mail Delivery Agent (MDA): Also called the Local Delivery Agent, it takes care of storing the email in the user’s mailbox. Usually invoked from the final MTA in the chain. It is a component of the email delivery process responsible for delivering incoming emails to the recipient's mailbox on a mail server.
* POP/IMAP Server: The Post Office Protocol (POP) and Internet Message Access Protocol (IMAP) are two different email retrieval protocols used by email clients to access messages from a mail server.

In the closed-source software world, products like Microsoft Exchange are bundled as comprehensive suites, containing only components approved or developed by the vendor. Users have limited options to select individual components.
In contrast, the open-source software landscape allows for modular inclusion or substitution of components. Users can mix and match individual components to create a customized solution. Some open-source packages are essentially well-integrated sets of independently developed components working together seamlessly.

### FILE SHARING

Samba allows a Linux machine to look and behave like a Windows machine so that it can share files and participate in a Windows domain. 
Netatalk project lets a Linux machine perform as an Apple Macintosh file server.
The native file-sharing protocol for UNIX/Linux is called the Network File System (NFS). 
One of the oldest network directory systems is the Domain Name System (DNS). It is used to convert a name like https://www.icann.org/ to an IP address like 192.0.43.7, which is a unique identifier of a computer on the Internet. DNS also holds global information like the address of the MTA for a given domain name.
The Internet Software Consortium maintains the most popular DNS server, simply called BIND after the name of the process that runs the service.

The Internet Software Consortium (ISC) is a non-profit organization that develops and maintains open-source software projects related to Internet infrastructure.

When a computer boots up, it needs an IP address for the local network so it can be uniquely identified. DHCP’s job is to listen for requests and to assign a free address from the DHCP pool. The Internet Systems Consortium (known until January 2004 as the Internet Software Consortium) also maintains the ISC DHCP server, which is the most common open-source DHCP server.


# LINUX DESKTOP APPLICATIONS

The mentioned applications and concepts are not exclusive to the Linux desktop environment. Instead, they represent a variety of software tools and functionalities commonly used in Linux systems, including desktop and server environments.

- Email: 
The Mozilla Foundation came out with Thunderbird, a full-featured desktop email client. Thunderbird connects to a POP or IMAP server, displays email locally, and sends email through an external SMTP server.

- Productivity: 
LibreOffice is a fork of the OpenOffice (sometimes called OpenOffice.org) application suite. Both offer a full office suite, including tools that strive for compatibility with Microsoft Office in both features and file formats. LibreOffice Calc = Spreadsheet while LibreOffice Writer = Documents.

- Web Browsers: 
Mozilla Firefox and Google Chrome, along with their commitment to supporting Linux, exemplifies how open source and healthy competition can drive continuous improvement and innovation in the world of web browsers. Users benefit from having multiple high-quality options, and developers can leverage cutting-edge technologies to build the next generation of web applications.

- Shells: 
The shell’s job is to accept commands, like file manipulations and starting applications, and to pass those to the Linux kernel for execution. ‌The Linux shell provides a rich language for iterating over files and customising the environment, all without leaving the shell.
Linux offers a variety of shells to choose from, mostly differing in how and what can be customised, and the syntax of the built-in scripting language. The two main families are the Bourne shell and the C shell. As both these shells were invented in the 1970s, there are more modern versions, the Bourne Again Shell (Bash) and the tcsh (pronounced as tee-cee-shell). Bash is the default shell on most systems, though tcsh is also typically available.

- Text Editors: 
Most Linux systems provide a choice of text editors which are commonly used at the console to edit configuration files. The two main applications are Vi (or the more modern Vim) and Emacs. Both Vi and Emacs are complex and have a steep learning curve, which is not helpful for simple editing of a small text file. Therefore, Pico and Nano are available on most systems and provide very basic text editing.

- Package Management: 
A package manager takes care of keeping track of which files belong to which package and even downloading updates from repositories, typically a remote server sharing the appropriate updates for distribution. Most of the commands associated with package management require root privileges. The rule of thumb is that if a command affects the state of a package, administrative access is required. In other words, a regular user can perform a query or a search, but to add, update, or remove a package requires the command to be executed as the root user. In Linux, there are many different software package management systems, but the two most popular are those from Debian and Red Hat.

    -  Debian Package Management: 
The Debian distribution, and its derivatives such as Ubuntu and Mint, use the Debian package management system. At the heart of Debian package management are software packages that are distributed as files ending in the .deb extension.

    - RPM Package Management: 
According to the Linux Standards Base, the standard package management system is RPM. RPM makes use of a .rpm file for each software package.
‌⁠Like the Debian system, RPM Package Management systems track dependencies between packages. Tracking dependencies ensures that when a package is installed, the system also installs any packages needed by that package to function correctly. Dependencies also ensure that software updates and removals are performed properly. The back-end tool most commonly used for RPM Package Management is the rpm command. While the rpm command can install, update, query, and remove packages, the command line front-end tools such as yum and up2date automate the process of resolving dependency issues.

