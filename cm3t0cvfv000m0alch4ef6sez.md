---
title: "What is Kubernetes - Kubernetes Architecture Explained ☸️"
datePublished: Fri Nov 22 2024 17:21:16 GMT+0000 (Coordinated Universal Time)
cuid: cm3t0cvfv000m0alch4ef6sez
slug: what-is-kubernetes-kubernetes-architecture-explained
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1732295963104/e7547c3b-2dd6-4692-a10b-9580d5e8d326.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1732296070021/e751f805-5758-4390-8774-c39390aa3be3.png
tags: kubernetes, devops, k8s, devops-articles, devops-trends, devops-journey, kubernetes-architecture, devopscommunity, 40daysofkubernetes

---

1. ### **Kubernetes Architecture:**[*https://chauhanrajatwork.hashnode.dev/kubernetes-architecture*](https://chauhanrajatwork.hashnode.dev/kubernetes-architecture)
    
2. ### **What Happens When You Run a** `kubectl` Command?
    
    `kubectl` is the Kubernetes command-line tool that allows users to interact with the Kubernetes cluster. Below is the flow of events that occur when you run a `kubectl` command:
    
    1. **Command Execution**: When you run a `kubectl` command, the tool first reads the Kubernetes configuration file (typically located at `~/.kube/config`) to locate the correct cluster and authentication details.
        
    2. **API Request**: `kubectl` sends a REST request to the Kubernetes API server. This request could be to fetch data (e.g., `kubectl get pods`) or to perform a specific action (e.g., `kubectl create deployment`).
        
    3. **Authentication & Authorization**: The API server authenticates the request (validating the user's identity) and authorizes whether the user has permission to execute the requested action.
        
    4. **Controller Manager Interaction**: If the request involves a state change (e.g., creating a pod or deploying an application), the API server communicates with the relevant controllers (via the controller manager) to ensure the desired state is achieved.
        
    5. **Scheduler**: If the request involves deploying a pod, the scheduler decides which node should run the pod, considering the available resources.
        
    6. **Etcd Update**: Once the state is successfully updated (for example, a pod has been scheduled), the changes are stored in `etcd`.
        
    7. **Kubelet Interaction**: The kubelet on the chosen node pulls the latest configuration from the API server and ensures that the containerized application starts on the node.
        
    8. **Kube Proxy**: If networking is involved, the kube proxy ensures that the right network rules are set up on the node for the services and pods.
        
    
    ---
    
    ### **3\. The Pod and Container in Kubernetes**
    
    #### **Pod:**
    
    A **pod** is the smallest and simplest unit of deployment in Kubernetes. It can contain one or more containers that share the same network namespace, storage, and resources. Pods are designed to run closely related application containers that need to share resources.
    
    Each pod is assigned a unique IP address within the cluster, and containers within a pod can communicate with each other via localhost. Pods are ephemeral, meaning they can be created, destroyed, and replaced automatically by the Kubernetes control plane as needed. Kubernetes ensures that the desired number of pod replicas are running at any given time.
    
    #### **Container:**
    
    A **container** is a lightweight, standalone executable package that includes everything needed to run an application: code, runtime, libraries, and dependencies. Containers are isolated from each other, making them portable and consistent across environments.
    
    In Kubernetes, containers are run inside pods. Each container within a pod shares the pod’s network namespace and can access the pod's storage. The container runtime (e.g., Docker or containerd) manages containers on each node.
    
    ---
    
    ### **4\. Functions of Each Control Plane Component**
    
    Here’s a straightforward explanation of the key control plane components:
    
    1. **API Server**: Acts as the "gateway" to interact with the Kubernetes cluster. It receives requests from users or components and communicates with other parts of the system to process them.
        
    2. **Scheduler**: Decides where to run a pod by evaluating available resources on the nodes and scheduling the pod accordingly.
        
    3. **Controller Manager**: Keeps the cluster running according to its desired state. It’s responsible for ensuring the right number of replicas, handling pod failures, and making necessary changes to the cluster.
        
    4. **etcd**: Stores all cluster data, such as configurations and states. It serves as the single source of truth for the cluster's state.
        
    

---

> ***💡 If you need help or have any questions, just leave them in the comments! 📝 I would be happy to answer them!***
> 
> ***💡 If you found this post useful, please give it a thumbs up 👍 and consider following for more helpful content. 😊***

### **Thank you for taking the time to read! 💚**