# Understanding AWS ALB Advanced Request Routing

### Advanced-Request Routing use cases

1. Separate bot/crawler traffic from human traffic.
2. Assign customers or groups of customers to distinct target groups and route traffic accordingly.
3. Implement A/B testing.
4. Perform blue/green or canary deployments.
5. Route traffic to microservice handlers based on method (PUT, GET, etc).
6. Implement access restrictions based on IP address or CDN (CloudFront).
7. Selectively route traffic to on-premises or in-cloud target groups.
8. Deliver different pages or user experiences to various types and categories of devices.

### What is Elastic Load Balancing?

1. ELB is a service that automatically distributes incoming application traffic to the underlying application.
2. ELB can be enabled within a single availability zone or across multiple availability zones to maintain consistent application performance.
3. ELB offers features like:
   - Detection of unhealthy EC2 instances.
   - Spreading EC2 instances across healthy channels only.
   - Centralized management of SSL certificates.
   - Optional public key authentication.
   - Support for both IPv4 and IPv6.

4. ELB accepts incoming traffic from clients and routes requests to its registered targets.
5. When an unhealthy target or instance is detected, ELB stops routing traffic to it and resumes only when the instance is healthy again.
6. ELB monitors the health of its registered targets and ensures that the traffic is routed only to healthy instances.
7. ELB's are configured to accept incoming traffic by specifying one or more listeners. A listener is a process that checks for connection requests.
8. Listeners are configured with a protocol and port number from the client to the ELB, and vise-versa i.e., back from ELB to target.
9. ELB supports 3 types of load balancers:
    - Application Load Balancers
    - Network Load Balancers
    - Classic Load Balancers

10. Each load balancer is configured differently.
11. For Application and Network Load Balancers, you register targets in target groups and route traffic to target groups.
12. For Classic Load Balancers, you register instances with the load balancer.
13. AWS recommends users to work with Application Load Balancer to use multiple Availability Zones because if one availability zone fails, the load balancer can continue to route traffic to the next available one.
14. We can have our load balancer be either internal or internet-facing.
15. The nodes of an internet-facing load balancer have Public IP addresses, and the DNS name is publicly resolvable to the Public IP addresses of the nodes.
16. Due to the point above, internet-facing load balancers can route requests from clients over the Internet.
17. The nodes of an internal load balancer have only Private IP addresses, and the DNS name is publicly resolvable to the Private IP addresses of the nodes.
18. Due to the point above, internal load balancers can only route requests from clients with access to the VPC for the load balancer.
19. Both internet-facing and internal load balancers route requests to your targets using Private IP addresses.
20. Your targets do not need Public IP addresses to receive requests from an internal or an internet-facing load balancer.


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b249123c-2906-49ee-a1f5-c3f9c85c58d5)


## Task 2: Launching an EC2 Instance with Bash Script

- Create an iNstance

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2f64217f-e5ec-428e-8452-7920b7d8b787)

- Create Key:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f63688b6-10e6-4093-92bc-1b00f4634c10)

- Inbound Security:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/12228c6c-07e9-44de-a01c-2cb31a353c91)

- Under User Data:

```bash
#!/bin/bash
sudo su 
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
cd /var/www/html/
wget https://labresources.whizlabs.com/92a9ca7235acf4a0ad31e9c76c42b92d/index.html
systemctl restart httpd

```

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/07e635d0-c3b6-4e11-b5b3-a2f11816b3b8)

- Access Web page:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9fc587ce-f522-4be5-91da-d541bcf516b4)




## Task 3: Create an Application Load Balancer

- Create a Load Balancer:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/95dea9ed-588c-47e9-b1fd-14354a7375d9)

- Select Application loadBalancer:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0f5895aa-bf0d-4293-8d7b-c0e184c469e7)


- Select all Az

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/01bcd226-8f94-4620-a7a5-26f1fc72b8d5)


- Listeners and Routing: 

Target group : Select Create Target Group hyperlink. You will be navigated to a new tab.

Choose a Target type: Select Instances

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/14f3b950-df55-4e84-9c22-16cc722113e9)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fafaf443-c9bc-4762-9416-9fd9299f8b69)

- Register Targets :
Under Instances, choose the EC2 instance which you created in the above step.

Check the running instance checkbox and select it now click on Include as pending below.(Important)

Click on Create Target Group button.

Navigate back to Load Balancer tab and click on refresh button under Default actions.

Select the Target group you created. 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/142abc84-71a0-49a9-a7af-7dbd0c4de28a)

- Return back on `Create LoadBalancer`

Click on Create load balancer button. It will take 5-10 minutes to create the same. 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/05e2d0bc-4c5a-4e77-8a23-9edcfec265d2)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3930bb92-e438-4a1e-978e-35ffb1745bfb)

- Copy the DNS of the load balancer and paste it in the browser. 


## Task 4: Configure Advanced-Request Routing

- Select the MyArrLoadBalancer LoadBalancer and select the Listeners and rules tab.
- Select the rule and under Managed rules, select Add rule.


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f822b957-2eac-4cff-b90a-4e757d837bc3)

- Create a rule:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4b6e6ac9-48bc-451b-adb7-761dc99955a3)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7b46d4a1-e860-48e7-b48d-a4756d1f2955)

- Add COndition:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f25b4f5d-f9d6-4001-8078-5bca3ccec7b8)



```html
<html>
<head>
<title>Super User</title>
</head>
<body>
<p>
<img width="400" src="https://labresources.whizlabs.com/92a9ca7235acf4a0ad31e9c76c42b92d/whiz-logo_07_38.png"/>
</p>
<br/>
<h1>Welcome to Super User Page</h1>
</body>
<style>
body {
    text-align: center;
    background-color: black;
    Color : white;
}
</style>
</html>

```
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/096d92dd-0d6f-4e74-b242-67272777f076)

- Add a second Rule:


  ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/86b68d47-6f52-468b-9edd-bfae343b981e)

```html
<html>
<head>
<title>User</title>
</head>
<body>
<p>
<img width="400" src="https://labresources.whizlabs.com/92a9ca7235acf4a0ad31e9c76c42b92d/whiz-logo_07_38.png"/>
</p>
<br/>
<h1>Welcome to Amazon Page</h1>
</body>
<style>
body {
    text-align: center;
    background-color: black;
    Color : white;
}
</style>
</html>
```
- With `Priority 2`

- Review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b05a5d52-ba30-433a-99ba-f148e41fa67b)


## Task 5: Test the ELB configuration

