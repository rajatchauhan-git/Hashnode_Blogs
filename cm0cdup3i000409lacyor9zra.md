---
title: "Day 1/40 - Docker Fundamentals"
datePublished: Tue Aug 27 2024 12:07:51 GMT+0000 (Coordinated Universal Time)
cuid: cm0cdup3i000409lacyor9zra
slug: day-140-docker-fundamentals
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724759942956/a86158a0-493b-4630-8ce9-018f65875cb6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724760452895/fe9fd5de-8921-47de-b4c1-05dbc730f361.png
tags: docker, cka, docker-images, certified-kubernetes-administrator, docker-architecture, 40daysofkubernetes, dockerd

---

### **Docker**

Docker is an open-source platform that automates the deployment of applications inside lightweight, portable containers. It provides a consistent environment for development, testing, and production, allowing applications to run reliably across different computing environments.

**Key Features of Docker:**

* **Containerization:** Docker packages an application and its dependencies into a single unit called a container.
    
* **Portability:** Containers can run consistently across any system that supports Docker, whether it's a developer's laptop, an on-premises server, or a cloud environment.
    
* **Isolation:** Docker containers run in isolated environments, ensuring that applications do not interfere with each other.
    
* **Efficiency:** Containers share the host system's operating system kernel, making them lightweight and faster to start compared to virtual machines.
    

### **Container**

A container is a standardized unit of software that encapsulates code and all its dependencies so that the application runs quickly and reliably in different computing environments.

**Key Characteristics of Containers:**

* **Lightweight:** Containers share the host operating system's kernel, reducing overhead compared to virtual machines.
    
* **Portable:** Since containers include everything the application needs to run, they can be moved across environments without compatibility issues.
    
* **Isolated:** Each container operates in its isolated environment, which prevents conflicts between different applications running on the same host.
    
* **Scalable:** Containers can be easily scaled up or down depending on demand, making them ideal for cloud-native applications.
    

---

### **Difference between Virtual machines and Containers**

| Aspect | Virtual Machines (VMs) | Containers |
| --- | --- | --- |
| Architecture | Full virtualization using a hypervisor | OS-level virtualization using a container engine (e.g., Docker) |
| Operating System | Each VM has its own OS, including kernel | Share the host OS kernel; no separate OS per container |
| Resource Efficiency | More resource-intensive due to full OS overhead | Lightweight, using fewer resources since they share the host OS |
| Isolation | Strong isolation with separate OS instances | Process-level isolation; less isolated than VMs |
| Boot Time | Slower, as the entire OS needs to boot | Fast, as only the containerized app starts |
| Size | Larger, includes the entire OS in addition to the application | Smaller, only the application and its dependencies |
| Portability | Less portable; VMs are tied to the underlying hypervisor | Highly portable; can run consistently across environments |
| Use Cases | Suitable for running multiple OS types or legacy apps | Ideal for microservices, DevOps, and CI/CD pipelines |
| Performance | Slightly lower performance due to OS overhead | Near-native performance due to sharing the host OS kernel |
| Management | More complex to manage due to the full OS lifecycle | Easier to manage, often automated with orchestration tools like Kubernetes |

---

### **Docker Architecture**

![img](https://i.postimg.cc/jjYxgVpg/docker-arch.png align="center")

Docker architecture is centered around the Docker Engine, which is a client-server application. The image you provided breaks down the various components and interactions within Docker's architecture. Here's an explanation:

### **1\. Client**

* The Docker client is the primary interface that users interact with. Commands like `docker build`, `docker push`, `docker pull`, and `docker run` are issued from the client. These commands are then sent to the Docker daemon (`dockerd`) to be executed.
    
* The client and the daemon can run on the same system or communicate remotely.
    

### **2\. Docker Daemon (**`dockerd`)

* The Docker daemon manages Docker objects like images, containers, networks, and volumes. It listens to the Docker API requests and processes them.
    
* The Docker daemon interacts with the Operating System kernel and manages resources like CPU, memory, network, and storage for containers.
    

### **3\. Dockerfile**

* The Dockerfile contains the instructions to build a Docker image. It is a text file with commands that specify the base image, application code, and dependencies required to build the image.
    
* The Docker daemon reads the Dockerfile to create the Docker image.
    

### **4\. Images**

* Images are immutable files that contain the source code, libraries, dependencies, tools, and other files needed to run an application.
    
* Once an image is built using the `docker build` command, it is stored locally on the Docker host. These images can then be pushed to a Docker registry or pulled when needed.
    

### **5\. Containers**

* Containers are the runnable instances of Docker images. They are lightweight, isolated, and have their filesystem, CPU, memory, process space, and network interface.
    
* Containers are created using the `docker run` command from an image. Each container is an isolated and secure application platform.
    

### **6\. Registry**

* A Docker registry is a storage and content delivery system that holds Docker images. The Docker Hub is a public registry, while private registries can also be used.
    
* After building an image, you can push it to a registry using the `docker push` command. Similarly, images can be pulled from a registry using the `docker pull` command.
    

### **Interaction Flow:**

1. **Build (docker build)**: The user provides a Dockerfile to the Docker client, which sends it to the Docker daemon to build the image.
    
2. **Store Dockerfile**: The Docker daemon reads the Dockerfile and creates an image based on the instructions provided.
    
3. **Manage Containers and Images**: The Docker daemon manages containers and images, ensuring the right resources are allocated.
    
4. **Push (docker push)**: Once an image is created, the user can push it to a registry for storage or distribution.
    
5. **Registry Storage**: The registry stores the pushed images.
    
6. **Pull (docker pull)**: When required, an image can be pulled from the registry to the Docker daemon on a host.
    
7. **Image Management**: The Docker daemon handles the pulled image, making it ready for running containers.
    
8. **Run (docker run)**: The user can run a container using the `docker run` command, which launches an image instance.
    

### **Docker Workflow**

![img](https://i.postimg.cc/LXpZmD96/docker-workflow.png align="center")

The Docker workflow depicted in the image demonstrates the process of building, pushing, and running Docker images across different environments (DEV, TEST, and PROD). Here's a step-by-step explanation:

1. **Dockerfile**:
    
    * This is the starting point of the workflow. A Dockerfile contains the instructions required to build a Docker image. It specifies the base image, dependencies, and commands that the image should include.
        
2. **Build Docker Image**:
    
    * Using the Dockerfile, a Docker image is built. The image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software, such as the code, runtime, libraries, environment variables, and configuration files.
        
3. **Push Docker Image to Registry**:
    
    * Once the Docker image is built, it is pushed to a Docker registry. The registry serves as a storage location for Docker images, allowing them to be shared and reused across different environments. Public registries like Docker Hub or private registries within organizations can be used.
        
4. **Pull Docker Image from Registry**:
    
    * After the image is stored in the registry, it can be pulled into various environments (DEV, TEST, PROD). Pulling the image means downloading it from the registry to the local system or server.
        
5. **Run Docker Image in Different Environments (DEV, TEST, PROD)**:
    
    * The image is then run in the different environments. The workflow highlights three key environments:
        
        * **DEV (Development)**: The image is first deployed in the development environment where developers can work on the application.
            
        * **TEST**: After development, the image is moved to the testing environment to validate the application with tests.
            
        * **PROD (Production)**: Finally, the image is deployed to the production environment where it is accessible to end users.
            

---

> ***💡 If you need help or have any questions, just leave them in the comments! 📝 I would be happy to answer them!***
> 
> ***💡 If you found this post useful, please give it a thumbs up 👍 and consider following for more helpful content. 😊***

### **Thank you for taking the time to read! 💚**