# Access Amazon SQS using Amazon VPC Interface Endpoint

__VPC endpoint for SQS__

VPC Endpoint allows us to securely connect your VPC and supported AWS services powered by AWS PrivateLink. AWS PrivateLink is a service that allows you to access AWS services by using private IP addresses. In this case, traffic does not leave Amazon’s network.

VPC endpoint does not require a NAT Gateway, NAT instance, Internet Gateway, or any VPN services to access AWS Services.

There are two types of VPC endpoints: Gateway and Interface.

VPC endpoint for SQS comes under Interface endpoint.

When you create a VPC endpoint for SQS, it asks for the VPC, Subnet, Security group, and the option of enabling the DNS Endpoint.


## Architecture Diagram:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8cd0f689-84ea-4d4a-8fbc-ab725236ee8b)


## Task 2: Create an SQS Queue and copy the Queue URL

- Navigate to the Services menu at the top, search for SQS and select it. You’ll be redirected to the SQS console page.

- Click on the Create Queue button.
- Now, under Details select Type as a Standard queue.
- Name: Enter MyWhizQueue
- Leave other settings as default and click on Create queue button.
- A queue will be created and your screen will look similar to the screenshot below:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/aa75c7b4-77a2-413a-88b5-aa5cbe73f789)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2a8c3f32-0274-4487-b8f2-81acc434c5c9)


## Task 3: Create a VPC and Enable DNS Hostnames option

- Create a new VPC by clicking on the Create VPC button.

Select VPC only option.
Name tag - optional: Enter MyVPC

IPv4 CIDR block: Enter 192.168.0.0/26

IPv6 CIDR block: No IPv6 CIDR block

Tenancy: Default

Click on the Create VPC button to create the MyVPC.

VPC is now created and by default DNS hostnames option is not enabled. Note down the VPC ID, required in the next steps.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6786e99b-daa0-4c81-bff2-74d5fea904af)

- To Enable the DNS hostnames option, click on the Actions button and select the Edit DNS hostnames option.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2cc4f38b-dffb-4703-a962-96b26de42c7a)


## Task 4: Create and attach an Internet Gateway with custom VPC

- By default, instances that are launched in a VPC cannot communicate with the Internet.

To enable Internet access, an Internet gateway needed to be attached to the VPC.

- Click on Internet Gateways from the left menu and click Create Internet Gateway.

Name Tag: Enter __MyInternetGateway__

Click on Create Internet gateway button.

- Select the Internet gateway you created from the list.

Click on Actions.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9455ea7b-ead1-40d9-8d1f-8c6e2c285476)

- Select the Attach to VPC.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/28c23e97-4234-4ebb-80ba-ae9818d12a8b)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ed7b5207-46d6-4ac7-a2a4-99ab433f9e00)


## Task 5: Create a Subnet

- To create a subnet click on Subnet the present in the VIRTUAL PRIVATE CLOUD section on the left sidebar.

Click on the Create Subnet button.

In the VPC ID, select MyVPC.

Create the first subnet, you will use this subnet to launch public instances, this subnet will be associated with the main route table of the VPC:

Subnet name: Enter Subnet

Availability Zone: Select US East (N. Virginia) / us-east-1a

IPV4 CIDR block: Enter 192.168.0.0/27

Click on the  Create Subnet button to create a subnet.

The subnet is now created.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/949ea792-730b-4f84-93b2-37a0a493db14)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8017dec0-893f-4cd6-b6b9-1bdab30e0a56)


## Task 6: Configure the Subnet to enable auto-assign public IPv4 address

- To modify the auto-assign IP settings for the Public subnet, do the following:

Select the Subnet

Click on the Actions button

- Choose Edit subnet settings from the options.
- Check the option Enable auto-assign public IPv4 address under Auto-assign IP settings

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/dd3bb58c-68b5-48d5-87be-426e82a60fd4)


## Task 7: Add an entry to the Internet (0.0.0.0/0) in the Main Route Table

- By default, custom VPC's main Route Table will have access to VPC's CIDR range only. For this lab, we need internet access.

- Let's add the route of the internet gateway as destination and 0.0.0.0/0 as Target.

Select Route tables from the left panel.

- To filter the correct route table, click on the search box and choose VPC as properties then select the VPC having ID same as copied.

 ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/290526a1-cb56-4c34-9640-2a566dcb4160)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c51c1ca5-3c7a-421c-9dc5-a61eec75c98c)

- Routes are now edited.
- Close the pane, and Check the Routes of this Main Route Table. Entry to the Internet i.e. 0.0.0.0/0 via Internet gateway is present in the Routes.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/984508b9-44e0-44db-bd28-d20f2c8bd3ff)

## Task 8: Create a Security Group for EC2 Instance


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a27168be-904a-4f3c-a9a4-31527a62fba7)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/75e424b4-4532-43ef-b920-124e8e41130b)


## Task 9: Launch an EC2 Instance

 - Use existing SG for instance creation

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6ec1e83f-e0e2-4071-81bf-a6229e465246)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0201dbda-a795-4abc-9b17-89a7a057cdc2)


## Task 10: SSH into the Endpoint instance

``
aws sqs send-message --region us-east-1 --endpoint-url https://sqs.us-east-1.amazonaws.com/ --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/MyWhizQueue --message-body "Hello from Amazon SQS."
``

## Task 11: Create a VPC Endpoint for SQS

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/68a38620-203b-42f1-ab62-2641783e5a6a)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d093dfe6-39c7-4465-92e4-d3216991a48e)




Done .... 🎌

