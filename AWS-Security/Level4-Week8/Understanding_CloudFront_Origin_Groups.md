# Understanding CloudFront Origin Groups

__What is CloudFront?__

Amazon CloudFront is a content delivery network (CDN) offered by AWS.

It provides a globally-distributed network of proxy servers that cache content closer to end-users.

CDN improves access speed by reducing latency and minimizing the number of internet hops required to retrieve content.

CloudFront works on a pay-as-you-go basis, allowing users to scale their content delivery as needed.

It integrates with various origin servers, such as Amazon S3 and Amazon EC2, where the content is stored.

When a request is made for content, CloudFront delivers it from the nearest edge server, reducing latency and improving performance.

It supports both "Progressive" and "Streaming" delivery of content, allowing for optimized video streaming and dynamic content acceleration.

CloudFront can be used to distribute web content, videos, software downloads, and other bulky media.


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2ee4dbf7-5897-420e-97b4-8915e301b442)


## Task 2: Create S3 Bucket

- Create a bucket:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/50c7fd45-6c28-419c-a4d7-47a7c860e0bd)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/07d7b94c-8a69-41b3-8d5a-65031a03af7b)


## Task 3: Upload a file to an S3 bucket

- Upload an html file in bucket

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c2ea0752-ae36-4c27-ad9e-6d0700d2e71f)


## Task 4: Make the objects publicly accessible

- Edit policy permissions with:

```json
{       
"Id": "Policy1",        
"Version": "2012-10-17",            
"Statement": [          
{           
"Sid": "Stmt1",         
"Action": [         
"s3:GetObject"              
],          
"Effect": "Allow",      
"Resource": "arn:aws:s3:::kekelabs1234/*",           
"Principal": "*"                
}               
]               
}

```

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3327728e-86bd-44e3-b37a-69ce8ebfa07d)


## Task 5: Creating CloudFront Distribution

Select CloudFront under Networking and Content Delivery from the Services menu.

Navigate to the left side and select Distributions tab.

Now click on the Create distribution button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/de11f473-5838-4d3a-a61d-a00b45b84471)


- Now configure distribution as follows

Origin Domain Name

On click of input space, select your S3 bucket:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e780abd2-7387-40d0-86d3-4716d8630179)

- The domain name that Amazon CloudFront assigns to your distribution appears in the list of distributions.

Copy and paste the domain of CloudFront distribution in the new tab of your browser.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ce0b80b2-9661-4313-bb66-e81f2a91fae9)

- Review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/50f2413d-1af9-4f09-8bb4-1805f84f1eef)



## Task 6: Launching an EC2 Instance

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/eec563ac-7412-44d8-9477-be55ff76f5c0)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7ad02c9c-ebc9-4397-8928-5b2a553d7669)


- Script for additional web server:

```sh
#!/bin/bash
yum update -y           
yum install -y httpd        
systemctl start httpd           
systemctl enable httpd          
echo "<h1>Hello, this index.html page from $(hostname -f)</h1>" > /var/www/html/index.html
chmod 644 /var/www/html/index.html
echo "<h1>Hello, this index2.html page from $(hostname -f)</h1>" > /var/www/html/index2.html
chmod 644 /var/www/html/index2.html
systemctl restart httpd

```

- Access server Web:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/32e699a8-1287-4f59-be5a-2f89d2750f73)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/26c411fe-2b37-43a1-8ded-d6dc9e21bfc3)


## Task 7: Add EC2 as the Origin and create Origin Group

- we are going to add the EC2 instance as an additional origin to the CloudFront distribution and create an origin group. This allows CloudFront to distribute the content from both the S3 bucket and the EC2 instance, providing redundancy and failover capabilities.        

Before adding EC2 Instance as Origin, make sure CloudFront distribution is having Enabled status

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a2d29012-39cd-417a-9dc4-964e6dec92e7)


Once the CloudFront distribution is having Enabled status, click on the ID to add the origin.

- In the first option Origin domain, paste the copied Public IPv4 DNS of EC2 Instance.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ce41a5f7-ff07-4d8d-b0e4-aadd6af8a26e)

- Review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b245022b-2eaa-4af1-8ec7-f98cdd3258a8)

- Switch to Origins tab and scroll below and click on the Create origin group button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2a9241f5-2bbf-4139-af8d-a575d0465c5d)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c51ecfb1-9630-4ffe-a994-d665b6fcd152)

- Now Switch to the Behaviors tab.
- Select the present behavior and click on the Edit button.
- On the Edit behavior page, for the Origin and origin groups option, select the present Origin Group i.e. Whiz-Origin-Group from the dropdown.
- In Cache key and origin requests, select CashingOptimized

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0525bfde-e947-417e-8f5f-66e92ad2d360)


## Task 8: Test the Origin group

- Copy the Distribution domain name and paste it into the new tab of your browser.

- This should now display the index.html page from EC2 Instance as it has the Private IP DNS name.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ba767abc-bf9e-423d-ab67-e832c73bde43)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8587e734-20d1-4754-b6b9-04f06886364f)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b779d49e-d60d-4a92-8e92-bcd4e4152476)

