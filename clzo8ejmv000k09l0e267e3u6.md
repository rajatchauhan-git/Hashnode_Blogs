---
title: "Complete Jenkins CI/CD Project"
datePublished: Sat Aug 10 2024 14:28:51 GMT+0000 (Coordinated Universal Time)
cuid: clzo8ejmv000k09l0e267e3u6
slug: complete-jenkins-cicd-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723299977553/40c121d1-3a79-49de-8512-3cd626c16979.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723300085212/c5b9f6ba-8767-4630-b97d-ef6d76dfef83.png
tags: docker, github, webhooks, jenkins, docker-compose, 90daysofdevops, trainwithshubham, githubwebhook

---

## Task 1

1. Fork [this repository.](https://github.com/rajatchauhan-git/node-todo-cicd)
    
2. [Set up a connecti](https://github.com/LondheShubham153/node-todo-cicd.git)on between [your Jenkins j](https://github.com/LondheShubham153/node-todo-cicd.git)ob and your GitHub repository through GitHub Integration.
    
3. Learn about [GitHub WebHooks](https://betterprogramming.pub/how-too-add-github-webhook-to-a-jenkins-pipeline-62b0be84e006) [and ensure you](https://github.com/LondheShubham153/node-todo-cicd.git) have configured the [CI/CD setup](https://betterprogramming.pub/how-too-add-github-webhook-to-a-jenkins-pipeline-62b0be84e006).
    

## Solution:

### 1\. **Fork the Repository**

* **Step 1:** Go to the repository on GitHub that [you need to fork](https://github.com/rajatchauhan-git/node-todo-cicd).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723295375397/229d00bc-114d-4667-b201-0ce66f5f450d.png align="center")

* **Step 2:** Click the **Fork** button at the top-right of the repository page.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723295463552/a1c1c7ee-c526-4f50-b5fb-48bb6d469cf6.png align="center")

* **Step 3:** Choose your GitHub account as the destination for the fork.
    
* **Step 4:** Now, you will have a copy of the repository in your GitHub account.
    

### 2\. **Set Up GitHub Integration with Jenkins**

* **Step 1:** Install the necessary Jenkins plugins:
    
    * Navigate to **Manage Jenkins** &gt; **Manage Plugins**.
        
    * Under the **Available** tab, search for "GitHub Integration" and "Git" plugins, then install them.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723295611143/6d906a87-d207-40fe-8c7a-5837b634c698.gif align="center")

* **Step 2:** Create a new Jenkins job:
    
    * Go to **New Item** in Jenkins.
        
    * Select **Freestyle Project** and name it according to your project.
        
    * Under **Source Code Management**, select **Git**.
        
* **Step 3:** Configure the Git repository:
    
    * Paste the URL of your forked GitHub repository.
        
    * Under **Credentials**, add your GitHub credentials (username and personal access token).
        
* **Step 4:** Set up GitHub WebHooks for CI/CD:
    
    * Go to your forked repository on GitHub.
        
    * Navigate to **Settings** &gt; **Webhooks** &gt; **Add webhook**.
        
    * In the **Payload URL** field, add your Jenkins server URL followed by `/github-webhook/` (e.g., [`http://your-jenkins-url/github-webhook/`](http://your-jenkins-url/github-webhook/)).
        
    * Choose the events you'd like to trigger the webhook on (usually, `Push` and `Pull request` events).
        
    * Click **Add webhook**.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723297014623/28b41747-4694-4ffb-9bff-a906c563d87d.gif align="center")

---

### **What Are GitHub WebHooks?**

* * GitHub WebHooks are a way for GitHub to notify Jenkins (or any other system) about events in your repository, such as code pushes, pull requests, etc.
        
        \* When a specified event occurs, GitHub sends a POST request to the configured URL with data describing the event.
        
* **Why Are WebHooks Important in CI/CD?**
    
    * WebHooks enables the automatic triggering of Jenkins jobs based on changes in your GitHub repository, ensuring continuous integration and deployment without manual intervention.
        

---

### 3\. **Ensure CI/CD Setup is Configured**

* **Step 1:** Set up build triggers in Jenkins:
    
    * In your Jenkins job configuration, under **Build Triggers**, check the box for the **GitHub hook trigger for GITScm polling**.
        
* **Step 2:** Define build steps:
    
    * Add necessary build steps like shell scripts, Docker build, or deploying to a server based on your project’s requirements.
        
* **Step 3:** Set up post-build actions:
    
    * You can add actions like notifying team members, pushing artifacts, or deploying to staging/production environments.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723297527297/03333f85-44bc-47c2-b144-d4d9956f7f15.gif align="center")

---

## Task 2

1. In the "Execute Shell" section of your Jenkins job, run the application using Docker Compose.
    
2. Create a Docker Compose file for this project (a valuable open-source contribution).
    
3. Run the project and celebrate your accomplishment! 🎉
    

## Solution:

#### Step 1: **Create a Docker Compose File**

You'll need to create a `docker-compose.yml` file that defines the services required for your application. Here’s an example template:

```yaml
version: '3.9'

services:
  web:
    image: "trainwithshubham/node-app-batch-6:latest"
    ports:
      - "8000:8000"
```

#### Step 2: **Add the Docker Compose Command in Jenkins**

Now, you’ll configure Jenkins to run the application using Docker Compose.

1. **Open Jenkins** and navigate to your project.
    
2. **Configure the Jenkins Job**:
    
    * Go to the **Build** section.
        
    * Select the **Add Build step** and choose **Execute Shell**.
        
    * In the command box, enter the following:
        
    
    ```yaml
    docker compose up -d
    ```
    
    This command will run the services defined in your `docker-compose.yml` file in detached mode.
    
3. **Save the Configuration**.
    

#### Step 3: **Run the Project**

* **Trigger the Jenkins Job**: Run the Jenkins job you configured. Jenkins will execute the shell command to bring up your application services using Docker Compose.
    
* **Verify the Application**: Your application should run once the job is completed. You can verify it by accessing the application URL or checking the status of the Docker containers using:
    
    ```yaml
    docker ps
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723298362342/17c3fc2a-1477-499f-9e17-bd92ff121d5a.gif align="center")