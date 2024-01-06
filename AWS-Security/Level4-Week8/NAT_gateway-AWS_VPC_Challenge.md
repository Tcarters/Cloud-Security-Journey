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

