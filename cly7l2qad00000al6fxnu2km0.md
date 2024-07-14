---
title: "Advanced Linux Shell Scripting for DevOps Engineers with User Management"
datePublished: Thu Jul 04 2024 18:11:47 GMT+0000 (Coordinated Universal Time)
cuid: cly7l2qad00000al6fxnu2km0
slug: advanced-linux-shell-scripting-for-devops-engineers-with-user-management
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720116648524/c8ea96fd-ec62-48c7-b0fa-6a2d245ac8b0.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720116701230/1364675e-1e8c-4308-a193-939a1418c177.png
tags: linux, automation, devops, backup, cronjob, shell-script, 90daysofdevops, trainwithshubham

---

**Task 1:** **Create Directories Using Shell Script:**

* Write a bash script [`createDirectories.sh`](http://createDirectories.sh) that, when executed with three arguments (directory name, start number of directories, and end number of directories), creates a specified number of directories with a dynamic directory name.
    
* Example 1: When executed as `./`[`createDirectories.sh`](http://createDirectories.sh) `day 1 90`, it creates 90 directories as `day1 day2 day3 ... day90`.
    
* Example 2: When executed as `./`[`createDirectories.sh`](http://createDirectories.sh) `Movie 20 50`, it creates 31 directories as `Movie20 Movie21 Movie22 ... Movie50`.
    

```bash
#!/bin/bash

#Assing Arguments

dir_name=$1
start_number=$2
end_number=$3

#Create Directories

for (( i=start_number; i<=end_number; i++ ))
do
        mkdir -p "${dir_name}${i}"
done

echo "Directories created from ${dir_name}${start_number} to ${dir_name}${end_number}"
```

**Task 2:** **Create a Script to Backup All Your Work:**

* Backups are an important part of a DevOps Engineer's day-to-day activities. The video in the references will help you understand how a DevOps Engineer takes backups (it can feel a bit difficult but keep trying, nothing is impossible).
    

```bash
#!/bin/bash

src_dir=/home/ubuntu/scripts
tgt_dir=/home/ubuntu/backups

curr_timestamp=$(date "+%Y-%m-%d-%H-%M-%S")

backup_file=$tgt_dir/$curr_timestamp.tgz

echo "Taking backup on $curr_timestamp"

tar czf $backup_file --absolute-names $src_dir

echo "Backup Complete"
```

## What is Cron?

Cron is a time-based job scheduler in Unix-like operating systems. It allows users to schedule jobs (commands or scripts) to run automatically at specified intervals. This could be anything from running a backup script every night at 2 AM, to sending out reminder emails every Monday morning, or cleaning up log files every hour.

Cron is started when the system boots up and runs in the background, checking the Crontab files to see if there are any jobs to execute.

## What is Crontab?

Crontab (Cron table) is a configuration file that specifies shell commands to run periodically on a given schedule. Each user on a system can have their own Crontab file, allowing for personalized automation.

The Crontab file consists of a series of lines, each line representing a job, with the time and date fields followed by the command to be executed.

### Crontab Syntax

A typical Crontab entry follows this format:

```scss
* * * * * command_to_execute
- - - - -
| | | | |
| | | | ----- Day of the week (0 - 7) (Sunday=0 or 7)
| | | ------- Month (1 - 12)
| | --------- Day of the month (1 - 31)
| ----------- Hour (0 - 23)
------------- Minute (0 - 59)
```

```javascript
30 2 * * * /path/to/backup.sh
```

### Editing Crontab

To edit your Crontab file, you use the `crontab -e` command. This opens your Crontab file in the default text editor, allowing you to add, modify, or remove jobs.

```javascript
Copy codecrontab -e
```

To view your current Crontab entries, use:

```javascript
Copy codecrontab -l
```

To remove all Crontab entries for the current user, use:

```javascript
Copy codecrontab -r
```

**Task 3: Read About Cron and Crontab to Automate the Backup Script:**

* Cron is the system's main scheduler for running jobs or tasks unattended. A command called crontab allows the user to submit, edit, or delete entries to cron. A crontab file is a user file that holds the scheduling information.
    

\- To take backup through crontab:

### Crontab:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720095907117/0ed42ea5-0a3a-4db9-83ef-82e86836ad2e.png align="center")

### BACKUP TAKEN BY THE CRON JOB

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720095863332/bb4745ea-3070-4502-b0aa-c8b91168745c.png align="center")

**Task 4: Read About User Management:**

* A user is an entity in a Linux operating system that can manipulate files and perform several other operations. Each user is assigned an ID that is unique within the system. IDs 0 to 999 are assigned to system users, and local user IDs start from 1000 onwards.
    
* Create 2 users and display their usernames.
    

## Why User Management Matters

User management in Linux is important for several reasons:

1. **Security**: Proper user management ensures that only authorized users have access to the system and its resources.
    
2. **Organization**: Different users can have different roles and permissions, keeping the system organized and efficient.
    
3. **Resource Allocation**: Managing users allows you to control resource allocation, ensuring fair usage and preventing resource hogging.
    

## Basic Concepts

### User Accounts

In Linux, a user account consists of several key components:

* **Username**: The unique identifier for the user.
    
* **UID (User ID)**: A numerical ID assigned to the user.
    
* **Home Directory**: The directory where the user's personal files and configuration settings are stored.
    
* **Shell**: The command-line interface assigned to the user, typically `/bin/bash`.
    

### User Groups

Groups are used to manage multiple users with similar permissions. Each user can belong to one or more groups.

* **GID (Group ID)**: A numerical ID assigned to the group.
    
* **Primary Group**: The main group associated with the user.
    
* **Secondary Groups**: Additional groups the user belongs to.
    

## Managing Users and Groups

### Adding a User

To add a new user, use the `useradd` command:

```javascript
sudo useradd -m username
```

* The `-m` option creates a home directory for the user.
    

To set a password for the new user, use the `passwd` command:

```javascript
sudo passwd username
```

### Removing a User

To remove a user, use the `userdel` command:

```javascript
sudo userdel username
```

To remove the user's home directory as well, add the `-r` option:

```javascript
sudo userdel -r username
```

### Modifying a User

To modify an existing user, use the `usermod` command. For example, to change a user's shell:

```javascript
sudo usermod -s /bin/zsh username
```

To add a user to a secondary group:

```javascript
sudo usermod -aG groupname username
```

### Viewing User Information

To view user information, use the `id` command:

```javascript
id username
```

This will display the user's UID, primary group, and secondary groups.

### Adding a Group

To add a new group, use the `groupadd` command:

```javascript
sudo groupadd groupname
```

### Removing a Group

To remove a group, use the `groupdel` command:

```javascript
sudo groupdel groupname
```

## User Configuration Files

Linux user and group information is stored in several configuration files:

* `/etc/passwd`: Contains user account information.
    
* `/etc/shadow`: Contains hashed user passwords and password-related information.
    
* `/etc/group`: Contains group information.
    

### Example Entries

* **/etc/passwd**:
    
    ```javascript
    username:x:UID:GID:User Info:Home Directory:Shell
    ```
    
    Example:
    
    ```javascript
    johndoe:x:1001:1001:John Doe:/home/johndoe:/bin/bash
    ```
    
* **/etc/shadow**:
    
    ```javascript
    username:hashed_password:last_password_change:minimum_age:maximum_age:warning_period:inactivity_period:expiration_date:reserved
    ```
    
    Example:
    
    ```javascript
    johndoe:$6$abcdefg$hijklmnopqrstuvwxyz:18475:0:99999:7:::
    ```
    
* **/etc/group**:
    
    ```javascript
    groupname:x:GID:members
    ```
    
    Example:
    
    ```javascript
    developers:x:1002:johndoe,janedoe
    ```
    

## Advanced User Management

### Sudo Access

Granting a user sudo access allows them to execute commands as the root user. To add a user to the `sudo` group:

```javascript
sudo usermod -aG sudo username
```

### Password Policies

You can enforce password policies using the `chage` command. For example, to set a password expiration date:

```javascript
sudo chage -E 2024-12-31 username
```

To set the minimum number of days between password changes:

```javascript
sudo chage -m 7 username
```

### Locking and Unlocking User Accounts

To lock a user account:

```javascript
sudo usermod -L username
```

To unlock a user account:

```javascript
sudo usermod -U username
```