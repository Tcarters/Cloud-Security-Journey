# Building a Resilient AWS Architecture to withstand hardware failovers and get notified using SNS from scratch

__What is Amazon RDS?__
Amazon RDS
Amazon Relational Database Service (Amazon RDS)  is a Relational Database service that offers high availability and throughput.

Amazon RDS comes with great features that include a Multi-AZ feature and Read Replica that ensures no data loss.

Amazon RDS also provides you with high scalability where you can scale up and scale down depending on your needs.

Amazon RDS provides you with six familiar database engines which include MySQL, Amazon Aurora, PostgreSQL, MariaDB, Oracle Database and SQL Server.
 

__Multi-AZ__
Multi-Availability Zone ( Multi-AZ ) is a feature that comes with Amazon RDS that provides you with high availability and durability for Database instances.

When we are opting for the Multi-AZ database instance, it will automatically create a Primary DB instance and parallelly replicate the data to the standby instances in different availability zones in that region. However, we can't access the standby instances, unlike primary instances.

The main purpose of Multi-AZ is to provide a failover option for primary RDS instances.

Amazon RDS uses the Failover mechanism for Oracle, MYSQL, MariaDB, and PostgreSQL instances.

The RDS Failover process happens automatically and is managed by AWS  without human intervention.

Amazon RDS uses the concept of SQL Mirroring for Replicating data to standby instances in the different availability zones and both primary and standby instances use the same endpoint.
 

__Reasons for Failover__
The failover process will take place due to one of the following reasons occurring in the primary instances:

Host Failure 

DB instance class modification.

Instance rebooting

Availability zone failure

RDS maintenance
     

__Conditions for enabling Multi-AZ on RDS__
A minimum of two different availability zones should be present in a DB subnet group where you are launching your Primary DB instance.


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a0617265-0340-4507-a570-d583dd287ec6)

## Task 2: Create a VPC

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7d4236bd-37de-49c8-ad43-6681dfc3da96)

## Task 3: Create and configure Internet Gateway

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/45bb300f-9952-4d39-a59a-4c0de6dff8c2)

- Select MyVPC which you created from the list and click on Attach Internet gateway button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/53683bdf-2e0c-4f00-8aee-ba0564e68a34)

## Task 4: Create public and private subnets

- We are creating a public subnet for our EC2 instance.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/dea29e87-2378-461a-83f9-ec526ddd42ac)

- We are now creating the First private subnet,

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0156121f-5000-4562-997c-e6b7891845d3)

- We are now creating the second private subnet,

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b2ff6381-7962-4031-b80e-bfee82e2b5e0)


## Task 5: Create a Public and Private Route Table

- Create a public Route Table:
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5a029f4c-0c3c-47eb-8135-d6e3e75eeb95)

- Now, add a route to allow Internet traffic to the VPC.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/56fd427d-cddf-4799-b905-0245cfb1e0d7)

- Now associate the subnets to the route tables.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6b267517-d256-4a54-a751-c66ede4a1a78)


