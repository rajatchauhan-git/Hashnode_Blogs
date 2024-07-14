---
title: "Basic Linux Shell Scripting for DevOps"
datePublished: Tue Jul 02 2024 15:10:57 GMT+0000 (Coordinated Universal Time)
cuid: cly4jqgg0000h09l881wgd6av
slug: basic-linux-shell-scripting-for-devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719932843839/5426c3f4-657b-4bc7-8f05-efcd633f5314.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1719933026807/d032cf7c-7599-4834-8cd2-19d72647208c.png
tags: linux, shell-scripting, shell-script, 90daysofdevops, trainwithshubham, 90daysofdevops-chanllenge

---

## What is a Kernel?

The kernel is the core component of an operating system. It acts as a bridge between applications and the hardware of a computer. The primary responsibilities of a kernel include managing system resources, such as the CPU, memory, and I/O devices, and ensuring that different processes can run simultaneously without interfering with each other.

### Key Functions of a Kernel

1. **Process Management**: The kernel handles the creation, scheduling, and termination of processes. It ensures that each process gets adequate CPU time and resources while maintaining overall system efficiency and responsiveness.
    
2. **Memory Management**: The kernel manages the system's memory, allocating and deallocating memory spaces as needed. It ensures that each process has its own memory space and prevents unauthorized access to memory areas.
    
3. **Device Management**: The kernel provides a standardized way for software to interact with hardware devices. It manages communication between software and hardware through device drivers, which translate generic commands into device-specific actions.
    
4. **File System Management**: The kernel handles file operations such as reading, writing, opening, and closing files. It manages file permissions and ensures data integrity and security within the file system.
    
5. **System Calls**: The kernel provides an interface for user applications to request services through system calls. These calls enable applications to perform tasks such as accessing hardware, managing files, and communicating with other processes.
    

![](https://static.javatpoint.com/linux/images/architecture-of-linux.png align="center")

## What is a Shell?

A shell is a command-line interface (CLI) that allows users to interact with the operating system by typing commands. It interprets user commands and converts them into actions performed by the system. Shells can be categorized into different types, including command-line shells and graphical shells.

### Types of Shells

1. **Command-Line Shell**: A command-line shell provides a text-based interface where users can type commands. Examples include the Bourne Shell (sh), Bourne Again Shell (bash), Korn Shell (ksh), and Z Shell (zsh).
    
2. **Graphical Shell**: A graphical shell provides a graphical user interface (GUI) where users can interact with the system using graphical elements like windows, icons, and menus. Examples include GNOME Shell and KDE Plasma.
    

### Key Functions of a Shell

1. **Command Interpretation**: The shell interprets user commands, executes them, and displays the results. It parses the commands, resolves filenames and variables, and determines the appropriate actions to take.
    
2. **Scripting**: Shells support scripting, allowing users to write scripts to automate repetitive tasks. Shell scripts are text files containing a series of commands that can be executed sequentially.
    
3. **Job Control**: The shell provides job control features, enabling users to manage multiple tasks simultaneously. Users can start, stop, resume, and terminate processes, as well as run processes in the background.
    
4. **Customization**: Users can customize the shell environment by setting environment variables, creating aliases, and configuring startup files. This allows for a personalized and efficient workflow.
    

## What is Linux Shell Scripting?

Linux shell scripting involves writing scripts using a shell, such as bash, to automate tasks on a Linux system. Shell scripts can be used for a wide range of purposes, from simple file manipulation to complex system administration tasks. Shell scripting is powerful because it leverages the shell's capabilities and the wide array of command-line tools available in Linux.

### Key Concepts in Shell Scripting

1. **Shebang (**`#!`): The shebang (`#!`) at the beginning of a script specifies the interpreter to be used to execute the script. For example, `#!/bin/bash` indicates that the script should be run using the bash shell.
    
2. **Variables**: Shell scripts can define and use variables to store and manipulate data. Variables can be assigned values and referenced within the script.
    
3. **Control Structures**: Shell scripting supports control structures such as conditionals (`if`, `else`, `elif`), loops (`for`, `while`, `until`), and case statements. These structures enable complex decision-making and repetitive tasks.
    
4. **Functions**: Functions in shell scripts allow for code reuse and modularity. A function is a block of code that can be defined once and called multiple times within the script.
    
5. **Input/Output Redirection**: Shell scripts can redirect input and output using operators like `>`, `<`, `>>`, and `|`. This allows for the manipulation of data streams and the chaining of commands.
    
6. **Error Handling**: Shell scripts can handle errors using techniques such as exit statuses, trapping signals, and conditional checks. Proper error handling ensures robustness and reliability.
    

### Examples of Shell Scripting Use Cases

1. **Automating System Administration**: Shell scripts can automate tasks like backups, software installations, and system updates. For example, a script can be created to regularly back up important files to a remote server.
    
2. **Data Processing**: Shell scripts can process and manipulate data, such as filtering log files, extracting information, and generating reports. For instance, a script can parse a log file to extract error messages and send an email notification.
    
3. **Environment Setup**: Shell scripts can set up development environments by installing dependencies, configuring settings, and launching services. A script can automate the setup of a development environment for a specific project.
    
4. **Task Scheduling**: Shell scripts can be scheduled to run at specific times using tools like cron. For example, a script can be scheduled to run every night to clean up temporary files.
    

---

**Task 1:** Explain in your own words and with examples what Shell Scripting means for DevOps.

> Shell scripting in DevOps automates routine tasks, manages system configurations, deploys applications, and monitors systems using commands in scripts (often in Bash). This boosts efficiency, ensures consistency, and reduces manual errors. For example, a script can back up databases, set environment variables, deploy web apps, or send alerts for high disk usage, making DevOps processes smoother and more reliable.

**Task 2:** What is `#!/bin/bash`? Can we write `#!/bin/sh` as well?

> The line `#!/bin/bash` at the top of a script tells the system to run the script using the Bash shell, while `#!/bin/sh` tells it to use the `sh` shell.
> 
> ### Key Differences
> 
> 1. **Bash (**`#!/bin/bash`):
>     
>     * Uses the Bash shell, which has many advanced features.
>         
>     * Good for scripts that need extra functionality.
>         
> 2. **sh (**`#!/bin/sh`):
>     
>     * Uses the `sh` shell, which is more basic and widely compatible.
>         
>     * Good for simpler, more portable scripts.
>         
> 
> ### In Short
> 
> * Use `#!/bin/bash` for more complex scripts with advanced features.
>     
> * Use `#!/bin/sh` for simpler, more portable scripts that work on many systems.
>     

**Task 3:** Write a Shell Script that prints `I will complete #90DaysOfDevOps challenge`.

```bash
#!/bin/bash
echo "I will complete #90DaysOfDevOps challenge."
```

**Task 4:** Write a Shell Script that takes user input, input from arguments, and prints the variables.

```bash
#!/bin/bash

# Taking user input
read -p "Enter your name: " user_name

# Taking arguments from the command line
arg1=$1
arg2=$2

# Printing the variables
echo "User Name: $user_name"
echo "Argument 1: $arg1"
echo "Argument 2: $arg2"
```

> **Make the Script Executable**:
> 
> * In the terminal, navigate to the directory where you saved the script.
>     
> * Run the command `chmod +x input_`[`script.sh`](http://script.sh) to make the script executable.
>     

**Task 5:** Provide an example of an If-Else statement in Shell Scripting by comparing two numbers.

```bash
#!/bin/bash

# Take two numbers as input
read -p "Enter the first number: " num1
read -p "Enter the second number: " num2

# Compare the numbers
if [ $num1 -gt $num2 ]; then
  echo "$num1 is greater than $num2"
elif [ $num1 -lt $num2 ]; then
  echo "$num1 is less than $num2"
else
  echo "$num1 is equal to $num2"
fi
```