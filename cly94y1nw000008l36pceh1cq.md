---
title: "File Permissions and Access Control Lists"
datePublished: Fri Jul 05 2024 20:15:47 GMT+0000 (Coordinated Universal Time)
cuid: cly94y1nw000008l36pceh1cq
slug: file-permissions-and-access-control-lists
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720210540654/89dfaaee-e449-4f94-8663-6e6272512157.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720210535471/5134cd77-70ca-4457-88d3-10057ebfb8a1.png
tags: linux, user, devops, file-permission, 90daysofdevops, trainwithshubham

---

### Introduction to File Permissions

File permissions in Linux control who can read, write, or execute a file. These permissions are critical for protecting data and ensuring that only authorized users can access or modify files. Each file and directory in a Linux system has an associated set of permissions.

### Types of File Permissions

Linux file permissions are divided into three categories:

* **User (Owner):** The user who owns the file.
    
* **Group:** Users who are part of a group assigned to the file.
    
* **Others:** All other users who have access to the system.
    

Each category has three types of permissions:

* **Read (r):** Permission to read the file or list the directory.
    
* **Write (w):** Permission to modify the file or the directory contents.
    
* **Execute (x):** Permission to execute the file or access the directory.
    

Permissions are typically represented in a symbolic or octal notation. For example, `rwxr-xr--` or `755`.

### Changing File Permissions

To view and modify file permissions, we use commands like `ls`, `chmod`, `chown`, and `chgrp`.

#### Viewing Permissions

Use `ls -l` to display file permissions:

```bash
$ ls -l
-rw-r--r-- 1 user group 1234 Jan 1 00:00 file.txt
```

#### Changing Permissions with `chmod`

The `chmod` command modifies file permissions. It can use symbolic or numeric (octal) notation.

**Symbolic Notation:**

```bash
$ chmod u+x file.txt   # Add execute permission for the owner
$ chmod g-w file.txt   # Remove write permission for the group
$ chmod o=r file.txt   # Set read-only permission for others
```

**Octal Notation:**

```bash
$ chmod 755 file.txt   # rwxr-xr-x
$ chmod 644 file.txt   # rw-r--r--
```

#### Changing Ownership with `chown`

The `chown` command changes the file's owner and group.

```bash
$ chown user:group file.txt
```

### File Permissions

#### Understanding File Permissions:

1. **Create a simple file and run**`ls -ltr` to see the details of the files. Refer to Notes.
    
    ```bash
    $ touch myfile.txt
    $ ls -ltr myfile.txt
    ```
    
2. **Each of the three permissions are assigned to three defined categories of users. The categories are:**
    
    * **Owner:** The owner of the file or application.
        
        * **Task:** Use `chown` to change the ownership permission of a file or directory.
            
        
        ```bash
        $ sudo chown newowner myfile.txt
        ```
        
    * **Group:** The group that owns the file or application.
        
        * **Task:** Use `chgrp` to change the group permission of a file or directory.
            
        
        ```bash
        $ sudo chgrp newgroup myfile.txt
        ```
        
    * **Others:** All users with access to the system (outside the users in a group).
        
        * **Task:** Use `chmod` to change the other users' permissions of a file or directory.
            
        
        ```bash
        $ chmod o+w myfile.txt
        ```
        
3. **Task:** Change the user permissions of the file and note the changes after running `ls -ltr`.
    
    ```bash
    $ chmod u+x myfile.txt
    $ ls -ltr myfile.txt
    ```
    

### Introduction to Access Control Lists (ACLs)

While traditional file permissions are sufficient for many use cases, they lack flexibility when you need to assign specific permissions to multiple users or groups. This is where Access Control Lists (ACLs) come in.

ACLs provide a more granular permission mechanism. They allow you to define different permissions for different users and groups on a single file or directory.

### 6\. Using ACLs for Advanced Permissions

#### Viewing ACLs

Use the `getfacl` command to view the ACLs of a file or directory:

```bash
$ getfacl file.txt
# file: file.txt
# owner: user
# group: group
user::rw-
user:anotheruser:rw-
group::r--
mask::rw-
other::r--
```

#### Modifying ACLs

The `setfacl` command is used to set ACLs on files and directories.

**Adding an ACL Entry:**

```bash
$ setfacl -m u:anotheruser:rw file.txt   # Give read and write permissions to 'anotheruser'
$ setfacl -m g:anothergroup:rx file.txt  # Give read and execute permissions to 'anothergroup'
```

**Removing an ACL Entry:**

```bash
$ setfacl -x u:anotheruser file.txt      # Remove ACL entry for 'anotheruser'
```

**Setting Default ACLs:** Default ACLs are inherited by all new files and directories created within a directory.

```bash
$ setfacl -d -m u:anotheruser:rw /mydir  # Set default ACL for 'anotheruser' in 'mydir'
```

#### Checking Effective Rights

Use `getfacl` to check the effective rights of a file or directory. The effective rights consider both the base permissions and the ACLs.

### Access Control Lists (ACLs)

1. **Read about ACL and try out the commands**`getfacl` and `setfacl`.
    
2. **Task:** Create a directory and set specific ACL permissions for different users and groups. Verify the permissions using `getfacl`.
    
    ```bash
    $ mkdir mydir
    $ setfacl -m u:anotheruser:rwx mydir
    $ setfacl -m g:anothergroup:rx mydir
    $ getfacl mydir
    ```
    
3. **Task:** Write an article about file permissions based on your understanding from the notes.
    

### Understanding Sticky Bit, SUID, and SGID

Sticky bit, SUID (Set User ID), and SGID (Set Group ID) are special types of permissions that provide additional security and functionality.

* **Sticky Bit:** When set on a directory, it ensures that only the file owner, the directory owner, or the root user can delete or rename files within that directory.
    
* **SUID:** When set on an executable file, it allows the file to be executed with the permissions of the file owner.
    
* **SGID:** When set on a directory, files created within the directory inherit the group ownership of the directory.
    

### Tasks: Sticky Bit, SUID, and SGID

1. **Read about sticky bit, SUID, and SGID.**
    
2. **Task:** Create examples demonstrating the use of sticky bit, SUID, and SGID, and explain their significance.
    
    ```bash
    # Sticky Bit
    $ mkdir /tmp/sticky
    $ chmod +t /tmp/sticky
    
    # SUID
    $ sudo chmod u+s /usr/bin/passwd
    
    # SGID
    $ mkdir /tmp/sgid
    $ chmod g+s /tmp/sgid
    ```
    

### Backup and Restore Permissions

Backing up and restoring file permissions is essential for maintaining system integrity during migrations or major changes.

### Tasks: Backup and Restore Permissions

1. **Task:** Create a script that backs up the current permissions of files in a directory to a file.
    
    ```bash
    $ getfacl -R /path/to/directory > permissions_backup.txt
    ```
    
2. **Task:** Create another script that restores the permissions from the backup file.
    
    ```bash
    $ setfacl --restore=permissions_backup.txt
    ```
    

### Best Practices for File Permissions and ACLs

1. **Principle of Least Privilege:** Grant the minimum necessary permissions to users and groups.
    
2. **Regular Audits:** Periodically review permissions and ACLs to ensure they are correctly set.
    
3. **Documentation:** Keep a record of permissions and ACLs for critical files and directories.
    
4. **User Training:** Educate users about the importance of proper permission management.