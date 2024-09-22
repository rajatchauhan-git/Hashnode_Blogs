---
title: "Dockerize a Project"
datePublished: Sun Sep 22 2024 12:44:42 GMT+0000 (Coordinated Universal Time)
cuid: cm1dkm848000i09mhbjeh3t6q
slug: dockerize-a-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727008182144/9e0883ca-7470-47cd-8b83-60063d0c8ca7.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1727009071253/0aa23e6e-1282-43f4-aea6-d9b3f0c5b2b4.png
tags: docker, cka, docker-images, docker-container, CKA-Exam-Objectives-Pdf, 40daysofkubernetes

---

### **1\. What is Docker?**

**Docker** is a platform designed to create, deploy, and run applications using containers. Containers allow developers to package applications with all necessary dependencies, ensuring they run seamlessly in any environment.

### **2\. Why Dockerize an Application?**

* **Consistency**: Docker eliminates the "works on my machine" issue.
    
* **Portability**: Docker containers can be moved across different environments.
    
* **Scalability**: Docker integrates easily with orchestration tools like Kubernetes.
    

By Dockerizing your application, you ensure it can run in any environment, be it local development, testing, or production, without configuration issues.

---

### **3\. Cloning the Repository**

First, clone your project repository from GitHub. If you don’t have a project, you can use an existing app from GitHub.

```yaml
git clone https://github.com/docker/getting-started-app.git
cd getting-started-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008364504/cb44eb17-b3ae-48e0-b426-ae0ef93da34c.png align="center")

---

### **4\. Exploring** `docker init` Command

Docker recently introduced a new command called `docker init` to generate Docker-related files (like `Dockerfile`, `.dockerignore`, etc.) automatically. This command simplifies the initial setup of Dockerization.

Run the following command in the project directory:

```yaml
docker init
```

This will prompt Docker to analyze the project and auto-generate the **Dockerfile**. You can then modify the file if needed, but the generated Dockerfile usually serves as a great starting point.

If `docker init` is not available, you can manually create the Dockerfile, which we’ll cover next.

---

### **5\. Creating a Dockerfile**

The **Dockerfile** is a script that contains instructions on how to build a Docker image for your application. Below is a simple Dockerfile for a Node.js project.

```yaml
#base image
FROM node:18-alpine
​
#workind Dir
WORKDIR /app
​
#copy code into contaioner
COPY . .
​
#compile code
RUN yarn install --production
​
#run
CMD ["node" , "src/index.js"]
​
#expose port
EXPOSE 3000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008387979/d362c705-f0d1-4c58-92a1-ed0342d83981.png align="center")

#### **1\.** `FROM node:18-alpine`

This line defines the **base image** for your Docker container. You're using `node:18-alpine`, a lightweight version of Node.js 18 based on the **Alpine Linux** distribution. The Alpine image is smaller in size, making the Docker image more efficient and faster to build and deploy.

* **Why Alpine?**: It’s minimal and has a reduced attack surface, which improves security.
    
* **Why Node.js 18?**: This specifies that your container will run with Node.js version 18.
    

#### **2\.** `WORKDIR /app`

This command sets the **working directory** inside the container to `/app`. It means that any subsequent commands (like `COPY` or `RUN`) will be executed inside this directory.

* **Purpose**: This ensures that your application files will be copied and run in a specific, isolated directory inside the container. This also helps prevent file clashes in other parts of the container.
    

#### **3\.** `COPY . .`

This command copies the content of your project’s root directory (on your host machine) into the working directory inside the container (`/app`).

* **First dot (.)**: Refers to the current directory on your **host machine** (where the Dockerfile is located).
    
* **Second dot (.)**: Refers to the current directory inside the **container** (`/app` in this case).
    

#### **4\.** `RUN yarn install --production`

This command **runs** the `yarn install --production` command inside the container. This installs the necessary **dependencies** for the application.

* `yarn install --production`: It installs only the production dependencies listed in the `package.json` file. Development dependencies are not installed, which reduces the container's size and increases its security.
    
* **Why** `yarn install` and not `npm install`?: Yarn is another package manager for JavaScript, like npm, and it’s used if your project setup includes Yarn. It offers performance benefits like faster dependency resolution and deterministic installs.
    

#### **5\.** `CMD ["node", "src/index.js"]`

This line specifies the **default command** that will be executed when the container starts.

* `CMD ["node", "src/index.js"]`: It tells Docker to run Node.js, and specifically execute the `index.js` file located in the `src` folder. This is usually the main entry point of your application.
    

#### **6\.** `EXPOSE 3000`

This command **informs Docker** that the container will listen on **port 3000** at runtime.

* **Port 3000**: This is the typical port used for Node.js applications. Exposing this port allows external traffic to communicate with your app when the container is running.
    

---

### **6\. Building an Image using Dockerfile**

```yaml
docker build -t day02-todo .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008486306/4af094a6-d834-431d-ab55-6bb522125f97.png align="center")

---

### **7\. Check docker images**

```yaml
docker images
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008533489/99a01074-5360-4816-90e2-1c9505dd908e.png align="center")

---

### **8\. Pushing the Docker Image to Docker Hub**

Once your Docker image is built and tested locally, you can share it with others by pushing it to **Docker Hub**. Follow these steps to log in to Docker Hub and push your image.

#### **Step 1: Log in to Docker Hub**

Before you can push your image, log in to your Docker Hub account. If you don't have an account, you can create one at Docker Hub.

Run the following command in your terminal:

```yaml
docker login
```

You will be prompted to enter your **Docker Hub username** and **password**. After entering your credentials, you should see a message confirming that the login was successful:

```yaml
Login Succeeded
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008782112/1f9e83d9-e82b-4857-8c86-223ef3502a65.png align="center")

#### **Step 2: Tag the Image**

Next, you need to tag your image so that Docker knows where to push it on Docker Hub. Use the following command to tag the image:

```yaml
docker tag day02-todo:latest chauhanrajat/test-repo:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008807399/202bf3c2-6619-4e7a-829f-c92a796cea09.png align="center")

#### **Step 3: Push the Image**

Now that the image is tagged, you can push it to Docker Hub:

```yaml
 docker push chauhanrajat/test-repo:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008847961/1f937fd3-a090-4dc6-a879-254710301112.png align="center")

Docker will begin uploading the image to Docker Hub. Once the process is complete, you should see the image listed in your Docker Hub account under "Repositories."

#### **Step 4: Pull and Run the Image**

Now that your image is available on Docker Hub, anyone can pull and run it using the following commands:

```yaml
 docker pull chauhanrajat/test-repo:latest
 docker run -dp 3000:3000 chauhanrajat/test-repo:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008873049/57fc346d-d6ed-4b4c-853f-81ef63832136.png align="center")

This will pull the image from Docker Hub and run the container on **port 3000**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008890052/80615024-023b-4d2c-aa3a-b01e7b8b9aa3.png align="center")

#### **Step 5: Check the running container**

```yaml
 docker ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008916984/6c768c29-6f9c-49cb-8174-39e7b6a431b3.png align="center")

---

### **9\. Enter into a running container**

```yaml
docker exec -it reverent_poitras sh
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727008973127/90815354-6a6c-4d16-83b3-b1c89ba2baa1.png align="center")

---

> ***💡 If you need help or have any questions, just leave them in the comments! 📝 I would be happy to answer them!***
> 
> ***💡 If you found this post useful, please give it a thumbs up 👍 and consider following for more helpful content. 😊***

### **Thank you for taking the time to read! 💚**