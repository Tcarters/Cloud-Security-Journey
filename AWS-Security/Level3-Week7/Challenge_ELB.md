


## Cloud Challenge Details

Your company is considering migrating a web application from an on-premise server to Amazon Elastic Compute Cloud (EC2). You have been tasked with setting up example infrastructure for hosting the web application and testing the path based routing with the help of Elastic Load Balancing (ELB).

In this lab challenge, you will use the AWS Management Console to complete the tasks that result in provisioning infrastructure to fulfill your company's requirements.

Follow the instructions given below to work on the challenge.

1. Create TWO Amazon EC2 Instances.
   - Admin EC2 Instance
        - Select Amazon Linux 2 AMI and t2.micro instance type with basic configuration.
        - SSH into the EC2 Instance and install apache server.
        - Host the admin HTML page mentioned below in EC2 Instance.
          `` https://labtask228.s3.amazonaws.com/admin/index.html ``

    - User EC2 Instance
      - Select Amazon Linux 2 AMI and t2.micro instance type with basic configuration..
      - SSH into the EC2 Instance and install apache server.
      - Host the user HTML page mentioned below in EC2 Instance.
        `` https://labtask228.s3.amazonaws.com/user/index.html``

2. Create an Elastic Load Balancer.
- If you enter the dns name with /admin, the request should be forwarded to EC2 Instance containing the admin HTML page.
- If you enter the dns name with /user, the request should be forwarded to EC2 Instance containing the user HTML page. 
- Any other path should be redirected to a success static plain text page with a note "Whizlabs ELB Challenge".

## Solution : follow 

- Script for Admin instance:

```bash
#!/bin/bash

# Switch to superuser (root) to execute commands that require elevated privileges
sudo su

# Update the system packages and software
yum update -y

# Install Apache HTTP Server (httpd) and PHP on the system
yum install httpd php -y

# Start the Apache HTTP Server service
systemctl start httpd

# Enable the Apache HTTP Server service to start on system boot
systemctl enable httpd

# Change the working directory to /var/www/html/ where web files are usually stored
cd /var/www/html/

# Download the index.html file from a specified URL
wget https://labtask228.s3.amazonaws.com/index.html

# Create a directory named 'admin'
mkdir admin

# Change the working directory to 'admin'
cd admin

# Download the index.html file for the admin section from a specified URL
wget https://labtask228.s3.amazonaws.com/admin/index.html

```

- Script for User instance:

```bash
#!/bin/bash

# Switch to superuser (root) to execute commands that require elevated privileges
sudo su

# Update the system packages and software
yum update -y

# Install Apache HTTP Server (httpd) and PHP on the system
yum install httpd php -y

# Start the Apache HTTP Server service
systemctl start httpd

# Enable the Apache HTTP Server service to start on system boot
systemctl enable httpd

# Change the working directory to /var/www/html/ where web files are usually stored
cd /var/www/html/

# Download the index.html file for the main site from a specified URL
wget https://labtask228.s3.amazonaws.com/index.html

# Create a directory named 'user' to store user-related web files
mkdir user

# Change the working directory to 'user'
cd user

# Download the index.html file for the user section from a specified URL
wget https://labtask228.s3.amazonaws.com/user/index.html

```

For the rest follow: https://github.com/Tcarters/Cloud-Security-Journey/blob/master/AWS-Security/Level3-Week7/Understanding_AWS_ALB_Path_Based_Routing.md


Done.... 🎌 🎌
