# Check the Compliance status of Security group using AWS Config


### What is Config

1. AWS Config comes under the Management & Governance category in the list of present categories and services.

2. Config takes care of an audit, evaluation, and assessment of AWS Resources in your account.

3. It is labeled as "Record and evaluates configurations of your AWS resources", according to AWS.

4. AWS Config does the following:
   - It retrieves current and historical configurations of the account.
   - Evaluated the configuration of your AWS resource for the desired setting and send you the notification whenever a resource is created, modified, or deleted. 
   - It also shows the relationships between AWS resources.



## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c47ceaf6-ed23-4b09-85a9-179c1f17af1b)


## Task 2: Setup Config with 1 Click option

Make sure you are in the N.Virginia Region.

Navigate to Config by clicking on the Services menu available under the Management & Governance section.

On the Home page of AWS Config, click on the 1-click setup option.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0bc58e14-683d-48fb-83cb-5510f4533594)

- Select confirm

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/08d44909-e463-4fd7-a1ba-62801aedc7ee)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0a86d10e-c442-4a96-b26a-a2019b09bf41)


## Task 3: Create a Config Rule

- On the left side panel, click on the Rules under AWS Config.

- Click on the Add rule button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c2639a12-c52e-4878-b035-e1e41ccb7700)


- Selet `ssh rule`

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f7d471a5-3d73-4956-9433-a4fd485604ea)

- Select the rule with the name restricted-ssh and click on the Next button.

- For Step-2, Configure rule, keep all the options as default, and click on the Next button.
- For Step-3, Review and create, review the settings and click on the Save button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/306ec2fd-2355-49f8-be54-3e462f9fe98d)


- Checking

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e8a83d9d-5848-4fd8-b04f-183da1c94468)


## Task 4: Create first Security Group

- Create a new security group
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3337a4d5-0c92-403c-bb8d-c8d1f9e1b40e)

- Click on the Add rule button under Inbound rules.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/422058af-ad99-44ac-82f7-55577cb192e8)

- Review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0a04097d-20e7-476a-8387-ca53a387be27)


## Task 5: Create second Security Group

- Same process for second security Group


## Task 6: Test the compliance status of the Security groups

- In this task, we are going to check if the security groups are marked as compliant or non-compliant by the AWS Config rule. 

Navigate to Config by clicking on the Services menu available under the __Management & Governance__ section.

On the left side bar, click on the Rules, and you will be able to see the rule is still in **compliant** status. 

- Check

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ee98f68f-a8e7-4183-9a28-839497e945c6)

- We canss on AWS Config that our created Sg are not compliance:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2cc821de-b312-4bcd-9c07-6a91c3fa29d7)

Done ... 🎌
