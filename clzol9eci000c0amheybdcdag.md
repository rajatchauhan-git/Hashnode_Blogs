---
title: "Jenkins Declarative Pipeline with Docker"
datePublished: Sat Aug 10 2024 20:28:46 GMT+0000 (Coordinated Universal Time)
cuid: clzol9eci000c0amheybdcdag
slug: jenkins-declarative-pipeline-with-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723305567909/39d0d5ff-adb5-44f1-ac14-d553367d8f6a.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723321568593/c1293c50-92ad-41e3-b0d1-36362cd1de93.png
tags: docker, devops, jenkins, dockerfile, docker-compose, docker-images, devops-articles, jenkins-devops, docker-network, devops-journey, jenkins-on-ubuntu, jenkins-pipeline, devopscommunity, declarative-pipeline

---

Jenkins is a widely-used tool for continuous integration and continuous delivery (CI/CD), and Docker provides a streamlined way to develop, ship, and run applications in containers. Integrating Docker with Jenkins enhances automation and consistency in your CI/CD workflows. In this blog, we'll dive deep into how to create a Docker-integrated Jenkins declarative pipeline, utilizing both shell commands and Groovy Docker syntax, and handling potential issues that arise when running jobs multiple times.

### 1\. Introduction

Continuous integration and deployment are critical aspects of modern software development. Jenkins, an open-source automation server, excels in automating these processes. Docker, with its containerization technology, complements Jenkins by encapsulating applications and their dependencies into portable containers. This blog will guide you through setting up a Jenkins pipeline that integrates Docker, providing examples and best practices for building and running Docker containers.

### 2\. Setting Up the Jenkins Declarative Pipeline

Jenkins declarative pipelines offer a structured and readable way to define your CI/CD workflows. Below are the steps to configure a basic Docker-integrated Jenkins pipeline using shell commands and Groovy Docker syntax.

# Task-01

* Create a docker-integrated Jenkins declarative pipeline
    
* Use the above-given syntax using `sh` inside the stage block
    
* You will face errors in case of running a job twice, as the docker container will be already created, so for that do task 2
    

#### 2.1 Using Shell Commands

In Jenkins declarative pipelines, you can use the `sh` step to execute shell commands. This approach is straightforward but might lead to issues when running jobs multiple times, especially if containers or images already exist.

**Pipeline Configuration with Shell Commands:**

```yaml
pipeline{

    agent any{

    stages{
        stage("code"){
            steps{
                git url: "https://github.com/rajatchauhan-git/node-todo-cicd", branch: "master"
                echo "code cloned sucessfully"

            }

        }
        stage("build"){
            steps{
                sh 'docker build -t node-app:latest .'
                echo "code build successfully"

            }
        }
        stage("Push to Private Docker Hub Repo"){
            stpes{
                withCredentials([usernamePassword(credentialsId:"DockerCreds",passwordVariable:"dockerPass", usernameVariable:"dockerUser")]){
                sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                sh "docker tag node-app:latest ${env.dockerUser}/node-app:latest"
                sh "docker push ${env.dockerUser}/node-app:latest"
                echo "Docker Image Pushed successfully"
                }
            }

        }
        stage("deploy"){
            steps{
                sh "docker-compose up -d"
                echo "Node-app deployed Sucessfully"

            }
            }

        }
    }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723321374889/32834ca1-8004-4d80-b97b-a034cdf11609.gif align="center")

# Task-02

* Create a docker-integrated Jenkins declarative pipeline using the `docker` groovy syntax inside the stage block.
    
* You won't face errors, you can Follow [this docume](https://tempora-mutantur.github.io/jenkins.io/github_pages_test/doc/book/pipeline/docker/)[ntation](https://tempora-mutantur.github.io/jenkins.io/github_pages_test/doc/book/pipeline/docker/)
    
* [Complete your prev](https://tempora-mutantur.github.io/jenkins.io/github_pages_test/doc/book/pipeline/docker/)ious projects using this Declarative pipeline approach
    

#### 2.2 Using Docker Groovy Syntax

Jenkin[s provides a `docke`](https://tempora-mutantur.github.io/jenkins.io/github_pages_test/doc/book/pipeline/docker/)`r` directive in the pipeline DSL, offering [a more integrated](https://tempora-mutantur.github.io/jenkins.io/github_pages_test/doc/book/pipeline/docker/) approach to manage Docker containers. This method helps handle errors and avoid common issues more gracefully.

**Pipeline Configuration with Docker Groovy Syntax:**

```yaml
pipeline {
    agent any

    stages {
        stage("code") {
            steps {
                git url: "https://github.com/rajatchauhan-git/node-todo-cicd", branch: "master"
                echo "code cloned successfully"
            }
        }

        stage("build") {
            steps {
                sh 'docker build -t node-todo-app:latest .'
                echo "code build successfully"
            }
        }

        stage("Push to Private Docker Hub Repo") {
            steps {
                withCredentials([usernamePassword(credentialsId:"DockerCreds",passwordVariable:"dockerPass", usernameVariable:"dockerUser")]) {
                    sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                    sh "docker tag node-todo-app:latest ${env.dockerUser}/node-todo-app:latest" // Corrected image name
                    sh "docker push ${env.dockerUser}/node-todo-app:latest" // Corrected image name
                    echo "Docker Image Pushed successfully"
                }
            }
        }

        stage("deploy") {
            steps {
                sh "docker-compose up -d" // Make sure docker-compose is installed and config is correct
                echo "Node-app deployed successfully"
            }
        }
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723321380924/1e2810f9-aa21-4986-aaa2-c2edc0e60f4a.gif align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723321493650/9e248f07-9be7-4287-adcb-bc8e765814b3.png align="center")

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">If you need help or have any questions, just leave them in the comments! 📝 I would be happy to answer them!</div>
</div>

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">If you found this post useful, please give it a thumbs up 👍 and consider following for more helpful content. 😊</div>
</div>

### Thank you for taking the time to read! 💚