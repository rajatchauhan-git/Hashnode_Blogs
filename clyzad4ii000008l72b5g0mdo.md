---
title: "Docker compose and YAML"
datePublished: Wed Jul 24 2024 03:29:30 GMT+0000 (Coordinated Universal Time)
cuid: clyzad4ii000008l72b5g0mdo
slug: docker-compose-and-yaml
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721791703081/cd030e41-9584-4584-a099-11f91b26f599.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721791763930/9054586e-31d4-423f-9603-30e9d541d689.png
tags: docker, automation, devops, yaml, containerization, docker-compose, 90daysofdevops, trainwithshubham

---

### Docker Compose: Simplifying Multi-Container Applications

Docker Compose is an essential tool for defining and sharing multi-container applications. It allows developers to manage multiple containers using a single command, streamlining the process of application deployment and management.

#### What is Docker Compose?

Docker Compose is a tool developed to help define and share multi-container applications. With Docker Compose, you can create a YAML file to define the services that make up your application, and with a single command, you can spin everything up or tear it all down. This capability is particularly useful in development, testing, and CI/CD environments where complex applications need to be easily managed and deployed.

#### Key Features of Docker Compose

1. **Service Definition**: Docker Compose allows you to define multiple services in a single YAML file. Each service corresponds to a container, and you can specify various configurations such as the image, ports, volumes, environment variables, and dependencies.
    
2. **Single Command Management**: With Docker Compose, you can manage your entire application stack with a single command. The `docker-compose up` command brings up all the defined services, while `docker-compose down` stops and removes them.
    
3. **Network Isolation**: Docker Compose creates a default network for all services defined in the YAML file, allowing them to communicate with each other while isolating them from external networks.
    
4. **Volume Management**: Docker Compose simplifies volume management, enabling data persistence and sharing between containers.
    
5. **Environment Configuration**: Environment variables can be easily managed and injected into containers using the `environment` key in the YAML file or an external `.env` file.
    
6. **Scaling Services**: Docker Compose supports scaling services horizontally. You can specify the number of instances for a particular service using the `scale` command or directly in the YAML file.
    

#### What is YAML?

YAML, which stands for "YAML Ain't Markup Language," is a data serialization language often used for writing configuration files. YAML emphasizes human readability and ease of understanding, making it a popular choice for configuration files in various applications.

##### Key Characteristics of YAML

1. **Human-Readable**: YAML is designed for humans to read and write easily. Its syntax is minimalistic and straightforward, reducing the chances of errors.
    
2. **Data Serialization**: YAML is primarily used for data serialization, making it suitable for representing hierarchical data structures such as configurations.
    
3. **File Extensions**: YAML files use either `.yml` or `.yaml` as their file extensions.
    
4. **Syntax**: YAML uses indentation to denote structure, similar to Python. Colons separate key-value pairs, dashes denote lists, and comments are indicated by the `#` symbol.
    

##### Example of a YAML File

Here is a simple example of a Docker Compose YAML file:

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
  database:
    image: postgres:latest
    environment:
      POSTGRES_USER: exampleuser
      POSTGRES_PASSWORD: examplepass
```

In this example, we define two services: `web` and `database`. The `web` service uses the Nginx image and maps port 80 of the host to port 80 of the container. The `database` service uses the PostgreSQL image and sets environment variables for the database user and password.

---

**TASK:** Pull a Pre-existing Docker Image and Run it as a Non-root User

#### Step 1: Install Docker

If Docker is not already installed on your machine, you can install it using the following commands:

**For Ubuntu:**

```bash
sudo apt-get update
sudo apt-get install -y docker.io
```

**For CentOS:**

```bash
sudo yum update -y
sudo yum install -y docker
```

#### Step 2: Start Docker Service

Make sure the Docker service is running:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

#### Step 3: Add User to Docker Group

Add your user to the `docker` group to run Docker commands without `sudo`:

```bash
sudo usermod -aG docker $USER
```

#### Step 4: Reboot the Machine

Reboot your machine for the group changes to take effect:

```bash
sudo reboot
```

#### Step 5: Pull a Docker Image

Once your machine has rebooted, log in and pull a Docker image from Docker Hub. For example, let's pull the `nginx` image:

```bash
docker pull nginx
```

#### Step 6: Run the Docker Container

Run the pulled image as a non-root user:

```bash
docker run -d --name mynginx -p 80:80 nginx
```

#### Step 7: Inspect the Container

Inspect the running container's processes and exposed ports:

```bash
docker inspect mynginx
```

#### Step 8: View Container Logs

View the log output of the running container:

```bash
docker logs mynginx
```

#### Step 9: Stop and Start the Container

Stop the container:

```bash
docker stop mynginx
```

Start the container:

```bash
docker start mynginx
```

#### Step 10: Remove the Container

Remove the container once you are done:

```bash
docker rm mynginx
```

### Summary of Commands

```bash
# Install Docker (Ubuntu)
sudo apt-get update
sudo apt-get install -y docker.io

# Install Docker (CentOS)
sudo yum update -y
sudo yum install -y docker

# Start Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Add user to Docker group
sudo usermod -aG docker $USER

# Reboot the machine
sudo reboot

# Pull the nginx image
docker pull nginx

# Run the nginx container
docker run -d --name mynginx -p 80:80 nginx

# Inspect the container
docker inspect mynginx

# View container logs
docker logs mynginx

# Stop the container
docker stop mynginx

# Start the container
docker start mynginx

# Remove the container
docker rm mnginx
```

Following these steps, you can pull a Docker image from a public repository, run it as a non-root user, inspect its processes and ports, view logs, and manage the container lifecycle.