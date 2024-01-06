# NAT gateway - AWS VPC Challenge


### Cloud Challenge Details

A company ABC launches two EC2 Instances, one to deploy a web application in Public subnet and the other to host another application in Private subnet. As a part of the infrastructure, they need internet access to Private Instance but secured. Now your are a Security Engineer and your challenge is to build the entire Infrastructure from scratch so, that the dev team can host their application in both EC2 Instances.

Follow the below instructions to complete this challenge.


#### Create an Amazon VPC named MyVPC with IPv4 CIDR: 10.0.0.0/16 and No IPv6 CIDR.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/884d835a-738a-4b43-a904-2f36ba9d215d)

#### Create Public and Private Subnets in MyVPC with IPv4 CIDR 10.0.0.0/24 and 10.0.1.0/24 Respectively.

- Create Public Subnet :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/906f640a-a671-4a6b-ad5b-15c6f973dbfc)

- Create Private Subnet:


#### Enable auto-assign public IPv4 address to Public subnet.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6717624a-c187-496b-b090-38e5a68db276)

#### Create an Internet gateway named MyIGW and attach it to MyVPC 

- Create Internet gw
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e99923b1-c9d4-41a0-8e2c-6ed4e64c58fa)

- Attach igw to VPC:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0a8d258e-c262-486a-8667-8783c8f58a4b)


#### Create a Public Route table in MyVPC and add Internet Gateway public route in it. 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2ddb038f-1fa1-4182-b86e-7d4b91070ea0)

- Associate it to Igw :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/082c4425-3319-4d63-929c-4ae677f1a30c)

#### Associate the Public Subnet to the Public route Table.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/41a237ce-647a-4967-a496-3b540d03e65b)

#### Launch an MyPublicEC2Server Instance in Public Subnet with the following configuration:

Select Amazon Linux 2 AMI 

Select t2.micro instance type

Create 8GB gp2 EBS Volume.

Select MyVPC and MYPublicSubnet and Enable Auto-assign Public IP

Create a new security group MyEC2Server_SG and add SSH port with source Anywhere.

Create a new Key Pair for the Public EC2 Instance.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/68c313cd-91a6-4514-8585-547df212a497)

#### Launch an MyPrivateEC2Server Instance in Private Subnet with the following configuration:

Select Amazon Linux 2 AMI 

Select t2.micro instance type

Create 8GB gp2 EBS Volume.

Select MyVPC and MYPrivateSubnet and Disable Auto-assign Public IP

Select the Security Group created for first instance.

Create a new Key Pair for the Private EC2 Instance.


#### SSH into Public EC2 Instance and test Internet Connectivity.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/76b25306-a9e2-431f-b932-f2fd87c239d1)

- Next SSH into Private EC2 Instance from Public EC2 Instance  and run the following Linux commands in Private EC2 Instance. (Since no internet access is provided for Private EC2 instances, you will not be able to run the bellow)


#### Create a MyNATGateway  in Public Subnet of VPC MyVPC to provide Internet access to the private instance. 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c709f961-9a8e-49b6-bd9a-843ff015937d)

- Update the Main Route table (which is different from one created by you) and Add NAT Gateway public Route.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c812796a-b5da-40b6-aa71-e591ff613029)

- SSH private instance from public instance:

  ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a6cec611-ec0d-429b-8173-0efef843170a)

- install packages in private instance :

``

You need to be root to perform this command.
[ec2-user@ip-10-0-1-120 ~]$ sudo yum -y update
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                                                                                       | 3.6 kB  00:00:00
amzn2extra-docker                                                                                | 2.9 kB  00:00:00
amzn2extra-kernel-5.10                                                                           | 3.0 kB  00:00:00
(1/7): amzn2-core/2/x86_64/group_gz                                                              | 2.7 kB  00:00:00
(2/7): amzn2-core/2/x86_64/updateinfo                                                            | 760 kB  00:00:00
(3/7): amzn2extra-docker/2/x86_64/updateinfo                                                     |  13 kB  00:00:00
(4/7): amzn2extra-kernel-5.10/2/x86_64/updateinfo                                                |  42 kB  00:00:00
(5/7): amzn2extra-docker/2/x86_64/primary_db                                                     | 105 kB  00:00:00
(6/7): amzn2extra-kernel-5.10/2/x86_64/primary_db                                                |  21 MB  00:00:00
(7/7): amzn2-core/2/x86_64/primary_db                                                            |  69 MB  00:00:01
No packages marked for update
[ec2-user@ip-10-0-1-120 ~]$ yum install httpd -y
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
You need to be root to perform this command.
[ec2-user@ip-10-0-1-120 ~]$ sudo yum install httpd -y
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Resolving Dependencies
--> Running transaction check
---> Package httpd.x86_64 0:2.4.58-1.amzn2 will be installed
--> Processing Dependency: httpd-filesystem = 2.4.58-1.amzn2 for package: httpd-2.4.58-1.amzn2.x86_64
--> Processing Dependency: httpd-tools = 2.4.58-1.amzn2 for package: httpd-2.4.58-1.amzn2.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.4.58-1.amzn2.x86_64
--> Processing Dependency: httpd-filesystem for package: httpd-2.4.58-1.amzn2.x86_64
--> Processing Dependency: mod_http2 for package: httpd-2.4.58-1.amzn2.x86_64
--> Processing Dependency: system-logos-httpd for package: httpd-2.4.58-1.amzn2.x86_64
--> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.4.58-1.amzn2.x86_64

``

- Check web server running on private

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/55c10beb-bc1f-4f3d-b10d-7cb8a328aa5f)


Game over 🎌


