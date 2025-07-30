![Alt text](/Host-a-Static-Website-on-AWS.png)

---

# Host a Static Website on AWS

This project demonstrates how to host a **static HTML website** on **Amazon Web Services (AWS)** using a robust DevOps infrastructure. It includes a high-availability architecture deployed across multiple Availability Zones and uses best practices in security, scalability, and automation.

📌 **[View Project Repository](https://github.com/aosnotes77/host-a-static-website-on-aws)**

---

## 🚀 Project Overview

The primary goal of this project was to deploy a static web application on AWS using an **Apache web server** running on **EC2 instances** within a **private subnet**. The infrastructure was designed with fault tolerance, scalability, and secure connectivity in mind.

---

## 🧱 Infrastructure Architecture

The architecture consists of the following components:

1. **Virtual Private Cloud (VPC)** with both **public and private subnets** distributed across **two Availability Zones (AZs)**.
2. **Internet Gateway (IGW)** to allow public subnet access to the Internet.
3. **Security Groups** configured as network firewalls for secure traffic flow.
4. **NAT Gateway** in a public subnet to enable outbound Internet access from private subnets.
5. **EC2 Instances** (web servers) hosted within private subnets.
6. **EC2 Instance Connect Endpoint** for secure remote access to private EC2 instances.
7. **Application Load Balancer (ALB)** in a public subnet for distributing incoming traffic.
8. **Auto Scaling Group (ASG)** managing EC2 instances for elasticity and availability.
9. **AWS Certificate Manager (ACM)** to enable HTTPS via SSL certificates.
10. **Amazon SNS** configured to send alerts for Auto Scaling Group events.
11. **Amazon Route 53** used to register the domain and manage DNS records.
12. **GitHub** for version control and deployment of web assets.

---

## 🔧 Deployment Script (User Data)

Below is the EC2 instance user data script used to automate the setup of the Apache web server and deploy website files from GitHub:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

---

## 🗂️ Repository Contents

* `infrastructure/` – CloudFormation templates or Terraform scripts (if applicable)
* `scripts/` – Deployment or automation scripts
* `static-site/` – HTML/CSS/JS files for the website
* `README.md` – Project documentation

---

## ✅ Key Features

* **Highly Available**: Multi-AZ deployment ensures fault tolerance
* **Secure**: Web servers run in private subnets, accessed only via secure endpoints
* **Scalable**: Auto Scaling Group manages instance count dynamically
* **Monitored**: SNS alerts for key events
* **Version Controlled**: Website code managed in GitHub

---

## 🌐 Domain and DNS

The domain name was registered and managed using **Amazon Route 53**, with DNS records pointing to the Application Load Balancer.

---

## 📧 Notifications

**Amazon SNS** is configured to notify administrators of key events in the Auto Scaling Group (such as instance launches or terminations).

---

## 🛡️ Security

* Only the Load Balancer is publicly accessible.
* EC2 instances reside in private subnets.
* Traffic is encrypted using SSL/TLS via ACM.
* EC2 Instance Connect Endpoint is used for secure access without public IPs.

---

## 📎 Reference Architecture Diagram

A full diagram of the AWS architecture is available in the [project repository](https://github.com/aosnotes77/host-a-static-website-on-aws).

---

## 👨‍💻 Author

**AOS Notes**
GitHub: [@aosnotes77](https://github.com/aosnotes77)

---

