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

- Now associate the Public subnets to the Public route tables.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6b267517-d256-4a54-a751-c66ede4a1a78)

- Create Private <Route table

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/832f25c8-e10d-4489-87ec-6b9fe18b92e2)

- Now associate the subnets to the route tables.

Click on the Edit Subnet association tab.

Select WhizPrivateSubnet-1, WhizPrivateSubnet-2 from the list.


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4920d577-843c-48cc-8a49-f8985fbbfbbd)


## Task 6: Create a security group for EC2 and RDS  

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/786af91b-d7f9-4ce7-bb0e-3f991e04534f)

- We are now creating a security group for RDS.

Click on Edit inbound rules button, and Click on Add rule button.

Choose Type: MySQL/Aurora

Source: Select the security group of EC2 that was created earlier EC2-SG

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c30109d4-7ce6-4c75-8656-57a0d9f7c23c)

## Task 7: Create a subnet group for RDS 

click on Create DB subnet group. Under subnet group details,

Name:  Enter RDSMultiAZ-SBG

Description: Enter Subnet group for RDS Multi-AZ

VPC: Select MyVPC

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1c9bafc7-67ae-4751-922b-c2c44b2c2374)

Under Add subnets section,

Availability Zones: select us-east-1a,us-east-1b

Subnets: Select both IPv4 addresses of the private subnets we have created.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d395ab42-5bc8-4df1-afd3-bb706965e90f)

## Task 8: Launching an EC2 instance

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/09962eb6-1b90-4998-b0b6-a32b550d4783)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/accf3f6a-6d3c-46b4-9d62-93c7d7cb7075)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/16b8d229-32b6-422a-a67b-38207f233604)


## Task 9: Create a RDS database instance

Navigate to RDS by clicking on the Services menu in the top, then click on RDS under the Database section.

Make sure you are in the US East (N. Virginia) Region.

RDS dashboard will be displayed.

Click on the Create Database button and you are navigated to the page where you will provide all the required details to create a MySQL database.

On the page, click on the option Standard create a method for our lab requirement.

In the Engine options, select MySQL engine type.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6cbff1f9-f919-44b7-9782-b2c52f2456a5)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/abaf3aeb-452b-4442-95f6-6c73e3177104)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8acc6182-36d6-4eaf-95b7-91c53ddd550d)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/420ad407-92e9-44fe-8800-fdaf853b02e5)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9f6cd238-92a2-4b6a-b7c4-b6b53af76faa)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/04337653-90c0-4f2b-923e-ddb5646114f2)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/737aec01-f385-4559-9d39-953c05af8f57)


## Task 10: Configuring Cloudwatch metrics and adding a subscription

Navigate to CloudWatch by clicking on the Services menu at the top, then click on CloudWatch under the Management & Governance section.

Make sure you are in the US East (N. Virginia) Region.

Click on All alarms under Alarms in the left panel and then click on Create alarm button.

Click on Select Metric to choose the metric that will trigger our alarm

Copy the instance id of the EC2 instance(WhizEC2) created.

Now paste the instance id in the search bar.

We can see this EC2 > Per-Instance Metrics, click on it.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/531b868b-0feb-4cca-9c53-3da4ca884ce7)

Select the StatusCheckFailed_System metric and click Select metric button.


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3b7ddba6-44d0-497d-8286-6782bf3532eb)

Now, add the following conditions to it:

Statistics: select  Average

Period: select 1 minute

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3ed345bb-7249-4b38-9828-b85f3f3544c1)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/30dc10b3-e06a-47f3-ad6c-55cc20ec4b48)

- For recovery of EC2, we will create EC2 action, to do so, scroll down and click on Add EC2 action button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/88b36045-df70-4359-9459-e8d64fec5355)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2884920d-646a-4113-b407-72a82919dcf9)

Go to your email address and you would receive a notification from AWS. Check your spam email if you have not received it in the inbox.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ce24dd0d-c6df-4697-87d0-306c1d8f2acd)


## Task 11: SSH into the EC2 instance

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8225afad-a38f-415d-b68b-3976f877dd9b)

## Task 12: Triggering cloud watch alarm for EC2 instance hardware failure

```bash
aws cloudwatch set-alarm-state --alarm-name "EC2Recover" --state-value ALARM --state-reason "Simulate Hardware Failure"

```

- After this command, go to CloudWatch alarms. You can see the alarm changed to In alarm from Ok.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/49c93369-a85a-4cd1-bdff-93d7b59779ee)

- we got email :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/26e3a56e-f67d-40da-8348-b6318813e97a)

## Task 13: Creating SNS subscription for RDS failover

Navigate to RDS under the Database section of the Services menu.

Make sure you are in the US East (N. Virginia) Region.

On the left panel, we can observe the Event Subscriptions section, click on it.

Click on the Create Event Subscription,

Event subscription name: Enter RDSfailover

Target: choose New Email topic

Topic Name: Enter RDSfailNotification

With these recipients: Enter your mail id

In the source section,

Source type: Select Instances

Instances to include: Choose specific instances

Specific instance: Select database-1

Event categories to include: Select All event categories

Click on Create button.

Now go to your emails, and you will receive a notification from the AWS side.If you have not received it check in your spam mail.

Click on Confirm subscription link.

Your email address is now subscribed to SNS Topic RDSfailNotification.

Now, navigate to Database instances, on the left panel, click on database-1

In action select Reboot, check Reboot with Failover option.

Click on Confirm button.

Wait for a few minutes to fail.

You will now get a notification/mail in your inbox or your spam about the database failover.


Done ..... 🏴🏴
