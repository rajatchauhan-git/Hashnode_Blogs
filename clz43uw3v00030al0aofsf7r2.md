---
title: "Docker for DevOps Engineers"
datePublished: Sat Jul 27 2024 12:26:12 GMT+0000 (Coordinated Universal Time)
cuid: clz43uw3v00030al0aofsf7r2
slug: docker-for-devops-engineers-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722083109392/ebfe0f52-cf6b-46a2-982a-338c77b5bfaf.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722083165468/6df156f4-ebdd-407c-b8f2-0752c2644692.png
tags: docker, docker-network, docker-volume, 90daysofdevops, volume, trainwithshubham

---

Docker Compose is a powerful tool for managing multi-container Docker applications. It simplifies defining and running multi-container Docker applications by allowing you to use a single YAML file to configure all the services, networks, and volumes your application needs. In this blog post, we'll dive deeper into Docker Volumes and Docker Networks, and provide practical examples to help you understand how to leverage these features for effective containerized applications.

## **Introduction to Docker Volumes**

Docker Volumes provide a way to persist data generated by and used by Docker containers. Without volumes, data stored in a container is lost when the container is removed. Volumes solve this problem by storing data in a specific location on the host machine, separate from the container’s filesystem. This means the data persists even if the container is stopped or removed.

### **Benefits of Using Docker Volumes**

1. **Persistence:** Data stored in volumes persists even if the container is deleted.
    
2. **Sharing Data:** Multiple containers can access and share the same volume.
    
3. **Data Management:** Volumes can be managed independently from containers.
    
4. **Backup & Restore:** Volumes can be easily backed up and restored.
    

### **Creating and Using Docker Volumes**

Here’s how you can use Docker Volumes:

1. **Creating a Volume**
    
    ```yaml
    docker volume create my-volume
    ```
    
    This command creates a named volume called `my-volume`.
    
2. **Using a Volume with** `docker run`
    
    ```yaml
    docker run -d -v my-volume:/data --name my-container alpine
    ```
    
    In this command:
    
    * `-d` runs the container in detached mode.
        
    * `-v my-volume:/data` mounts the volume `my-volume` to the `/data` directory in the container.
        
3. **Listing Volumes**
    
    ```yaml
    dedocker volume ls
    ```
    
    This lists all volumes on your system.
    
4. **Inspecting a Volume**
    
    ```yaml
    dedocker volume inspect my-volume
    ```
    
    This command provides detailed information about the volume.
    
5. **Removing a Volume**
    
    ```yaml
    docker volume rm my-volume
    ```
    
    This removes the specified volume.
    

## **Introduction to Docker Networks**

Docker Networks allow you to create virtual networks for your containers, enabling them to communicate with each other and with the host machine. Networks are essential for setting up isolated environments for different applications or services while allowing them to interact.

### **Benefits of Using Docker Networks**

1. **Isolation:** Networks isolate container traffic, improving security.
    
2. **Service Discovery:** Containers on the same network can communicate using container names.
    
3. **Custom Network Configurations:** You can define network settings and controls for container communications.
    

### **Creating and Using Docker Networks**

1. **Creating a Network**
    
    ```yaml
    docker network create my-network
    ```
    
    This command creates a new network called `my-network`.
    
2. **Connecting Containers to a Network**
    
    ```yaml
    docker run -d --network my-network --name my-container1 alpine
    docker run -d --network my-network --name my-container2 alpine
    ```
    
    Both containers are connected and can communicate with each other using their container names.
    
3. **Listing Networks**
    
    ```yaml
    docker network ls
    ```
    
    This command lists all networks.
    
4. **Inspecting a Network**
    
    ```yaml
    docker network inspect my-network
    ```
    
    This provides detailed information about the network.
    
5. **Removing a Network**
    
    ```yaml
    docker network rm my-network
    ```
    
    This removes the specified network.
    

## **Task 1: Multi-Container Docker Compose File**

In this task, we will create a Docker Compose file that brings up a multi-container application with an application container and a database container.

### **Creating** `docker-compose.yml`

Here's a basic example of a `docker-compose.yml` file that defines a web application and a MySQL database:

```yaml
version: '3.8'

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    networks:
      - webnet

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: example
    networks:
      - webnet
    volumes:
      - dbdata:/var/lib/mysql

networks:
  webnet:

volumes:
  dbdata:
```

In this file:

* The `web` service uses the `nginx` image and maps port 8080 on the host to port 80 in the container.
    
* The `db` service uses the `mysql` image and set a root password.
    
* Both services are connected to the `webnet` network.
    
* The `db` service uses a named volume `dbdata` for persistent storage.
    

### **Commands to Manage the Multi-Container Application**

* **Start the Application:**
    
    ```yaml
    docker-compose up -d
    ```
    
    This command starts the containers defined in `docker-compose.yml` in detached mode.
    
* **Scale the Application:**
    
    ```yaml
    docker-compose up -d --scale web=3
    ```
    
    This command scales the `web` service to 3 replicas.
    
* **View Container Status:**
    
    ```yaml
    docker-compose ps
    ```
    
    This command shows the status of all containers.
    
* **View Logs:**
    
    ```yaml
    docker-compose logs web
    ```
    
    This command shows logs for the `web` service.
    
* **Stop and Remove Containers:**
    
    ```yaml
    docker-compose down
    ```
    
    This command stops and removes all containers, networks, and volumes defined in the `docker-compose.yml` file.
    

## **Task 2: Using Docker Volumes with Multiple Containers**

In this task, we will create two containers that share a volume and verify data consistency.

### **Creating Containers with Shared Volume**

1. **Run Containers with Shared Volume**
    
    ```yaml
    docker run -d --name container1 -v shared-volume:/data alpine
    docker run -d --name container2 -v shared-volume:/data alpine
    ```
    
    Both containers use the `shared-volume` volume mounted to the `/data` directory.
    
2. **Write Data to the Volume**
    
    ```yaml
    docker exec container1 sh -c "echo 'Hello from container1' > /data/message.txt"
    ```
    
    This command writes a message to a file inside the volume from `container1`.
    
3. **Read Data from the Volume**
    
    ```yaml
    docker exec container2 cat /data/message.txt
    ```
    
    This command reads the message from the file inside the volume from `container2`, verifying that both containers share the same data.
    
4. **List Volumes**
    
    ```yaml
    docker volume ls
    ```
    
    This command lists all volumes, including `shared-volume`.
    
5. **Remove the Volume**
    
    ```yaml
    docker volume rm shared-volume
    ```
    
    This command removes the volume when you are done.