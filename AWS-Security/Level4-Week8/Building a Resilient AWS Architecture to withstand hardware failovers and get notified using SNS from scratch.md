# Building a Resilient AWS Architecture to withstand hardware failovers and get notified using SNS from scratch

What is Amazon RDS?
Amazon RDS
Amazon Relational Database Service (Amazon RDS)  is a Relational Database service that offers high availability and throughput.

Amazon RDS comes with great features that include a Multi-AZ feature and Read Replica that ensures no data loss.

Amazon RDS also provides you with high scalability where you can scale up and scale down depending on your needs.

Amazon RDS provides you with six familiar database engines which include MySQL, Amazon Aurora, PostgreSQL, MariaDB, Oracle Database and SQL Server.
 

Multi-AZ
Multi-Availability Zone ( Multi-AZ ) is a feature that comes with Amazon RDS that provides you with high availability and durability for Database instances.

When we are opting for the Multi-AZ database instance, it will automatically create a Primary DB instance and parallelly replicate the data to the standby instances in different availability zones in that region. However, we can't access the standby instances, unlike primary instances.

The main purpose of Multi-AZ is to provide a failover option for primary RDS instances.

Amazon RDS uses the Failover mechanism for Oracle, MYSQL, MariaDB, and PostgreSQL instances.

The RDS Failover process happens automatically and is managed by AWS  without human intervention.

Amazon RDS uses the concept of SQL Mirroring for Replicating data to standby instances in the different availability zones and both primary and standby instances use the same endpoint.
 

Reasons for Failover
The failover process will take place due to one of the following reasons occurring in the primary instances:

Host Failure 

DB instance class modification.

Instance rebooting

Availability zone failure

RDS maintenance
     

Conditions for enabling Multi-AZ on RDS
A minimum of two different availability zones should be present in a DB subnet group where you are launching your Primary DB instance.
