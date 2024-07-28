---
title: "Difference between declarative and scripted pipeline"
datePublished: Sun Jul 28 2024 15:44:42 GMT+0000 (Coordinated Universal Time)
cuid: clz5qe04f000209lafec17ji3
slug: difference-between-declarative-and-scripted-pipeline
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722181222541/4480df65-20e8-47fe-8786-c3b2281bf452.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1722181424644/bbd82dc0-589d-4981-bc9b-ec0796f9c2d8.png
tags: linux, devops, jenkins, pipeline, 90daysofdevops, declarative-pipeline, scripted-pipeline

---

In Jenkins, the terms "declarative" and "script" refer to two different types of syntax for defining Jenkins pipelines. Here’s a breakdown of each:

### Declarative Pipeline

**Declarative Pipeline** syntax is a more structured and simplified way to define Jenkins pipelines. It uses a domain-specific language (DSL) that is designed to be more readable and easier to understand. It’s built on top of the Pipeline DSL and offers a more user-friendly experience, especially for those who may not be as familiar with Groovy scripting.

**Key Features:**

* **Structured Format**: It uses a predefined structure and syntax. For example, it defines stages, steps, and other elements in a more organized manner.
    
* **Simplified Syntax**: The declarative syntax is more concise and less error-prone.
    
* **Built-in Features**: It provides built-in support for common pipeline features like environment variables, tools, and post-build actions.
    
* **Validation**: The declarative syntax is validated before the pipeline runs, which helps catch errors early.
    

**Example:**

```yaml
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
    post {
        always {
            echo 'This will always run after the pipeline completes.'
        }
    }
}
```

### Scripted Pipeline

**Scripted Pipeline** syntax provides more flexibility but is also more complex. It’s essentially a Groovy script that defines the pipeline using a more traditional programming approach. This syntax allows for greater control and customization but requires a deeper understanding of Groovy and Jenkins internals.

**Key Features:**

* **Flexibility**: Allows for more complex logic and custom behavior.
    
* **Groovy Script**: The entire pipeline is defined using Groovy code, which can include loops, conditionals, and other programming constructs.
    
* **Manual Control**: You have full control over the pipeline execution and can define steps in any way you choose.
    

**Example:**

```yaml
node {
    stage('Build') {
        echo 'Building...'
    }
    stage('Test') {
        echo 'Testing...'
    }
    stage('Deploy') {
        echo 'Deploying...'
    }
    post {
        always {
            echo 'This will always run after the pipeline completes.'
        }
    }
}
```

### Comparison

* **Readability**: Declarative pipelines are generally easier to read and maintain due to their structured format. Scripted pipelines can be harder to understand, especially for those unfamiliar with Groovy.
    
* **Complexity**: Scripted pipelines offer more flexibility and can handle more complex scenarios but may become cumbersome for simpler tasks.
    
* **Error Handling**: Declarative pipelines often provide better error handling and validation before execution compared to scripted pipelines.
    
* **Customization**: Scripted pipelines allow for more granular control and customization, which can be useful for advanced use cases.
    

---

Follow me:

[LinkTree](https://linktr.ee/chauhanrajat.work)