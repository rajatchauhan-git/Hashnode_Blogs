---
title: "Kubernetes Architecture and Components,
Kubernetes Installation and Configuration"
datePublished: Tue Aug 13 2024 00:24:11 GMT+0000 (Coordinated Universal Time)
cuid: clzroju9v000009js75ey93ir
slug: kubernetes-architecture-and-components-kubernetes-installation-and-configuration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723507435177/a879c800-26f4-40ed-ac9c-5e8aa6e232f8.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723508596325/8ffe5b91-90de-4db5-ba0d-2cdceb24db72.png
tags: aws, kubernetes, devops, devops-articles, kubernetes-container, devops-journey, kubernetes-architecture, 90daysofdevops, trainwithshubham, devopscommunity, kubeweek, kubernetes-installation

---

### <mark>For Kubernetes architecture refer -&gt; </mark> [**<mark>k8s Architecture</mark>**](https://chauhanrajatwork.hashnode.dev/kubernetes-architecture)

This guide provides step-by-step instructions for <mark>installing Minikube on Ubuntu</mark>. Minikube allows you to run a single-node Kubernetes cluster locally for development and testing purposes.

## Pre-requisites

* Ubuntu OS
    
* sudo privileges
    
* Internet access
    
* Virtualization support enabled (Check with `egrep -c '(vmx|svm)' /proc/cpuinfo`, 0=disabled 1=enabled)
    

---

### Step 1: Update System Packages

Update your package lists to make sure you are getting the latest version and dependencies.

```yaml
sudo apt update
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723507879924/d5a3282a-8981-4bb1-92b5-1e8defd0a568.png align="center")

### Step 2: Install Required Packages

Install some basic required packages.

```yaml
sudo apt install -y curl wget apt-transport-https
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723507948126/1ae09a1b-d90c-4765-9b52-037a55b87c81.png align="center")

---

### Step 3: Install Docker

Minikube can run a Kubernetes cluster either in a VM or locally via Docker. This guide demonstrates the Docker method.

```yaml
sudo apt install -y docker.io
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723507977655/c3e23a31-b2ca-4fdb-bdd2-b84d63b2bbf4.png align="center")

Start and enable Docker.

```yaml
sudo systemctl enable --now docker
```

Add current user to docker group (To use docker without root)

```yaml
sudo usermod -aG docker $USER && newgrp docker
```

Now, logout (use `exit` command) and connect again.

---

### Step 4: Install Minikube

First, download the Minikube binary using `curl`:

```yaml
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723508030927/d974a788-8044-45a8-ab73-534a8ab34d8f.png align="center")

Make it executable and move it into your path:

```yaml
chmod +x minikube
sudo mv minikube /usr/local/bin/
```

---

### Step 5: Install kubectl

Download kubectl, which is a Kubernetes command-line tool.

```yaml
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723508086502/2ab0ca76-6919-4dc9-a1d7-301f7ce95e6b.png align="center")

**Check the above image ⬆️ Make it executable and move it into your path:**

```yaml
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

---

### Step 6: Start Minikube

Now, you can start Minikube with the following command:

```yaml
minikube start --driver=docker --vm=true 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723508374217/e10318c2-a6e2-4726-b4d8-d3fee54e90bc.png align="center")

This command will start a single-node Kubernetes cluster inside a Docker container.

---

### Step 7: Check Cluster Status

Check the cluster status with:

```yaml
minikube status
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723508400459/cb6e303f-a0cb-4f64-a185-08ee01cb429f.png align="center")

You can also use `kubectl` to interact with your cluster:

```yaml
kubectl get nodes
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723508419796/2b0fd8c9-7bd0-449e-bbed-5284a92d2624.png align="center")

---

### Step 8: Stop Minikube

When you are done, you can stop the Minikube cluster with:

```yaml
minikube stop
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723508454905/9ff3a9b0-1cf8-4958-b123-768f3f492136.png align="center")

---

### Delete Minikube Cluster (Optional)

If you wish to delete the Minikube cluster entirely, you can do so with:

```yaml
minikube delete
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723508479450/f11787c8-9f7a-40b3-bc95-7c41e2f58f05.png align="center")

---

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">If you need help or have any questions, just leave them in the comments! 📝 I would be happy to answer them!</div>
</div>

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">If you found this post useful, please give it a thumbs up 👍 and consider following for more helpful content. 😊</div>
</div>

### Thank you for taking the time to read! 💚