# Filter inbound Internet traffic with Azure Firewall policy DNAT

What is a DNAT?
- DNAT is required when the server is on an internal network and must be accessed through another external IP address on a perimeter device. When traffic is received on the public IP address the destination IP address is replaced by the internal IP address.
- Once internal hosts can access the internet or WAN, the next test is to expose something on the internal network, such as a web server, and make it available from the internet. Since a device on the internet cannot connect directly to a device on someone’s private network, they need to have the traffic forwarded from the perimeter device to the internal device. This process is sometimes called port forwarding or Destination Network Address Translation (DNAT).
- You can configure Azure Firewall policy Destination Network Address Translation (DNAT) to translate and filter inbound Internet traffic to your subnets. When you configure DNAT, the rule collection action is set to DNAT. Each rule in the NAT rule collection can then be used to translate your firewall public IP address and port to a private IP address and port.
- DNAT rules implicitly add a corresponding network rule to allow the translated traffic. For security reasons, the recommended approach is to add a specific Internet source to allow DNAT access to the network and avoid using wildcards. 

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7d04fa22-52a3-44b1-965a-08bd3f2be7c6)

## Task 2: Create a Hub VNet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/53d36c5b-e3bf-4a8d-b2a4-91d43af22a45)


## Task 3: Create a Spoke VNet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8a3894a9-c57d-48f1-a45f-210ef79a5501)

## Task 4: Peer the VNets

- Add a subnetfirewall on 1st virt net

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/934f878f-8222-4f6c-9ba4-512ffbd8d72e)

- Add ^peering:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/14b08085-2765-410e-944c-be8385b3bfcf)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ad163cdf-d94c-4905-a66c-d808baa3880e)

Review:
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/170ecb56-3638-496d-a250-c36058a86bb2)

## Task 5: Create a virtual machine

- configure network for vm:
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/38a073c4-429c-4f18-b1af-c90422ce8b69)


## Task 6: Deploy the firewall and policy

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/301de1f5-6d0c-438b-af73-63bc30d6c560)

- PrivateIP:
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d5e91b43-d8cf-473c-bf4d-91fb3fabe4b7)

- PublicIP:
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/bcb489d4-f419-4af8-9ec4-a18a59634b85)

## Task 7: Create a default route

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/df409131-b592-4657-a73d-6b35b3674ca7)

- ASSOCIATE SUBNET in route table:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cdfcf4c3-abb4-410d-a6a1-fe29d8b551a1)

- ADD ROUTE
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/94456e18-58de-413d-8a07-1ee9b7d9201d)

