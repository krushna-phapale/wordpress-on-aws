# Wordpress Deployment on AWS EC2 Instance

## Overview
The project involves deploying a WordPress website on an AWS EC2 instance using PHP and SQL for dynamic functionality and database management. It focuses on configuring a scalable, secure, and reliable infrastructure while providing hands-on experience with AWS cloud services and backend development.

- **Objective**: The purpose of the project is to deploy a WordPress website on an AWS EC2 instance, providing practical experience in cloud infrastructure management and web development. It aims to demonstrate how to set up and configure scalable, secure, and reliable hosting for a dynamic website using PHP and SQL. Through this project, you'll learn how to use AWS services like EC2 for hosting, security groups for managing access, and possibly RDS for database integration, while gaining skills in deploying real-world web applications on the cloud.
- **Technologies Used**:
  - AWS EC2
  - SQL
  - PHP
  - MobaXterm
  - Linux

## Prerequisites
**Prerequisites for the Project:**
- EC2 instance with 2GB RAM and 12GB memory
- Ubuntu OS as the server environment
- Enabled ports: HTTP (80), HTTPS (443), MySQL (3306), and SSH (22) for web access, database connectivity, and secure server management
- PHP and SQL installed and configured for WordPress backend functionalities

- **AWS Account**: Sign up for an [AWS account](https://aws.amazon.com/free/).
- **Software**: MobaXterm

## To install MobaXterm software refer below GitHub repository :-
(https://github.com/krushna-phapale/AWS-MobaXterm-PuTTY-Setup.git)



## Steps

### Step 1: Launch EC2 Instance
[Follow this link for Instance launching and connecting using MobaXterm](https://github.com/krushna-phapale/Launching-EC2-Instance.git)

1. Navigate to the [EC2 Dashboard](https://console.aws.amazon.com/ec2/) and click on **Launch Instance**.
2. Select **Ubuntu** as the AMI.
3. Choose the instance type (e.g., `t2.micro` for free tier).
4. Configure security groups to allow:
   - SSH (port 22)
   - HTTP (port 80)
   - MySQL/Aurora (if required for database, port 3306)
5. Launch the instance and connect using SSH:

   ```bash
   ssh -i your-key.pem ubuntu@your-instance-ip
