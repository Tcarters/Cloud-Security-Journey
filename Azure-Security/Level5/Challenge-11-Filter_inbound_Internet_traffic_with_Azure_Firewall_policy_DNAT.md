# Challenge 11 - Filter inbound Internet traffic with Azure Firewall policy DNAT


__Cloud Challenge Details__

__
You are a skilled Azure network engineer at CloudCore Solutions, a renowned company known for its expertise in cloud-based solutions. Your client, a rapidly growing online business, relies heavily on Azure services to deliver their products and services to customers around the world. While their growth is a positive sign, it has brought challenges related to the security and management of inbound Internet traffic. The client is particularly concerned about ensuring the security of their Azure resources and the performance of their online services. They want to establish a robust and centralized approach to filter, inspect, and manage incoming Internet traffic effectively. To achieve this, they have chosen Azure Firewall as the primary tool for enhancing network security and controlling traffic flow. This will help them to enhance security, manage traffic effectively, and ensure that only authorized requests reach their backend systems.

Now, your challenge is to configure an Azure Firewall policy to filter inbound Internet traffic using DNAT. After successfully completing the challenge, you will have demonstrated your capability to create and configure an Azure Firewall policy to filter inbound Internet traffic using DNAT (Destination Network Address Translation).

Follow the below instructions to complete this challenge:

Create a Hub VNet.

Create a Spoke VNet.

Peer the VNets that you have created.

Create a Virtual Machine with the following instructions:

Select  Windows Server 2019 Datacenter - Gen2 as Image.

Select No infrastructure redundancy required as Availability options.

Select Standard_B2s as Size.

Select Standard SSD as OS disk type.

Deploy the Firewalls and Policy with the following instructions:

Select Firewall SKU as Basic.

Select Pricing tier as Basic.

Create a default route.

Configure the NAT rule.

Test the Firewall.
__


## SOlution 

### Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f32102ef-3da2-42a2-85e4-20cd47c67679)


### Create a Hub Net
- For subnet 
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/862fac73-f039-4829-8130-7fbb51890b0b)

- Review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9446d8b3-895e-4d1c-a7f0-ccbf21b9efaa)


### Create a spoke VNet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ae539264-466a-491a-be52-c79208557644)

- Review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/bbd0970f-5b2e-41ab-bad3-e19645d251e4)


### Peer the VNets that you have created.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/394d719e-ac47-484f-9dd1-ca948f1a6889)

### Create a virtual machine
- Sv-workload VM
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/39b86a03-262d-48df-8527-4979f2931152)


### Deploy the Firewall

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/336e17b7-e5f2-45be-9453-d197a1249767)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/527f8052-fa01-4018-885e-2327e1ddf2fa)



For rest follow: Cloud-Security-Journey/Azure-Security/Level2/Filter_inbound_Internet_traffic_with_Azure_Firewall_policy_DNAT.md

- - -
