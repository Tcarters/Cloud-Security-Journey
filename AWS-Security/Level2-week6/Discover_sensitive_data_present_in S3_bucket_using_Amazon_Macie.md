# Discover sensitive data present in S3 bucket using Amazon Macie


What is Amazon Macie ?
Amazon Macie uses pattern matching and machine learning to protect the sensitive data stored in S3 buckets.

It detects a list of data types including PII (Personally identifiable information) such as names, addresses, credit card numbers, etc.

Along with detecting data, it gives you complete visibility of your S3 buckets and its information like publicly accessible buckets, unencrypted buckets, and buckets shared with other accounts.

To get started with Amazon Macie, you can use its free trial of 30 days for bucket evaluation.

The free trial does not include the discovery of sensitive data present in S3 buckets.


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c894f23b-35dd-453e-8176-ff139a9f0224)


### Task 2: Enable Macie for the account

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5ede17cd-a298-4b80-9f5e-4918cf1872c9)

- On the Get started page, click on the Enable Macie button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/10c703db-8918-49e3-8b32-414a5f73ce44)

### Task 3: Create a Macie job

- Macie will try to find out all the details of the account, which may take some time. No need to wait, simply click on the __Create job__ button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6161c862-fa49-4184-bb7b-ff14d1209a9c)


- Select existing bucket :


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0446d656-f593-4458-b35f-f2918a6994b5)

- Select next

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fa6af876-2a9c-454a-bb53-8a9387b45fdf)

- Next

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8812516e-1158-48d3-9172-aff55e7a2fe2)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/de90930d-8b9b-455d-b350-58ce6ab95919)

- Click next to create a custom data identifer:
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d8699cec-2ff7-4f4e-8e3d-f9d274fce0d7)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7ac9f8a4-5cbf-43f5-a229-8d79604758a9)


- Review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/551b3391-0dcf-43f2-a5fb-58810b089c2f)

- For Step-7, In General Setting : Enter a name and description,

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ef3cba29-8b9b-4e14-8a55-d2e98c0dc503)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4c75605d-d712-4a67-9a0d-46acd0cedd4c)

- Review everything, click on the Submit button present below.
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/da53dd4e-d52a-4694-bcd0-e671dd0167d9)



## Task 4: Macie job run and findings

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/77eb8e8d-6c19-4f9e-82e6-c309b60261c1)

Once the job is created, it will start running immediately. 

The job runs for approximately 10 minutes and gathers the findings.

After 10 minutes, the status is changed to Complete.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6d2da17b-cced-46ce-967c-f45931be584b)

To view the Findings for the job, perform the following:

Click on the Job present there.

Select Show results

And Choose Show findings


- Finding generated:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2372de6e-4cfa-4446-a548-fe9501679c64)

DOne... 🎌
