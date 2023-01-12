# Linux Fundamentals

Tags: #🧑‍🎓 
Related to: [[addgroup]], [[apropos]], [[apt]], [[aptitude]], [[awk]], [[bg]], [[cat]], [[cd]], [[chmod chown]], [[clear]], [[column]], [[cp]], [[curl]], [[cut]], [[delgroup]], [[dpkg]], [[env]], [[fg]], [[find]], [[gem]], [[git]], [[grep]], [[head]] , [[hostname]], [[id]], [[ifconfig]], [[ip]], [[jobs]], [[journalctl]], [[kill]], [[less more]], [[locate]], [[ls]], [[lsblk]], [[lsof]], [[lspci]], [[lsusb]], [[man]], [[mkdir]], [[mv]], [[nano]], [[netstat]], [[passwd]], [[pip]], [[ps]], [[pwd]], [[python]], [[sed]], [[snap]], [[sort]], [[ss]], [[su]], [[sudo]], [[systemctl]], [[tail]], [[touch]], [[tr]], [[tree]], [[uname]], [[updatedb]], [[useradd]], [[userdel]], [[usermod]], [[wc]], [[wget]], [[which]], [[who]], [[whoami]]
See also:
Previous: [[HTB Academy]]

![[logo_linux_fundamentals.png]]

This module covers the fundamentals required to work comfortably with the Linux operating system and shell.

### Cheatsheet

| **Command** | **Description** |
| --------------|-------------------|
| `man <tool>` | Opens man pages for the specified tool. | 
| `<tool> -h` | Prints the help page of the tool. | 
| `apropos <keyword>` | Searches through man pages' descriptions for instances of a given keyword. | 
| `cat` | Concatenate and print files. |
| `whoami` | Displays current username. | 
| `id` | Returns users identity. | 
| `hostname` | Sets or prints the name of the current host system. | 
| `uname` | Prints operating system name. | 
| `pwd` | Returns working directory name. | 
| `ifconfig` | The `ifconfig` utility is used to assign or view an address to a network interface and/or configure network interface parameters. | 
| `ip` | Ip is a utility to show or manipulate routing, network devices, interfaces, and tunnels. | 
| `netstat` | Shows network status. | 
| `ss` | Another utility to investigate sockets. | 
| `ps` | Shows process status. | 
| `who` | Displays who is logged in. | 
| `env` | Prints environment or sets and executes a command. | 
| `lsblk` | Lists block devices. | 
| `lsusb` | Lists USB devices. | 
| `lsof` | Lists opened files. | 
| `lspci` | Lists PCI devices. | 
| `sudo` | Execute command as a different user. | 
| `su` | The `su` utility requests appropriate user credentials via PAM and switches to that user ID (the default user is the superuser).  A shell is then executed. | 
| `useradd` | Creates a new user or update default new user information. | 
| `userdel` | Deletes a user account and related files. |
| `usermod` | Modifies a user account. | 
| `addgroup` | Adds a group to the system. | 
| `delgroup` | Removes a group from the system. | 
| `passwd` | Changes user password. |
| `dpkg` | Install, remove and configure Debian-based packages. | 
| `apt` | High-level package management command-line utility. | 
| `aptitude` | Alternative to `apt`. | 
| `snap` | Install, remove and configure snap packages. |
| `gem` | Standard package manager for Ruby. | 
| `pip` | Standard package manager for Python. | 
| `git` | Revision control system command-line utility. | 
| `systemctl` | Command-line based service and systemd control manager. |
| `ps` | Prints a snapshot of the current processes. | 
| `journalctl` | Query the systemd journal. | 
| `kill` | Sends a signal to a process. | 
| `bg` | Puts a process into background. |
| `jobs` | Lists all processes that are running in the background. | 
| `fg` | Puts a process into the foreground. | 
| `curl` | Command-line utility to transfer data from or to a server. | 
| `wget` | An alternative to `curl` that downloads files from FTP or HTTP(s) server. |
| `python3 -m http.server` | Starts a Python3 web server on TCP port 8000. | 
| `ls` | Lists directory contents. | 
| `cd` | Changes the directory. |
| `clear` | Clears the terminal. | 
| `touch` | Creates an empty file. |
| `mkdir` | Creates a directory. | 
| `tree` | Lists the contents of a directory recursively. |
| `mv` | Move or rename files or directories. | 
| `cp` | Copy files or directories. |
| `nano` | Terminal based text editor. | 
| `which` | Returns the path to a file or link. |
| `find` | Searches for files in a directory hierarchy. | 
| `updatedb` | Updates the locale database for existing contents on the system. |
| `locate` | Uses the locale database to find contents on the system. | 
| `more` | Pager that is used to read STDOUT or files. |
| `less` | An alternative to `more` with more features. | 
| `head` | Prints the first ten lines of STDOUT or a file. |
| `tail` | Prints the last ten lines of STDOUT or a file. | 
| `sort` | Sorts the contents of STDOUT or a file. |
| `grep` | Searches for specific results that contain given patterns. | 
| `cut` | Removes sections from each line of files. |
| `tr` | Replaces certain characters. | 
| `column` | Command-line based utility that formats its input into multiple columns. |
| `awk` | Pattern scanning and processing language. |
| `sed` | A stream editor for filtering and transforming text. | 
| `wc` | Prints newline, word, and byte counts for a given input. |
| `chmod` | Changes permission of a file or directory. |
| `chown` | Changes the owner and group of a file or directory. |

### Module Summary

Linux is an indispensable tool and system in the field of cybersecurity. Many servers run on Linux and offer a wide range of possibilities for offensive security practitioners, network defenders, and systems administrators. This module covers the essentials for starting with the Linux operating system and terminal.

In this module, we will cover:

-   Linux structure
-   Using the shell
-   Navigating the Linux operating system
-   Working with files and directories
-   Linux administration
-   Service management
-   Permissions management

This module is broken down into sections with accompanying hands-on exercises to practice each of the tactics and techniques we cover. The module ends with a practical hands-on skills assessment to gauge your understanding of the various topic areas.

As you work through the module, you will see example commands and command output for the various topics introduced. It is worth reproducing as many of these examples as possible to reinforce further the concepts introduced in each section. You can do this in the Pwnbox provided in the interactive sections or your own virtual machine.

You can start and stop the module at any time and pick up where you left off. There is no time limit or "grading," but you must complete all of the exercises and the skills assessment to receive the maximum number of cubes and have this module marked as complete in any paths you have chosen.

The module is classified as "Fundamental." It assumes that the user has little to no prior experience with the Linux operating system but is generally comfortable navigating a graphical operating system such as Windows.

This module has no prerequisites but serves as the basis for many of the modules contained within the Academy. Completion and an in-depth understanding of this module are crucial for success as you progress through the Academy and Hack the Box platforms.

# Introduction

## Linux Structure

* * * * *

### History
-------

Many events led up to creating the first Linux kernel and, ultimately, the Linux operating system (OS), starting with the Unix operating system's release by Ken Thompson and Dennis Ritchie (whom both worked for AT&T at the time) in 1970. The Berkeley Software Distribution (BSD) was released in 1977, but since it contained the Unix code owned by AT&T, a resulting lawsuit limited the development of BSD. Richard Stallman started the GNU project in 1983. His goal was to create a free Unix-like operating system, and part of his work resulted in the GNU General Public License (GPL) being created. Projects by others over the years failed to result in a working, free kernel that would become widely adopted until the creation of the Linux kernel.

At first, Linux was a personal project started in 1991 by a Finnish student named Linus Torvalds. His goal was to create a new, free operating system kernel. Over the years, the Linux kernel has gone from a small number of files written in C under licensing that prohibited commercial distribution to the latest version with over 23 million source code lines (comments excluded), licensed under the GNU General Public License v2.

Linux is available in over 600 distributions (or an operating system based on the Linux kernel and supporting software and libraries). Some of the most popular and well-known being Ubuntu, Debian, Fedora, OpenSUSE, elementary, Manjaro, Gentoo Linux, RedHat, and Linux Mint.

Linux is generally considered more secure than other operating systems, and while it has had many kernel vulnerabilities in the past, it is becoming less and less frequent. It is less susceptible to malware than Windows operating systems and is very frequently updated. Linux is also very stable and generally affords very high performance to the end-user. However, it can be more difficult for beginners and does not have as many hardware drivers as Windows.

Since Linux is free and open-source, the source code can be modified and distributed commercially or non-commercially by anyone. Linux-based operating systems run on servers, mainframes, desktops, embedded systems such as routers, televisions, video game consoles, and more. The overall Android operating system that runs on smartphones and tablets is based on the Linux kernel, and because of this, Linux is the most widely installed operating system.

Linux is an operating system like Windows, iOS, Android, or macOS. An OS is software that manages all of the hardware resources associated with our computer. That means that an OS manages the whole communication between software and hardware. Also, there exist many different distributions (distro). It is like a version of Windows operating systems.

With the interactive instances, we get access to the Pwnbox, a customized version of Parrot OS. This will be the primary OS we will work with through the modules. Parrot OS is a Debian-based Linux distribution that focuses on security, privacy, and development.

* * * * *

### Philosophy
----------

Linux follows five core principles:

| Principle | Description |
| --- | --- |
| `Everything is a file` | All configuration files for the various services running on the Linux operating system are stored in one or more text files. |
| `Small, single-purpose programs` | Linux offers many different tools that we will work with, which can be combined to work together. |
| `Ability to chain programs together to perform complex tasks` | The integration and combination of different tools enable us to carry out many large and complex tasks, such as processing or filtering specific data results. |
| `Avoid captive user interfaces` | Linux is designed to work mainly with the shell (or terminal), which gives the user greater control over the operating system. |
| `Configuration data stored in a text file` | An example of such a file is the `/etc/passwd` file, which stores all users registered on the system. |

* * * * *

### Components
----------

| Component | Description |
| --- | --- |
| `Bootloader` | A piece of code that runs to guide the booting process to start the operating system. Parrot Linux uses the GRUB Bootloader. |
| `OS Kernel` | The kernel is the main component of an operating system. It manages the resources for system's I/O devices at the hardware level. |
| `Daemons` | Background services are called "daemons" in Linux. Their purpose is to ensure that key functions such as scheduling, printing, and multimedia are working correctly. These small programs load after we booted or log into the computer. |
| `OS Shell` | The operating system shell or the command language interpreter (also known as the command line) is the interface between the OS and the user. This interface allows the user to tell the OS what to do. The most commonly used shells are Bash, Tcsh/Csh, Ksh, Zsh, and Fish. |
| `Graphics server` | This provides a graphical sub-system (server) called "X" or "X-server" that allows graphical programs to run locally or remotely on the X-windowing system. |
| `Window Manager` | Also known as a graphical user interface (GUI). There are many options, including GNOME, KDE, MATE, Unity, and Cinnamon. A desktop environment usually has several applications, including file and web browsers. These allow the user to access and manage the essential and frequently accessed features and services of an operating system. |
| `Utilities` | Applications or utilities are programs that perform particular functions for the user or another program. |

* * * * *

### Linux Architecture
------------------

The Linux operating system can be broken down into layers:

| Layer | Description |
| --- | --- |
| `Hardware` | Peripheral devices such as the system's RAM, hard drive, CPU, and others. |
| `Kernel` | The core of the Linux operating system whose function is to virtualize and control common computer hardware resources like CPU, allocated memory, accessed data, and others. The kernel gives each process its own virtual resources and prevents/mitigates conflicts between different processes. |
| `Shell` | A command-line interface (CLI), also known as a shell that a user can enter commands into to execute the kernel's functions. |
| `System Utility` | Makes available to the user all of the operating system's functionality. |

* * * * *

### File System Hierarchy
---------------------

The Linux operating system is structured in a tree-like hierarchy and is documented in the [Filesystem Hierarchy](http://www.pathname.com/fhs/) Standard (FHS). Linux is structured with the following standard top-level directories:

![[NEW_filesystem.png]]

| Path | Description |
| --- | --- |
| `/` | The top-level directory is the root filesystem and contains all of the files required to boot the operating system before other filesystems are mounted as well as the files required to boot the other filesystems. After boot, all of the other filesystems are mounted at standard mount points as subdirectories of the root. |
| `/bin` | Contains essential command binaries. |
| `/boot` | Consists of the static bootloader, kernel executable, and files required to boot the Linux OS. |
| `/dev` | Contains device files to facilitate access to every hardware device attached to the system. |
| `/etc` | Local system configuration files. Configuration files for installed applications may be saved here as well. |
| `/home` | Each user on the system has a subdirectory here for storage. |
| `/lib` | Shared library files that are required for system boot. |
| `/media` | External removable media devices such as USB drives are mounted here. |
| `/mnt` | Temporary mount point for regular filesystems. |
| `/opt` | Optional files such as third-party tools can be saved here. |
| `/root` | The home directory for the root user. |
| `/sbin` | This directory contains executables used for system administration (binary system files). |
| `/tmp` | The operating system and many programs use this directory to store temporary files. This directory is generally cleared upon system boot and may be deleted at other times without any warning. |
| `/usr` | Contains executables, libraries, man files, etc. |
| `/var` | This directory contains variable data files such as log files, email in-boxes, web application related files, cron files, and more. |

## Introduction to Shell

* * * * *

It is crucial to learn how to use the Linux shell, as there are many servers based on Linux. These are often used because Linux is less error-prone as opposed to Windows servers. For example, web servers are often based on Linux. Knowing how to use the operating system to control it effectively requires understanding and mastering Linux's essential part, the `Shell`. When we first switched from Windows to Linux, does it look something like this:

![[first_linux2.png]]

A Linux terminal, also called a `shell` or command line, provides a text-based input/output (I/O) interface between users and the kernel for a computer system. The term console is also typical but does not refer to a window but a screen in text mode. In the terminal window, commands can be executed to control the system.

* * * * *

### Terminal Emulators
------------------

Terminal emulators are often used for this. Terminal emulation is software that emulates the function of a terminal. It allows the use of text-based programs within a graphical user interface (`GUI`). Many different terminal emulators exist, such as `GNOME Terminal`, `XFCE4 Terminal`, `XTerm`, and many others. There are also so-called command-line interfaces that run as additional terminals in one terminal and thus are `multiplexers`. These multiplexers include `Tmux`, `GNU Screen`, and others. In short, a terminal serves as an interface to the shell interpreter.

Terminal emulators and multiplexers are beneficial extensions for the terminal. They provide us with different methods and functions to work with the terminal, such as splitting the terminal in one window, working in multiple directories, creating different workspaces, and much more. An example of the use of such a multiplexer called Tmux could look something like this:

![[tmux.png]]

* * * * *

### Shell
-----

The most commonly used shell in Linux is the `Bourne-Again Shell` (`BASH`) and is part of the GNU project. Everything we do through the GUI we can do with the shell. The shell gives us many more possibilities to interact with programs and processes to get information faster. Besides, many processes can be easily automated with smaller or larger scripts that make manual work much easier.

Besides Bash, there also exist other shells like [Tcsh/Csh](https://en.wikipedia.org/wiki/Tcsh), [Ksh](https://en.wikipedia.org/wiki/KornShell), [Zsh](https://en.wikipedia.org/wiki/Z_shell), [Fish](https://en.wikipedia.org/wiki/Friendly_interactive_shell) shell, and others.

# The Shell

## Prompt Description

---

The bash prompt is easy to understand and, by default, includes information such as the user, hostname, and current working directory. The format can look something like this:

```text
<username>@<hostname><current working directory>$
```

The home directory for a user is marked with a tilde <`~`> and is the default folder when we log in.

```text
<username>@<hostname>[~]$
```

The dollar sign, in this case, stands for a user. As soon as we log in as `root`, the character changes to a `hash` <`#`> and looks like this:

```text
root@htb[/htb]#
```

We see here the same as when we work on the Windows GUI. We are logged in as a user on a computer with a specific name, and we know which directory we are in when we navigate through our system. Bash prompt can also be customized and changed to our own needs. The adjustment of the bash prompt is outside the scope for this module. However, we can look at the [bashrcgenerator](http://bashrcgenerator.com/) and [powerline](https://github.com/powerline/powerline), which gives us the possibility to adapt our prompt to our needs.

## Getting Help

* * * * *

We will always stumble across tools whose optional parameters we do not know from memory or tools we have never seen before. Therefore it is vital to know how we can help ourselves to get familiar with those tools. The first two ways are the man pages and the help functions. It is always a good idea to familiarize ourselves with the tool we want to try first. We will also learn some possible tricks with some of the tools that we thought were not possible. In the man pages, we will find the detailed manuals with detailed explanations.

#### Syntax:

	man <tool>

Let us have a look at an example:

#### Example:

	man curl

```text
curl(1)                                                             Curl Manual                                                            curl(1)

NAME
       curl - transfer a URL

SYNOPSIS
       curl [options] [URL...]

DESCRIPTION
       curl  is  a tool to transfer data from or to a server, using one of the supported protocols (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS,  
       IMAP, IMAPS,  LDAP,  LDAPS,  POP3,  POP3S,  RTMP, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET, and TFTP). The command is designed to work without user interaction.

       curl offers a busload of useful tricks like proxy support, user authentication, FTP upload, HTTP post, SSL connections, cookies, file transfer resume, Metalink,  and more. As we will see below, the number of features will make our head spin!

       curl is powered by libcurl for all transfer-related features.  See libcurl(3) for details.

Manual page curl(1) line 1 (press h for help or q to quit)
```

After looking at some examples, we can also quickly look at the optional parameters without browsing through the complete documentation. We have several ways to do that.

#### Syntax:

	<tool> --help

#### Example:

	curl --help

```text
Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --anyauth       Pick any authentication method
 -a, --append        Append to target file when uploading
     --basic         Use HTTP Basic Authentication
     --cacert <file> CA certificate to verify peer against
     --capath <dir>  CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
<SNIP>
```

We can also use the short version of it:

#### Syntax:

	<tool> -h

#### Example:

	curl -h

```text
Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --anyauth       Pick any authentication method
 -a, --append        Append to target file when uploading
     --basic         Use HTTP Basic Authentication
     --cacert <file> CA certificate to verify peer against
     --capath <dir>  CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
<SNIP>
```

As we can see, the results from each other do not differ in this example. Another tool that can be useful in the beginning is `apropos`. Each manual page has a short description available within it. This tool searches the descriptions for instances of a given keyword.

#### Syntax:

	apropos <keyword>

#### Example:

	apropos sudo

```text
sudo (8)             - execute a command as another user
sudo.conf (5)        - configuration for sudo front end
sudo_plugin (8)      - Sudo Plugin API
sudo_root (8)        - How to run administrative commands
sudoedit (8)         - execute a command as another user
sudoers (5)          - default sudo security policy plugin
sudoreplay (8)       - replay sudo session logs
visudo (8)           - edit the sudoers file
```

Another useful resource to get help if we have issues to understand a long command is: [https://explainshell.com/](https://explainshell.com/)

## System Information

* * * * *

Since we will be working with many different Linux systems, we need to learn the structure and the information about the system, its processes, network configurations, users, directories, user settings, and the corresponding parameters. Here is a list of the necessary tools that will help us get the above information. Most of them are installed by default.

| Command | Description |
| --- | --- |
| `whoami` | Displays current username. |
| `id` | Returns users identity |
| `hostname` | Sets or prints the name of current host system. |
| `uname` | Prints basic information about the operating system name and system hardware. |
| `pwd` | Returns working directory name. |
| `ifconfig` | The ifconfig utility is used to assign or to view an address to a network interface and/or configure network interface parameters. |
| `ip` | Ip is a utility to show or manipulate routing, network devices, interfaces and tunnels. |
| `netstat` | Shows network status. |
| `ss` | Another utility to investigate sockets. |
| `ps` | Shows process status. |
| `who` | Displays who is logged in. |
| `env` | Prints environment or sets and executes command. |
| `lsblk` | Lists block devices. |
| `lsusb` | Lists USB devices |
| `lsof` | Lists opened files. |
| `lspci` | Lists PCI devices. |

Let us look at a few examples.

#### Hostname

The `hostname` command is pretty self-explanatory and will just print the name of the computer that we are logged into

	hostname

```text
nixfund
```

#### Whoami

This quick and easy command can be used on both Windows and Linux systems to get our current username. During a security assessment, we obtain reverse shell access on a host, and one of the first bits of situational awareness we should do is figuring out what user we are running as. From there, we can figure out if the user has any special privileges/access.

	whoami

```text
cry0l1t3
```

#### Id

The `id` command expands on the `whoami` command and prints out our effective group membership and IDs. This can be of interest to penetration testers looking to see what access a user may have and sysadmins looking to audit account permissions and group membership. In this output, the `hackthebox` group is of interest because it is non-standard, the `adm` group means that the user can read log files in `/var/log` and could potentially gain access to sensitive information, membership in the `sudo` group is of particular interest as this means our user can run some or all commands as the all-powerful `root` user. Sudo rights could help us escalate privileges or could be a sign to a sysadmin that they may need to audit permissions and group memberships to remove any access that is not required for a given user to carry out their day-to-day tasks.

	id

```text
uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),1337(hackthebox),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
```

#### Uname

Let's dig into the `uname` command a bit more. If we type `man uname` in our terminal, we will bring up the man page for the command, which will show the possible options we can run with the command and the results.

```text
UNAME(1)                                    User Commands                                   UNAME(1)

NAME
       uname - print system information

SYNOPSIS
       uname [OPTION]...

DESCRIPTION
       Print certain system information.  With no OPTION, same as -s.

       -a, --all
              print all information, in the following order, except omit -p and -i if unknown:

       -s, --kernel-name
              print the kernel name

       -n, --nodename
              print the network node hostname

       -r, --kernel-release
              print the kernel release

       -v, --kernel-version
              print the kernel version

       -m, --machine
              print the machine hardware name

       -p, --processor
              print the processor type (non-portable)

       -i, --hardware-platform
              print the hardware platform (non-portable)

       -o, --operating-system
```

Running `uname -a` will print all information about the machine in a specific order: kernel name, hostname, the kernel release, kernel version, machine hardware name, and operating system. The `-a` flag will omit `-p` (processor type) and `-i` (hardware platform) if they are unknown.

	uname -a

```text
Linux box 4.15.0-99-generic #100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```

From the above command, we can see that the kernel name is `Linux`, the hostname is `box`, the kernel release is `4.15.0-99-generic`, the kernel version is `#100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020`, and so on. Running any of these options on their own will give us the specific bit output we are interested in.

#### Uname to Obtain Kernel Release

Suppose we want to print out the kernel release to search for potential kernel exploits quickly. We can type `uname -r` to obtain this information.

	uname -r

```text
4.15.0-99-generic
```

With this info, we could go and search for "4.15.0-99-generic exploit," and the first [result](https://www.exploit-db.com/exploits/47163) immediately appears useful to us.

It is highly recommended to study the commands and understand what they are for and what information they can provide. Though a bit tedious, we can learn much from studying the manpages for common commands. We may even find out things that we did not even know were possible with a given command. This information is not only used for working with Linux. However, it will also be used later to discover vulnerabilities and misconfigurations on the Linux system that may contribute to privilege escalation. Here are a few optional exercises that we can solve for practice purposes, which will help us become familiar with some of the commands.

* * * * *

### Logging In via SSH
------------------

`Secure Shell` (`SSH`) refers to a protocol that allows clients to access and execute commands or actions on remote computers. On Linux-based hosts and servers running or another Unix-like operating system, SSH is one of the permanently installed standard tools and is the preferred choice for many administrators to configure and maintain a computer through remote access. It is an older and very proven protocol that does not require or offer a graphical user interface (GUI). For this reason, it works very efficiently and occupies very few resources. We use this type of connection in the following sections and in most of the other modules to offer the possibility to try out the learned commands and actions in a safe environment. We can connect to our targets with the following command:

#### SSH Login

	ssh [username]@[IP address]

#### Questions

>Find out the machine hardware name and submit it as the answer.

>What is the path to htb-student's home directory?

>What is the path to the htb-student's mail?

>Which shell is specified for the htb-student user?

>Which kernel version is installed on the system? (Format: 1.22.3)

>What is the name of the network interface that MTU is set to 1500?

# System Management

## User Management

* * * * *

User management is an essential part of Linux administration. Sometimes we need to create new users or add other users to specific groups. Another possibility is to execute commands as a different user. After all, it is not too rare that users of only one specific group have the permissions to view or edit specific files or directories. This, in turn, allows us to collect more information locally on the machine, which can be very important. Let us take a look at the following example of how to execute code as a different user.

#### Execution as a user

	cat /etc/shadow

```text
cat: /etc/shadow: Permission denied
```

#### Execution as root

	sudo cat /etc/shadow

```text
root:<SNIP>:18395:0:99999:7:::
daemon:*:17737:0:99999:7:::
bin:*:17737:0:99999:7:::
<SNIP>
```

Here is a list that will help us to better understand and deal with user management.

| Command | Description |
| --- | --- |
| `sudo` | Execute command as a different user. |
| `su` | The `su` utility requests appropriate user credentials via PAM and switches to that user ID (the default user is the superuser). A shell is then executed. |
| `useradd` | Creates a new user or update default new user information. |
| `userdel` | Deletes a user account and related files. |
| `usermod` | Modifies a user account. |
| `addgroup` | Adds a group to the system. |
| `delgroup` | Removes a group from the system. |
| `passwd` | Changes user password. |

User management is essential in any operating system, and the best way to become familiar with it is to try out the individual commands in conjunction with their various options.

#### Questions

>Which option needs to be set to create a home directory for a new user using "useradd" command?
>
>`-m`

>Which option needs to be set to lock a user account using the "usermod" command? (long version of the option)
>
>`--lock`

>Which option needs to be set to execute a command as a different user using the "su" command? (long version of the option)
>
>`--command`

## Package Management

* * * * *

Whether working as a system administrator, maintaining our own Linux machines at home, or building/upgrading/maintaining our penetration testing distribution of choice, it is crucial to have a firm grasp on the available Linux package managers and the various ways to utilize them to install, update, or remove packages. Packages are archives that contain binaries of software, configuration files, information about dependencies and keep track of updates and upgrades. The features that most package management systems provide are:

-   Package downloading
-   Dependency resolution
-   A standard binary package format
-   Common installation and configuration locations
-   Additional system-related configuration and functionality
-   Quality control

We can use many different package management systems that cover different types of files like ".deb", ".rpm", and others. The package management requirement is that the software to be installed is available as a corresponding package. Typically this is created, offered, and maintained centrally under Linux distributions. In this way, the software is integrated directly into the system, and its various directories are distributed throughout the system. The package management software changes to the system to install the package are taken from the package and implemented by the package management software. If the package management software recognizes that additional packages are required for the proper functioning of the package that has not yet been installed, a dependency is included and either warn the administrator or tries to reload the missing software from a repository, for example, and install it in advance.

If an installed software has been deleted, the package management system then retakes the package's information, modifies it based on its configuration, and deletes files. There are different package management programs that we can use for this. Here is a list of examples of such programs:

| Command | Description |
| --- | --- |
| `dpkg` | The `dpkg` is a tool to install, build, remove, and manage Debian packages. The primary and more user-friendly front-end for `dpkg` is aptitude. |
| `apt` | Apt provides a high-level command-line interface for the package management system. |
| `aptitude` | Aptitude is an alternative to apt and is a high-level interface to the package manager. |
| `snap` | Install, configure, refresh, and remove snap packages. Snaps enable the secure distribution of the latest apps and utilities for the cloud, servers, desktops, and the internet of things. |
| `gem` | Gem is the front-end to RubyGems, the standard package manager for Ruby. |
| `pip` | Pip is a Python package installer recommended for installing Python packages that are not available in the Debian archive. It can work with version control repositories (currently only Git, Mercurial, and Bazaar repositories), logs output extensively, and prevents partial installs by downloading all requirements before starting installation. |
| `git` | Git is a fast, scalable, distributed revision control system with an unusually rich command set that provides both high-level operations and full access to internals. |

It is highly recommended to set up our virtual machine (VM) locally to experiment with it. Let us experiment a bit in our local VM and extend it with a few additional packages. First, let us install `git` by using `apt`.

* * * * *

#### Advanced Package Manager (APT)

Debian-based Linux distributions use the `APT` package manager. A package is an archive file containing multiple ".deb" files. The `dpkg` utility is used to install programs from the associated ".deb" file. `APT` makes updating and installing programs easier because many programs have dependencies. When installing a program from a standalone ".deb" file, we may run into dependency issues and need to download and install one or multiple additional packages. `APT` makes this easier and more efficient by packaging together all of the dependencies needed to install a program.

Each Linux distribution uses software repositories that are updated often. When we update a program or install a new one, the system queries these repositories for the desired package. Repositories can be labeled as stable, testing, or unstable. Most Linux distributions utilize the most stable or "main" repository. This can be checked by viewing the contents of the `/etc/apt/sources.list` file. The repository list for Parrot OS is at `/etc/apt/sources.list.d/parrot.list`.

	cat /etc/apt/sources.list.d/parrot.list

```text
#parrot repository
#this file was automatically generated by parrot-mirror-selector
deb http://htb.deb.parrot.sh/parrot/ rolling main contrib non-free
#deb-src https://deb.parrot.sh/parrot/ rolling main contrib non-free
deb http://htb.deb.parrot.sh/parrot/ rolling-security main contrib non-free
#deb-src https://deb.parrot.sh/parrot/ rolling-security main contrib non-free
```

APT uses a database called the APT cache. This is used to provide information about packages installed on our system offline. We can search the APT cache, for example, to find all `Impacket` related packages.

	apt-cache search impacket

```text
impacket-scripts - Links to useful impacket scripts examples
polenum - Extracts the password policy from a Windows system
python-pcapy - Python interface to the libpcap packet capture library (Python 2)
python3-impacket - Python3 module to easily build and dissect network protocols
python3-pcapy - Python interface to the libpcap packet capture library (Python 3)
```

We can then view additional information about a package.

	apt-cache show impacket-scripts

```text
Package: impacket-scripts
Version: 1.4
Architecture: all
Maintainer: Kali Developers <devel@kali.org>
Installed-Size: 13
Depends: python3-impacket (>= 0.9.20), python3-ldap3 (>= 2.5.0), python3-ldapdomaindump
Breaks: python-impacket (<< 0.9.18)
Replaces: python-impacket (<< 0.9.18)
Priority: optional
Section: misc
Filename: pool/main/i/impacket-scripts/impacket-scripts_1.4_all.deb
Size: 2080
<SNIP>
```

We can also list all installed packages.

	apt list --installed

```text
Listing... Done
accountsservice/rolling,now 0.6.55-2 amd64 [installed,automatic]
adapta-gtk-theme/rolling,now 3.95.0.11-1 all [installed]
adduser/rolling,now 3.118 all [installed]
adwaita-icon-theme/rolling,now 3.36.1-2 all [installed,automatic]
aircrack-ng/rolling,now 1:1.6-4 amd64 [installed,automatic]
<SNIP>
```

If we are missing some packages, we can search for it and install it using the following command.

	sudo apt install impacket-scripts -y

```text
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  impacket-scripts
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 2,080 B of archives.
After this operation, 13.3 kB of additional disk space will be used.
Get:1 https://euro2-emea-mirror.parrot.sh/mirrors/parrot rolling/main amd64 impacket-scripts all 1.4 [2,080 B]
Fetched 2,080 B in 0s (15.2 kB/s)
Selecting previously unselected package impacket-scripts.
(Reading database ... 378459 files and directories currently installed.)
Preparing to unpack .../impacket-scripts_1.4_all.deb ...
Unpacking impacket-scripts (1.4) ...
Setting up impacket-scripts (1.4) ...
Scanning application launchers
Removing duplicate launchers from Debian
Launchers are updated
```

* * * * *

### Git
---

Now that we have `git` installed, we can use it to download useful tools from Github. One such project is called 'Nishang'. We will deal with and work with the project itself later. First, we need to navigate to the [project's repository](https://github.com/samratashok/nishang) and copy the Github link before using git to download it.

![[git-nishang.png]]

Nevertheless, before we download the project and its scripts and lists, we should create a particular folder.

	mkdir ~/nishang/ && git clone https://github.com/samratashok/nishang.git ~/nishang

```text
Cloning into '/opt/nishang/'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 1691 (delta 4), reused 6 (delta 2), pack-reused 1676
Receiving objects: 100% (1691/1691), 7.84 MiB | 4.86 MiB/s, done.
Resolving deltas: 100% (1055/1055), done.
```

* * * * *

### DPKG
----

We can also download the programs and tools from the repositories separately. In this example, we download 'strace' for Ubuntu 18.04 LTS.

	wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb

```text
--2020-05-15 03:27:17--  http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
Resolving archive.ubuntu.com (archive.ubuntu.com)... 91.189.88.142, 91.189.88.152, 2001:67c:1562::18, ...
Connecting to archive.ubuntu.com (archive.ubuntu.com)|91.189.88.142|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 333388 (326K) [application/x-debian-package]
Saving to: ‘strace_4.21-1ubuntu1_amd64.deb’

strace_4.21-1ubuntu1_amd64.deb       100%[===================================================================>] 325,57K  --.-KB/s    in 0,1s    

2020-05-15 03:27:18 (2,69 MB/s) - ‘strace_4.21-1ubuntu1_amd64.deb’ saved [333388/333388]
```

Furthermore, now we can use both `apt` and `dpkg` to install the package. Since we have already worked with `apt`, we will turn to `dpkg` in the next example.

	sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb 

```text
(Reading database ... 154680 files and directories currently installed.)
Preparing to unpack strace_4.21-1ubuntu1_amd64.deb ...
Unpacking strace (4.21-1ubuntu1) over (4.21-1ubuntu1) ...
Setting up strace (4.21-1ubuntu1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
```

With this, we have already installed the tool and can test if it works properly.

	strace -h

```text
usage: strace [-CdffhiqrtttTvVwxxy] [-I n] [-e expr]...
              [-a column] [-o file] [-s strsize] [-P path]...
              -p pid... / [-D] [-E var=val]... [-u username] PROG [ARGS]
   or: strace -c[dfw] [-I n] [-e expr]... [-O overhead] [-S sortby]
              -p pid... / [-D] [-E var=val]... [-u username] PROG [ARGS]

Output format:
  -a column      alignment COLUMN for printing syscall results (default 40)
  -i             print instruction pointer at time of syscall
```

##### Optional Exercise:

>Search for "evil-winrm" tool on Github and install it on our interactive instances. Try all the different installation methods.

## Service and Process Management

* * * * *

In general, there are two types of services: internal, the relevant services that are required at system startup, which for example, perform hardware-related tasks, and services that are installed by the user, which usually include all server services. Such services run in the background without any user interaction. These are also called `daemons` and are identified by the letter '`d`' at the end of the program name, for example, `sshd` or `systemd`.

Most Linux distributions have now switched to `systemd`. This daemon is an `Init process` started first and thus has the process ID (PID) 1. This daemon monitors and takes care of the orderly starting and stopping of other services. All processes have an assigned PID that can be viewed under `/proc/` with the corresponding number. Such a process can have a parent process ID (PPID), known as the child process.

Besides `systemctl` we can also use `update-rc.d` to manage SysV init script links. Let us have a look at some examples. We will use the `OpenSSH` server in these examples. If we do not have this installed, please install it before proceeding to this section.

* * * * *

### Systemctl
---------

After installing `OpenSSH` on our VM, we can start the service with the following command.

	systemctl start ssh

After we have started the service, we can now check if it runs without errors.

	systemctl status ssh

```text
● ssh.service - OpenBSD Secure Shell server
   Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-05-14 15:08:23 CEST; 24h ago
   Main PID: 846 (sshd)
   Tasks: 1 (limit: 4681)
   CGroup: /system.slice/ssh.service
           └─846 /usr/sbin/sshd -D

Mai 14 15:08:22 inlane systemd[1]: Starting OpenBSD Secure Shell server...
Mai 14 15:08:23 inlane sshd[846]: Server listening on 0.0.0.0 port 22.
Mai 14 15:08:23 inlane sshd[846]: Server listening on :: port 22.
Mai 14 15:08:23 inlane systemd[1]: Started OpenBSD Secure Shell server.
Mai 14 15:08:30 inlane systemd[1]: Reloading OpenBSD Secure Shell server.
Mai 14 15:08:31 inlane sshd[846]: Received SIGHUP; restarting.
Mai 14 15:08:31 inlane sshd[846]: Server listening on 0.0.0.0 port 22.
Mai 14 15:08:31 inlane sshd[846]: Server listening on :: port 22.
```

To add OpenSSH to the SysV script to tell the system to run this service after startup, we can link it with the following command:

	systemctl enable ssh

```text
Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable ssh
```

Once we reboot the system, the OpenSSH server will automatically run. We can check this with a tool called `ps`.

	ps -aux | grep ssh

```text
root       846  0.0  0.1  72300  5660 ?        Ss   Mai14   0:00 /usr/sbin/sshd -D
```

We can also use `systemctl` to list all services.

	systemctl list-units --type=service

```text
UNIT                                                       LOAD   ACTIVE SUB     DESCRIPTION              
accounts-daemon.service                                    loaded active running Accounts Service         
acpid.service                                              loaded active running ACPI event daemon        
apache2.service                                            loaded active running The Apache HTTP Server   
apparmor.service                                           loaded active exited  AppArmor initialization  
apport.service                                             loaded active exited  LSB: automatic crash repor
avahi-daemon.service                                       loaded active running Avahi mDNS/DNS-SD Stack  
bolt.service                                               loaded active running Thunderbolt system service
```

It is quite possible that the services do not start due to an error. To see the problem, we can use the tool `journalctl` to view the logs.

	journalctl -u ssh.service --no-pager

```text
-- Logs begin at Wed 2020-05-13 17:30:52 CEST, end at Fri 2020-05-15 16:00:14 CEST. --
Mai 13 20:38:44 inlane systemd[1]: Starting OpenBSD Secure Shell server...
Mai 13 20:38:44 inlane sshd[2722]: Server listening on 0.0.0.0 port 22.
Mai 13 20:38:44 inlane sshd[2722]: Server listening on :: port 22.
Mai 13 20:38:44 inlane systemd[1]: Started OpenBSD Secure Shell server.
Mai 13 20:39:06 inlane sshd[3939]: Connection closed by 10.22.2.1 port 36444 [preauth]
Mai 13 20:39:27 inlane sshd[3942]: Accepted password for master from 10.22.2.1 port 36452 ssh2
Mai 13 20:39:27 inlane sshd[3942]: pam_unix(sshd:session): session opened for user master by (uid=0)
Mai 13 20:39:28 inlane sshd[3942]: pam_unix(sshd:session): session closed for user master
Mai 14 02:04:49 inlane sshd[2722]: Received signal 15; terminating.
Mai 14 02:04:49 inlane systemd[1]: Stopping OpenBSD Secure Shell server...
Mai 14 02:04:49 inlane systemd[1]: Stopped OpenBSD Secure Shell server.
-- Reboot --
```

* * * * *

### Kill a Process
--------------

A process can be in the following states:

-   Running
-   Waiting (waiting for an event or system resource)
-   Stopped
-   Zombie (stopped but still has an entry in the process table).

Processes can be controlled using `kill`, `pkill`, `pgrep`, and `killall`. To interact with a process, we must send a signal to it. We can view all signals with the following command:

	kill -l

```text
 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
63) SIGRTMAX-1  64) SIGRTMAX
```

The most commonly used are:

| Signal | Description |
| --- | --- |
| `1` | `SIGHUP` - This is sent to a process when the terminal that controls it is closed. |
| `2` | `SIGINT` - Sent when a user presses `[Ctrl] + C` in the controlling terminal to interrupt a process. |
| `3` | `SIGQUIT` - Sent when a user presses `[Ctrl] + D` to quit. |
| `9` | `SIGKILL` - Immediately kill a process with no clean-up operations. |
| `15` | `SIGTERM` - Program termination. |
| `19` | `SIGSTOP` - Stop the program. It cannot be handled anymore. |
| `20` | `SIGTSTP` - Sent when a user presses `[Ctrl] + Z` to request for a service to suspend. The user can handle it afterward. |

For example, if a program were to freeze, we could force to kill it with the following command:

	kill 9 <PID> 

### Background a Process
--------------------

Sometimes it will be necessary to put the scan or process we just started in the background to continue using the current session to interact with the system or start other processes. As we have already seen, we can do this with the shortcut `[Ctrl + Z]`. As mentioned above, we send the `SIGTSTP` signal to the kernel, which suspends the process.

	ping -c 10 www.hackthebox.eu
	vim tmpfile
	[Ctrl + Z]

```text
[2]+  Stopped                 vim tmpfile
```

Now all background processes can be displayed with the following command.

	jobs

```text
[1]+  Stopped                 ping -c 10 www.hackthebox.eu
[2]+  Stopped                 vim tmpfile
```

The `[Ctrl] + Z` shortcut suspends the processes, and they will not be executed further. To keep it running in the background, we have to enter the command `bg` to put the process in the background.

	bg

```text
--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 113482ms

[ENTER]
[1]+  Exit 1                  ping -c 10 www.hackthebox.eu
```

Another option is to automatically set the process with an AND sign (`&`) at the end of the command.

	ping -c 10 www.hackthebox.eu &

```text
[1] 10825
PING www.hackthebox.eu (172.67.1.1) 56(84) bytes of data.
```

Once the process finishes, we will see the results.

```text
--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 9210ms

[ENTER]
[1]+  Exit 1                  ping -c 10 www.hackthebox.eu
```

* * * * *

### Foreground a Process
--------------------

After that, we can use the `jobs` command to list all background processes. Backgrounded processes do not require user interaction, and we can use the same shell session without waiting until the process finishes first. Once the scan or process finishes its work, we will get notified by the terminal that the process is finished.

	jobs

```text
[1]+  Running                 ping -c 10 www.hackthebox.eu &
```

If we want to get the background process into the foreground and interact with it again, we can use the `fg <ID>` command.

	fg 1
	ping -c 10 www.hackthebox.eu

```text
--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 9206ms
```

### Execute Multiple Commands
-------------------------

There are three possibilities to run several commands, one after the other. These are separated by:

-   Semicolon (`;`)
-   Double `ampersand` characters (`&&`)
-   Pipes (`|`)

The difference between them lies in the previous processes' treatment and depends on whether the previous process was completed successfully or with errors. The semicolon (`;`) is a command separator and executes the commands by ignoring previous commands' results and errors.

	echo '1'; echo '2'; echo '3'

```text
1
2
3
```

For example, if we execute the same command but replace it in second place, the command `ls` with a file that does not exist, we get an error, and the third command will be executed nevertheless.

	echo '1'; ls MISSING_FILE; echo '3'

```text
1
ls: cannot access 'MISSING_FILE': No such file or directory
3
```

However, it looks different if we use the double AND characters (`&&`) to run the commands one after the other. If there is an error in one of the commands, the following ones will not be executed anymore, and the whole process will be stopped.

	echo '1' && ls MISSING_FILE && echo '3'

```text
1
ls: cannot access 'MISSING_FILE': No such file or directory
```

Pipes (`|`) depend not only on the correct and error-free operation of the previous processes but also on the previous processes' results. We will deal with the pipes later in the `File Descriptors and Redirections` section.

#### Questions

>Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer.

## Working with Web Services

* * * * *

Another essential component is the communication with the web servers. There are many different ways to set up web servers on Linux operating systems. One of the most used and widespread web servers, besides IIS and Nginx, is Apache. For an Apache web server, we can use appropriate modules, which can encrypt the communication between browser and web server (mod_ssl), use as a proxy server (mod_proxy), or perform complex manipulations of HTTP header data (mod_headers) and URLs (mod_rewrite).

Apache offers the possibility to create web pages dynamically using server-side scripting languages. Commonly used scripting languages are PHP, Perl, or Ruby. Other languages are Python, JavaScript, Lua, and .NET, which can be used for this. We can install the Apache webserver with the following command.

	apt install apache2 -y

```text
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  apache2-doc apache2-suexec-pristine | apache2-suexec-custom
The following NEW packages will be installed:
  apache2
0 upgraded, 1 newly installed, 0 to remove and 17 not upgraded.
Need to get 95,1 kB of archives.
After this operation, 535 kB of additional disk space will be used.
Get:1 http://de.archive.ubuntu.com/ubuntu bionic-updates/main amd64 apache2 amd64 2.4.29-1ubuntu4.13 [95,1 kB]
Fetched 95,1 kB in 0s (270 kB/s)   
<SNIP>
```

After we have started it, we can navigate using our browser to the default page (http://localhost).

![[apache-default.png]]

This is the default page after installation and serves to confirm that the webserver is working correctly.

* * * * *

### CURL
----

`cURL` is a tool that allows us to transfer files from the shell over protocols like `HTTP`, `HTTPS`, `FTP`, `SFTP`, `FTPS`, or `SCP`. This tool gives us the possibility to control and test websites remotely. Besides the remote servers' content, we can also view individual requests to look at the client's and server's communication. Usually, `cURL` is already installed on most Linux systems. This is another critical reason to familiarize ourselves with this tool, as it can make some processes much easier later on.

	curl http://localhost

```text
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <!--
    Modified from the Debian original for Ubuntu
    Last updated: 2016-11-16
    See: https://launchpad.net/bugs/1288690
  -->
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Apache2 Ubuntu Default Page: It works</title>
    <style type="text/css" media="screen">
...SNIP...
```

In the title tag, we can see that it is the same text as from our browser. This allows us to inspect the source code of the website and get information from it. Nevertheless, we will come back to this in another module.

* * * * *

### Wget
----

An alternative to curl is the tool `wget`. With this tool, we can download files from FTP or HTTP servers directly from the terminal and serves as a good download manager. If we use wget in the same way, the difference to curl is that the website content is downloaded and stored locally, as shown in the following example.

	wget http://localhost

```text
--2020-05-15 17:43:52--  http://localhost/
Resolving localhost (localhost)... 127.0.0.1
Connecting to localhost (localhost)|127.0.0.1|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10918 (11K) [text/html]
Saving to: 'index.html'

index.html                 100%[=======================================>]  10,66K  --.-KB/s    in 0s      

2020-05-15 17:43:52 (33,0 MB/s) - ‘index.html’ saved [10918/10918]
```

* * * * *

### Python 3
--------

Another option that is often used when it comes to data transfer is the use of Python 3. In this case, the web server's root directory is where the command is executed to start the server. For this example, we are in a directory where WordPress is installed and contains a "readme.html." Now, let us start the Python 3 web server and see if we can access it using the browser.

	python3 -m http.server

```text
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

![[python3-browser.png]]

We can see what requests were made if we now look at our Python 3 web server's events.

	python3 -m http.server

```text
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
127.0.0.1 - - [15/May/2020 17:56:29] "GET /readme.html HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/css/install.css?ver=20100228 HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/images/wordpress-logo.png HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/images/wordpress-logo.svg?ver=20131107 HTTP/1.1" 200 -
```

#### Questions

>Find a way to start a simple HTTP server inside Pwnbox or your local VM using "npm". Submit the command that starts the web server on port 8080 (use the short argument to specify the port number).
>
>`http-server -p 8080`

>Find a way to start a simple HTTP server inside Pwnbox or your local VM using "php". Submit the command that starts the web server on the localhost (127.0.0.1) on port 8080.
>
>`php -S 127.0.0.1:8080`

# Workflow

## Navigation

* * * * *

One of the best ways to learn something new is to experiment with it. Here we cover the sections on how to navigate through Linux, create, move, edit and delete files and folders, find them on the operating system, different types of redirects, and what file descriptors are. Then we will find some shortcuts that will make our work with the shell easier. It is recommended to experiment on our locally hosted VM. Make sure we have created a snapshot for our VM in case our system gets unexpectedly damaged.

Let us start with the navigation. Before we move through the system, we have to find out in which directory we are. We can find out where we are with the command `pwd`.

	pwd

```text
/home/cry0l1t3
```

Only the `ls` command is needed for navigation. It has many additional options that can complement the display of the content in the current folder.

	ls

```text
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```

	ls -l

```text
total 32
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:37 Desktop
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Documents
drwxr-xr-x 3 cry0l1t3 cry0l1t3 4096 Nov 15 03:26 Downloads
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Music
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Pictures
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Public
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Templates
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Videos
```

However, we will not see everything that is in this folder. To list the contents of a directory, we do not necessarily need to navigate there first. We can also use "`ls`" to specify the path where we want to know the contents.

	ls -l /var/

```text
total 52
drwxr-xr-x  2 root root     4096 Mai 15 18:54 backups
drwxr-xr-x 18 root root     4096 Nov 15 16:55 cache
drwxrwsrwt  2 root whoopsie 4096 Jul 25  2018 crash
drwxr-xr-x 66 root root     4096 Mai 15 03:08 lib
drwxrwsr-x  2 root staff    4096 Nov 24  2018 local 
<SNIP>
```

We can do the same thing if we want to navigate to the directory. To move through the directories, we use the command `cd`. Let us change to the `/dev/shm` directory. Of course, we can go to the `/dev` directory first and then `/shm`. Nevertheless, we can also directly enter the full path and jump directly there.

	cd /dev/shm

```text
cry0l1t3@htb[/dev/shm]$
```

Since we were in the home directory before, we can quickly jump back to the directory we were last in.

	cd -

```text
cry0l1t3@htb[/dev/shm]$
```

Since we were in the home directory before, we can quickly jump back to the directory we were last in.

	cd -

```text
cry0l1t3@htb[~]$ 
```

The shell also offers us the auto-complete function, which makes navigation easier. If we now type `cd /dev/s` and then press `[TAB] twice`, we will get all entries starting with the letter "`s`" in the directory of `/dev/`.

	cd /dev/s [TAB 2x]

```text
shm/ snd/
```

If we add the letter "`h`" to the letter "`s`," the shell will complete the input since otherwise there will be no folders in this directory beginning with the letters "`sh`". If we now display all contents of the directory, we will only see the following contents.

	ls -la

```text
total 0
drwxrwxrwt  2 root root   40 Mai 15 18:31 .
drwxr-xr-x 17 root root 4000 Mai 14 20:45 ..
```

The first entry with a single dot (`.`) indicates the current directory we are currently in. The second entry with two dots (`..`) represents the parent directory `/dev`. This means that we can jump to the parent directory with the following command.

	cd ..

```text
cry0l1t3@htb[/dev]$
```

Since our shell is filled with some records, we can clean the shell with the command `clear`. However, let us return to the directory `/dev/shm` before.

	cd shm && clear

#### Questions

>What is the name of the hidden "history" file in the htb-user's home directory?
>
>`.bash_history`

>What is the index number of the "sudoers" file in the "/etc" directory?

## Working with Files and Directories

* * * * *

### Create, Move, and Copy
----------------------

Next, let us work with files and directories and learn how to create, rename, move, copy, and delete. First, let us create an empty file and a directory. We can use `touch` to create an empty file and `mkdir` to create a directory.

The syntax for this is the following:

#### Syntax - touch

	touch <name>

#### Syntax - mkdir

	mkdir <name>

In this example, we name the file `info.txt` and the directory `Storage`. To create these, we follow the commands and their syntax shown above.

#### Create an Empty File

	touch info.txt

#### Create a Directory

	mkdir Storage

We may want to have specific directories in the directory, and it would be very time-consuming to create this command for every single directory. The command `mkdir` has an option marked `-p` to add parent directories.

	mkdir -p Storage/local/user/documents

We can look at the whole structure after creating the parent directories with the tool `tree`.

	tree .

```text
.
├── info.txt
└── Storage
    └── local
        └── user
            └── documents

4 directories, 1 file
```

We can also create files directly in the directories by specifying the path where the file should be stored. The trick is to use the single dot (`.`) to tell the system that we want to start from the current directory. So the command for creating another empty file looks like this:

#### Create userinfo.txt

	touch ./Storage/local/user/userinfo.txt
	tree .

```text
.
├── info.txt
└── Storage
    └── local
        └── user
            ├── documents
            └── userinfo.txt

4 directories, 2 files
```

With the command `mv`, we can move and also rename files and directories. The syntax for this looks like this:

#### Syntax - mv

	mv <file/directory> <renamed file/directory>

First, let us rename the file `info.txt` to `information.txt` and then move it to the directory `Storage`.

#### Rename File

	mv info.txt information.txt

Now let us create a file named `readme.txt` in the current directory and then copy the files `information.txt` and `readme.txt` into the `Storage/` directory.

#### Create readme.txt

	touch readme.txt 

#### Move Files to Specific Directory

	mv information.txt readme.txt Storage/

	tree .

```text
.
└── Storage
    ├── information.txt
    ├── local
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt

4 directories, 3 files
```

Let us assume we want to have the `readme.txt` in the `local/` directory. Then we can copy them there with the paths specified.

#### Copy readme.txt

	cp Storage/readme.txt Storage/local/

Now we can check if the file is thereby using the tool `tree` again.

	tree .

```text
.
└── Storage
    ├── information.txt
    ├── local
    │   ├── readme.txt
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt

4 directories, 4 files
```

##### Optional Exercise:

>Use the tools we already know to find out how to delete files and directories.

#### Questions

>What is the name of the last modified file in the "/var/backups" directory?

>What is the inode number of the "shadow.bak" file in the "/var/backups" directory?

## Editing Files
-------------

* * * * *

There are several ways to edit a file. One of the most common text editors for this is `Vi` and `Vim`. More rarely, there is the `Nano` editor. We will first deal with the Nano editor here, as it is a bit easier to understand. We can create a new file directly with the Nano editor by specifying the file's name directly as the first parameter. In this case, we create a new file named `notes.txt`.

	nano notes.txt

Now we should see a so-called "`pager`" open, and we can freely enter or insert any text. Our shell should then look something like this.

#### Nano Editor

```text
  GNU nano 2.9.3                                    notes.txt                                              

Here we can type everything we want and make our notes.▓


^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify     ^C Cur Pos     M-U Undo
^X Exit        ^R Read File   ^\ Replace     ^U Uncut Text  ^T To Spell    ^_ Go To Line  M-E Redo
```

Below we see two lines with short descriptions. The `caret` (`^`) stands for our "`[CTRL]`" key. For example, if we press `[CTRL + W]`, a "`Search:`" line appears at the bottom of the editor, where we can enter the word or words we are looking for. If we now search for the word "`we`" and press `[ENTER]`, the cursor will move to the first word that matches.

```text
GNU nano 2.9.3                                    notes.txt                                              

Here ▓we can type everything we want and make our notes.

Search:   notes                                                                                            
^G Get Help    M-C Case Sens  M-B Backwards  M-J FullJstify ^W Beg of Par  ^Y First Line  ^P PrevHstory
^C Cancel      M-R Regexp     ^R Replace     ^T Go To Line  ^O End of Par  ^V Last Line   ^N NextHstory
```

To jump to the next match with the cursor, we press `[CTRL + W]` again and confirm with `[ENTER]` without any additional information.

```text
GNU nano 2.9.3                                    notes.txt                                              

Here we can type everything ▓we want and make our notes.

Search [we]:                                                                                               
^G Get Help    M-C Case Sens  M-B Backwards  M-J FullJstify ^W Beg of Par  ^Y First Line  ^P PrevHstory
^C Cancel      M-R Regexp     ^R Replace     ^T Go To Line  ^O End of Par  ^V Last Line   ^N NextHstory
```

Now we can save the file by pressing `[CTRL + O]` and confirm the file name with `[ENTER]`.

```text
GNU nano 2.9.3                                    notes.txt                                              

Here we can type everything we want and make our notes.

File Name to Write: notes.txt▓                                                                           
^G Get Help    M-C Case Sens  M-B Backwards  M-J FullJstify ^W Beg of Par  ^Y First Line  ^P PrevHstory
^C Cancel      M-R Regexp     ^R Replace     ^T Go To Line  ^O End of Par  ^V Last Line   ^N NextHstory
```

After we have saved the file, we can leave the editor with `[CTRL + X]`.

#### Back on the Shell

To view the contents of the file, we can use the command `cat`.

	cat notes.txt

```text
Here we can type everything we want and make our notes.
```

There are many files on Linux systems that can play an essential role for us as penetration testers whose rights have not been correctly set by the administrators. Such files may include the file "`/etc/passwd`".

* * * * *

### VIM
---

`Vim` is an open-source editor for all kinds of ASCII text, just like Nano. It is an improved clone of the previous Vi. It is an extremely powerful editor that focuses on the essentials, namely editing text. For tasks that go beyond that, Vim provides an interface to external programs, such as `grep`, `awk`, `sed`, etc., which can handle their specific tasks much better than a corresponding function directly implemented in an editor usually can. This makes the editor small and compact, fast, powerful, flexible, and less error-prone.

Vim follows the Unix principle here: many small specialized programs that are well tested and proven, when combined and communicating with each other, resulting in a flexible and powerful system.

#### Vim

	vim

```text
  1 $
~
~                              VIM - Vi IMproved                                
~                                                                               
~                               version 8.0.1453                                
~                           by Bram Moolenaar et al.                            
~           Modified by pkg-vim-maintainers@lists.alioth.debian.org             
~                 Vim is open source and freely distributable                   
~                                                                               
~                           Sponsor Vim development!                            
~                type  :help sponsor<Enter>    for information                  
~                                                                               
~                type  :q<Enter>               to exit                          
~                type  :help<Enter>  or  <F1>  for on-line help                 
~                type  :help version8<Enter>   for version info                 
~                                                                               
                                                                         
                                                                    0,0-1         All
```

In contrast to Nano, `Vim` is a modal editor that can distinguish between text and command input. Vim offers a total of six fundamental modes that make our work easier and make this editor so powerful:

| Mode | Description |
| --- | --- |
| `Normal` | In normal mode, all inputs are considered as editor commands. So there is no insertion of the entered characters into the editor buffer, as is the case with most other editors. After starting the editor, we are usually in the normal mode. |
| `Insert` | With a few exceptions, all entered characters are inserted into the buffer. |
| `Visual` | The visual mode is used to mark a contiguous part of the text, which will be visually highlighted. By positioning the cursor, we change the selected area. The highlighted area can then be edited in various ways, such as deleting, copying, or replacing it. |
| `Command` | It allows us to enter single-line commands at the bottom of the editor. This can be used for sorting, replacing text sections, or deleting them, for example. |
| `Replace` | In replace mode, the newly entered text will overwrite existing text characters unless there are no more old characters at the current cursor position. Then the newly entered text will be added. |

When we have the Vim editor open, we can go into command mode by typing "`:`" and then typing "`q`" to close Vim.

```text
  1 $
~
~                              VIM - Vi IMproved                                
~                                                                               
~                               version 8.0.1453                                
~                           by Bram Moolenaar et al.                            
~           Modified by pkg-vim-maintainers@lists.alioth.debian.org             
~                 Vim is open source and freely distributable                   
~                                                                               
~                           Sponsor Vim development!                            
~                type  :help sponsor<Enter>    for information                  
~                                                                               
~                type  :q<Enter>               to exit                          
~                type  :help<Enter>  or  <F1>  for on-line help                 
~                type  :help version8<Enter>   for version info                 
~                                                                               
:q▓
```

Vim offers an excellent opportunity called `vimtutor` to practice and get familiar with the editor. It may seem very difficult and complicated at first, but it will only feel that way for a short time. The efficiency we gain from Vim once we get used to it is enormous.

#### VimTutor

	vimtutor

```text
===============================================================================
=    W e l c o m e   t o   t h e   V I M   T u t o r    -    Version 1.7      =
===============================================================================

     Vim is a very powerful editor that has many commands, too many to
     explain in a tutor such as this.  This tutor is designed to describe
     enough of the commands that you will be able to easily use Vim as
     an all-purpose editor.

     The approximate time required to complete the tutor is 25-30 minutes,
     depending upon how much time is spent with experimentation.

     ATTENTION:
     The commands in the lessons will modify the text.  Make a copy of this
     file to practice on (if you started "vimtutor" this is already a copy).

     It is important to remember that this tutor is set up to teach by
     use.  That means that you need to execute the commands to learn them
     properly.  If you only read the text, you will forget the commands!

     Now, make sure that your Caps-Lock key is NOT depressed and press
     the   j   key enough times to move the cursor so that lesson 1.1
     completely fills the screen.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

##### Optional Exercise:

>Play with the vimtutor. Get familiar with the editor and experiment with their features.

## Find Files and Directories

* * * * *

### Importance of the Search
------------------------

It is crucial to be able to find the files and folders we need. Once we have gained access to a Linux based system, it will be essential to find configuration files, scripts created by users or the administrator, and other files and folders. We do not have to manually browse through every single folder and check when modified for the last time. There are some tools we can use to make this work easier.

* * * * *

### Which
-----

One of the common tools is `which`. This tool returns the path to the file or link that should be executed. This allows us to determine if specific programs, like cURL, netcat, wget, python, gcc, are available on the operating system. Let us use it to search for Python in our interactive instance.

	which python

```text
/usr/bin/python
```

If the program we search for does not exist, no results will be displayed.

* * * * *

### Find
----

Another handy tool is `find`. Besides the function to find files and folders, this tool also contains the function to filter the results. We can use filter parameters like the size of the file or the date. We can also specify if we only search for files or folders.

#### Syntax - find

	find <location> <options>

Let us look at an example of what such a command with multiple options would look like.

	find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

```text
-rw-r--r-- 1 root root 136392 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/auto.conf
-rw-r--r-- 1 root root 82290 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/tristate.conf
-rw-r--r-- 1 root root 95813 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats32.conf
-rw-r--r-- 1 root root 60346 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dynamic.conf
-rw-r--r-- 1 root root 96249 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb32.conf
-rw-r--r-- 1 root root 54755 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats16.conf
-rw-r--r-- 1 root root 22635 May  7 14:33 /usr/share/metasploit-framework/data/jtr/korelogic.conf
-rwxr-xr-x 1 root root 108534 May  7 14:33 /usr/share/metasploit-framework/data/jtr/john.conf
-rw-r--r-- 1 root root 55285 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb16.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /usr/share/doc/sqlmap/examples/sqlmap.conf
-rw-r--r-- 1 root root 25086 Mar  4 22:04 /etc/dnsmasq.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /etc/sqlmap/sqlmap.conf
```

Now let us take a closer look at the options we used in the previous command. If we hover the mouse over the respective options, a small window will appear with an explanation. These explanations will also be found in other modules, which should help us if we are not yet familiar with one of the tools.

| Option | Description |
| --- | --- |
| `-type f` | Hereby, we define the type of the searched object. In this case, '`f`' stands for '`file`'. |
| `-name *.conf` | With '`-name`', we indicate the name of the file we are looking for. The asterisk (`*`) stands for 'all' files with the '`.conf`' extension. |
| `-user root` | This option filters all files whose owner is the root user. |
| `-size +20k` | We can then filter all the located files and specify that we only want to see the files that are larger than 20 KiB. |
| `-newermt 2020-03-03` | With this option, we set the date. Only files newer than the specified date will be presented. |
| `-exec ls -al {} \;` | This option executes the specified command, using the curly brackets as placeholders for each result. The backslash escapes the next character from being interpreted by the shell because otherwise, the semicolon would terminate the command and not reach the redirection. |
| `2>/dev/null` | This is a `STDERR` redirection to the '`null device`', which we will come back to in the next section. This redirection ensures that no errors are displayed in the terminal. This redirection must `not` be an option of the 'find' command. |

* * * * *

### Locate
------

It will take much time to search through the whole system for our files and directories to perform many different searches. The command `locate` offers us a quicker way to search through the system. In contrast to the `find` command, `locate` works with a local database that contains all information about existing files and folders. We can update this database with the following command.

	sudo updatedb

If we now search for all files with the "`.conf`" extension, you will find that this search produces results much faster than using `find`.

	locate *.conf

```text
/etc/GeoIP.conf
/etc/NetworkManager/NetworkManager.conf
/etc/UPower/UPower.conf
/etc/adduser.conf
<SNIP>
```

However, this tool does not have as many filter options that we can use. So it is always worth considering whether we can use the `locate` command or instead use the `find` command. It always depends on what we are looking for.

##### Optional Exercise:

>Try the different utilities and find everything related to the **netcat** / **nc** tool.

#### Questions

>What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?

>How many files exist on the system that have the ".bak" extension?

>Submit the full path of the "xxd" binary.
>
>`/usr/bin/xxd`

## File Descriptors and Redirections

* * * * *

### File Descriptors
----------------

A file descriptor (FD) in Unix/Linux operating systems is an indicator of connection maintained by the kernel to perform Input/Output (I/O) operations. In Windows-based operating systems, it is called filehandle. It is the connection (generally to a file) from the Operating system to perform I/O operations (Input/Output of Bytes). By default, the first three file descriptors in Linux are:

1.  Data Stream for Input
    -   `STDIN -- 0`
2.  Data Stream for Output
    -   `STDOUT -- 1`
3.  Data Stream for Output that relates to an error occurring.
    -   `STDERR -- 2`

* * * * *

#### STDIN and STDOUT

Let us see an example with `cat`. When running `cat`, we give the running program our standard input (`STDIN - FD 0`), marked `green`, wherein this case "SOME INPUT" is. As soon as we have confirmed our input with `[ENTER]`, it is returned to the terminal as standard output (`STDOUT - FD 1`), marked red.

![[find0.png]]

* * * * *

#### STDOUT and STDERR

In the next example, by using the `find` command, we will see the standard output (`STDOUT - FD 1`) marked in `green` and standard error (`STDERR - FD 2`) marked in red.

![[find1.png]]

* * * * *

In this case, the error is marked and displayed with "`Permission denied`". We can check this by redirecting the file descriptor for the errors (`FD 2 - STDERR`) to "`/dev/null`." This way, we redirect the resulting errors to the "null device," which discards all data.

	find /etc/ -name shadow 2>/dev/null

![[find2.png]]

* * * * *

#### Redirect STDOUT to a File

Now we can see that all errors (`STDERR`) previously presented with "`Permission denied`" are no longer displayed. The only result we see now is the standard output (`STDOUT`), which we can also redirect to a file with the name `results.txt` that will only contain standard output without the standard errors.

	find /etc/ -name shadow 2>/dev/null > results.txt

![[find3.png]]

* * * * *

#### Redirect STDOUT and STDERR to Separate Files

We should have noticed that we did not use a number before the greater-than sign (`>`) in the last example. That is because we redirected all the standard errors to the "`null device`" before, and the only output we get is the standard output (`FD 1 - STDOUT`). To make this more precise, we will redirect standard error (`FD 2 - STDERR`) and standard output (`FD 1 - STDOUT`) to different files.

	find /etc/ -name shadow 2> stderr.txt 1> stdout.txt

![[find4.png]]

* * * * *

#### Redirect STDIN

As we have already seen, in combination with the file descriptors, we can redirect errors and output with greater-than character (`>`). This also works with the lower-than sign (`<`). However, the lower-than sign serves as standard input (`FD 0 - STDIN`). These characters can be seen as "`direction`" in the form of an arrow that tells us "`from where`" and "`where to`" the data should be redirected. We use the `cat` command to use the contents of the file "`stdout.txt`" as `STDIN`.

	cat < stdout.txt

![[find5.png]]

* * * * *

#### Redirect STDOUT and Append to a File

When we use the greater-than sign (`>`) to redirect our `STDOUT`, a new file is automatically created if it does not already exist. If this file exists, it will be overwritten without asking for confirmation. If we want to append `STDOUT` to our existing file, we can use the double greater-than sign (`>>`).

	find /etc/ -name passwd >> stdout.txt 2>/dev/null

![[find9.png]]

#### Redirect STDIN Stream to a File

We can also use the double lower-than characters (`<<`) to add our standard input through a stream. We can use the so-called `End-Of-File` (`EOF`) function of a Linux system file, which defines the input's end. In the next example, we will use the `cat` command to read our streaming input through the stream and direct it to a file called "`stream.txt`."

	cat << EOF > stream.txt

![[find6.png]]

* * * * *

#### Pipes

Another way to redirect `STDOUT` is to use pipes (`|`). These are useful when we want to use the `STDOUT` from one program to be processed by another. One of the most commonly used tools is `grep`, which we will use in the next example. Grep is used to filter `STDOUT` according to the pattern we define. In the next example, we use the `find` command to search for all files in the "`/etc/`" directory with a "`.conf`" extension. Any errors are redirected to the "`null device`" (`/dev/null`). Using `grep`, we filter out the results and specify that only the lines containing the pattern "`systemd`" should be displayed.

	find /etc/ -name *.conf 2>/dev/null | grep systemd

![[find7.png]]

The redirections work, not only once. We can use the obtained results to redirect them to another program. For the next example, we will use the tool called `wc`, which should count the total number of obtained results.

	find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l

![[find8.png]]

#### Questions

>How many files exist on the system that have the ".log" file extension?

>How many total packages are installed on the target system?

## Filter Contents

* * * * *

In the last section, we learned about the redirections we can use to redirect results from one program to another for processing. To read files, we do not necessarily have to use an editor for that. There are two tools called `more` and `less`, which are very identical. These are fundamental `pagers` that allow us to scroll through the file in an interactive view. Let us have a look at some examples.

* * * * *

### More
----

	more /etc/passwd

After we read the content using `cat` and redirected it to `more`, the already mentioned `pager` opens, and we will automatically start at the beginning of the file.

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
<SNIP>
--More--
```

With the `[Q]` key, we can leave this `pager`. We will notice that the output remains in the terminal.

* * * * *

### Less
----

If we now take a look at the tool `less`, we will notice on the man page that it contains many more features than `more`.

	less /etc/passwd

The presentation is almost the same as with `more`.

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
<SNIP>
:
```

When closing `less` with the `[Q]` key, we will notice that the output we have seen, unlike `more`, does not remain in the terminal.

* * * * *

### Head
----

Sometimes we will only be interested in specific issues either at the beginning of the file or the end. If we only want to get the `first` lines of the file, we can use the tool `head`. By default, `head` prints the first ten lines of the given file or input, if not specified otherwise.

	head /etc/passwd

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
```

* * * * *

### Tail
----

If we only want to see the last parts of a file or results, we can use the counterpart of `head` called `tail`, which returns the `last` ten lines.

	tail /etc/passwd

```text
miredo:x:115:65534::/var/run/miredo:/usr/sbin/nologin
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
rtkit:x:117:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
nm-openvpn:x:118:120:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
nm-openconnect:x:119:121:NetworkManager OpenConnect plugin,,,:/var/lib/NetworkManager:/usr/sbin/nologin
pulse:x:120:122:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
beef-xss:x:121:124::/var/lib/beef-xss:/usr/sbin/nologin
lightdm:x:122:125:Light Display Manager:/var/lib/lightdm:/bin/false
do-agent:x:998:998::/home/do-agent:/bin/false
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

* * * * *

### Sort
----

Depending on which results and files are dealt with, they are rarely sorted. Often it is necessary to sort the desired results alphabetically or numerically to get a better overview. For this, we can use a tool called `sort`.

	cat /etc/passwd | sort

```text
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
dovecot:x:114:117:Dovecot mail server,,,:/usr/lib/dovecot:/usr/sbin/nologin
dovenull:x:115:118:Dovecot login user,,,:/nonexistent:/usr/sbin/nologin
ftp:x:113:65534::/srv/ftp:/usr/sbin/nologin
games:x:5:60:games:/usr/games:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
htb-student:x:1002:1002::/home/htb-student:/bin/bash
<SNIP>
```

As we can see now, the output no longer starts with root but is now sorted alphabetically.

* * * * *

### Grep
----

More often, we will only search for specific results that contain patterns we have defined. One of the most used tools for this is `grep`, which offers many different features. Accordingly, we can search for users who have the default shell "`/bin/bash`" set as an example.

	cat /etc/passwd | grep "/bin/bash"

```text
root:x:0:0:root:/root:/bin/bash
mrb3n:x:1000:1000:mrb3n:/home/mrb3n:/bin/bash
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
htb-student:x:1002:1002::/home/htb-student:/bin/bash
```

Another possibility is to exclude specific results. For this, the option "`-v`" is used with `grep`. In the next example, we exclude all users who have disabled the standard shell with the name "`/bin/false`" or "`/usr/bin/nologin`".

	cat /etc/passwd | grep -v "false\|nologin"

```text
root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
postgres:x:111:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

* * * * *

### Cut
---

Specific results with different characters may be separated as delimiters. Here it is handy to know how to remove specific delimiters and show the words on a line in a specified position. One of the tools that can be used for this is `cut`. Therefore we use the option "`-d`" and set the delimiter to the colon character (`:`) and define with the option "`-f`" the position in the line we want to output.

	cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1

```text
root
sync
mrb3n
cry0l1t3
htb-student
```

* * * * *

### Tr
--

Another possibility to replace certain characters from a line with characters defined by us is the tool `tr`. As the first option, we define which character we want to replace, and as a second option, we define the character we want to replace it with. In the next example, we replace the colon character with space.

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " "

```text
root x 0 0 root /root /bin/bash
sync x 4 65534 sync /bin /bin/sync
mrb3n x 1000 1000 mrb3n /home/mrb3n /bin/bash
cry0l1t3 x 1001 1001  /home/cry0l1t3 /bin/bash
htb-student x 1002 1002  /home/htb-student /bin/bash
```

* * * * *

### Column
------

Since such results can often have an unclear representation, the tool `column` is well suited to display such results in tabular form using the "`-t`."

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t

```text
root         x  0     0      root               /root        /bin/bash
sync         x  4     65534  sync               /bin         /bin/sync
mrb3n        x  1000  1000   mrb3n              /home/mrb3n  /bin/bash
cry0l1t3     x  1001  1001   /home/cry0l1t3     /bin/bash
htb-student  x  1002  1002   /home/htb-student  /bin/bash
```

* * * * *

### Awk
---

As we may have noticed, the user "`postgres`" has one row too many. To keep it as simple as possible to sort out such results, the (`g`)`awk` programming is beneficial, which allows us to display the first (`$1`) and last (`$NF`) result of the line.

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

```text
root /bin/bash
sync /bin/sync
mrb3n /bin/bash
cry0l1t3 /bin/bash
htb-student /bin/bash
```

* * * * *

### Sed
---

There will come moments when we want to change specific names in the whole file or standard input. One of the tools we can use for this is the stream editor called `sed`. One of the most common uses of this is substituting text. Here, `sed` looks for patterns we have defined in the form of regular expressions (regex) and replaces them with another pattern that we have also defined. Let us stick to the last results and say we want to replace the word "`bin`" with "`HTB`."

The "`s`" flag at the beginning stands for the substitute command. Then we specify the pattern we want to replace. After the slash (`/`), we enter the pattern we want to use as a replacement in the third position. Finally, we use the "`g`" flag, which stands for replacing all matches.

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'

```text
root /HTB/bash
sync /HTB/sync
mrb3n /HTB/bash
cry0l1t3 /HTB/bash
htb-student /HTB/bash
```

* * * * *

### Wc
--

Last but not least, it will often be useful to know how many successful matches we have. To avoid counting the lines or characters manually, we can use the tool `wc`. With the "`-l`" option, we specify that only the lines are counted.

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l

```text
5
```

* * * * *

### Practice
--------

It may be a bit overwhelming at first to deal with so many different tools and their functions if we are not familiar with them. Take your time and experiment with the tools. Have a look at the man pages (`man <tool>`) or call the help for it (`<tool> -h` / `<tool> --help`). The best way to become familiar with all the tools is to practice. Try to use them as often as possible, and we will be able to filter many things intuitively after a short time.

#### Questions

>How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)

>Determine what user the ProFTPd server is running under. Submit the username as the answer.

>Use cURL from your Pwnbox (not the target machine) to obtain the source code of the "https://www.inlanefreight.com" website and filter all unique paths of that domain. Submit the number of these paths as the answer.

## Permission Management

* * * * *

### Overview
--------

Under Linux, permissions are assigned to users and groups. Each user can be a member of different groups, and membership in these groups gives the user specific, additional permissions. Each file and directory belongs to a specific user and a specific group. So the permissions for users and groups that defined a file are also defined for the respective owners. When we create new files or directories, they belong to the group we belong to and us. The whole permission system on Linux systems is based on the octal number system, and basically, there are three different types of permissions a file or directory can be assigned:

-   (`r`) - Read
-   (`w`) - Write
-   (`x`) - Execute

The permissions can be set for the `owner`, `group`, and `others` like presented in the next example with their corresponding permissions.

	ls -l /etc/passwd

```text
- rwx rw- r--   1 root root 1641 May  4 23:42 /etc/passwd
- --- --- ---   |  |    |    |   |__________|
|  |   |   |    |  |    |    |        |_ Date
|  |   |   |    |  |    |    |__________ File Size
|  |   |   |    |  |    |_______________ Group
|  |   |   |    |  |____________________ User
|  |   |   |    |_______________________ Number of hard links
|  |   |   |_ Permission of others (read)
|  |   |_____ Permissions of the group (read, write)
|  |_________ Permissions of the owner (read, write, execute)
|____________ File type (- = File, d = Directory, l = Link, ... )
```

* * * * *

### Change Permissions
------------------

We can modify permissions using the `chmod` command, permission group references (`u` - owner, `g` - Group, `o` - others, `a` - All users), and either a [`+`] or a [`-`] to add remove the designated permissions. In the following example, a user creates a new shell script owned by that user, not executable, and set with read/write permissions for all users.

	ls -l shell

```text
-rwxr-x--x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

We can then apply `read` permissions for all users and see the result.

	chmod a+r shell && ls -l shell

```text
-rwxr-xr-x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

We can also set the permissions for all other users to `read` only using the octal value assignment.

	chmod 754 shell && ls -l shell

```text
-rwxr-xr--   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

Let us look at all the representations associated with it to understand better how the permission assignment is calculated.

```text
Binary Notation:                4 2 1  |  4 2 1  |  4 2 1
----------------------------------------------------------
Binary Representation:          1 1 1  |  1 0 1  |  1 0 0
----------------------------------------------------------
Octal Value:                      7    |    5    |    4
----------------------------------------------------------
Permission Representation:      r w x  |  r - x  |  r - -
```

If we sum the set bits from the `Binary Representation` assigned to the values from `Binary Notation` together, we get the `Octal Value`. The `Permission Representation` represents the bits set in the `Binary Representation` by using the three characters, which only recognizes the set permissions easier.

* * * * *

### Change Owner
------------

To change the owner and/or the group assignments of a file or directory, we can use the `chown` command. The syntax is like following:

#### Syntax - chown

	chown <user>:<group> <file/directory>

In this example, "shell" can be replaced with any arbitrary file or folder.

	chown root:root shell && ls -l shell

```text
-rwxr-xr--   1 root root 0 May  4 22:12 shell
```

* * * * *

### SUID & GUID
-----------

Besides assigning direct user and group permissions, we can also configure special permissions for files by setting the `Set User ID` (`SUID`) and `Set Group ID` (`GUID`) bits. These `SUID`/`GUID` bits allow, for example, users to run programs with the rights of another user. Administrators often use this to give their users special rights for certain applications or files. The letter "`s`" is used instead of an "`x`". When executing such a program, the SUID/GUID of the file owner is used.

It is often the case that administrators are not familiar with the applications but still assign the SUID/GUID bits, which leads to a high-security risk. Such programs may contain functions that allow the execution of a shell from the pager, such as the application "`journalctl`."

If the administrator sets the SUID bit to "`journalctl`," any user with access to this application could execute a shell as `root`. More information about this and other such applications can be found at [GTFObins](https://gtfobins.github.io/gtfobins/journalctl/).

# Tips & Tricks

## Shortcuts

* * * * *

There are many shortcuts that we can use to make working with Linux easier and faster. After we have familiarized ourselves with the most important of them and have made them a habit, we will save ourselves much typing. Some of them will even help us to avoid using our mouse in the terminal.

* * * * *

#### Auto-Complete

`[TAB]` - Initiates auto-complete. This will suggest to us different options based on the `STDIN` we provide. These can be specific suggestions like directories in our current working environment, commands starting with the same number of characters we already typed, or options.

* * * * *

#### Cursor Movement

`[CTRL] + A` - Move the cursor to the `beginning` of the current line.

`[CTRL] + E` - Move the cursor to the `end` of the current line.

`[CTRL] + [←]` / `[→]` - Jump at the beginning of the current/previous word.

`[ALT] + B` / `F` - Jump backward/forward one word.

* * * * *

#### Erase The Current Line

`[CTRL] + U` - Erase everything from the current position of the cursor to the `beginning` of the line.

`[Ctrl] + K` - Erase everything from the current position of the cursor to the `end` of the line.

`[Ctrl] + W` - Erase the word preceding the cursor position.

* * * * *

#### Paste Erased Contents

`[Ctrl] + Y` - Pastes the erased text or word.

* * * * *

#### Ends Task

`[CTRL] + C` - Ends the current task/process by sending the `SIGINT` signal. For example, this can be a scan that is running by a tool. If we are watching the scan, we can stop it / kill this process by using this shortcut. While not configured and developed by the tool we are using. The process will be killed without asking us for confirmation.

* * * * *

#### End-of-File (EOF)

`[CTRL] + D` - Close `STDIN` pipe that is also known as End-of-File (EOF) or End-of-Transmission.

* * * * *

#### Clear Terminal

`[CTRL] + L` - Clears the terminal. An alternative to this shortcut is the `clear` command you can type to clear our terminal.

* * * * *

#### Background a Process

`[CTRL] + Z` - Suspend the current process by sending the `SIGTSTP` signal.

* * * * *

#### Search Through Command History

`[CTRL] + R` - Search through command history for commands we typed previously that match our search patterns.

`[↑]` / `[↓]` - Go to the previous/next command in the command history.

* * * * *

#### Switch Between Applications

`[ALT] + [TAB]` - Switch between opened applications.

* * * * *

#### Zoom

`[CTRL] + [+]` - Zoom in.

`[CTRL] + [-]` - Zoom out.

## Linux Security

* * * * *

All computer systems have an inherent risk of intrusion. Some present more of a risk than others, such as an internet-facing web server hosting multiple complex web applications. Linux systems are also less prone to viruses that affect Windows operating systems and do not present as large an attack surface as Active Directory domain-joined hosts. Regardless, it is essential to have certain fundamentals in place to secure any Linux system.

One of the Linux operating systems' most important security measures is keeping the OS and installed packages up to date. This can be achieved with a command such as:

	apt update && apt dist-upgrade

If firewall rules are not appropriately set at the network level, we can use the Linux firewall and/or `iptables` to restrict traffic into/out of the host.

If SSH is open on the server, the configuration should be set up to disallow password login and disallow the root user from logging in via SSH. It is also important to avoid logging into and administering the system as the root user whenever possible and adequately managing access control. Users' access should be determined based on the principle of least privilege. For example, if a user needs to run a command as root, then that command should be specified in the `sudoers` configuration instead of giving them full sudo rights. Another common protection mechanism that can be used is `fail2ban`. This tool counts the number of failed login attempts, and if a user has reached the maximum number, the host that tried to connect will be handled as configured.

It is also important to periodically audit the system to ensure that issues do not exist that could facilitate privilege escalation, such as an out-of-date kernel, user permission issues, world-writable files, and misconfigured cron jobs, or misconfigured services. Many administrators forget about the possibility that some kernel versions have to be updated manually.

An option for further locking down Linux systems is `Security-Enhanced Linux` (`SELinux`) or `AppArmor`. This is a kernel security module that can be used for security access control policies. In SELinux, every process, file, directory, and system object is given a label. Policy rules are created to control access between these labeled processes and objects and are enforced by the kernel. This means that access can be set up to control which users and applications can access which resources. SELinux provides very granular access controls, such as specifying who can append to a file or move it.

Besides, there are different applications and services such as [Snort](https://www.snort.org/), [chkrootkit](http://www.chkrootkit.org/), [rkhunter](https://packages.debian.org/sid/rkhunter), [Lynis](https://cisofy.com/lynis/), and others that can contribute to Linux's security. In addition, some security settings should be made, such as:

-   Removing or disabling all unnecessary services and software
-   Removing all services that rely on unencrypted authentication mechanisms
-   Ensure NTP is enabled and Syslog is running
-   Ensure that each user has its own account
-   Enforce the use of strong passwords
-   Set up password aging and restrict the use of previous passwords
-   Locking user accounts after login failures
-   Disable all unwanted SUID/SGID binaries

This list is incomplete, as safety is not a product but a process. This means that specific steps must always be taken to protect the systems better, and it depends on the administrators how well they know their operating systems. The better the administrators are familiar with the system, and the more they are trained, the better and more secure their security precautions and security measures will be.