# Wordpress Deployment on AWS EC2 Instance

## Overview
The project involves deploying a WordPress website on an AWS EC2 instance using PHP and SQL for dynamic functionality and database management. It focuses on configuring a scalable, secure, and reliable infrastructure while providing hands-on experience with AWS cloud services and backend development.

- **Objective**: 
The purpose of the project is to deploy a WordPress website on an AWS EC2 instance, providing practical experience in cloud infrastructure management and web development. It aims to demonstrate how to set up and configure scalable, secure, and reliable hosting for a dynamic website using PHP and SQL. Through this project, you'll learn how to use AWS services like EC2 for hosting, security groups for managing access, and possibly RDS for database integration, while gaining skills in deploying real-world web applications on the cloud.

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
[Click here for MobaXterm Installation](https://github.com/krushna-phapale/AWS-MobaXterm-PuTTY-Setup.git)


## Steps

### Step 1: Launch EC2 Instance
[Follow this link for detailed Instance launching and connecting using MobaXterm](https://github.com/krushna-phapale/Launching-EC2-Instance.git)

1. Navigate to the [EC2 Dashboard](https://console.aws.amazon.com/ec2/) and click on **Launch Instance**.
2. Select **Ubuntu** as the AMI.
3. Choose the instance type (e.g., `t2.micro` for free tier).
4. Configure security groups to allow:
   - SSH (port 22)
   - HTTP (port 80)
   - MySQL/Aurora (port 3306)
5. Launch the instance and connect using MobaXterm :-
```bash
   ssh -i your-key.pem ubuntu@your-instance-ip
```

### Step 2: Install Software on EC2

1. Update packages on your EC2 instance.
```bash
   sudo apt update -y
```
2. Install necessary software ( Apache, MySQL, PHP for a LAMP stack).
```bash
   sudo apt install apache2 -y
   sudo apt install mariadb-server -y
   sudo apt install php libapache2-mod-php php-mysql -y

```
### Step 3: Start installed softwares

1. Start and enable Apache:
```bash
   sudo systemctl start apache2
   sudo systemctl enable apache2
```
2. Start MariaDB:
```bash
   sudo systemctl start mariadb
```
### Step 4: Set Up MySQL for WordPress

1. Secure your MySQL installation:
```bash
   sudo mysql_secure_installation
```
2. Create a MySQL database and user:
```bash
   sudo mysql -u root -p
```
3. Then, in the MySQL prompt, run:
```SQL
   CREATE DATABASE wordpress;
   CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'your_password';
   GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
   FLUSH PRIVILEGES;
EXIT;
```
**Note :- In place of password enter your password**

### Step 5: Download and Set Up WordPress

1. Navigate to the web directory:
```bash
   cd /var/www/html
```
2. Download WordPress:
```bash
   wget https://wordpress.org/latest.tar.gz
```
3. Extract the WordPress files:
```bash
   tar -xvzf latest.tar.gz
```
4. Move the extracted WordPress files:
```bash
   sudo mv wordpress/* /var/www/html/
```
5. You need to remove it so that WordPress can be served:
```bash
   sudo rm /var/www/html/index.html
```
### Step 6: Configure WordPress

1. Rename and edit the WordPress configuration file:
```bash
   sudo mv wp-config-sample.php wp-config.php
   sudo nano wp-config.php
```
2. Update the database details:
```php
   define( 'DB_NAME', 'wordpress' );
   define( 'DB_USER', 'wpuser' );
   define( 'DB_PASSWORD', 'your_password' );
   define( 'DB_HOST', 'localhost' );
```
### Step 7: Set Permissions

1. Change ownership of the WordPress files to ensure Apache can access them:
```bash
   sudo chown -R www-data:www-data /var/www/html
```
### Step 8: Restart Apache

1. Restart Apache for the changes to take effect:
```bash
   sudo systemctl restart apache2
```
### Step 9: Access WordPress

1. Open your browser and visit the public IP address of your EC2 instance. You should now see the WordPress setup page.

