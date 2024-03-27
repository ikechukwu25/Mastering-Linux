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


In Linux, The variety of distributions and accompanying software allows the operating system to be significantly more flexible and customisable. Distributions are available for a much wider variety of systems, from commercial offerings for the traditional server or desktop roles, to specialised distributions designed to turn an old computer into a network firewall; from distributions created to power a supercomputer, to those that enable embedded systems.

Linux distributions can be broadly classed in two main categories: enthusiast and enterprise. An enthusiast distribution such as openSUSE’s Tumbleweed has a fast update cycle, is not supported for enterprise and may not contain (or drop) features or software in the next version that are in the current one. Red Hat’s Fedora project uses a similar method of development and release cycle, as does Ubuntu Desktop.
Enterprise distributions are almost the exact opposite, in that they take care to be stable and consistent, and offer enterprise-grade support for extended periods, anywhere from 5-13 years in the case of SUSE. Enterprise distributions are fewer by far, being offered mainly by Red Hat, Canonical and SUSE.

In summary, while enthusiast distributions offer the latest features and rapid updates, they are not typically recommended for enterprise use due to potential stability concerns. Enterprise distributions prioritize stability, long-term support, and a predictable environment, making them suitable for mission-critical applications in business settings.

For example, some distributions offer stable, testing, and unstable releases. A business may value stability and want long release cycles, while a hobbyist or a startup may want the latest software and opt for a shorter release cycle. To satisfy the latter group, Red Hat sponsors the Fedora Project which makes a personal desktop comprising the latest software but is still built on the same foundations as the enterprise version.

Fedora = Enthusiast     WHILE    Red Hat Enterprise Linux = Enterprise. 

SUSE, originally derived from Slackware, was one of the first comprehensive Linux distributions, it has many similarities to Red Hat Enterprise Linux. While SUSE Linux Enterprise contains proprietary code and is sold as a server product, openSUSE is a completely open, free version with multiple desktop packages similar to CentOS and Linux Mint.

_Proprietary code, also known as closed-source or non-free code, refers to computer program code that is not freely available for the public to view, modify, or distribute._

