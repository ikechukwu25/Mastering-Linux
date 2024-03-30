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

- **Role**: 
Servers typically sit in a rack and share a keyboard and monitor with many other computers, since console access is generally only used for configuration and troubleshooting. Servers generally run as a CLI, which frees up resources for the real purpose of the computer: serving information to clients (any user or system that accesses resources remotely). Desktop systems primarily run a GUI for the ease of use of their users.

- **Stability**: 
When a software release has many new features that haven’t been tested, it’s typically referred to as beta. After being tested in the field, its designation changes to stable. Users who need the latest features can decide to use beta software. This is often done in the development phase of a new deployment and provides the ability to request features not available on the stable release. Software in the open source realm is often released for peer review very early on in its development process, and can very quickly be put into testing and even production environments, providing extremely useful feedback and code submissions to fix issues found or features needed.

- **Compatibility**: 
Another loosely related concept is backward compatibility which refers to the ability of later operating systems to be compatible with software made for earlier versions.

- **Cost**:
Cost is always a factor when specifying new systems. Microsoft has annual licensing fees that apply to users, servers, and other software, as do many other software companies. Ultimately, the choice of the operating system will be affected by available hardware, staff resources, and skills, cost of purchase, maintenance, and projected future requirements.

- **Interface**: 
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
* **Server Applications**: Software that has no direct interaction with the monitor and keyboard of the machine it runs on. Its purpose is to serve information to other computers, called clients. Sometimes server applications may not talk to other computers but only sit there and crunch data.
* **Desktop Applications**: Web browsers, text editors, music players, or other applications with which users interact directly. In many cases, such as a web browser, the application is talking to a server on the other end and interpreting the data. This is the “client” side of a client/server application.
* **Tools**: A loose category of software that exists to make it easier to manage computer systems. Tools can help configure displays, provide a Linux shell that users type commands into, or even more sophisticated tools, called compilers, that convert source code to application programs that the computer can execute.

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

- **Email**: 
The Mozilla Foundation came out with Thunderbird, a full-featured desktop email client. Thunderbird connects to a POP or IMAP server, displays email locally, and sends email through an external SMTP server.

- **Productivity**: 
LibreOffice is a fork of the OpenOffice (sometimes called OpenOffice.org) application suite. Both offer a full office suite, including tools that strive for compatibility with Microsoft Office in both features and file formats. LibreOffice Calc = Spreadsheet while LibreOffice Writer = Documents.

- **Web Browsers**: 
Mozilla Firefox and Google Chrome, along with their commitment to supporting Linux, exemplifies how open source and healthy competition can drive continuous improvement and innovation in the world of web browsers. Users benefit from having multiple high-quality options, and developers can leverage cutting-edge technologies to build the next generation of web applications.

- **Shells**: 
The shell’s job is to accept commands, like file manipulations and starting applications, and to pass those to the Linux kernel for execution. ‌The Linux shell provides a rich language for iterating over files and customising the environment, all without leaving the shell.
Linux offers a variety of shells to choose from, mostly differing in how and what can be customised, and the syntax of the built-in scripting language. The two main families are the Bourne shell and the C shell. As both these shells were invented in the 1970s, there are more modern versions, the Bourne Again Shell (Bash) and the tcsh (pronounced as tee-cee-shell). Bash is the default shell on most systems, though tcsh is also typically available.

- **Text Editors**: 
Most Linux systems provide a choice of text editors which are commonly used at the console to edit configuration files. The two main applications are Vi (or the more modern Vim) and Emacs. Both Vi and Emacs are complex and have a steep learning curve, which is not helpful for simple editing of a small text file. Therefore, Pico and Nano are available on most systems and provide very basic text editing.

- **Package Management**: 
A package manager takes care of keeping track of which files belong to which package and even downloading updates from repositories, typically a remote server sharing the appropriate updates for distribution. Most of the commands associated with package management require root privileges. The rule of thumb is that if a command affects the state of a package, administrative access is required. In other words, a regular user can perform a query or a search, but to add, update, or remove a package requires the command to be executed as the root user. In Linux, there are many different software package management systems, but the two most popular are those from Debian and Red Hat.

    -  **Debian Package Management**: 
The Debian distribution, and its derivatives such as Ubuntu and Mint, use the Debian package management system. At the heart of Debian package management are software packages that are distributed as files ending in the .deb extension.

    - **RPM Package Management**: 
According to the Linux Standards Base, the standard package management system is RPM. RPM makes use of a .rpm file for each software package.
‌⁠Like the Debian system, RPM Package Management systems track dependencies between packages. Tracking dependencies ensures that when a package is installed, the system also installs any packages needed by that package to function correctly. Dependencies also ensure that software updates and removals are performed properly. The back-end tool most commonly used for RPM Package Management is the rpm command. While the rpm command can install, update, query, and remove packages, the command line front-end tools such as yum and up2date automate the process of resolving dependency issues.

# DEVELOPMENT LANGUAGES

Computer programming languages provide a way for a programmer to enter instructions in a more human-readable format, and for those instructions to eventually become translated into something the computer understands. 
Languages fall into one of two camps: Interpreted or Compiled. An interpreted language translates the written code into computer code as the program runs, and a compiled language is translated all at once.

In compiled languages, the entire source code is translated into machine code or an intermediate code by a compiler before the program is executed.

Linux itself was written in a compiled language called **C**. The main benefit of C is that the language itself maps closely to the generated machine code so that a skilled programmer can write code that is small and efficient. 
C has been extended over the years. There is C++, which adds object support to C (a different style of programming), and Objective C which took another direction and is in heavy use in Apple products.

Java takes a unique approach to compilation. Instead of directly compiling machine code, it first compiles code into a hypothetical CPU language called Java Virtual Machine (JVM) bytecode. Each computer runs JVM software to translate this bytecode into native instructions. This design makes Java versatile, as the simple JVM can be implemented on various devices, from powerful computers to low-power devices. Moreover, compiled Java files can run on any computer with a JVM implementation.

Interpreted languages also tend to offer more features than compiled languages, meaning that often less code is needed.

Object-oriented programming simplifies complex actions and processes, allowing end-users to focus on basic tasks.


# SECURITY

Security is paramount for Linux systems. They are known for their robust security features, including built-in encryption tools, access controls, and secure networking protocols. Additionally, regular security updates and patches are provided by the Linux community to address any vulnerabilities and ensure the ongoing security of Linux-based systems.

### COOKIES
Cookies are the primary mechanism that websites use to track users. While sometimes this tracking is beneficial, such as for keeping track of shopping carts or maintaining login sessions, it can also raise privacy concerns. As you browse the web, a web server can send back a cookie—a small piece of text—along with the web page, which your browser stores and sends back with every request to the same site. Typically, cookies are only sent back to the site they originated from. </br>
However, many sites include embedded scripts from third parties, such as banner advertisements or Google Analytics pixels. If multiple sites have tracking pixels from the same advertiser, the same cookie will be sent when browsing those sites, allowing the advertiser to track user activity across different websites. Tweaking privacy settings can enhance anonymity online, but it may lead to issues with sites that rely on third-party cookies, requiring users to explicitly permit certain cookies to be saved.

### PRIVACY TOOLS
- **Encryption**: Encryption is one of the most widely deployed privacy tools today. It involves scrambling data using authentication keys to ensure secure communication. One well-known example is HTTPS (HyperText Transfer Protocol Secure), which encrypts data transmitted between users and online resources, preventing interception of data as it travels over the internet.

- **Virtual Private Networks (VPN)**: VPNs have long been used by companies to connect remote servers and employees securely. They are now gaining popularity among ordinary users seeking online privacy. VPNs create an encrypted channel of communication between two systems, ensuring that data transmitted between them is protected from interception by encrypting it with an algorithm known only to the systems involved.


# THE CLOUD
- **Public Cloud**: A public cloud is a cloud infrastructure deployed by a provider to offer cloud services to the general public and organizations over the Internet. 
- **Private Cloud**: A private cloud is a cloud infrastructure that is set up for the sole use of a particular organization. 
- **Community Cloud**: A community cloud is a cloud infrastructure that is set up for the sole use by a group of organizations with common goals or requirements.
- **Hybrid Cloud**: A hybrid cloud is composed of two or more individual clouds, each of which can be a private, community, or public cloud.

## LINUX IN THE CLOUD

Linux plays a pivotal role in cloud computing. It powers 90% of the public cloud workload, most virtual servers are based on some version of the Linux kernel, and Linux is often used to host the applications behind cloud computing services.
Many cloud providers, including major platforms like Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP), offer Linux-based virtual machines as part of their infrastructure services. Users can deploy Linux instances to run applications and services in the cloud.
Linux is also fundamental to containerization technologies like Docker and Kubernetes, which are widely used in cloud environments

Many Linux servers in the cloud are handled by automated programs, not people. This allows administrators to focus on monitoring operations rather than manually setting up and updating systems.

### VIRTUALIZATION

Virtualization is a process where a single physical computer, known as the host, runs multiple instances of an operating system, called guests. Guest images are copies of operating systems that run on the host. These images can be pre-configured for specific tasks, allowing for quick and often automated deployment when needed. The pre-configured nature of guest images facilitates rapid deployment, saving time and resources. This is particularly beneficial in scenarios where quick scaling or provisioning of resources is required.  The host system runs software called a hypervisor. The hypervisor manages and allocates resources, such as CPU, memory, and storage, among the various guest images. It acts as an intermediary, ensuring each guest operates independently. The role of the hypervisor in managing resources among guests is likened to the way the Linux kernel manages processes. It ensures efficient allocation and utilization of resources for each running instance.

Since it is possible to run multiple instances of an operating system on one physical machine and connect to it over the network, the location of the machine doesn’t matter. Cloud computing takes this approach and allows administrators to have virtual machines in a remote data center owned by another company, and only pay for the resources used. Cloud computing vendors can take advantage of scales of economy to offer computing resources at far lower prices than operating an on-site data center.


# OPEN-SOURCE SOFTWARE AND LICENSING

Software projects take the form of source code, which is a human-readable set of computer instructions. Since source code is not understood directly by the computer, it must be compiled into machine instructions by a compiler. The compiler is a special program that gathers all of the source code files and generates instructions that can be run on the computer, such as by the Linux kernel.

Source code compiled into binary programs is one method of creating programs and running computing instructions. Another is the many types of interpreted languages, such as PERL, Python, and even BASH scripting, where the code is not compiled, but fed to an interpreting program, typically a binary executable that understands and implements the instructions contained in the source code or scripts.

Open source takes a source-centric view of software. The open source philosophy is that users have the right to obtain the software source code, and to expand and modify programs for their use. 

The standardization of application programming interfaces (APIs) allows programs written for one specific UNIX or Linux operating system to be ported (converted) relatively easily to run on another. 

Groups like the IEEE (Institute of Electrical and Electronics Engineers) and POSIX (Portable Operating System Interface), allow professionals from different companies and institutions to collaborate on specifications that make it possible for different operating systems and programs to work together. 
It doesn’t matter if a program is closed or open source, simple or complex, if it is written to these standards others will be able to use and modify it in the future. Every innovation in computing is built on the work of others who came before. 	

## OPEN SOURCE LICENSING

When talking about buying software, there are three distinct components:
* Ownership – Who owns the intellectual property behind the software?
* Money Transfer – How does money change hands, if at all?
* Licensing – What do you get? What can you do with the software? Can you use it on only one computer? Can you give it to someone else?

Linux is owned by Linus Torvalds. He has placed the code under a license called GNU General Public License version 2 (GPLv2). This license, among other things, says that the source code must be made available to anyone who asks and that anyone is allowed to make changes. 

In general, when someone creates something, they also get the right to decide how it is used and distributed. Free and Open Source Software (FOSS) refers to software where this right has been given up; anyone is allowed to view the source code and redistribute it.

Linus Torvalds has done that with Linux – even though he created Linux he can’t forbid someone from using it on their computer because he has given up that right through the GPLv2 license.

### THE FREE SOFTWARE FOUNDATION (FSF)

Two groups can be considered the most influential forces in the world of open source: the Free Software Foundation and the Open Source Initiative.

Only a few years after the development of the GNU project, Richard Stallman founded the Free Software Foundation (FSF) in 1985 to promote free software. In this context, the word "free" does not refer to the price, but to the freedom to share, study, and modify the underlying source code. 

The FSF (Free Software Foundation) promotes the idea that software licenses should ensure that any modifications made to free software are shared when the modified software is distributed again. This philosophy is known as **copyleft**. In essence, if you modify and share free software, you should also share the changes you've made.

The FSF has developed its own set of licenses which are free for anyone to use based on the original GNU General Public License (GPL). FSF currently maintains GNU General Public License version 2 (GPLv2) and version 3 (GPLv3), as well as the GNU Lesser General Public Licenses version 2 (LGPLv2) and version 3 (LGPLv3).

The changes between GPLv2 and GPLv3 largely focused on using free software on a closed hardware device which has been coined **Tivoization**. TiVo used Linux for their software but locked down their hardware to prevent modified versions from running. While TiVo complied with GPLv2 by releasing the source code, the FSF found this restrictive and added a clause in GPLv3 to address it. Linus Torvalds, the creator of Linux, opted to stick with GPLv2, aligning with TiVo's stance on this issue.

### THE ‌⁠OPEN-SOURCE INITIATIVE (OSI)

The Open Source Initiative (OSI) was founded in 1998 by Bruce Perens and Eric Raymond. They believed that the Free Software Foundation was too politically charged and that less extreme licenses were necessary, particularly around the copyleft aspects of FSF licenses.
OSI believes that not only should the source be freely available, but also that no restrictions should be placed on the use of the software, no matter what the intended use.

Unlike the FSF, the OSI does not have its own set of licenses. Instead, the OSI has a set of principles and adds licenses to that list if they meet those principles, called open source licenses. One type of Open Source license is the BSD (Berkeley Software Distribution) and its derivatives, which are much simpler than GPL.
There are currently two actual "BSD" licenses approved by OSI, a 2-Clause and a 3-Clause. These licenses state that you may redistribute the source and binaries as long as you maintain copyright notices and don’t imply that the original creator endorses your version. In other words "do what you want with this software, just don’t say you wrote it."

FSF licenses, such as GPLv2, are also open-source licenses. However, many open source licenses such as BSD and MIT do not contain the copyleft provisions and are thus not acceptable to the FSF. These licenses are called permissive free software licenses because they are permissive in how you can redistribute the software. You can take BSD-licensed software and include it in a closed software product as long as you give proper attribution.

**DIFFERENCES**
"Open source" emphasizes the practical benefits of collaborative development and accessibility of source code, while "free software" underscores the ethical and freedom-focused aspects of software usage and distribution.

### CREATIVE COMMONS 

Creative Commons (CC) is a non-profit organization that provides a set of licenses to the public, allowing creators to share their work under specific terms and conditions.
These licenses are designed to give creators flexibility in how they permit others to use, share, and build upon their creative works, including text, images, music, and more. 

The CC licenses are made up of the following set of conditions the creator can apply to their work:
* **Attribution (BY)** – All CC licenses require that the creator must be given credit, without implying that the creator endorses the use.
* **ShareAlike (SA)** – This allows others to copy, distribute, perform, and modify the work, provided they do so under the same terms.
* **NonCommercial (NC)** – This allows others to distribute, display, perform, and modify the work for any purpose other than commercially.
* **NoDerivatives (ND)** – This allows others to distribute, display, and perform only original copies of the work. They must obtain the creator’s permission to modify it.

These conditions are then combined to create the six main licenses offered by Creative Commons:
* **Attribution (CC BY)** – Much like the BSD license, you can use CC BY content for any use but must credit the copyright holder.
* **Attribution ShareAlike (CC BY-SA)** – A copyleft version of the Attribution license. Derived works must be shared under the same license, much like in the Free Software ideals.
* **Attribution NoDerivs (CC BY-ND)** – You may redistribute the content under the same conditions as CC-BY but may not change it.
* **Attribution-NonCommercial (CC BY-NC)** – Just like CC BY, but you may not use it for commercial purposes.
* **Attribution-NonCommercial-ShareAlike (CC BY-NC-SA)** – Builds on the CC BY-NC license but requires that your changes be shared under the same license.
* **Attribution-NonCommercial-NoDerivs (CC BY-NC-ND)** – You are sharing the content to be used for non-commercial purposes, but people may not change the content.
* **No Rights Reserved (CC0)** – This is the Creative Commons version of the public domain.


# SHELL

Once a user has entered a command the terminal then accepts what the user has typed and passes it to a shell. The shell is the command line interpreter that translates commands entered by a user into actions to be performed by the operating system.

The Bash shell also has other popular features, a few of which are listed below:
* **Scripting**: The ability to place commands in a file and then interpret (effectively use Bash to execute the contents of) the file, resulting in all of the commands being executed. This feature also has some programming features, such as conditional statements and the ability to create functions (AKA subroutines).
* **Aliases**: The ability to create short nicknames for longer commands.
* **Variables**: Used to store information for the Bash shell and for the user. These variables can be used to modify how commands and features work as well as provide vital system information.

Here are representations of command line prompts in a Unix/Linux environment. 

* User Name: `ikechukwu`@ubuntu:~$ 
* System Name: ikechukwu@`ubuntu`:~$
* Current Directory: ikechukwu@ubuntu:`~`$

### VARIABLES

A variable is a feature that allows the user or the shell to store data. his data can be used to provide critical system information or to change the behavior of how the Bash shell (or other commands) works. Variables are given names and stored temporarily in memory. There are two types of variables used in the Bash shell: local and environment.

### LOCAL VARIABLES
Local or shell variables exist only in the current shell, and cannot affect other commands or applications. When the user closes a terminal window or shell, all of the variables are lost. 

`ikechukwu@ubuntu:~$ variable1='Something'` </br>
`ikechukwu@ubuntu:~$ echo $variable1`  </br>                            
`Something`

### ENVIRONMENT VARIABLES
Environment variables, also called global variables, are available system-wide, in all shells used by Bash when interpreting commands and performing tasks.

The **HISTSIZE** variable defines how many previous commands to store in the history list. When run without arguments, the `env` command outputs a list of the environment variables. The `export` command is used to turn a local variable into an environment variable.

`export MY_VARIABLE="World"`

After executing this command, whenever you reference $MY_VARIABLE in your shell session or in scripts, it will have the value "World" until you either change it again or unset it.

To concatenate the value of two environment variables, use the assignment expression:

`ikechukwu@ubuntu:~$ variable1=$variable1' '$variable2`              
`ikechukwu@ubuntu:~$ echo $variable1`                                
`Something Else`

So, if variable1 had the value "Something" and variable2 had the value "Else", after executing these commands, variable1 will have the value "Something Else".

### PATH VARIABLE
One of the most important Bash shell variables to understand is the PATH variable. It contains a list that defines which directories the shell looks in to find commands. If a valid command is entered and the shell returns a "command not found" error, it is because the Bash shell was unable to locate a command by that name in any of the directories included in the path.

### EXTERNAL COMMANDS
External commands are binary executables stored in directories that are searched by the shell. If a user types the ls command, then the shell searches through the directories that are listed in the PATH variable to try to find a file named ls that it can execute.

If a command does not behave as expected or if a command is not accessible that should be, it can be beneficial to know where the shell is finding the command or which version it is using. It would be tedious to have to manually look in each directory that is listed in the PATH variable. Instead, use the `which` command to display the full path to the command in question.

### FUNCTIONS
Functions can also be built using existing commands to either create new commands or to override commands built-in to the shell or commands stored in files.

function_name () </br>
{ </br>
    commands </br>
} </br>


# SINGLE QUOTES

Single quotes prevent the shell from doing any interpreting of special characters, including globs, variables, command substitution, and other metacharacters that have not been discussed yet.

`ikechukwu@ubuntu:~$ echo The car costs $100`                           
`The car costs 00`                                                        
`ikechukwu@ubuntu:~$ echo 'The car costs $100'`                        
`The car costs $100`

### BACKLASH CHARACTER:
If you want to have $PATH treated as a variable and $1 not?
In this case, use a backslash \ character in front of the dollar sign $ character to prevent the shell from interpreting it. The command below demonstrates using the \ character:

`ikechukwu@ubuntu:~$ echo The service costs \$1 and the path is $PATH`
`The service costs $1 and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games`

### BACKQUOTES:
Backquotes, or backticks, are used to specify a command within a command, a process called command **substitution**. This allows for powerful and sophisticated use of commands.

`ikechukwu@ubuntu:~$ echo Today is `\`date\`                       
`Today is Mon Nov 4 03:40:04 UTC 2018`

### SEMICOLON
`command1; command2; command3`
The semicolon; character can be used to run multiple commands, one after the other. Each command runs independently and consecutively; regardless of the result of the first command, the second command runs once the first has completed, then the third, and so on.

### DOUBLE AMPERSAND
`command1 && command2`
The double ampersand && acts as a logical "and"; if the first command is successful, then the second command will also run. If the first command fails, then the second command will not run.

### DOUBLE PIPE
`command1 || command2`
The double pipe || is a logical "or". Depending on the result of the first command, the second command will either run or be skipped.
With the double pipe, if the first command runs successfully, the second command is skipped; if the first command fails, then the second command is run. In other words, you are essentially telling the shell, "Either run this first command or the second one”.


# QUOTING

- **Single quotes** (' ‘): prevent the shell from interpreting or expanding special characters in a string, preserving it exactly as written. This is useful when you want to pass a string as a parameter to a command without changes. When enclosing characters in single quotes, everything between the single quotes is treated as a literal string.

- **Double quotes** (" “): prevent the expansion of glob characters but allow for variable expansion and command substitution to occur. This is useful when you want to include variables or execute commands within a string. Double quotes are used to create a quoted string where variable substitution and command substitution are allowed. Variables inside double quotes are expanded to their values, and commands enclosed with $() or backticks are executed, with their output substituted.

- **Backticks** (\` \`): enable command substitution, allowing the output of a command to replace the backquoted expression in a line. Backticks are used for command substitution. Anything enclosed within backticks is treated as a command to be executed, and the output of that command is substituted in place.


# GETTING HELP IN LINUX

In Linux, getting help is essential for mastering the operating system and its various commands. Here are some common methods to get help:

### MAN PAGES

The Manual Pages (man pages) in Linux systems provide documentation for various commands, functions, system calls, and configurations. By default, there are nine sections in the man pages, each covering different aspects of the system:

- General Commands (Section 1): Documentation for general user commands and utilities typically used on the command line.
- System Calls (Section 2): Describes system calls, which are functions provided by the kernel for programmatic interaction with the operating system.
- Library Calls (Section 3): Covers library functions provided by the C library and other libraries, often used by developers when writing programs in C.
- Special Files (Section 4): Information about special files representing devices or interfaces in the system, found in the /dev directory.
- File Formats and Conventions (Section 5): Documents file formats, conventions, and specific configuration files used by the system.
- Games (Section 6): Documentation for games available on the system.
- Miscellaneous (Section 7): Includes miscellaneous documentation on topics like macro packages and conventions.
- System Administration Commands (Section 8): Documentation for commands primarily used by system administrators to manage and configure the system.
- Kernel Routines (Section 9): Provides documentation for kernel routines, often of interest to kernel developers.

On most Linux distributions:

The `whatis` command and `man -f` command are functionally equivalent, providing a brief description of commands.

The `apropos` command and `man -k` command are functionally equivalent, searching for keywords in man page names and descriptions.

To search for man pages by name, use the `-f` option with the man command to display man pages matching a specific name and provide their section number and a brief description.

To search for the location of a command or its man pages, use the `whereis` command, which searches for commands, source files, and man pages in typical locations where these files are stored. 

NB: The man page is displayed with the less command

##### SHORTCUTS:
- h         => getting help
- q         => quit
- enter     => show next line
- space     => show next screen
- /string   => search forward for a string
- ?string   => search backward for a string
- n / N     => next/previous appearance

### HELP

When dealing with shell built-in commands in Linux, you can use the `help` command followed by the built-in command name to get information about its usage and options. For example:

help command    => Ex: `help cd`
command --help  => Ex: `rm --help`

On most systems, there is a directory where additional documentation (such as documentation files stored by third-party software vendors) is found.
‌⁠
These documentation files are often called readme files since the files typically have names such as README or readme.txt. The location of these files can vary depending on the distribution that you are using. Typical locations include `/usr/share/doc` and `/usr/doc`.
Typically, this directory is where system administrators go to learn how to set up more complex software services. However, sometimes regular users also find this documentation to be useful.


# DIRECTORY STRUCTURE

On a Windows system, the top level of the directory structure is called My Computer. Physical devices, such as hard drives, USB drives, and network drives, show up under My Computer and are each assigned a drive letter, such as C: or D:

Like Windows, the Linux directory structure, typically called a filesystem, also has a top level. However instead of My Computer, it is called the root directory, and it is symbolized by the slash(/) character. Additionally, there are no drives in Linux; each physical device is accessible under a directory, as opposed to a drive letter.

Most of the hidden files are customization files, designed to customize how Linux, your shell, or programs work. For example, the .bashrc file in the home directory customizes features of the shell, such as creating or modifying variables and aliases.


# GLOBBING

Globbing refers to the process of using wildcards or special characters, such as '*' and '?', in a command-line interface to match files or directories based on patterns.

### ASTERISK (*) CHARACTER
  
The asterisk * character is used to represent zero or more of any character in a filename. For example, to display all of the files in the /etc directory that begin with the letter t:

`ikechukwu@ubuntu:~$ echo /etc/t*`                              
`/etc/terminfo /etc/timezone /etc/tmpfiles.d`

The following matches any filename in the /etc directory that ends with .d:

`ikechukwu@ubuntu:~$ echo /etc/*.d`                                 
`/etc/apparmor.d /etc/binfmt.d /etc/cron.d` 

All of the files in the /etc directory that begin with the letter r and end with .conf are displayed:

`ikechukwu@ubuntu:~$ echo /etc/r*.conf`                             
`/etc/resolv.conf /etc/rsyslog.conf`

### QUESTION MARK (?) CHARACTER
  
The question mark character represents any single character. Each question mark character matches exactly one character, no more and no less.
Suppose you want to display all of the files in the /etc directory that begin with the letter t and have exactly 7 characters after the t character:

`ikechukwu@ubuntu:~$ echo /etc/t???????`      
`/etc/terminfo /etc/timezone`

The ? character can be used to match exactly 1 character in a file name. Execute the following command to display all of the files in the /etc directory that are exactly four characters long:

`ikechukwu@ubuntu:~$ ls -d /etc/????`

Glob characters can be used together to find even more complex patterns. The pattern /etc/*???????????????????? only matches files in the /etc directory with twenty or more characters in the filename:

`ikechukwu@ubuntu:~$ echo /etc/*????????????????????`            
`/etc/bindresvport.blacklist /etc/ca-certificates.conf`

The asterisk and question mark could also be used together to look for files with three-letter extensions by using the /etc/*.??? pattern:

`ikechukwu@ubuntu:~$ echo /etc/*.???`              
`/etc/issue.net /etc/locale.gen`


# BRACKET [ ] CHARACTERS
The bracket [ ] characters are used to match a single character by representing a range of characters that are possible match characters. For example, the `/etc/[gu]*` pattern matches any file that begins with either a "g" or "u" character and contains zero or more additional characters:

`ikechukwu@ubuntu:~$ echo /etc/[gu]*`                            
`/etc/gai.conf /etc/groff /etc/group /etc/group- /etc/gshadow /etc/gshadow- /etc/
gss /etc/ucf.conf /etc/udev /etc/ufw /etc/update-motd.d /etc/updatedb.conf`           

By using square brackets [ ] you can specify a single character to match from a set of characters. Execute the following command to display all of the files in the /etc directory that begin with the letters a, b, c, or d:

`ikechukwu@ubuntu:~$ ls –d /etc/[abcd]*`

Brackets can also be used to represent a range of characters. For example, the `/etc/[a-d]*` pattern matches all files that begin with any letter between and including a and d. 

The `/etc/*[0-9]*` pattern displays any file that contains at least one number:

Exclamation Point (!) Character
The exclamation point character is used in conjunction with the square brackets to negate a range. For example, the pattern `/etc/[!DP]*` matches any file that does not begin with a D or P.

`ikechukwu@ubuntu:~$ echo /etc/[!a-t]*`
`/etc/X11 /etc/ucf.conf /etc/udev /etc/ufw /etc/update-motd.d /etc/updatedb.conf 
/etc/vim /etc/vtrgb /etc/wgetrc /etc/xdg`


# KEYBOARD SHORTCUTS

* TAB - autocompletes the command or the filename if it's unique

* TAB TAB (press twice) - displays all commands or filenames that start with those letters

* Clearing the terminal - CTRL + L

* Closing the shell (exit) - CTRL + D

* Cutting (removing) the current line  - CTRL + U

* Moving the cursor to the start of the line - CTRL + A

* Moving the cursor to the end of the line - Ctrl + E

* Stopping the current command - CTRL + C

* Sleeping a running program - CTRL + Z

* Opening a terminal  - CTRL + ALT + T

* Search for commands in history. - CTRL + R

* Previous command in history - Ctrl + P

* Leave the history search mode without running a command. - Ctrl + G

* Leave the root environment - Ctrl + D

