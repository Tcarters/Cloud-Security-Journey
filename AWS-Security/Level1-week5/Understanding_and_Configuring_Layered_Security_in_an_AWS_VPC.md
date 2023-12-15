# Understanding and Configuring Layered Security in an AWS VPC

__Amazon Virtual Private Cloud__
Amazon VPC allows us to launch AWS resources in an isolated network that is defined by us in a more private and secure environment.

This feature enables us to increase the security level of the AWS resources.

The AWS resources can be protected using multilayered VPC which includes security groups and Network Access Control list.

The VPC security group provides security at instance level which acts like a firewall and controls both inbound and outbound traffic.

The VPC NACL provides security at Network Level i.e subnet level which acts like a firewall for associated subnets and controls inbound and outbound traffic.




## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/160ad61e-9903-45c4-8368-035a1612d14d)



## Task 2: Creating a new VPC

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3830022f-0189-4a69-9eea-dea9cc45fa86)

- Create VPC

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f87a4bd5-cb3f-46bc-b925-dc44903b9c2c)



## Task 3: Creating and attaching an Internet gateway

1. Click on __Internet Gateways__ from the left menu and click on Create internet gateway button and enter the following details:
* Name tag: Enter kekelabs_IGW
* Click on Create __internet gateway__ button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/bf5a1a4c-1a13-4e8b-bbec-45ef873d48b8)

2. Select the Internet gateway you created from the list.

Click on Actions button.
Click on Attach to VPC button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fe6d6523-aa48-43ce-8e6d-7ed83c6a94ac)


## Task 4: Creating two Subnets

1. You will create 2 Subnets, one for public and another for private resources. First, we will create a __public subnet__. 
- Public Subnet
  VPC ID: Select __kekelabs_VPC__ (Select the VPC which you created from the dropdown) 

Name tag: Enter public_subnet

Availability zone: Select No Preference

IPv4 CIDR block: Enter 10.0.1.0/24

Click on __Create subnet__ button

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1e4ecd91-1a86-453d-8516-56db74cc4953)


- Private Subnet
  VPC ID: Select kekelabs_VPC (Select the VPC which you created from the dropdown) 

Name tag: Enter private_subnet

Availability zone: Select No Preference

IPv4 CIDR block: Enter 10.0.2.0/24

Click on Create subnet button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e073ae06-bb6f-4cf0-9616-c9f2ba51d629)


## Task 5: Creating Route tables, configuring routes and associating them with Subnets 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d079f0be-133e-40ad-81f5-7d78b2f1e0e5)

1. You will create 2 route tables, one for public routes and another for private routes.
2. Go to Route Tables from the left menu and click on Create route table button. 

Name tag: Enter public_route

VPC: Select whizlabs_VPC (Select the VPC you created from the dropdown)

Click on Create route table button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1b78c397-9cf8-4b76-817b-e0a7432ecf34)

- Private route

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/65a2b4da-9621-443a-a03d-6bfc7a6d80b2)


4. Now, you need to add routes to the Route Tables. 

- Select public_route.
- Go to the Routes tab. Click on Edit routes. On the next page, click on Add route.
- Specify the following values: 
  Destination: Enter 0.0.0.0/0
  Target: Select Internet Gateway from the dropdown menu to select whizlabs_IGW.
  Click on Save changes button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8f4d3dc6-d35e-476a-a218-87ce616a90b0)


5. Next, you need to associate the public_subnet with this public_route. Select the public_route and go to the Actions and in that go to Edit Subnet Associations tab.

- Click on Edit Subnet Associations.
- Select public_subnet from the list.
- Click on Save Associations button. 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/bbf8265f-a6f2-4773-a7ce-c5dd5a39fc0a)

- Similarly, you need to associate the private_subnet with this private_route. Select the private_route and go to the Actions and in that go to Edit Subnet Associations tab.
- Click on Edit Subnet Associations.
- Select private_subnet from the list.
- Click on Save Associations button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a10dcf90-461f-42a1-bfeb-1e6b96a514ba)

## Task 6: Creating Security Group

In this task, we are going to create a security group for the EC2 Instance. 

Go to Security Group from the left menu and click on Create security group button and then provide the following details:

Security group name: Enter whizlabs_securitygroup

Description: Enter Security group for multilayered VPC

VPC: Select whizlabs_VPC (select from the dropdown)

Under Inbound Rules, click on Add Rule button.

To add SSH,

Choose Type: Select SSH 

Source: Custom - 0.0.0.0/0

To add All ICMP - IPv4,

Click on Add Rule

Choose Type: Select All ICMP - IPv4 

Source: Anywhere IPv4

Click on Create security group button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/dfc123d2-f670-47e9-a7c2-41b3bbf5b9f7)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a5b670bd-8845-4b4d-b1cc-e784d57cf0eb)


## Task 7: Creating and configuring Network ACL

Go to Network ACLs from the left menu and click on Create network ACL. Provide the following details:

Name tag: Enter whizlabs_NACL

VPC: Select whizlabs_VPC (Select the VPC which you created from the dropdown)

Click on Create network ACL button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d6f27248-da3e-4ee6-b830-183303e7825a)

2. Select whizlabs_NACL and go to Inbound rules tab. Click on Edit inbound rules and then click on the Add new rule. 

Add the following rules:

For SSH, click on Add new rule,

Rule number : Enter 100

Type: Choose SSH (22) 

Source: Enter 0.0.0.0/0

Allow / Deny: Select Allow

For ALL ICMP- IPv4, click on Add new rule,

Rule number : Enter 200

Type: Choose ALL ICMP - IPv4 

Source: Enter 0.0.0.0/0

Allow / Deny: Select Allow

Click on Save changes button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0f6d7d44-60a9-48dc-8cb5-e09a70a4a8d2)

4. NACLs are stateless. You need to add the rules in Outbound rules too. 

Select whizlabs_NACL and go to Onbound rules tab. Click on Edit onbound rules and then click on the Add Rule button.

For ALL ICMP- IPv4, click on Add new rule,

Rule# : Enter 100

Type: Choose ALL ICMP - IPv4 

Destination: Enter 0.0.0.0/0

Allow / Deny: Select Allow

For Custom TCP Rule, click on Add new rule,

Rule# : Enter 200

Type: Choose Custom TCP Rule 

Port Range: Enter 1024 - 65535

Destination: Enter 0.0.0.0/0

Allow / Deny: Select Allow

Click on Save changes button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/24095190-dd98-4d85-95d6-5188c87432bd)


- You need to associate both public and private subnets with the NACL. 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/02255322-463a-4db7-8975-de619f39c5d1)

- Save

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8d02032b-cdd6-4b4d-9d7a-fbf72a540665)


## Task 8: Launching 2 EC2 Instances
1.  Navigate to Services and choose EC2 under Compute
2.  Navigate to Instances on the left panel and click on Launch Instances button.
3.  Name : Enter public_instance
4.  For Amazon Machine Image (AMI): Search for Amazon Linux 2 AMI in the search box and click on the select button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4d9e81d9-5d4b-41c1-a0fe-b644edbfcf2b)

- Create ssh key
 
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4ba466b0-6dbb-4b4d-aa94-9509d8f3ae64)

-  In Network Settings Click on Edit button:

VPC: Select kekelabs_VPC 

Subnet: Select public_subnet 

Auto-assign public IP: Enable

Choose Select an existing security group and remove default one then select kekelabs_securitygroup 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b95c43c7-4085-4342-89a5-f365831f5d2e)

- Same for private instance

Similar to the above, launch another EC2 instance:

Name the instance as private_instance 

Key pair : Select the existing one

VPC: Select keklabs_VPC 

Subnet: Select private_subnet 

Auto-assign public IP: Disable

Choose Select an existing security group and remove default one then select kekelabs_securitygroup

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/560a2b8a-6898-4c27-9ba1-c62695116bbd)

## Task 9: Testing the EC2 instances


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b959b182-8f18-4285-b110-176788dbcbc6)

- Select the publc_instance from the EC2 dashboard and copy the public IPv4 address.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7c8f542b-c969-4072-8899-1f23e98dcf7b)

- Then ping  private instance from public machine:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b51f31b8-ea6f-4dc8-acb9-286148f67582)


DOne ....

