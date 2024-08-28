---
title: "Mastering Advanced Terraform Topics: Workspaces, Remote Execution, Collaboration, and Best Practices"
datePublished: Wed Aug 28 2024 02:30:09 GMT+0000 (Coordinated Universal Time)
cuid: cm0d8nmhc00050ajs2zczeykx
slug: mastering-advanced-terraform-topics-workspaces-remote-execution-collaboration-and-best-practices
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724811467867/70e8d305-382d-47a7-b04e-2340cf338390.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1724811940163/e7a1183a-7b10-492e-add7-97f04b85bece.png
tags: devops, terraform, devops-articles, terraform-state, terraform-cloud, devops-trends, devops-journey, 90daysofdevops, terraform-module, trainwithshubham, devopscommunity, terraweekchallenge

---

As we wrap up TerraWeek, it’s time to dive deep into advanced Terraform topics. This blog will guide you through creating a complete AWS infrastructure project using Terraform, exploring concepts like workspaces, remote execution, collaboration, best practices, and additional Terraform features.

---

### **Project Overview: Scalable AWS Infrastructure**

In this project, you’ll:

1. **Set up Terraform workspaces** to manage different environments (development, staging, production).
    
2. **Configure remote backend using AWS S3** for centralized state management.
    
3. **Deploy a VPC, EC2 instances, and RDS database** using Terraform modules.
    
4. **Integrate Terraform with GitLab CI for continuous integration and deployment.**
    
5. **Use Terraform Cloud for collaboration and remote execution.**
    

### **Task 1: Workspaces, Remote Execution, and Collaboration**

#### **Step 1: Set Up Terraform Workspaces**

Terraform workspaces allow you to manage multiple environments (e.g., development, staging, production) using the same Terraform configuration.  
  
**Create the Directory Structure**

Begin by organizing your project with the following directory structure:

```yaml
terraform-aws-project/
├── modules/
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── ec2/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── rds/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── envs/
│   ├── dev/
│   │   ├── main.tf
│   │   └── backend.tf
│   ├── staging/
│   │   ├── main.tf
│   │   └── backend.tf
│   └── prod/
│       ├── main.tf
│       └── backend.tf
└── main.tf
```

---

### **2\. Content of Each File**

#### **2.1.** `modules/vpc/`[`main.tf`](http://main.tf)

This file defines the main configuration for the VPC module.

```yaml
resource "aws_vpc" "main" {
  cidr_block = var.cidr_block

  tags = {
    Name = "${var.name}-vpc"
  }
}

resource "aws_subnet" "public" {
  count = length(var.public_subnets)

  vpc_id            = aws_vpc.main.id
  cidr_block        = var.public_subnets[count.index]
  availability_zone = element(var.availability_zones, count.index)

  tags = {
    Name = "${var.name}-public-${count.index}"
  }
}
```

#### **2.2.** `modules/vpc/`[`variables.tf`](http://variables.tf)

This file defines the input variables for the VPC module.

```yaml
variable "cidr_block" {
  description = "The CIDR block for the VPC."
  type        = string
}

variable "public_subnets" {
  description = "List of public subnet CIDR blocks."
  type        = list(string)
}

variable "availability_zones" {
  description = "List of availability zones."
  type        = list(string)
}

variable "name" {
  description = "The name to apply to all resources."
  type        = string
}
```

#### **2.3.** `modules/vpc/`[`outputs.tf`](http://outputs.tf)

This file defines the outputs from the VPC module.

```yaml
output "vpc_id" {
  description = "The ID of the VPC."
  value       = aws_vpc.main.id
}

output "public_subnets" {
  description = "The public subnet IDs."
  value       = aws_subnet.public[*].id
}
```

#### **2.4.** `modules/ec2/`[`main.tf`](http://main.tf)

This file defines the EC2 instance configuration.

```yaml
resource "aws_instance" "app" {
  count         = var.instance_count
  ami           = var.ami_id
  instance_type = var.instance_type
  subnet_id     = element(var.subnet_ids, count.index)

  tags = {
    Name = "${var.name}-app-${count.index}"
  }

  user_data = var.user_data
}
```

#### **2.5.** `modules/ec2/`[`variables.tf`](http://variables.tf)

This file defines the input variables for the EC2 module.

```yaml
variable "instance_count" {
  description = "The number of instances to create."
  type        = number
  default     = 1
}

variable "ami_id" {
  description = "The AMI ID to use for the instances."
  type        = string
}

variable "instance_type" {
  description = "The type of instance to create."
  type        = string
  default     = "t3.micro"
}

variable "subnet_ids" {
  description = "List of subnet IDs where the instances will be launched."
  type        = list(string)
}

variable "name" {
  description = "The name to apply to all resources."
  type        = string
}

variable "user_data" {
  description = "The user data script to use for instance initialization."
  type        = string
  default     = ""
}
```

#### **2.6.** `modules/ec2/`[`outputs.tf`](http://outputs.tf)

This file defines the outputs from the EC2 module.

```yaml
output "instance_ids" {
  description = "The IDs of the EC2 instances."
  value       = aws_instance.app[*].id
}

output "public_ips" {
  description = "The public IP addresses of the instances."
  value       = aws_instance.app[*].public_ip
}
```

#### **2.7.** `modules/rds/`[`main.tf`](http://main.tf)

This file defines the RDS database configuration.

```yaml
resource "aws_db_instance" "db" {
  allocated_storage    = var.allocated_storage
  engine               = var.engine
  engine_version       = var.engine_version
  instance_class       = var.instance_class
  name                 = var.db_name
  username             = var.username
  password             = var.password
  parameter_group_name = var.parameter_group_name
  vpc_security_group_ids = var.vpc_security_group_ids
  db_subnet_group_name = var.subnet_group_name

  tags = {
    Name = "${var.name}-rds"
  }
}
```

#### **2.8.** `modules/rds/`[`variables.tf`](http://variables.tf)

This file defines the input variables for the RDS module.

```yaml
variable "allocated_storage" {
  description = "The allocated storage in gigabytes."
  type        = number
  default     = 20
}

variable "engine" {
  description = "The database engine to use."
  type        = string
  default     = "mysql"
}

variable "engine_version" {
  description = "The version of the database engine."
  type        = string
  default     = "5.7"
}

variable "instance_class" {
  description = "The instance type for the database."
  type        = string
  default     = "db.t3.micro"
}

variable "db_name" {
  description = "The name of the database to create."
  type        = string
  default     = "mydb"
}

variable "username" {
  description = "The username for the database."
  type        = string
}

variable "password" {
  description = "The password for the database."
  type        = string
}

variable "parameter_group_name" {
  description = "The name of the DB parameter group."
  type        = string
  default     = "default.mysql5.7"
}

variable "vpc_security_group_ids" {
  description = "The VPC security group IDs to associate with the RDS instance."
  type        = list(string)
}

variable "subnet_group_name" {
  description = "The DB subnet group name."
  type        = string
}

variable "name" {
  description = "The name to apply to all resources."
  type        = string
}
```

#### **2.9.** `modules/rds/`[`outputs.tf`](http://outputs.tf)

This file defines the outputs from the RDS module.

```yaml
output "db_instance_id" {
  description = "The ID of the RDS instance."
  value       = aws_db_instance.db.id
}

output "db_endpoint" {
  description = "The endpoint of the RDS instance."
  value       = aws_db_instance.db.endpoint
}
```

---

### **3\. Environment-Specific Configuration**

#### **3.1.** `envs/dev/`[`main.tf`](http://main.tf)

This file defines the environment-specific configurations for the dev environment.

```yaml
module "vpc" {
  source = "../../modules/vpc"
  cidr_block = "10.0.0.0/16"
  public_subnets = ["10.0.1.0/24", "10.0.2.0/24"]
  availability_zones = ["us-west-2a", "us-west-2b"]
  name = "dev"
}

module "ec2" {
  source = "../../modules/ec2"
  instance_count = 2
  ami_id = "ami-12345678"
  instance_type = "t3.micro"
  subnet_ids = module.vpc.public_subnets
  name = "dev"
  user_data = <<-EOF
              #!/bin/bash
              echo "Hello, Dev Environment!" > /var/www/html/index.html
              EOF
}

module "rds" {
  source = "../../modules/rds"
  allocated_storage = 20
  engine = "mysql"
  instance_class = "db.t3.micro"
  db_name = "devdb"
  username = "admin"
  password = "password123"
  vpc_security_group_ids = [module.vpc.public_subnets[0]]
  subnet_group_name = "my-dev-subnet-group"
  name = "dev"
}
```

#### **3.2.** `envs/dev/`[`backend.tf`](http://backend.tf)

This file configures the remote backend for the dev environment.

```yaml
terraform {
  backend "s3" {
    bucket = "my-terraform-state-bucket"
    key    = "envs/dev/terraform.tfstate"
    region = "us-west-2"
  }
}
```

#### **3.3.** `envs/staging/`[`main.tf`](http://main.tf)

This file defines the environment-specific configurations for the staging environment.

```yaml
module "vpc" {
  source = "../../modules/vpc"
  cidr_block = "10.1.0.0/16"
  public_subnets = ["10.1.1.0/24", "10.1.2.0/24"]
  availability_zones = ["us-west-2a", "us-west-2b"]
  name = "staging"
}

module "ec2" {
  source = "../../modules/ec2"
  instance_count = 2
  ami_id = "ami-12345678"
  instance_type = "t3.micro"
  subnet_ids = module.vpc.public_subnets
  name = "staging"
  user_data = <<-EOF
              #!/bin/bash
              echo "Hello, Staging Environment!" > /var/www/html/index.html
              EOF
}

module "rds" {
  source = "../../modules/rds"
  allocated_storage = 20
  engine = "mysql"
  instance_class = "db.t3.micro"
  db_name = "stagingdb"
  username = "admin"
  password = "password123"
  vpc_security_group_ids = [module.vpc.public_subnets[0]]
  subnet_group_name = "my-staging-subnet-group"
  name = "staging"
}
```

#### **3.4.** `envs/staging/`[`backend.tf`](http://backend.tf)

This file configures the remote backend for the staging environment.

```yaml
terraform {
  backend "s3" {
    bucket = "my-terraform-state-bucket"
    key    = "envs/staging/terraform.tfstate"
    region = "us-west-2"
  }
}
```

#### **3.5.** `envs/prod/`[`main.tf`](http://main.tf)

This file defines the environment-specific configurations for the prod environment.

```yaml
module "vpc" {
  source = "../../modules/vpc"
  cidr_block = "10.2.0.0/16"
  public_subnets = ["10.2.1.0/24", "10.2.2.0/24"]
  availability_zones = ["us-west-2a", "us-west-2b"]
  name = "prod"
}

module "ec2" {
  source = "../../modules/ec2"
  instance_count = 2
  ami_id = "ami-12345678"
  instance_type = "t3.micro"
  subnet_ids = module.vpc.public_subnets
  name = "prod"
  user_data = <<-EOF
              #!/bin/bash
              echo "Hello, Production Environment!" > /var/www/html/index.html
              EOF
}

module "rds" {
  source = "../../modules/rds"
  allocated_storage = 20
  engine = "mysql"
  instance_class = "db.t3.micro"
  db_name = "proddb"
  username = "admin"
  password = "password123"
  vpc_security_group_ids = [module.vpc.public_subnets[0]]
  subnet_group_name = "my-prod-subnet-group"
  name = "prod"
}
```

#### **3.6.** `envs/prod/`[`backend.tf`](http://backend.tf)

This file configures the remote backend for the prod environment.

```yaml
terraform {
  backend "s3" {
    bucket = "my-terraform-state-bucket"
    key    = "envs/prod/terraform.tfstate"
    region = "us-west-2"
  }
}
```

#### **3.7.** [`main.tf`](http://main.tf)

This file defines the global configuration and references the environment-specific files.

```yaml
terraform {
  required_version = ">= 1.0.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = "us-west-2"
}

module "vpc" {
  source = "./modules/vpc"
}

module "ec2" {
  source = "./modules/ec2"
}

module "rds" {
  source = "./modules/rds"
}
```

1. **Initialize the Default Workspace**
    
    Start by initializing Terraform in the `dev` environment:
    
    ```yaml
    cd envs/dev
    terraform init
    ```
    
2. **Create and Switch Workspaces**
    
    Create workspaces for staging and production environments:
    
    ```yaml
    terraform workspace new staging
    terraform workspace new prod
    ```
    
    You can switch between workspaces as needed:
    
    ```yaml
    terraform workspace select staging
    ```
    
    This setup allows you to deploy infrastructure for different environments without conflicts.
    

#### **Step 2: Configure Remote Backend Using AWS S3**

Centralized state management is crucial for collaboration and consistency across environments. Here’s how to configure AWS S3 as the remote backend:

1. **Create an S3 Bucket for State Files**
    
    Use the AWS CLI to create an S3 bucket:
    
    ```yaml
    aws s3api create-bucket --bucket my-terraform-state-bucket --region us-west-2
    ```
    
    Enable versioning on the bucket to maintain a history of state files:
    
    ```yaml
    aws s3api put-bucket-versioning --bucket my-terraform-state-bucket --versioning-configuration Status=Enabled
    ```
    
2. **Configure the Remote Backend**
    
    In each environment folder (`dev/`[`backend.tf`](http://backend.tf), `staging/`[`backend.tf`](http://backend.tf), `prod/`[`backend.tf`](http://backend.tf)), add the following configuration:
    
    ```yaml
    terraform {
      backend "s3" {
        bucket = "my-terraform-state-bucket"
        key    = "envs/${terraform.workspace}/terraform.tfstate"
        region = "us-west-2"
      }
    }
    ```
    
    This setup ensures that each workspace has its own state file, stored securely in S3.
    
3. **Initialize the Backend**
    
    Run `terraform init` in each environment to configure the backend:
    
    ```yaml
    terraform init
    ```
    
    Terraform will prompt to migrate the state file to S3.
    

#### **Step 3: Collaborate Using Terraform Cloud**

Terraform Cloud offers enhanced collaboration features, including remote execution, state management, and version control integration.

1. **Set Up Terraform Cloud Account**
    
    Sign up for a Terraform Cloud account if you haven’t already, and create a new workspace.
    
2. **Link Your Repository**
    
    Link your Git repository to Terraform Cloud to automatically trigger Terraform runs on code changes.
    
3. **Configure Remote Execution**
    
    Update the [`backend.tf`](http://backend.tf) file in each environment to use Terraform Cloud:
    
    ```yaml
    terraform {
      backend "remote" {
        organization = "my-org"
    
        workspaces {
          name = "my-terraform-cloud-workspace"
        }
      }
    }
    ```
    
    Run `terraform init` to configure the new backend.
    
4. **Collaborate with Your Team**
    
    Use Terraform Cloud’s features to collaborate with team members, review plans, and manage infrastructure changes efficiently.
    

---

### **Task 2: Terraform Best Practices**

#### **Step 4: Modularize and Organize Your Code**

Following best practices for Terraform code organization ensures maintainability and scalability.

1. **Create Reusable Modules**
    
    Define modules for VPC, EC2, and RDS in the `modules/` directory. For example, the `vpc/`[`main.tf`](http://main.tf) might look like this:
    
    ```yaml
    resource "aws_vpc" "main" {
      cidr_block = var.cidr_block
    
      tags = {
        Name = var.name
      }
    }
    
    resource "aws_subnet" "public" {
      count = length(var.public_subnets)
    
      vpc_id            = aws_vpc.main.id
      cidr_block        = var.public_subnets[count.index]
      availability_zone = element(var.availability_zones, count.index)
    
      tags = {
        Name = "${var.name}-public-${count.index}"
      }
    }
    ```
    
    The [`variables.tf`](http://variables.tf) file might define the input variables:
    
    ```yaml
    variable "cidr_block" {
      description = "The CIDR block for the VPC."
      type        = string
    }
    
    variable "public_subnets" {
      description = "List of public subnet CIDR blocks."
      type        = list(string)
    }
    
    variable "availability_zones" {
      description = "List of availability zones."
      type        = list(string)
    }
    ```
    
2. **Use Naming Conventions**
    
    Apply consistent naming conventions to resources and variables to make your code more readable and manageable.
    
3. **Separate Environment Configurations**
    
    Use the `envs/` directory to maintain separate configurations for each environment. For instance, in `dev/`[`main.tf`](http://main.tf), you could define:
    
    ```yaml
    module "vpc" {
      source          = "../../modules/vpc"
      cidr_block      = "10.0.0.0/16"
      public_subnets  = ["10.0.1.0/24", "10.0.2.0/24"]
      availability_zones = ["us-west-2a", "us-west-2b"]
    
      tags = {
        Environment = "dev"
      }
    }
    ```
    

#### **Step 5: Integrate Terraform with CI/CD**

Automating Terraform workflows through CI/CD pipelines enhances reliability and reduces manual intervention.

1. **Set Up a GitLab CI Pipeline**
    
    Create a `.gitlab-ci.yml` file to automate Terraform validation and deployment:
    
    ```yaml
    stages:
      - validate
      - plan
      - apply
    
    variables:
      TF_VERSION: "1.4.5"
      TF_WORKSPACE: "dev"
      TF_VAR_region: "us-west-2"
    
    before_script:
      - terraform --version
      - terraform init -backend-config="backend.tfvars"
    
    validate:
      stage: validate
      script:
        - terraform validate
    
    plan:
      stage: plan
      script:
        - terraform plan -out=tfplan
    
    apply:
      stage: apply
      script:
        - terraform apply -auto-approve tfplan
      when: manual
    ```
    
2. **Manage AWS Credentials**
    
    Store AWS credentials securely in GitLab’s CI/CD settings as environment variables (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`).
    
3. **Automate Deployments**
    
    With the CI pipeline in place, every change to the repository will trigger a validation, and you can manually approve the plan to apply it.
    

---

### **Task 3: Exploring Additional Features**

#### **Step 6: Leverage Terraform Cloud and Registry**

1. **Enhance Collaboration with Terraform Cloud**
    
    Terraform Cloud’s workspace-based collaboration and remote execution ensure that your team can work on infrastructure as code without stepping on each other's toes.
    
2. **Use the Terraform Registry**
    
    Extend your Terraform project using modules from the Terraform Registry. For example, if you need a highly available RDS setup, you can leverage a community module:
    
    ```yaml
    module "rds" {
      source = "terraform-aws-modules/rds/aws"
      version = "~> 5.0"
    
      identifier = "my-rds-instance"
      engine = "mysql"
      instance_class = "db.t3.micro"
      allocated_storage = 20
      name = "mydb"
      username = "foo"
      password = "foobarbaz"
      parameter_group_name = "default.mysql5.7"
    
      vpc_security_group_ids = [module.vpc.default_security_group_id]
      subnet_ids = module.vpc.private_subnets
    
      tags = {
        Name = "my-rds-instance"
        Environment = terraform.workspace
      }
    }
    ```
    
3. **Utilize Terraform Cloud’s Advanced Features**
    
    Explore additional Terraform Cloud features like cost estimation, policy enforcement, and drift detection to keep your infrastructure in check.
    

---

> Note: Multiple files are generated using ChatGPT

> ***💡 If you need help or have any questions, just leave them in the comments! 📝 I would be happy to answer them!***
> 
> ***💡 If you found this post useful, please give it a thumbs up 👍 and consider following for more helpful content. 😊***

### **Thank you for taking the time to read! 💚**