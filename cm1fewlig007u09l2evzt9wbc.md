---
title: "Multi-Stage Docker Build"
datePublished: Mon Sep 23 2024 19:40:20 GMT+0000 (Coordinated Universal Time)
cuid: cm1fewlig007u09l2evzt9wbc
slug: multi-stage-docker-build
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727119788637/7f1c30a5-6072-4f85-ac43-75a748acab20.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1727120411999/621d75a6-517f-4163-ae03-b3680e41b9f9.png
tags: docker, dockerfile, cka, docker-images, multistage-docker-build, 40daysofkubernetes

---

Containerization has become a critical part of modern application development and deployment workflows. Docker allows developers to package their applications, including all dependencies, into a portable image. One of the best practices in Dockerfile creation is using **multistage builds**, which helps in creating lightweight, production-ready images. In this blog, we will walk through the process of containerizing a Node.js ToDo app using Docker, while following Dockerfile best practices.

#### Benefits of Docker Multistage Builds:

1. **Reduced Image Size**: Multistage builds allow you to separate the build environment from the runtime environment. This means that all build dependencies, source code, and other large assets can be excluded from the final image, significantly reducing its size.
    
2. **Improved Security**: By eliminating unnecessary files and dependencies, you reduce the attack surface of your containers. Only the minimal set of files needed to run the application is included in the final image.
    
3. **Simplified Build Process**: Multistage builds allow you to define multiple stages in a single Dockerfile, improving maintainability. This simplifies the build process by consolidating everything into one file.
    
4. **Environment Optimization**: By separating stages, you can use different base images to build and run your application. For example, you might use a full Node.js image to build your app but switch to an optimized Nginx image to serve the built files.
    

#### Best Practices for Writing Dockerfiles:

Before we dive into the technical steps, here are some **best practices** when creating a Dockerfile to ensure efficient, secure, and maintainable Docker images:

* **Use Official Images**: Start from minimal, official base images, such as `alpine` or specific language runtime images like `node:alpine`, to minimize vulnerabilities and unnecessary software.
    
* **Leverage Docker’s Layer Caching**: Order your `RUN`, `COPY`, and `ADD` commands wisely. Docker caches each layer, so placing commands that change frequently (like copying the source code) near the end will help leverage caching and speed up builds.
    
* **Minimize Layers**: Each `RUN`, `COPY`, and `ADD` the command creates a new layer in the image. To optimize image size, combine multiple commands into a single `RUN` instruction when possible.
    
* **Exclude Unnecessary Files**: Use `.dockerignore` to exclude files and directories that are not needed in the container, such as local development files, `node_modules` (if building in a multistage), or configuration files.
    
* **Use Multi-Stage Builds**: As discussed earlier, multistage builds allow for separate build and deployment stages, resulting in smaller, more secure images.
    

Now that we’ve covered the benefits and best practices, let’s dive into containerizing our Node.js application.

---

#### Step 1: Clone the Application Repository

We’ll start by cloning a sample ToDo app repository, which has a simple Node.js web application. You can use the one linked below or any other Node.js application of your choice.

```yaml
git clone https://github.com/piyushsachdeva/todoapp-docker.git
cd todoapp-docker/
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727119947265/8b6e6a0d-4d22-4f12-bebd-2f08805167ee.png align="center")

#### Step 2: Create a Dockerfile

Now, we’ll create a Dockerfile. A Dockerfile contains instructions to build a Docker image. In this file, we’ll specify how to set up the environment for our application.

```yaml
touch Dockerfile
```

Open the `Dockerfile` in your favorite text editor (e.g., `nano`, `vim`, or Visual Studio Code), and paste the following content:

```yaml
# Stage 1: Build the application
FROM node:18-alpine AS installer
WORKDIR /app
COPY package*.json ./
RUN npm install 
COPY . .
RUN npm run build

# Stage 2: Run the application using Nginx
FROM nginx:latest AS deployer
COPY --from=installer /app/build /usr/share/nginx/html
```

##### Explanation:

1. **First Stage (installer):**
    
    * We are using the `node:18-alpine` image, which is a lightweight Node.js image.
        
    * The `WORKDIR` the command sets the working directory inside the container to `/app`.
        
    * The `COPY package*.json ./` copies both the `package.json` and `package-lock.json` files from the host system to the `/app` directory in the container.
        
    * The `RUN npm install` the command installs the necessary dependencies.
        
    * The `COPY . .` the command copies the entire project to the `/app` directory.
        
    * The `RUN npm run build` command builds the production-ready version of the application.
        
2. **Second Stage (deployer):**
    
    * We are using the `nginx:latest` image to serve our static files.
        
    * The `COPY --from=installer /app/build /usr/share/nginx/html` command copies the built application from the first stage into the Nginx container’s HTML directory, which serves the web application.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120000147/1e584857-58b2-4cc5-b787-9b2f5a3741d5.png align="center")

#### Step 3: Build the Docker Image

Now, let’s build the Docker image using the `docker build` command.

```yaml
docker build -t todoapp-docker .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120035351/9271b76a-b16b-47f6-b9ce-c5ccd2697e7c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120081861/c8c4963e-a763-42dd-a1e1-ba8b80fba6a6.png align="center")

This command creates an image with the tag `todoapp-docker`. The `-t` option is used to name the image, and the `.` at the end refers to the current directory, which contains the Dockerfile and the application code.

#### Step 4: Verify the Docker Image

Once the image is built, you can verify that it’s created and stored locally by running:

```yaml
docker images
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120100409/74fc4b02-fae6-4a43-9ea6-61c16ec12ba1.png align="center")

This command lists all the images present on your local Docker environment.

#### Step 5: Push the Image to Docker Hub

To share the image with others or deploy it to different environments, you can push the Docker image to a public repository on Docker Hub. First, login to Docker Hub using:

```yaml
docker login
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120116038/923f6380-595a-4144-8542-ae8dc8b9e770.png align="center")

Once logged in, tag the image so that it can be pushed to your Docker Hub account.

```yaml
docker tag todoapp-docker:latest chauhanrajat/test-repo:todoapp-docker
```

Now, push the image to your Docker Hub repository:

```yaml
docker push chauhanrajat/test-repo:todoapp-docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120192719/c80fb584-e457-4fa8-ae31-5938c6e692b4.png align="center")

#### Step 6: Pull the Image on Another Environment

To pull this Docker image from another environment or machine, use the `docker pull` command:

```yaml
docker pull chauhanrajat/test-repo:todoapp-docker
```

#### Step 7: Run the Docker Container

To start a container from the Docker image and expose it on port 3000, run the following command:

```yaml
docker run -dp 3000:80 chauhanrajat/test-repo:todoapp-docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120222992/b4b53911-72ca-440d-8b05-580af3b2011e.png align="center")

This command maps port 80 inside the container to port 3000 on the host system.

#### Step 8: Verify the Application

If you’ve followed the steps correctly, your app should now be accessible via [`http://localhost:3000`](http://localhost:3000). Open a browser and navigate to that URL to see the ToDo app running inside the Docker container.

#### Step 9: Accessing the Running Container

To enter into the running container, use the `docker exec` command:

```yaml
docker exec -it containername sh
```

You can also use the container ID instead of the container name.

#### Step 10: Viewing Docker Logs

To view the logs generated by the container, you can use the following commands:

```yaml
docker logs containername
# or
docker logs containerid
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120296796/83b45f89-ef06-42ef-af28-42bcfe799d82.png align="center")

#### Step 11: Inspecting the Container

To inspect the details of the container, such as its IP address, volumes, or network settings, use:

```yaml
docker inspect containername
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1727120264181/b65740b7-eb1b-421e-815b-92b015c0f3d4.png align="center")

#### Step 12: Clean Up Old Docker Images

Over time, old Docker images can pile up and take up space. You can remove unused images using the following command:

```yaml
docker image rm image-id
```

You can get the image ID by running `docker images` and removing the ones you no longer need.

---

> ***💡 If you need help or have any questions, just leave them in the comments! 📝 I would be happy to answer them!***
> 
> ***💡 If you found this post useful, please give it a thumbs up 👍 and consider following for more helpful content. 😊***

### **Thank you for taking the time to read! 💚**