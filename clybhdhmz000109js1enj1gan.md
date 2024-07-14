---
title: "Understanding Package Manager and Systemctl"
datePublished: Sun Jul 07 2024 11:39:16 GMT+0000 (Coordinated Universal Time)
cuid: clybhdhmz000109js1enj1gan
slug: understanding-package-manager-and-systemctl
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720352327471/f8d8d33c-d292-442c-ab18-9a9f2df902cd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720352279679/56a2805e-6738-4cd7-ad11-5ba8cbe3206e.png
tags: linux, devops, services, package-manager, systemctl, 90daysofdevops, trainwithshubham

---

##   
What is a Package Manager?

Imagine you’ve just bought a new gadget. To make it work, you need to install various components, follow a setup guide, and sometimes, even configure settings. A package manager does all this heavy lifting for software on your Linux system. In simpler terms, a package manager is a tool that automates the process of installing, removing, upgrading, configuring, and managing software packages. It’s like having a personal assistant for your software needs.

### Key Functions of a Package Manager:

* **Installation**: Install new software packages with a single command.
    
* **Removal**: Uninstall software you no longer need without leaving behind any clutter.
    
* **Upgrade**: Keep your software up to date effortlessly.
    
* **Configuration**: Handle initial setup and ongoing configuration of software.
    
* **Dependency Management**: Automatically manage and resolve software dependencies.
    

## What is a Package?

To truly appreciate package managers, you need to understand what a package is. A package can be thought of as a bundle containing everything needed to install a piece of software. This could be a graphical application, a command-line tool, or even a library that other software programs rely on.

### Components of a Package:

* **Binary Executable**: The compiled program ready to run on your system.
    
* **Configuration Files**: Files that help customize the software for your system.
    
* **Dependencies**: Information about other packages needed for the software to function correctly.
    

Packages are often distributed in a compressed format to save space and bandwidth. When you install a package, the package manager unpacks it and places the files in the appropriate directories.

## Different Kinds of Package Managers

Package managers vary based on the packaging system they support, and sometimes, there are multiple package managers for the same packaging system. Here’s a look at some common ones:

### RPM (Red Hat Package Manager)

* **Yum (Yellowdog Updater Modified)**: Used in older Red Hat-based distributions like CentOS and Fedora. It's known for its simplicity and ease of use.
    
* **DNF (Dandified Yum)**: The modern replacement for Yum, offering better performance and improved dependency resolution.
    

### DEB (Debian Package)

* **apt-get**: A command-line tool used in Debian-based distributions like Ubuntu. It's powerful and widely used.
    
* **aptitude**: Offers a text-based interface on top of `apt-get`, providing additional features and a more user-friendly experience.
    
* **dpkg**: The base tool for handling `.deb` packages, often used under the hood by `apt-get` and `aptitude`.
    

### Pacman (Package Manager for Arch Linux)

* **pacman**: The package manager for Arch Linux, known for its speed and simplicity. It’s a favorite among Arch users for its efficiency.
    

### Zypper (SUSE Linux)

* **zypper**: The command-line interface for the ZYpp package management engine, used in openSUSE and SUSE Linux Enterprise. It's robust and versatile.
    

### Portage (Gentoo Linux)

* **emerge**: The command-line tool for Gentoo Linux, known for its flexibility and the ability to compile software from source. It’s highly customizable.
    

## How Package Managers Work

At the heart of a package manager is a database of software available from one or more repositories. Repositories are servers that host software packages and their metadata. When you install a package, the package manager communicates with these repositories to download and install the required files. Here's a typical workflow:

### Workflow of a Package Manager:

1. **Update Package List**: The package manager fetches the latest list of available packages from the repositories.
    
2. **Install Package**: You issue a command to install a package. The package manager checks for dependencies and downloads the necessary files.
    
3. **Resolve Dependencies**: The package manager ensures all dependencies are met, downloading and installing any additional packages required.
    
4. **Configure Software**: During installation, you might be prompted to configure certain aspects of the software.
    
5. **Complete Installation**: The package is installed and ready to use.
    

## Example: Using `apt-get` on Debian-based Systems

Let’s explore some common commands using `apt-get`, a popular package manager for Debian-based distributions like Ubuntu:

* **Update Package List**:
    
    ```bash
    sudo apt-get update
    ```
    
    This command updates the local package index with the latest changes made in the repositories.
    
* **Install a Package**:
    
    ```bash
    sudo apt-get install package_name
    ```
    
    Replace `package_name` with the name of the software you want to install.
    
* **Remove a Package**:
    
    ```bash
    sudo apt-get remove package_name
    ```
    
    This command removes the specified package from your system.
    
* **Upgrade All Packages**:
    
    ```bash
    sudo apt-get upgrade
    ```
    
    This upgrades all the installed packages to their latest versions.
    

## Why Package Managers Matter

Package managers are the backbone of the Linux software ecosystem. They not only simplify the process of software management but also ensure that your system remains stable and secure by handling dependencies and updates efficiently.

Imagine manually downloading software, tracking dependencies, and configuring everything yourself—it would be a nightmare! Package managers take away that complexity, allowing you to focus on what matters most: using your system productively.

---

Task1: **Install Docker and Jenkins:**

* Install Docker and Jenkins on your system from your terminal using package managers.
    

```bash
sudo apt install docker.io
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350010613/3682cc5f-661b-47f6-a5a4-883847f271a9.png align="center")

* While installing Jenkins I got below error and to resolve this issue please follow below steps:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720350304034/aa33ff9a-d355-4775-9a2f-7aed2868bb5c.png align="center")

It seems like Jenkins is not available in the default repositories of your distribution.  
Before adding new repositories, it's always a good idea to update your system to ensure you have the latest package lists.

```bash
sudo apt-get update
sudo apt-get upgrade
```

Jenkins requires Java to run. You can install OpenJDK (an open-source implementation of Java) with the following command.

```bash
sudo apt-get install openjdk-11-jdk -y
```

Verify the Java installation:

```bash
java -version
```

You should see output similar to:

```bash
openjdk version "11.0.23" 2024-04-16
```

Add the Jenkins Debian repository to your system's software repository list.

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

Update your package list to include the Jenkins repository.

```bash
sudo apt-get update
```

Now you can install Jenkins with the following command.

```bash
sudo apt-get install jenkins
```

Start the Jenkins service and enable it to start on boot.

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Jenkins runs on port 8080 by default. Open your web browser and navigate to

```basic
http://your_server_ip_or_domain:8080
```

Task2: **Check Docker Service Status:**

* Check the status of the Docker service on your system (ensure you have completed the installation tasks above).
    

```bash
sudo systemctl status docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720351250802/779463f0-f8df-498b-8bc8-96d8bc7cb528.png align="center")

Task3: **Manage Jenkins Service:**

* Stop the Jenkins service and post before and after screenshots.
    

```bash
sudo systemctl status jenkins
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720351339911/5f94f966-31a1-4ad8-9dec-a5ecbb3221ed.png align="center")

```bash
sudo systemctl stop jenkins
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720351376164/c7d7238d-966e-4f70-9e4b-3ce277789261.png align="center")

---

Managing services in Linux is a fundamental task, and two of the most common commands for this purpose are `systemctl` and `service`. Both are used to control and manage system services, but they have differences in usage, functionality, and underlying mechanisms. In this blog post, we'll explore these differences, understand when to use each command, and provide practical examples to illustrate their usage.

## Overview of `systemctl` and `service`

### `systemctl`

`systemctl` is the command used to interact with the systemd system and service manager. Systemd is a suite of tools that provides a range of functionalities for managing Linux systems, including service management, system initialization, and more. `systemctl` is the primary tool to manage systemd services.

### `service`

`service` is a command used to interact with the init system, specifically SysVinit and Upstart, which were common before systemd became widely adopted. The `service` command provides a way to start, stop, and check the status of system services, and it abstracts the underlying init system to provide a consistent interface.

## Key Differences

### 1\. **Underlying System**

* **systemctl**: Operates with systemd, which is now the default init system for many major Linux distributions, including Ubuntu, Fedora, and Debian.
    
* **service**: Typically works with older init systems like SysVinit and Upstart. In systemd-based systems, `service` is often implemented as a compatibility layer.
    

### 2\. **Command Syntax**

* **systemctl**: Uses a more modern and versatile syntax. For example:
    
    ```bash
    systemctl status docker
    systemctl start docker
    systemctl stop docker
    systemctl restart docker
    systemctl enable docker
    systemctl disable docker
    ```
    
* **service**: Uses a simpler and more traditional syntax. For example:
    
    ```bash
    service docker status
    service docker start
    service docker stop
    service docker restart
    ```
    

### 3\. **Capabilities**

* **systemctl**: Provides extensive control over systemd units (services, sockets, timers, etc.). It can manage dependencies, isolate services, and change service properties on-the-fly. It offers advanced features like:
    
    * Reloading service configurations without restarting.
        
    * Masking/unmasking services.
        
    * Listing dependencies and viewing logs.
        
* **service**: Primarily focused on starting, stopping, and checking the status of services. It lacks the advanced capabilities and granular control provided by `systemctl`.
    

### 4\. **Service Management**

* **systemctl**: Handles unit files, which are configuration files that describe services, sockets, timers, and other entities managed by systemd. It can manage various types of units beyond just services.
    
* **service**: Limited to managing SysVinit or Upstart scripts located in `/etc/init.d/`.
    

## Practical Examples

### Checking Service Status

* **Using** `systemctl`:
    
    ```bash
    systemctl status docker
    ```
    
    **Output**:
    
    ```bash
    docker.service - Docker Application Container Engine
       Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
       Active: active (running) since Mon 2024-07-07 10:35:21 UTC; 1 day 2h ago
         Docs: https://docs.docker.com
     Main PID: 1234 (dockerd)
        Tasks: 29
       Memory: 53.1M
       CGroup: /system.slice/docker.service
               └─1234 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
    ```
    
* **Using** `service`:
    
    ```bash
    service docker status
    ```
    
    **Output**:
    
    ```bash
    docker.service - Docker Application Container Engine
       Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
       Active: active (running) since Mon 2024-07-07 10:35:21 UTC; 1 day 2h ago
         Docs: https://docs.docker.com
     Main PID: 1234 (dockerd)
        Tasks: 29
       Memory: 53.1M
       CGroup: /system.slice/docker.service
               └─1234 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
    ```
    

### Starting a Service

* **Using** `systemctl`:
    
    ```bash
    systemctl start docker
    ```
    
* **Using** `service`:
    
    ```bash
    service docker start
    ```
    

### Stopping a Service

* **Using** `systemctl`:
    
    ```bash
    systemctl stop docker
    ```
    
* **Using** `service`:
    
    ```bash
    service docker stop
    ```
    

### Enabling a Service to Start on Boot

* **Using** `systemctl`:
    
    ```bash
    systemctl enable docker
    ```
    
* **Using** `service`: Note: The `service` command itself does not handle enabling services at boot. This is typically managed by updating runlevel symlinks directly or using `chkconfig` or `update-rc.d`.