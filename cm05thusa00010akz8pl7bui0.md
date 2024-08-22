---
title: "Mastering Terraform with AWS EC2"
datePublished: Thu Aug 22 2024 21:51:22 GMT+0000 (Coordinated Universal Time)
cuid: cm05thusa00010akz8pl7bui0
slug: mastering-terraform-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724363220728/d0f9544e-b597-4a3d-a5c4-683d2769a2a1.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724363474543/5d1114ec-3644-4366-9414-276bf028f1d3.png
tags: aws, devops, terraform, devops-articles, terraform-state, terraform-cloud, devops-trends, devops-journey, 90daysofdevops, terraform-module, trainwithshubham, devopscommunity, terraweek, terraweekchallenge

---

On Day 3 of TerraWeek, we delve into the practical use of Terraform to manage infrastructure as code. Today’s focus is on creating and managing resources like AWS EC2 instances, Azure storage accounts, or Google Compute Engine resources using Terraform. We’ll cover writing configuration files, validating them, and using provisioners and lifecycle management configurations.

---

### **Task 1: Create a Terraform Configuration File**

For this example, we'll create an AWS EC2 instance. Start by defining the resource in a `.tf` file.

**Example** [`main.tf`](http://main.tf):

```yaml
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "TerraWeek-EC2"
  }
}
```

This configuration sets up an AWS EC2 instance in the `us-west-2` region using a specific Amazon Machine Image (AMI) and tags the instance with the name "TerraWeek-EC2."

### **Task 2: Check State Files and Validate Configuration**

Before running the `plan` and `apply` commands, it’s essential to check the state files and validate the configuration.

**Check State Files:**

To inspect state files, you can use:

```yaml
terraform state list
```

This command lists the resources currently managed by Terraform in your state file.

**Validate Configuration:**

Use the `validate` command to check your configuration file for syntax errors.

```yaml
terraform validate
```

**Expected Output:**

If everything is correct, you should see:

```yaml
Success! The configuration is valid.
```

Now, you can proceed with the `plan` and `apply` commands:

```yaml
terraform plan
terraform apply
```

### **Task 3: Add a Provisioner**

Provisioners in Terraform execute scripts on a local or remote machine as part of resource creation or destruction. Here, we’ll add a simple `file` provisioner to copy a file to the EC2 instance.

**Updated** [`main.tf`](http://main.tf):

```yaml
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "TerraWeek-EC2"
  }

  provisioner "file" {
    source      = "script.sh"
    destination = "/tmp/script.sh"
  }

  provisioner "remote-exec" {
    inline = [
      "chmod +x /tmp/script.sh",
      "/tmp/script.sh"
    ]
  }
}
```

**Apply the Changes:**

After adding the provisioner, run:

```yaml
terraform apply
```

**Destroy the Resources:**

To remove the resources:

```yaml
terraform destroy
```

### **Task 4: Lifecycle Management**

Terraform’s lifecycle management lets you control when and how resources are created, updated, or destroyed. We’ll add lifecycle rules to prevent the EC2 instance from being accidentally killed.

**Updated** [`main.tf`](http://main.tf):

```yaml
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "TerraWeek-EC2"
  }

  lifecycle {
    prevent_destroy = true
  }

  provisioner "file" {
    source      = "script.sh"
    destination = "/tmp/script.sh"
  }

  provisioner "remote-exec" {
    inline = [
      "chmod +x /tmp/script.sh",
      "/tmp/script.sh"
    ]
  }
}
```

**Apply Lifecycle Changes:**

Run:

```yaml
terraform apply
```

**Testing Lifecycle Configuration:**

Attempting to destroy the resource should now trigger a warning due to the `prevent_destroy` lifecycle setting:

```yaml
terraform destroy
```

**Expected Output:**

```yaml
Error: Instance cannot be destroyed
```

This prevents accidental destruction of critical infrastructure.

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