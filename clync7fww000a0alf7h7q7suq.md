---
title: "Linux Cheat Sheet"
datePublished: Mon Jul 15 2024 18:47:50 GMT+0000 (Coordinated Universal Time)
cuid: clync7fww000a0alf7h7q7suq
slug: linux-cheat-sheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721069161874/10cff70f-89e2-47fa-853e-09eb7315d18f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721069233532/4e886cc1-1be1-40e4-b600-4ab6f28b329b.png
tags: linux, learning, devops, cheatsheet, 90daysofdevops

---

### Basic Commands

### Navigation

* `pwd`: Print the current working directory.
    
* `cd [dir]`: Change directory to `[dir]`. Use `cd ..` to go up one level.
    
* `ls`: List directory contents.
    
    * `ls -l`: List in long format.
        
    * `ls -a`: List all files including hidden files (those starting with a dot).
        
    * `ls -lh`: Long format with human-readable file sizes.
        

#### File Operations

* `touch [file]`: Create an empty file or update the timestamp of the file.
    
* `cp [source] [destination]`: Copy file or directory.
    
    * `cp -r [source] [destination]`: Copy directories recursively.
        
* `mv [source] [destination]`: Move or rename file or directory.
    
* `rm [file]`: Remove file.
    
    * `rm -r [dir]`: Remove directory and its contents recursively.
        
    * `rm -i [file]`: Remove with a prompt before every removal.
        

### File Viewing

* `cat [file]`: Concatenate and display file content.
    
* `less [file]`: View file content one screen at a time.
    
* `more [file]`: View file content, similar to `less`.
    
* `head [file]`: Display the first 10 lines of a file.
    
    * `head -n [num] [file]`: Display the first `[num]` lines of a file.
        
* `tail [file]`: Display the last 10 lines of a file.
    
    * `tail -n [num] [file]`: Display the last `[num]` lines of a file.
        
    * `tail -f [file]`: Follow the file content as it grows.
        

### File Permissions

* `chmod [permissions] [file]`: Change the file permissions.
    
    * `chmod 755 [file]`: Set permissions to rwxr-xr-x.
        
    * `chmod u+x [file]`: Add execute permission for the owner.
        
* `chown [owner]:[group] [file]`: Change file owner and group.
    
* `chgrp [group] [file]`: Change group ownership.
    

### File Permissions Symbols

* `r`: Read permission.
    
* `w`: Write permission.
    
* `x`: Execute permission.
    
* `-`: No permission.
    

### Access Control Lists (ACL)

* `getfacl [file]`: Get ACL of a file.
    
* `setfacl -m u:[user]:[permissions] [file]`: Set ACL for a user.
    
* `setfacl -m g:[group]:[permissions] [file]`: Set ACL for a group.
    
* `setfacl -x u:[user] [file]`: Remove ACL for a user.
    

### Process Management

* `ps`: Display current processes.
    
    * `ps aux`: Display detailed information about all running processes.
        
* `top`: Display dynamic real-time view of running processes.
    
* `htop`: Enhanced version of `top` (needs to be installed).
    
* `kill [pid]`: Terminate process with process ID `[pid]`.
    
    * `kill -9 [pid]`: Forcefully terminate process with process ID `[pid]`.
        
* `killall [process_name]`: Terminate all processes with the specified name.
    
* `bg`: Resume a suspended job in the background.
    
* `fg`: Bring a background job to the foreground.
    
* `jobs`: List all background jobs.
    

### Disk Usage

* `df`: Report file system disk space usage.
    
    * `df -h`: Human-readable format.
        
* `du [file/dir]`: Estimate file space usage.
    
    * `du -sh [file/dir]`: Display summary in human-readable format.
        

### Networking

* `ping [host]`: Check the network connection to a server.
    
* `ifconfig`: Configure network interfaces (deprecated; use `ip`).
    
* `ip addr`: Show IP addresses and network interfaces.
    
* `netstat`: Network statistics.
    
    * `netstat -tuln`: List all listening ports.
        
* `wget [url]`: Download files from the web.
    
* `curl [url]`: Transfer data from or to a server.
    

### Searching

* `grep [pattern] [file]`: Search for a pattern in a file.
    
    * `grep -r [pattern] [dir]`: Search recursively in a directory.
        
    * `grep -i [pattern] [file]`: Case-insensitive search.
        
* `find [dir] -name [pattern]`: Find files by name.
    
* `locate [name]`: Find files by name (uses a database, needs to be updated with `updatedb`).
    

### Archiving and Compression

* `tar -cvf [archive.tar] [file/dir]`: Create a tar archive.
    
* `tar -xvf [archive.tar]`: Extract a tar archive.
    
* `tar -czvf [archive.tar.gz] [file/dir]`: Create a compressed tar archive with gzip.
    
* `tar -xzvf [archive.tar.gz]`: Extract a compressed tar archive with gzip.
    
* `zip [`[`archive.zip`](http://archive.zip)`] [file/dir]`: Create a zip archive.
    
* `unzip [`[`archive.zip`](http://archive.zip)`]`: Extract a zip archive.
    

### Package Management

* **Debian/Ubuntu:**
    
    * `apt update`: Update package lists.
        
    * `apt upgrade`: Upgrade installed packages.
        
    * `apt install [package]`: Install a package.
        
    * `apt remove [package]`: Remove a package.
        
    * `apt autoremove`: Remove unnecessary packages.
        
* **Red Hat/CentOS:**
    
    * `yum update`: Update package lists and upgrade packages.
        
    * `yum install [package]`: Install a package.
        
    * `yum remove [package]`: Remove a package.
        
    * `yum autoremove`: Remove unnecessary packages.
        

### Service Management

* **Systemd:**
    
    * `systemctl start [service]`: Start a service.
        
    * `systemctl stop [service]`: Stop a service.
        
    * `systemctl restart [service]`: Restart a service.
        
    * `systemctl status [service]`: Check the status of a service.
        
    * `systemctl enable [service]`: Enable a service to start on boot.
        
    * `systemctl disable [service]`: Disable a service from starting on boot.
        

### User Management

* `adduser [username]`: Add a new user.
    
* `passwd [username]`: Change user password.
    
* `deluser [username]`: Remove a user.
    
* `usermod -aG [group] [username]`: Add a user to a group.
    
* `groups [username]`: List the groups a user is in.
    

### Shell Scripting

* **Basic Structure:**
    
    ```bash
    #!/bin/bash
    echo "Hello, World!"
    ```
    
* **Variables:**
    
    ```bash
    NAME="John"
    echo "Hello, $NAME"
    ```
    
* **Conditional Statements:**
    
    ```bash
    if [ condition ]; then
      # Commands
    elif [ condition ]; then
      # Commands
    else
      # Commands
    fi
    ```
    
* **Loops:**
    
    ```bash
    for i in {1..5}; do
      echo "Iteration $i"
    done
    
    while [ condition ]; do
      # Commands
    done
    ```
    

### Additional Useful Commands

* `echo [text]`: Display text.
    
* `date`: Display or set the system date and time.
    
* `uptime`: Show how long the system has been running.
    
* `who`: Show who is logged on.
    
* `uname -a`: Show system information.
    
* `history`: Show command history.