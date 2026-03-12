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

