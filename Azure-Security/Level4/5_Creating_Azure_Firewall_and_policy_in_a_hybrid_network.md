# Creating Azure Firewall and policy in a hybrid network


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/438cf034-7caa-409f-9389-31db9bbda2e6)

## Task 2: Create the firewall hub virtual network

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/42e0e6e0-2dad-4377-8893-f8d0112a4e24)

- Add Subnet 1 for Firewall

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/05920d68-f835-4510-b491-990cf82df54a)

- Add second Subnet FirewallManagement:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fe1a9f30-8a5a-4b91-9697-369cf2f2bd18)

- Add a 3rd Subnet for Gateway

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/109779ff-d88f-4d3a-9977-281c69519fb2)

- Final

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d83d7406-ee3f-4f51-8d48-2714b60eae42)


## Task 3: Create the spoke virtual network

- With one Subnet:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d6f67e62-0f1b-49bd-9885-afb95b9f29cf)

## Task 4: Create the on-premises virtual network


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5d2277a7-108b-408a-8dbb-287f72bcfbc3)

- Add a second subnet for gateway:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/94e53923-e064-463a-97c6-0721b9dafa12)

- Final
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cdc91d97-f7c5-4c5a-8c0a-ef959a7cd53d)


## Task 5: Configure and deploy the firewall

- Public IP for Firewall

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ec2fcd19-aca1-4e4c-aac6-f952bc4a7772)

- Public Mgnt IP:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5159a0d5-edb7-4442-8f67-b55cd64d001e)

- Review:
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2ed38d7c-170d-4bce-b96c-b49f5423962b)

- After deployment completes, go to the resource group, and select the __edmAzFW01__ firewall.

## Task 6: Configure network rules

- First, add a network rule to allow web traffic.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/22e24ed9-6fb3-4bd0-8f69-09cf59496c43)

- Network rules:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8681ea62-538c-493e-a8b1-5e5e65c25950)

- Add a __rule collection__

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/df0179ef-2840-404b-bfb2-2c4b1bdf96df)

## Task 7: Create a VPN gateway for the hub virtual network

-  Now create the VPN gateway for the hub virtual network. Network-to-network configurations require a RouteBased VpnType.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c61d790c-fc90-4254-98fd-c1d78a3003c3)



## Task 8: Create a VPN gateway for the on-premises virtual network

- Add second VPN Gateway for On-Prem

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/49fa9a15-ce30-40f5-86e1-56f3e466b9f9)


## Task 9: Create the VPN connections

- Create the connection from the hub virtual network to the on-premises virtual network. You'll see a shared key referenced in the examples. You can use your own values for the shared key. The important thing is that the shared key must match for both connections.
- Creating a connection can take a short while to complete.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/48c0217f-414c-4ffc-ae12-4b180ce0c713)

- Settings connections

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7831d9a1-4da9-421e-a9cf-b5a74cd954db)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/488b3f16-e7e0-42e2-b8d9-880db2e4ed4c)

- Same Process of On-Prem



## Task 10: Peer the hub and spoke virtual networks


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/91fe13cd-26f7-4ae8-8eaa-e6e67620482f)

- Select __Peerings__

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a596327b-20c4-4b27-95b9-92cdf7fd3fca)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/44b9418e-c280-4aa2-95e6-d9cd8365643f)

- Remote Virt

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d3bead80-8259-46e2-8919-15c5e3412fe3)


## Task 11: Create the routes

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/17aad6f2-25cd-41e8-9bef-d671139dc6b6)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4f6c57a4-e1b6-4601-9be6-483d384a0f9b)

- Associate

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/798d37ba-9d6f-4f3e-8f73-1a83735a5224)





## Task 12: Create virtual machines

- Create spoke vm on spoke-Virtual Net with RDP port allowed
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0d5e2225-0f10-482c-8e86-715e278025b3)


- Create the on-premises virtual machine on the On-Prem Virtual Net with RDP port allowed

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6f1db5f4-11fd-4e45-ab61-689e0d0c8cb8)



#### Mission Not successful , lots of outdated steps From Documentation ....



