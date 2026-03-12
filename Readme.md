# Terraform AWS EC2 Instance with Nginx

This project demonstrates how to use **Terraform** to provision an **AWS EC2 instance** and automatically install **Nginx** using a shell script.

---

## Project Overview

In this project we will:

* Create an **IAM User**
* Generate **AWS Access Key & Secret Key**
* Configure **Terraform AWS Provider**
* Create an **EC2 Instance**
* Create a **Security Group**
* Automatically install **Nginx** using `user_data`
* Retrieve **Public and Private IPs**

---

## Prerequisites

Before starting, ensure you have:

* AWS Account
* Terraform installed
* Git installed
* VS Code or any code editor

---

# Step 1: Create IAM User in AWS

1. Go to **AWS Console**
2. Navigate to **IAM → Users**
3. Click **Create User**
4. Provide a **Username**
5. Click **Next**

### Set Permissions

* Select **Attach Policies Directly**
* Attach **AdministratorAccess** (for learning purpose)

Click **Create User**

---

# Step 2: Create Access Key

1. Click the **Username**
2. Go to **Security Credentials**
3. Scroll to **Access Keys**
4. Click **Create Access Key**

Select:

Command Line Interface (CLI)

Check confirmation box and click **Next**

Add description:

```
terraform
```

Click **Create Access Key**

Copy:
OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOB
OBOBOBOBOB* Access Key
OBOBOBOBOBOB* Secret Key

OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBSave them safely.

OAOAOAOAOAOAOAOAOAOAOAOAOAOA---

# Step 3: Terraform Project Setup
OB
OBOBOBOBOBOBOBOBOBOBOBOBOpen terminal and run:

```
OBOBOBOBOBOBOBOBOBOBOBOBOBterraform
cmd
OBOBOBOBOBOBOBcode .
```

OBCreate file:

```
OBOBOBmain.tf
```

---

# Step 4: Terraform Configuration

## main.tf

OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOB```hcl
OBOBOBprovider "aws" {
OBOBOBOB  region     = "ap-south-1"
OBOBOBOBOBOB  access_key = ""
OBOBOBOB  secret_key = ""
}
OBOBOBOBOB
resource "aws_instance" "app_server" {
OBOBOBOBOBOBOB  ami           = "ami-019715e0d74f695be"
OBOBOBOBOBOBOB  instance_type = "t3.micro"
  key_name      = ""
OBOBOBOBOBOB  count         = 1

OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOB  root_block_device {
OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOB    volume_size = 20
OBOBOBOBOBOB    volume_type = "gp3"
OBOBOB  }

  tags = {
    Name = "sak_server"
OBOBOBOBOBOBOBOBOBOBOBOBOB  }

OB  security_groups = [aws_security_group.app_sg.name]

  user_data = file("sample.sh")
OBOBOBOBOB}

resource "aws_security_group" "app_sg" {

  tags = {
    Name = "sak_sg"
OBOBOBOBOBOBOBOBOBOBOBOBOBOB  }
OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOB
OAOAOAOAOAOAOAOAOAOAOAOAOAOAOAOAOAOAOAOA  ingress {
OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOB    from_port   = 22
    to_port     = 22
OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOB    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
OBOBOBOB
  ingress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
OBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOBOB  }

OBOB  egress {
    from_port   = 0
OBOBOBOBOBOBOBOBOBOBOBOB    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
OBOB  }

}

OBoutput "public_ips" {
  value = [for instance in aws_instance.app_server : instance.public_ip]
}

output "private_ips" {
  value = [for instance in aws_instance.app_server : instance.private_ip]
}
```

---

# Step 5: Create Shell Script

Create file:

```
sample.sh
```

### sample.sh

```bash
#!/bin/bash

apt update -y
apt install nginx -y
systemctl start nginx
systemctl enable nginx
```

This script installs **Nginx automatically when the EC2 instance starts.**

---

# Step 6: Terraform Commands

Run the following commands in terminal:

### Initialize Terraform

```
terraform init
```

### Validate configuration

```
terraform validate
```

### Format Terraform files

```
terraform fmt
```

### Preview infrastructure changes

```
terraform plan
```

### Create Infrastructure

```
terraform apply
```

Type:

```
yes
```

Terraform will create:

* EC2 Instance
* Security Group
* Install Nginx automatically

---

# Step 7: Verify Deployment

Go to **AWS EC2 Console**

Copy the **Public IP**

Open browser:

```
http://PUBLIC_IP
```

You should see the **Nginx Welcome Page**.

---

# Step 8: Destroy Infrastructure

To delete all created resources:

```
terraform destroy --auto-approve
```

---

# Project Structure

```
terraform-nginx-project
│
├── main.tf
├── sample.sh
└── README.md
```

---

# Author

DevOps Terraform Project
AWS EC2 + Nginx Automation using Terraform

---

```

