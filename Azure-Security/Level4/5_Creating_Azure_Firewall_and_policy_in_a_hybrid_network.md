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





