---
title: "Linux Fundamentals and Basic Commands"
datePublished: Mon Jul 01 2024 17:22:10 GMT+0000 (Coordinated Universal Time)
cuid: cly38zchj000e09l524e5hvsi
slug: linux-fundamentals-and-basic-commands-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719854475243/ceb98af3-1cda-4e88-b78e-79461847c5aa.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1719854515579/1d3c97f6-5805-4c20-8371-918f939c3915.png
tags: linux, linux-for-beginners, linux-basics, linux-commands, 90daysofdevops, trainwithshubham

---

✨ What is Linux?  
\- Linux is an open-source operating system modeled on UNIX. It's the foundation  
of many cloud infrastructures and has a significant presence in the server world, among other places.

✨ Basic Fundamentals of Linux:  
\- Kernel: It's the core component of the system that interacts with hardware.  
\- Shell: An interface that allows users to interact with the kernel using command lines or scripts.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698089858960/40c58b90-7554-4130-a676-bfc894158307.jpeg align="center")

\- File System: Hierarchical structure where all the data is organized.

\*\*Note: [Comprehensive Insight into the Linux File System](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-the-linux-filesystem-explained)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698089922892/7a3114dc-e908-4ed7-bd57-153e9eacb1b5.jpeg align="center")

\- Processes: Running instances of programs. Linux treats almost everything as a process.

\- User & Groups: Security and permissions are based on users and groups.

✨ The Command Line Interface (CLI)

One of the defining features of Linux is the command line interface or CLI. Unlike graphical user interfaces (GUIs), the CLI requires users to type commands to interact with the system. This might seem intimidating at first, but it offers significant advantages, such as greater control and efficiency.

Common Linux CLI commands:

* `ls`: List files and directories.
    
* `cd`: Change the current directory.
    
* `mkdir`: Create a new directory.
    
* `touch`: Create a new file.
    
* `cp`: Copy files or directories.
    
* `mv`: Move or rename files or directories.
    
* `rm`: Remove files or directories.
    
* `pwd`: Print the current working directory.
    

✨ File System Hierarchy

Linux organizes files and directories in a hierarchical structure. The root directory is denoted by `/`, and all other directories and files branch out from there. Understanding this hierarchy is crucial for navigation and proper file management.

Common directories include:

* `/bin`: Essential system binaries.
    
* `/etc`: Configuration files.
    
* `/home`: User home directories.
    
* `/usr`: User-installed software.
    
* `/var`: Variable data (e.g., logs).
    
* `/tmp`: Temporary files.
    
* `/dev`: Device files.
    

✨ Users and Permissions

Linux is known for its robust user and permission management system. Each user has a unique username and belongs to one or more groups. File permissions are specified using a combination of read (r), write (w), and execute (x) permissions for the owner, group, and others.

The `chmod` command is used to change file permissions, while `chown` is used to change file ownership. Understanding and managing these permissions is crucial for securing your system.

✨ Package Management

Linux distributions come with package management systems that make it easy to install, update, and remove software. For instance, Ubuntu uses `apt`, while CentOS uses `yum`. These tools fetch software from online repositories, ensuring that you always have access to the latest updates and security patches.

To install a package, you typically use a command like:

`sudo apt-get install package_name`

✨ Update and Upgrade

Regular system updates and upgrades are essential to keep your Linux system secure and up-to-date. Use the following commands to perform these tasks:

* `sudo apt-get update`: Update the package lists.
    
* `sudo apt-get upgrade`: Upgrade installed packages.
    

`sudo apt-get dist-upgrade`: Upgrade the distribution.

✨ System Information

You can retrieve important system information using various commands, such as:

* `uname -a`: Display system information.
    
* `df -h`: Show disk usage.
    
* `free -h`: Display memory usage.
    
* `top` or `htop`: Monitor system processes.
    

### Linux Commands You Must Know as a Regular User

1. **ls** - The most frequently used command in Linux to list directories
    
2. **pwd** - Print working directory command in Linux
    
3. **cd** - Linux command to navigate through directories
    
4. **mkdir** - Command used to create directories in Linux
    
5. **mv** - Move or rename files in Linux
    
6. **cp** - Similar usage as mv but for copying files in Linux
    
7. **rm** - Delete files or directories
    
8. **touch** - Create blank/empty files
    
9. **ln** - Create symbolic links (shortcuts) to other files
    
10. **cat** - Display file contents on the terminal
    
11. **clear** - Clear the terminal display
    
12. **echo** - Print any text that follows the command
    
13. **less** - Linux command to display paged outputs in the terminal
    
14. **man** - Access manual pages for all Linux commands
    
15. **uname** - Linux command to get basic information about the OS
    
16. **whoami** - Get the active username
    
17. **tar** - Command to extract and compress files in Linux
    
18. **grep** - Search for a string within an output
    
19. **head** - Return the specified number of lines from the top
    
20. **tail** - Return the specified number of lines from the bottom
    
21. **diff** - Find the difference between two files
    
22. **cmp** - Allows you to check if two files are identical
    
23. **comm** - Combines the functionality of diff and cmp
    
24. **sort** - Linux command to sort the content of a file while outputting
    
25. **export** - Export environment variables in Linux
    
26. **zip** - Zip files in Linux
    
27. **unzip** - Unzip files in Linux
    
28. **ssh** - Secure Shell command in Linux
    
29. **service** - Linux command to start and stop services
    
30. **ps** - Display active processes
    
31. **kill and killall** - Kill active processes by process ID or name
    
32. **df** - Display disk filesystem information
    
33. **mount** - Mount file systems in Linux
    
34. **chmod** - Command to change file permissions
    
35. **chown** - Command for granting ownership of files or folders
    
36. **ipconfig** - Display network interfaces and IP addresses
    
37. **traceroute** - Trace all the network hops to reach the destination
    
38. **wget** - Direct download files from the internet
    
39. **ufw** - Firewall command
    
40. **iptables** - Base firewall for all other firewall utilities to interface with
    
41. **apt, pacman, yum, rpm** - Package managers depending on the distro
    
42. **sudo** - Command to escalate privileges in Linux
    
43. **cal** - View a command-line calendar
    
44. **alias -** Create custom shortcuts for your regularly used commands
    
45. **dd** - Majorly used for creating bootable USB sticks
    
46. **whereis** - Locate the binary, source, and manual pages for a command
    
47. **whatis** - Find what a command is used for
    
48. **top** - View active processes live with their system usage
    
49. **useradd and usermod** - Add new user or change existing users data
    
50. **passwd** - Create or update passwords for existing users