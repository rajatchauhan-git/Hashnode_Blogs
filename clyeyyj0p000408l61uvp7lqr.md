---
title: "Shell Scripting Challenge Directory Backup with Rotation"
datePublished: Tue Jul 09 2024 22:14:49 GMT+0000 (Coordinated Universal Time)
cuid: clyeyyj0p000408l61uvp7lqr
slug: shell-scripting-challenge-directory-backup-with-rotation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720562070108/1115dbca-9764-459b-ba62-31d3eb367fb9.png
tags: linux, shell, backup, shell-script, 90daysofdevops, trainwithshubham

---

In the realm of DevOps, automation ensures reliability and consistency in managing systems and applications. A critical automation task involves backing up directories. While backups are vital for data protection, managing them can be challenging with numerous files. Here's how a Bash script automates directory backups with a rotation mechanism to retain only the last three backups.

### Objectives

Our script will:

1. Take a directory path as a command-line argument.
    
2. Create a timestamped backup folder inside the specified directory.
    
3. Copy all files from the specified directory into the backup folder.
    
4. Implement a rotation mechanism to keep only the last three backups, removing older ones.
    

### The Script

Below is the Bash script named `backup_with_`[`rotation.sh`](http://rotation.sh) that implements the described functionality:

```bash
#!/bin/bash

<<readme
This script takes backup of a directory with timestamped folders and implements rotation.
Usage:
./backup_with_rotation.sh <path of directory>
readme

# Ensure correct number of arguments
if [ $# -ne 1 ]; then
    echo "Usage: $0 <path of directory>"
    exit 1
fi

source_dir="$1"
target_dir="${source_dir}"

# Create target directory if it does not exist
if [ ! -d "$target_dir" ]; then
    mkdir -p "$target_dir"
fi

timestamp=$(date '+%Y-%m-%d_%H-%M-%S')

backup_dir="${target_dir}/backup_${timestamp}"

function create_backup {
    # Create the backup
    zip -r "${backup_dir}.zip" "${source_dir}" > /dev/null

    if [ $? -eq 0 ]; then
        echo "Backup created: ${backup_dir}.zip"
    else
        echo "Backup was not performed for $timestamp"
    fi
}

function perform_rotation {
    # List backups, sorted by modification time, newest first
    backups=($(ls -t "${target_dir}/backup_"*.zip))

    if [ "${#backups[@]}" -gt 3 ]; then
        backups_to_remove=("${backups[@]:3}")
        for backup in "${backups_to_remove[@]}"; do
            rm -f -- "$backup"
            if [ $? -eq 0 ]; then
                echo "Removed old backup: $backup"
            else
                echo "Failed to remove old backup: $backup"
            fi
        done
    fi
}

create_backup
perform_rotation
```

### Understanding the Script

```bash
#!/bin/bash

<<readme
This script takes backup of a directory with timestamped folders and implements rotation.
Usage:
./backup_with_rotation.sh <path of directory>
readme
```

* **Shebang**: `#!/bin/bash` specifies that the script should be executed using the Bash interpreter.
    
* **Here Document**: `<<readme ... readme` is used for multi-line comments. It provides a description of the script's purpose and usage.
    

```bash
# Ensure correct number of arguments
if [ $# -ne 1 ]; then
    echo "Usage: $0 <path of directory>"
    exit 1
fi
```

* **Argument Handling**: `if [ $# -ne 1 ]; then ... fi` checks if the script is provided exactly one argument (the directory path). If not, it prints usage instructions and exits with an error code.
    

```bash
source_dir="$1"
target_dir="${source_dir}"

# Create target directory if it does not exist
if [ ! -d "$target_dir" ]; then
    mkdir -p "$target_dir"
fi
```

* **Directory Setup**: `source_dir="$1"` assigns the first argument (directory path) to `source_dir`. `target_dir="${source_dir}"` sets `target_dir` to the same path as `source_dir`.
    
* **Directory Creation**: If `target_dir` doesn't exist (`if [ ! -d "$target_dir" ]; then ... fi`), it creates it using `mkdir -p "$target_dir"`.
    

```bash
timestamp=$(date '+%Y-%m-%d_%H-%M-%S')

backup_dir="${target_dir}/backup_${timestamp}"
```

* **Timestamp Generation**: `timestamp=$(date '+%Y-%m-%d_%H-%M-%S')` uses `date` command to generate a timestamp in the format `YYYY-MM-DD_HH-MM-SS`.
    
* **Backup Directory**: `backup_dir="${target_dir}/backup_${timestamp}"` sets `backup_dir` to a directory path with the current timestamp appended.
    

```bash
function create_backup {
    # Create the backup
    zip -r "${backup_dir}.zip" "${source_dir}" > /dev/null

    if [ $? -eq 0 ]; then
        echo "Backup created: ${backup_dir}.zip"
    else
        echo "Backup was not performed for $timestamp"
    fi
}
```

* **Backup Creation**: `create_backup` function compresses (`zip -r`) `source_dir` into `${backup_dir}.zip`. Redirects output to `/dev/null` to suppress zip command output.
    
* **Backup Status**: Checks if the backup operation was successful (`if [ $? -eq 0 ]; then ... fi`) and prints appropriate messages.
    

```bash
function perform_rotation {
    # List backups, sorted by modification time, newest first
    backups=($(ls -t "${target_dir}/backup_"*.zip))

    if [ "${#backups[@]}" -gt 3 ]; then
        backups_to_remove=("${backups[@]:3}")
        for backup in "${backups_to_remove[@]}"; do
            rm -f -- "$backup"
            if [ $? -eq 0 ]; then
                echo "Removed old backup: $backup"
            else
                echo "Failed to remove old backup: $backup"
            fi
        done
    fi
}
```

* **Rotation Mechanism**: `perform_rotation` function lists existing backups (`ls -t "${target_dir}/backup_"*.zip`), sorts them by modification time (newest first).
    
* **Backup Removal**: If more than 3 backups exist (`if [ "${#backups[@]}" -gt 3 ]; then ... fi`), it removes older backups (`rm -f -- "$backup"`).
    

```bash
create_backup
perform_rotation
```

* **Execution**: Finally, it calls `create_backup` to create a new backup and `perform_rotation` to manage existing backups.
    

### How to Use the Script

1. **Save the Script**: Save the script as `backup_with_`[`rotation.sh`](http://rotation.sh).
    
2. **Make the Script Executable**: Run the following command to make the script executable:
    
    ```bash
    chmod +x backup_with_rotation.sh
    ```
    
3. **Execute the Script**: Run the script with the directory path as an argument:
    
    ```bash
    ./backup_with_rotation.sh /path/to/directory
    ```