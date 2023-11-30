# Creating Azure Firewall

***What is Azure Firewall service?***

1. An Azure Firewall is a fully managed cloud based network security service.
2. It can be used to protect your resources in an Azure Virtual Network
3. Within this service you can create and enforce application and network connectivity policies
4. This service can automatically scale up based on demand.

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/56cdcf58-07e7-4c42-b140-f5daaef014d9)


## Task 2: Create a Virtual Network

- Click on Create a resource button.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e5ee8061-6018-4072-8129-3f4bdf97dfe4)

- Add Firewall Subnet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e1eb1d61-77c5-4d58-a0ca-e186c98376db)

- Add second Subnet for WOrkload

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3af19705-c798-4144-8db8-e24adf19b1ce)

- Add a 3rd Subnet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/98bdd801-917a-4954-9c30-a33504065f37)

- Add a 4th Subnet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/946dd287-9d3d-4436-9047-00e2c787ed2b)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8a279068-715c-4cf1-a451-51533c709145)

## Task 3: Deploy Virtual Machines

- Create a __Jump win server 2019 Vm__

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/07b9815f-a5d2-44bb-a764-f86f29b3241d)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/43c5437b-7cad-4ec3-9687-ab93b389b9fa)

- Create a __Srv-Work Vm__

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c180b13a-f2bc-4e6d-865e-064404a2f1bd)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/26a1983e-6d49-44b7-a5f0-58e5ab05eec3)


## Task 4: Deploy Firewall and Policy

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/808eaedc-9fc1-4f9a-97e5-9f49d9bb4d5c)

- Correct one

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cf9cc538-8389-4e59-8281-69d7afa71dad)


- Copy the public ip address of the firewall.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fe015c4d-3de1-456a-ab1b-00459af0276b)



## Task 5: Create a Default Route

- Create Route
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e2d0c2da-3f82-44eb-bf41-a7ec71f9decb)

- Add Route 

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/df2c0790-df58-4a34-93a7-21485ac6cfbf)

- Add subnets

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ca044c2e-2b2a-413c-86eb-3e30b51d029a)

## Task 6: Configure an Application rule

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3b45620e-31c1-4ff0-8df9-956d54e5d82b)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/09b13e8d-d6f7-4967-8fd7-e9fff4eac2be)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/44b2a275-8156-4142-8569-9d205d848595)


## Task 7: Configure a Network Rule

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e6999bf2-af61-4319-a79d-dd7dc7073485)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d6116e71-3ef3-462d-91f6-39a5fef06f49)

## Task 9: Change the primary and secondary DNS address for the Srv-work virtual machine


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0333f591-9748-4dd7-8eff-f3879c1d5a6a)


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/306531da-a260-4bcc-8a38-f55a6f6fb844)

## Task 10: Test the Firewall

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4e7c284a-7828-46c8-95f8-24e02c964274)







