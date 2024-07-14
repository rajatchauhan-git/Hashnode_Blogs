---
title: "Error Handling in Shell Scripting"
datePublished: Fri Jul 12 2024 20:58:35 GMT+0000 (Coordinated Universal Time)
cuid: clyj6k1k5000e09js8k5sb4w8
slug: error-handling-in-shell-scripting
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720817879601/d904358c-44ee-41b8-aab4-969ced0fa7a6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720817910893/eefd0483-6d3c-4c46-a09d-a2165a6b016f.png
tags: bash, devops, shell, shell-script, 90daysofdevops, trainwithshubham, linuix

---

Understanding how to handle errors in shell scripts is crucial for creating robust and reliable scripts. Today, you'll learn how to use various techniques to handle errors effectively in your bash scripts.

### Topics to Cover

1. **Understanding Exit Status**: Every command returns an exit status (0 for success and non-zero for failure). Learn how to check and use exit statuses.
    
2. **Using if Statements for Error Checking**: Learn how to use if statements to handle errors.
    
3. **Using trap for Cleanup**: Understand how to use the trap command to handle unexpected errors and perform cleanup.
    
4. **Redirecting Errors**: Learn how to redirect errors to a file or `/dev/null`.
    
5. **Creating Custom Error Messages**: Understand how to create meaningful error messages for debugging and user information.
    

### Tasks

#### Task 1: Checking Exit Status

Write a script that attempts to create a directory and checks if the command was successful. If not, print an error message.

```bash
#!/bin/bash

my_directory=$1

mkdir $1

if [ $? -ne 0 ]; then
  echo "Error: Failed to create directory "$1"."
  exit 1
fi
echo "Directory "$1" created successfully."
```

#### Task 2: Using if Statements for Error Checking

Modify the script from Task 1 to include more commands (e.g., creating a file inside the directory) and use if statements to handle errors at each step.

```bash
#!/bin/bash
my_directory=$1
my_file=$2

mkdir $1

if [ $? -ne 0 ]; then
  echo "Error: Failed to create directory "$1"."
  exit 1
fi

echo "Directory "$1" created successfully."

touch "$1"/"$2"

if [ $? -ne 0 ]; then
  echo "Error: Failed to create file "$2" inside "$1"."
  exit 1
fi

echo "File "$1" created successfully in "$1"."
```

#### Task 3: Using trap for Cleanup

Write a script that creates a temporary file and sets a trap to delete the file if the script exits unexpectedly.

```bash
#!/bin/bash

temp_file=$(mktemp)

trap "rm -f $temp_file; echo 'Temporary file deleted.'" EXIT

echo "Temporary file created at $temp_file."

# Simulate some work
sleep 5

# Simulate unexpected exit
exit 1
```

#### Task 4: Redirecting Errors

Write a script that tries to read a non-existent file and redirects the error message to a file called `error.log`.

```bash
#!/bin/bash

cat non_existent_file.txt 2> error.log

if [ $? -ne 0 ]; then
  echo "Error: Failed to read 'non_existent_file.txt'. Check 'error.log' for details."
fi
```

#### Task 5: Creating Custom Error Messages

Modify one of the previous scripts to include custom error messages that provide more context about what went wrong.

```bash
#!/bin/bash
my_directory=$1
my_file=$2

mkdir $1

if [ $? -ne 0 ]; then
  echo "Error: Failed to create directory "$1". Please check if the directory already exists or if you have the necessary permissions."
  exit 1
fi

echo "Directory "$1" created successfully."

touch "$1"/"$2"

if [ $? -ne 0 ]; then
  echo "Error: Failed to create file '$2' inside "$1". Ensure you have write permissions in the directory."
  exit 1
fi

echo "File "$2" created successfully in "$1"."
```

These tasks and examples will help you understand how to effectively handle errors in your bash scripts, making them more robust and reliable.