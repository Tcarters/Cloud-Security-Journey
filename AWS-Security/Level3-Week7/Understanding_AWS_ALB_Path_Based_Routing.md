# Understanding AWS ALB Path Based Routing


### What is Path-Based Routing?

1. Path-Based Routing is a feature offered by Application Load Balancer (ALB) in Amazon Web Services (AWS).

2. It allows the ALB to route incoming requests to different destinations (target groups) based on the path specified in the URL's URI (Uniform Resource Identifier).

3. When a client sends a request to the ALB, the ALB examines the path component of the URI (the part of the URL after the domain name) and uses this information to determine where to forward the request.

4. Each path can be associated with a specific target group, which represents a set of EC2 instances or other resources capable of handling the incoming traffic.

 ### What is Elastic Load Balancing?

- Elastic Load Balancing (ELB) in AWS is a fully managed service that automatically distributes incoming application traffic across multiple resources, such as Amazon EC2 instances, containers, or IP addresses.

- It helps maintain high availability, fault tolerance, and scalable performance for applications by evenly distributing traffic and efficiently managing connections.

- ELB offers features like:
  1. Load Balancing: ELB acts as a load balancer that distributes incoming traffic across multiple backend resources to prevent overloading any single resource and optimize application performance.

  2. High Availability: ELB ensures high availability by distributing traffic across multiple resources in multiple availability zones. If one availability zone becomes unavailable, ELB can route traffic to healthy instances in other zones.

  3. Auto Scaling Integration: ELB seamlessly integrates with AWS Auto Scaling, allowing it to automatically adjust the number of resources based on demand. This ensures that applications can handle varying levels of traffic without manual intervention.

  4. Health Checks: ELB regularly performs health checks on registered instances to determine their availability and health status. Unhealthy instances are automatically removed from the load balancer, and traffic is directed to healthy instances.

- ELB supports 3 types of load balancers:

  1. Application Load Balancers
  2. Network Load Balancers
  3. Classic Load Balancers


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/16c1c62f-f4c3-4cda-956b-260db9dae00b)


## Task 2: Launching two EC2 Instance using Bash script

- Script in User Data:

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

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/43275a1d-d700-4d7c-9e6b-f1f750b15d5f)

- View the PHP file in the webserver :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9c533571-892c-401b-af43-ba2ecdddd98a)


- Now to access the admin page.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8ea7b89f-3e8f-4f78-a9ab-cd5d8b05277d)


#### Lanuch server 2

- Name: MyWebServer2

- Script for web server 2:

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

- review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/629b62e8-574d-4443-88e4-f1d4f82fd3ce)

- View the PHP file in the webserver for Second server:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/acf86962-0a10-480e-bf4f-958bafebac42)

- View User path:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c69eec69-e02d-4870-9994-2375576153d9)


## Task 3: Create an application Load Balancer

- n the left side menu, scroll down to the bottom and select Load balancer under Load Balancing.

Click on the Create Load Balancer button.

Click on Create button under the Application Load Balancer

The next five screens will require some custom configurations. If a field is not mentioned, leave it as default or empty.

Configure Load Balancer:
Load balancer name : Enter MyLoadBalancer

Scheme : Select internet-facing 

IP address type : Select IPv4

Network mapping:

VPC : Select default VPC. (scroll down)

Mappings: Select all available zones using the checkbox

Security Groups: 

Assign a security group : Select Select an existing security group 

Only choose MyWebserverSG (the Security Group created during EC2 instances launch).

Listeners: 

Load Balancer Protocol : HTTP

Load Balancer Port  : 80

- Click on the Create target group link.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/88414364-1ed0-4516-b24b-cf935c2b8f0d)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6601f075-cf95-49ab-839f-e49a8a30ae2b)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/18bfed71-f5c2-4ded-93d2-0160f63fcac6)

- __Register targets__


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/24650a7d-528a-4f64-b9c2-426f2b88c59a)

- Click on the Create target group.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/07f1ca48-8269-40bd-a1e4-d51207641cf5)

- For loadBalancer:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/12df110d-5e9e-4c77-8218-dfb48a777910)

- Sample DNS 


## Task 4: Configure Path Based Routing

- First lets create a path based route to the Admin page in Webserver1 EC2 Instance.

Now Navigate to the Target Groups in the left-side panel under Load Balancer in the Load Balancing section.

Click on the Create terget group button.

Basic configuration : 

Choose a target type : Select Instance

Target group name : Enter AdminTargetGroup

Health check path : Enter /admin/index.html

Leave all others as default.

Click on the Next button.

Under Register targets : 

Select the MyWebServer1 EC2 only.

Click on the Include as pending below.

Now MyWebServer1 is added to the Target section as shown below.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1c81dd8f-dd46-4803-a01c-c6ea25d07ea6)

- create Target Group for Admin for server 1

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/90777bf8-926e-4ab1-99d5-7ef616962d0d)


- Create TargetGroup for user: `UserTargetGroup`

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5e7dd30c-e242-4700-b054-16168d69f477)


- Add rules in LoadBalancer:

Rule for admin

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5d5ac476-c7fc-4935-89f1-1b3b53897235)

- WIth targetgrouop:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5b026bc1-f515-4091-8780-677e4a5f3f68)

- Add rule for `user` :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4ba4a6bf-00a0-458b-9fb2-bfacf19cf4ee)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b61f0eb9-80fd-4c72-a2b3-e22f9d51933d)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4246e91b-260c-4968-929e-1a735d737cbb)

- review Target Groups:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/51a98136-0cfd-4239-97bf-f8e59ff51d56)


## Task 5: Test the ELB configuration

- Acces Admin Page using ELB:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a0d42688-a47b-4e23-8e1c-01fcfaf0db66)

- Access User Page using ELB:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/821d8746-ae88-44d9-ac90-08c874068730)


Doneee........... 🎌 🎌
