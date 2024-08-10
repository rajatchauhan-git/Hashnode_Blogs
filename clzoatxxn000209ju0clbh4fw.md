---
title: "Jenkins Declarative Pipeline"
datePublished: Sat Aug 10 2024 15:36:49 GMT+0000 (Coordinated Universal Time)
cuid: clzoatxxn000209ju0clbh4fw
slug: jenkins-declarative-pipeline
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723304108697/5b81f31c-d736-4332-a36b-d9433d080be4.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723304197425/14ed18bd-eade-4d38-965b-b4164e29a8f0.png
tags: trends, devops, jenkins, trending, pipeline, devops-articles, declarative, devops-journey, devopscommunity, declarative-pipeline

---

**1\. What is a Pipeline?**

A **pipeline** in Jenkins is a collection of steps or jobs that are interlinked in a sequence to automate the process of building, testing, and deploying software. Pipelines provide a robust way to manage continuous integration and continuous delivery (CI/CD) workflows, allowing teams to define complex processes in a simple, automated fashion.

**2\. Declarative Pipeline**

The **declarative pipeline** is a more recent and advanced implementation of pipeline-as-code in Jenkins. It is structured, making it easier to read and write, especially for beginners or those who prefer a more formal syntax. The declarative pipeline is built with a specific syntax that simplifies the creation and management of pipelines by providing a clear structure with predefined sections and stages.

**3\. Scripted Pipeline**

The **scripted pipeline** was the first and most traditional implementation of pipeline-as-code in Jenkins. It was designed as a general-purpose DSL (Domain Specific Language) built with Groovy. Although it offers more flexibility and control, it requires a deeper understanding of Groovy scripting and is less structured compared to the declarative pipeline.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723302900152/5cc48528-3323-4e77-b8e2-46198c777971.png align="center")

### Why You Should Use a Pipeline

The definition of a Jenkins Pipeline is written into a text file called a **Jenkinsfile**, which can be committed to a project’s source control repository. This is the foundation of "Pipeline-as-code," treating the CD pipeline as part of the application, which can be versioned and reviewed like any other code.

Creating a Jenkinsfile and committing it to source control provides several immediate benefits:

* **Automatic Pipeline Creation**: A pipeline build process is automatically created for all branches and pull requests, streamlining CI/CD workflows.
    
* **Code Review and Iteration**: The pipeline code can be reviewed and iterated along with the remaining source code, ensuring quality and consistency across the entire project.
    

### Pipeline Syntax

Below is an example of a basic declarative pipeline syntax:

```yaml
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Add build steps here
            }
        }
        stage('Test') {
            steps {
                // Add test steps here
            }
        }
        stage('Deploy') {
            steps {
                // Add deploy steps here
            }
        }
    }
}
```

This pipeline is divided into stages: **Build**, **Test**, and **Deploy**. Each stage contains steps that define the tasks to be executed.

---

### Task: Creating a Jenkins Pipeline

**Task-01: Create a New Job Using a Pipeline**

1. **Create a New Job**: Start by creating a new job in Jenkins, selecting "Pipeline" instead of "Freestyle Project."
    
2. **Follow the Official Jenkins "Hello World" Example**: Jenkins provides an official "Hello World" example using a pipeline. You can follow this example to understand the basics of how pipelines work.
    
3. **Complete the Example Using the Declarative Pipeline**: Implement the example using the declarative pipeline syntax. This will help you get hands-on experience with the pipeline's structure and functionality.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723303938520/52afc18e-f36a-4a70-9a50-c955226d98ae.gif align="center")

By following these steps, you'll gain a solid understanding of Jenkins pipelines and how to integrate them into your CI/CD processes effectively.