
# AWS Access control alerts with CloudWatch and CloudTrail


### Cloudwatch

1. AWS Cloudwatch is the service that is used to monitor and collect the metrics from services periodically. This helps provide a clear picture for the users to understand how the resources are performing.

2.It collects data in the form of logs, events and metrics and provides you with an organized view of AWS resources, services and applications that run on AWS.

3. You can use CloudWatch to detect anomalous behavior in your environments and to set alarms, You can visualize data from the logs and take actions to troubleshoot the issue.

4. You can monitor AWS resources such as Amazon EC2, Amazon RDS, Amazon DynamoDB tables, and many others using CloudWatch.

5. You can monitor resource utilization in your account by setting up rules and events tto stop or terminate underutilized resources, reducing unnecessary cost.

6. In Autoscaling, servers are stopped or launched based on the events we create in CloudWatch.

7. CloudWatch also offers a feature to store logs for the services running in our account. For example, the logs for lambda functions will be stored within log groups in CloudWatch. Here we can get a detailed error log from any specific function.

### CloudTrail

- AWS CloudTrail is a service that helps us monitor, survey, and audit our AWS Account. 

- With the help of AWS CloudTrail, the user will be able to log, monitor, and retain account activity associated with actions across the AWS infrastructure. 

- CloudTrail provides complete account activity of the Amazon Web Services. CloudTrail also manages the functions performed with the help of the AWS Management Console, program line tools, AWS SDKs, and various other AWS services.

- This event history simplifies security analysis, resource amendment trailing, and troubleshooting.


## Architecture Diagram


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e473af8a-a09a-48ad-a0b1-0f0d110e1272)


### Task 2: Creating a CloudTrail

- Navigate and click on CloudTrail, which will be available under the  Management & Governance section of Services.

- Click on Create Trail on the right side.

- Under Create Trail, enter these details:

- Trail name: Enter __My_cloudtrail__.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4e16b22f-4fe7-47d2-9080-14e6549f14eb)


- Select the trail you have created, click on it. Scroll down you can see Cloudwatch logs section. 
    Click on the Edit button.

- CloudWatch Logs  :  Check Enabled

- Log group : Leave it as default (i.e New and default log group name)

- IAM Role : Select New and give the Role name as __clwatch_role__.

- Click on Save changes button 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a3059b7c-3aa2-478d-bb79-1e587107ed9b)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5c06c156-d70b-4462-810a-fdd7e9d11903)


## Task 3: Creating Metric Filters for Log Groups in Cloudwatch

1. Make sure you are in the N.Virginia Region.
2. Click on Services and navigate to the CloudWatch dashboard under Management & Governance.
3. Click on Log groups under Logs in the left panel.
4. Click on the log group we just created and click on the Actions.
5. Click on create metric filter as shown below:
6. Under Create filter pattern, provide the pattern you need to filter on. For this lab, we are going to filter for stopped instances.
7. Filter pattern                 :
   Enter the pattern { $.eventName= "StopInstances" }
   Select log data to test  : Select the cloudtrail log  in drop-down.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e1675e1c-f381-472e-93d9-dd44ed66ec15)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/59dd2d31-4cf6-47af-9083-faad1c82f9b4)

- Next we will create a filter using the following details:
- Filter name: Enter stoppedInstancecount
  - Metric details:
  - Metric namespace  : Enter CloudTrailMetrics
  - Metric name            : Enter EC2stoppedInstanceEventCount
  - Metric value            : Enter 1
  - Default value           : Leave default
- Finally, click on and Next review the given details. Click on Create metric filter to complete the metric filter creation.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8e2cb42c-960c-4e18-9452-dd5be410085c)

- review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cceb532b-0528-4bcc-9c02-dcda169dc17c)


## Task 4: Creating an Alarm

- In CloudWatch, select the log group created for our CloudTrail and then click on metric filters at the bottom.

- Select the Metric filter created in the above step and then click on create alarm as shown below:


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4aa913c0-432e-4ca9-b458-5cdaca2ae846)

- Specify the metric conditions as follows:

Namespace : CloudTrailMetrics (default)

Metric name : EC2stoppedInstanceEventCount (default)

Statistic        : sum (default)

Period          : 5 minute (default)

Conditions:

Threshold type: Select Static

Whenever EC2stoppedInstanceEventCount is :    than 1.

Click on Next.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c354cc8d-1079-45fb-9ced-ec7cee09dbde)

- Next we'll configure actions

Alarm state trigger                                              : Select in alarm

Select an SNS topic                                            : select Create new topic

Create a new topic                                              : Enter the topic name as My_Ec2count_topic

Email endpoints that will receive the notification :  Enter your Email address to receive the alert

Once you provide these details, click on create topic.

AWS will send a confirmation email to the Email address provided above. You will need to confirm the email subscription 

Note: If you are not getting any mail from AWS confirmation, Please check your spam

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b4c65684-0992-4a88-8f80-3e05e775120b)

- Confirmation Mail:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e0cf0681-29fd-4c65-9903-c435f17d1cf7)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1f06bcf7-f67e-4ca9-a32e-cae7eb0789b3)

- Review:

  ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7aa46f1a-5e52-487b-9c35-4d5de6a396e9)

### Test
- Stop Instance

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5eb3bf81-8911-4b9e-a5c0-0493023ff74e)

- Email Notification :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d2b297ad-fa71-4ccf-86da-ee1bb2081a41)




## Task 5: Creating an EC2 Instance to Trigger our Alarm

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4b8d61ba-8c10-4b75-a607-0fc621d4f0df)

- Key

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1a740684-a36b-48a3-9ef1-e39669493cf2)

- Secruity Group :
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d524d827-98d4-44db-a61d-d240fdee9bef)


Done 🎌
