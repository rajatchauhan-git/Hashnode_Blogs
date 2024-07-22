---
title: "Docker Project for DevOps Engineers"
datePublished: Mon Jul 22 2024 17:39:02 GMT+0000 (Coordinated Universal Time)
cuid: clyx9ty2q00020alca84r0ced
slug: docker-project-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721669863967/159a76bb-f11b-4a03-8ecb-f674fc2a3494.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1721669879655/23b0dd3f-e58e-4123-8611-a52ce7788066.png
tags: docker, devops, containers, dockerfile, iamge, docker-images, dockerhub, 90daysofdevops, trainwithshubham

---

* Create a Dockerfile for a simple web application (e.g. a Node.js or Python app)
    
* Build the image using the Dockerfile and run the container
    
* Verify that the application is working as expected by accessing it in a web browser
    
* Push the image to a public or private repository (e.g. Docker Hub)
    

---

**Steps to set up the Project:**

* **Install Git**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668531906/77c9f028-910e-4b69-b296-3c5c2acad491.png align="center")

* **Install Docker engine**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668570790/1dd60689-2362-4718-a6cf-b679edd61a9e.png align="center")

* **Make a directory for your project**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668601075/44dd0147-8952-4d05-985e-2c23a49b40ec.png align="center")

* **Clone GitHub repository**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668657178/ee694b18-dd33-4507-a29c-c3ebcaf9fe2c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668668953/a0e6bd2e-2af1-43a3-8677-7fbfcb76c8bc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668681971/1828e6af-1ebe-471a-8161-170eb2b4b514.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668691095/42e9dbd7-cd90-405f-a896-9a3afcc7779c.png align="center")

**Docker File of our application**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668710874/f34ee3f7-836f-4fa9-835d-39452c5b1f79.png align="center")

**Breakdown of Dockerfile:**

* This line sets the base image to Python 3.11
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668757112/6e629839-019a-4ed3-bd95-7e135e64eb13.png align="center")

* Sets the working directory inside the container to /app.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668778579/98125276-fbec-4d83-a9cc-a5d9c59f526c.png align="center")

* It will copy all the source code from the local to the container
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668857998/86dc0fa0-4d0b-4458-a682-930783196cc7.png align="center")

* It will update pip and install the required dependencies.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668869599/d80d173e-3584-42b4-932e-0f69422737eb.png align="center")

* The command used to run the app.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668881329/0b16c039-d8a0-48ff-9679-437e5058d48a.png align="center")

**Build Docket image from Dockerfile**

* Building a Docker image is a crucial step in containerizing your Flask application.
    
* **It involves packaging your application and its dependencies into a single, portable image**.
    
* To build the Docker image, open a terminal and navigate to the directory containing your Dockerfile and application code.
    

Execute the following command:  
1.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668981309/4932d21d-e74b-4024-b05d-7de72c75c691.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721668995969/27a18ca7-a4e8-4c30-92d5-c32b8589f39e.png align="center")

2.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669007424/151fc735-d62f-4131-ab7c-17516fce5431.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669042218/bf359d40-0b85-4ce7-8b79-ec30b5e2b13b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669058904/7b9dc326-6122-45c4-8906-8b50f5430e2d.png align="center")

**Run the Docker image as a container**

* Once you have successfully built your Docker image, the next step is to run it as a container.
    
* This involves creating an instance of your image, a runnable environment for your Flask application.
    
* Execute the following command in the terminal:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669081035/0aa0b662-211e-4efb-be10-08226714350b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669093064/c47d2a8e-9854-41e0-a9aa-b037a5934d27.png align="center")

**Run the Flask Application on the browser**

* Goto &lt;public\_ip&gt;:host\_port
    
* [http://3.141.23.121:4000/](http://3.141.23.121:4000/)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669123470/712bba24-140c-49e0-9790-28b036e8112d.png align="center")

**API Response**

* [http://3.141.23.121:4000/api/status](http://3.141.23.121:4000/api/status)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669151133/1f9cae7d-005c-4bdf-b83a-3c23d01b14d6.png align="center")

**Stop Container:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669177528/812c090d-4a67-4b5d-afc8-a2751de5d658.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669184720/708d0b48-4796-402e-916a-b75a95d25a45.png align="center")

**Delete Container:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669202887/c9d332f6-3920-4792-b970-8c804d9c6a7d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669208849/b3f133f1-302b-4a92-8489-1abb4f5578ee.png align="center")

**Push the Docker image to Docker Hub**

* Log in to Docker Hub and create a repository
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669226408/a43be4a0-f9c7-45e4-b354-26b8a715b49a.png align="center")

* Use the below command to log in on the Ubuntu machine, from where you have to push the image on Docker Hub and provide your username and password.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669304396/60078db4-d03e-44c2-b83b-a7ba23a554d9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669317099/e6653e94-b69c-4c83-af74-de933cfaa24d.png align="center")

* Run below command to push the image
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669475468/421426af-0598-4aee-b7ba-c4a28f34769e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669481245/0406077e-32c1-4e53-a45a-fe585f508684.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721669486280/a1e569fa-1b21-4e91-9999-325be0ff052b.png align="center")