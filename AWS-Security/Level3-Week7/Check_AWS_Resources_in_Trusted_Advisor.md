# Check AWS Resources in Trusted Advisor

## What is AWS Trusted Advisor ?
AWS Trusted Advisor is an automated cloud service provided by Amazon Web Services (AWS).It offers real-time guidance and recommendations to help customers optimize their AWS infrastructure.

Trusted Advisor analyzes an organization's AWS resources and configurations.It compares the resources against AWS best practices and industry standards.

Trusted Advisor provides actionable insights to improve security, performance, and cost efficiency.

It covers various categories, including cost optimization, performance, security, fault tolerance, and service limits.

The service continuously monitors the customer's AWS environment for potential issues and optimization opportunities.

Trusted Advisor sends proactive notifications and alerts to keep customers informed about their infrastructure health.

It offers personalized recommendations tailored to the specific AWS resources and configurations used by each customer.

Trusted Advisor helps identify idle resources, underutilized instances, security vulnerabilities, and other optimization opportunities.

Customers can access Trusted Advisor through the AWS Management Console.

It integrates with other AWS services and third-party tools for enhanced functionality and integration options.

Trusted Advisor is available to AWS customers with an Enterprise-level support plan at no additional cost.


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a8614a47-35b8-4106-97d3-99bebbd5c9c4)


## Task 2: Checking the initial status of the Trusted advisor dashboard

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d1873675-19b9-4954-89b2-60d816dea385)

- We will create 2 unrestricted security groups and 2 public S3 buckets to understand more about Trusted Advisor.


## Task 3: Create a first unrestricted Security Group

- Create a first security group
- Security group name: Enter Security Group 1
- Description: Enter Second Security group
- VPC: Select Default VPC
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b623aa83-f6f8-4e0e-b157-21b8edd07a65)

- select an Inbound rule for SSH

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d9ad61a7-8e1f-447d-8490-263ba9ca045d)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3b8f1fa9-b70e-454f-8614-8bbab0145708)


## Task 4: Create a second unrestricted Security Group
- We are going to create a Security group for the ECS cluster.
- Same process as First security Group

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e65dff99-fc0d-4d80-adb6-c400401870a3)


## Task 5: Creating 2 Public S3 Buckets

- Create 1st S3 bucket
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/569d274f-cca8-46c9-8efd-fcf3330fa37d)

- Note: Making the bucket public .

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ca0215b5-6575-4ff0-ac62-862bc288fb13)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cbb523a1-2ca8-4a34-9a06-793d7ef363c9)

- Click on the bucket name and make it public using Bucket policy
- Click on the Permissions tab to configure your bucket.
- In the Permissions tab, Click on Edit button.

- Update S3 bucket policy with following code:

```json
{                       
  "Id":"Policy1",                   
  "Version":"2012-10-17",                   
     "Statement":[                      
     {                      
      "Sid":"Stmt1",            
      "Action":[    
        "s3:GetObject"      
         ], 
           "Effect":"Allow",    
           "Resource":"arn:aws:s3:::keke-s3-first/*",         
           "Principal":"*"  
       }                    
   ]                        
}       
```
- Click on Save changes button.

- Same process of Second S3 buckets

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9a5cd2a8-4cde-46db-a158-527c3a1fe8f4)


## Task 6: Refresh the Trusted advisor dashboard

- Back on Trusted Advisor page, we can see:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cb675a5f-3ba5-47e7-9230-9f2f83702545)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4a0a54fa-f36d-450d-95c8-7dd5d53984b5)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4113bf7d-06ef-43d6-a7a3-17f9a616f5a3)


DOne ....🎌
