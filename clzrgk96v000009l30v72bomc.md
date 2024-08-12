---
title: "Jenkins Agents"
datePublished: Mon Aug 12 2024 20:40:33 GMT+0000 (Coordinated Universal Time)
cuid: clzrgk96v000009l30v72bomc
slug: jenkins-agents
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723495146989/ac405156-e045-4650-aec1-4777cefc188f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723495205476/9cca2f49-8531-4d0b-9a60-159a42ad12ab.png
tags: linux, aws, jenkins, jenkins-devops, agent, jenkins-pipeline, jenkins-agent

---

Jenkins is a widely used open-source automation server that helps streamline the CI/CD pipeline by automating tasks related to building, testing, and deploying software. At the core of this architecture lies the **Jenkins master** (server), which orchestrates workflows, schedules jobs, monitors their status, and manages configurations. However, as the number of projects and jobs increases, a single Jenkins installation may become a bottleneck, requiring the need for **Jenkins agents** to offload tasks and enable distributed job execution.

In this blog, we will explore how to set up Jenkins agents on an AWS EC2 instance, establish a connection between the master and agent, and run Jenkins jobs on the newly created agent.

![](https://user-images.githubusercontent.com/115981550/215276859-fa140ab7-e905-41c9-8ae2-1eef577c5e72.png align="center")

---

### Jenkins Master (Server)

The Jenkins master server serves as the central control unit responsible for the overall orchestration of workflows defined in pipelines. It handles crucial tasks such as:

* **Scheduling Jobs:** The master determines when and how jobs should be executed.
    
* **Monitoring Job Status:** It keeps track of job execution and provides real-time feedback via the Jenkins UI.
    
* **Managing Configurations:** The master manages global settings, job configurations, plugins, and other essential aspects of Jenkins.
    

The master also hosts the Jenkins user interface (UI), the control node that delegates job execution to agents.

### Jenkins Agent

A Jenkins agent is a separate machine or container that carries out the tasks defined in Jenkins jobs. When a job is triggered on the master, the actual execution occurs on the assigned agent. Each agent is identified by a unique label, enabling the master to delegate jobs to the appropriate agent based on those labels.

For small teams or projects, a single Jenkins installation (master only) may suffice. However, as your CI/CD workload grows, you’ll need to scale by connecting the master to multiple agents. This setup allows for distributed job execution, improving build performance and resource utilization.

---

### Prerequisites

To set up an agent, you’ll need the following:

1. **A fresh Ubuntu 22.04 Linux installation** on the agent machine.
    
2. **Java** (the same version installed on the Jenkins master server) is installed on the agent.
    
3. **Docker** is installed on the agent machine to support containerized builds and deployments.
    
4. Proper permissions, rights, and ownership are set for Jenkins users on the agent machine.
    

**Note:** Ensure that the Java version on the agent matches the version on the Jenkins master server to avoid compatibility issues.

---

### Task 01: Create an Agent

#### Step 1: AWS EC2 Instance Setup

1. **Launch an EC2 Instance:**
    
    * Open the AWS Management Console and navigate to the EC2 dashboard.
        
    * Click on "Launch Instance" and select an Ubuntu 22.04 AMI.
        
    * Choose an appropriate instance type (e.g., `t2.micro` for testing or small-scale use).
        
    * Configure the instance details, including setting up security groups for SSH access (port 22).
        
    * Launch the instance and download the private key file (e.g., `xyz.pem`) to your local machine.
        
2. **Connect to the EC2 Instance:**
    
    * Use the following SSH command to connect to your EC2 instance:
        
        ```yaml
        ssh -i "xyz.pem" ubuntu@<ec2-public-ip>
        ```
        
    * Once connected, update the package list and install Java and Docker:
        
        ```yaml
        sudo apt update
        sudo apt install openjdk-11-jdk docker.io -y
        ```
        
    * Verify the installation:
        
        ```yaml
        java -version
        docker --version
        ```
        

#### Step 2: Create a New Node in Jenkins

1. **Access the Jenkins Master UI:**
    
    * Log in to your Jenkins master server’s web interface.
        
2. **Add a New Node:**
    
    * Navigate to `Manage Jenkins` &gt; `Manage Nodes and Clouds` &gt; `New Node`.
        
    * Enter a name for the agent (e.g., `aws-agent`) and select "Permanent Agent."
        
    * Configure the agent settings as follows:
        
        * **Remote root directory:** `/home/ubuntu/jenkins`
            
        * **Labels:** Assign labels such as `linux`, `docker`, or `aws-agent` based on the agent's role.
            
        * **Launch method:** Select `Launch agents via SSH`.
            
        * **Host:** Enter the public IP of your EC2 instance.
            
        * **Credentials:** Add the SSH credentials by using the private key file (`jenkins-agent.pem`).
            
    * Save the configuration.
        

#### Step 3: Establishing the Master-Agent Connection

1. **Set Up SSH Connection:**
    
    * Ensure the Jenkins master can securely connect to the agent via SSH using the following command:
        
        ```yaml
        ssh -i "xyz.pem" ubuntu@<ec2-public-ip>
        ```
        
    * If the connection is successful, Jenkins will establish a link to the agent node.
        
2. **Verify the Agent’s Status:**
    
    * In the Jenkins UI, navigate to `Manage Jenkins` &gt; `Manage Nodes and Clouds`.
        
    * The agent should appear in the "Nodes" section with a green indicator, showing that it is connected and ready to execute jobs.
        

---

### Task 02: Run Previous Jobs on the New Agent

With the agent successfully set up and connected to the master, you can now configure Jenkins jobs to run on the new agent.

#### Step 1: Labeling the Agent

1. **Assign Labels to the Agent:**
    
    * In the Jenkins UI, go to `Manage Jenkins` &gt; `Manage Nodes and Clouds` and select the agent.
        
    * Add labels to the agent, such as `aws-agent` or `docker`, based on the types of jobs you want it to handle.
        
2. **Configure Jobs to Use the Agent:**
    
    * Open the configuration page of the Jenkins jobs you built on Day 26 and Day 27.
        
    * In the "Restrict where this project can be run" section, enter the label assigned to the agent (e.g., `aws-agent`).
        

#### Step 2: Running Jobs on the Agent

1. **Trigger the Jobs:**
    
    * Manually trigger the Jenkins jobs to verify that they execute on the new agent.
        
    * Jenkins will delegate the job execution to the agent, ensuring that the tasks run on the designated machine.
        
2. **Monitor Job Execution:**
    
    * Check the console output of the jobs to ensure they are running on the intended agent.
        
    * Verify that the jobs are completed successfully without any errors related to the master-agent setup.