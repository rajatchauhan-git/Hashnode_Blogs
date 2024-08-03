---
title: "Jenkins Freestyle Project for DevOps Engineers"
datePublished: Sat Aug 03 2024 20:09:40 GMT+0000 (Coordinated Universal Time)
cuid: clzekhvr1000909kzat7i63vm
slug: jenkins-freestyle-project-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722715641605/8102f72c-e6c8-4b6c-ae37-88266de718e1.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722715721948/1b914c2c-4ee2-4123-89a8-54bc5dd2a9bb.png
tags: docker, devops, jenkins, docker-compose, docker-images, 90daysofdevops, trainwithshubham, jenkins-pipeline

---

### Introduction

In the ever-evolving software development landscape, Continuous Integration (CI) and Continuous Delivery (CD) have become indispensable practices. These methodologies streamline the development process, enhance collaboration, and ensure high-quality software's rapid and reliable delivery. In this blog, we'll dive deep into CI/CD, explore build jobs in Jenkins, and walk through practical tasks involving Docker and Docker Compose.

### What is CI/CD?

#### Continuous Integration (CI)

Continuous Integration is a development practice that requires developers to integrate code into a shared repository several times a day. An automated build and automated tests verify each integration. The primary goals of CI are to:

* Detect and address bugs early.
    
* Simplify the integration process across development teams.
    
* Enhance software quality.
    
* Reduce the time required to release new features.
    

**Key Components of CI:**

1. **Central Code Repository:** Developers commit code changes frequently to a shared repository such as GitHub, Bitbucket, or GitLab.
    
2. **Automated Builds:** Tools like Jenkins, Travis CI, or CircleCI automate the process of compiling and building the code.
    
3. **Automated Testing:** Unit tests, integration tests, and other automated tests are executed to ensure the code is functional and bug-free.
    

#### Continuous Delivery (CD)

Continuous Delivery is an extension of Continuous Integration. It ensures that code changes are automatically prepared for a production release. CD involves rigorous automated testing in a staging environment that mimics production, ensuring that the software is always in a deployable state.

**Key Components of CD:**

1. **Automated Deployment:** Deployment scripts or tools like Jenkins, GitLab CI/CD, or AWS CodePipeline automate the release process.
    
2. **Staging Environment:** A staging environment identical to production is used to test the software before the final release.
    
3. **Automated Testing:** Integration tests, regression tests, and performance tests ensure the stability and performance of the software.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722682421791/4ada86b9-781e-4007-8dab-4aea020070e8.gif align="center")

### What Is a Build Job?

A build job in Jenkins represents the configuration for automating various tasks or steps in the software development lifecycle. These tasks can include:

* Gathering dependencies.
    
* Compiling code.
    
* Running tests.
    
* Archiving artifacts.
    
* Deploying applications to different environments.
    

**Types of Jenkins Build Jobs:**  

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722700552498/0de34020-f0b7-489c-ac80-b1cbedd6afe8.png align="center")

1. **Freestyle Projects:** Simple, flexible projects that allow a variety of build steps and post-build actions.
    
2. **Pipelines:** Scripted or declarative workflows that define the entire CI/CD process.
    
3. **Multi-Configuration Projects:** Useful for running the same job on different environments or configurations.
    
4. **Multibranch Pipelines:** Automatically create pipelines for each branch in your repository.
    
5. **Organization Folders:** Automatically manage jobs for a project or organization.
    

### What is a Freestyle Project?

A freestyle project in Jenkins is a type of project that provides a simple way to configure and run builds. It is highly flexible and can be used to perform a wide range of tasks. Here are some practical tasks you can accomplish with a Jenkins freestyle project:

### Tasks with Jenkins Freestyle Projects

#### Task 1: Build and Run a Docker Container

1. **Create an Agent for Your App:**
    
    * Ensure you have Docker installed on the Jenkins agent machine.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722701684560/8eaed35f-d67b-43f3-977a-0f027cad1611.png align="center")

1. **Create a New Jenkins Freestyle Project:**
    
    * Go to Jenkins dashboard and click on "New Item."
        
    * Enter a name for the project and select "Freestyle project."
        
2. **Configure the Build Steps:**
    
    * In the "Build" section, add a build step to run the Docker build command to build the image for the container:
        
        ```yaml
        docker build -t my-app-image .
        ```
        
    * Add another build step to run the Docker run command to start a container using the image created in the previous step:
        
        ```yaml
        docker run -d --name my-app-container my-app-image
        ```
        

### Output

```yaml
Started by user rajat chauhan
Running as SYSTEM
Building remotely on Jenkins-node (dev) in workspace /home/ubuntu/app/workspace/Docker Build
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /home/ubuntu/app/workspace/Docker Build/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/rajatchauhan-git/django-notes-app.git # timeout=10
Fetching upstream changes from https://github.com/rajatchauhan-git/django-notes-app.git
 > git --version # timeout=10
 > git --version # 'git version 2.34.1'
 > git fetch --tags --force --progress -- https://github.com/rajatchauhan-git/django-notes-app.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision 65f44c7f404f478427c53ecc26de9bf0e7f8392c (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 65f44c7f404f478427c53ecc26de9bf0e7f8392c # timeout=10
Commit message: "Update Jenkinsfile"
 > git rev-list --no-walk 65f44c7f404f478427c53ecc26de9bf0e7f8392c # timeout=10
[Docker Build] $ /bin/sh -xe /tmp/jenkins18156272903494791131.sh
+ docker build -t note-app:latest .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  8.399MB

Step 1/7 : FROM python:3.9
 ---> c83186e94709
Step 2/7 : WORKDIR /app/backend
 ---> Using cache
 ---> ece508785961
Step 3/7 : COPY requirements.txt /app/backend
 ---> Using cache
 ---> 900277fb90f9
Step 4/7 : RUN pip install -r requirements.txt
 ---> Using cache
 ---> 0a5dc0062b06
Step 5/7 : COPY . /app/backend
 ---> Using cache
 ---> bfc18df8fdfd
Step 6/7 : EXPOSE 8000
 ---> Using cache
 ---> e460fb1a4d4f
Step 7/7 : CMD python /app/backend/manage.py runserver 0.0.0.0:8000
 ---> Using cache
 ---> fe696bc6ac02
Successfully built fe696bc6ac02
Successfully tagged note-app:latest
+ docker run -d --name note-app note-app:latest
33a08826d2084c096c16431068550266598cf2ed88d0f501f816bbb729c5cd5c
Finished: SUCCESS
```

#### Task 2: Use Docker Compose with Jenkins

1. **Create a Jenkins Project for Docker Compose:**
    
    * Go to Jenkins dashboard and click on "New Item."
        
    * Enter a name for the project and select "Freestyle project."
        
2. **Configure the Build Steps:**
    
    * In the "Build" section, add a build step to run the Docker Compose up command to start multiple containers defined in the compose file:
        
        ```yaml
        docker-compose up -d
        ```
        
3. **Set Up a Cleanup Step:**
    
    * Add a post-build action to run the Docker Compose down command to stop and remove the containers defined in the compose file:
        
        ```yaml
        docker-compose down
        ```