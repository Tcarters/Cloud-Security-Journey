# Mission1- Understand Network Security Group rules

### What are Azure Network Security Groups (NSGs) ?
- A network security group contains security rules that allow or deny inbound and outbound network traffic, to and from, several types of Azure resources. You can specify source and destination, port, and protocol for each rule.
- A network security group contains zero, or as many rules as desired, within Azure subscription limits.
- An Azure network security group is used to filter network traffic to and from Azure resources in an Azure virtual network.
- NSGs can be linked with subnets or individual virtual machine instances within that subnet. When an NSG is associated with a subnet, the ACL (access control list) rules apply to all Virtual Machine instances of that subnet. In addition, traffic to an individual virtual machine can be further restricted by associating an NSG directly to that virtual machine.


### Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6e9f3ebb-93ce-4376-bcd7-d6b55e5c5b55)


### Step 2: Create a virtual machine

- In the Create a Virtual machine tab, enter or select the following values in the Basics tab.

* Resource group : Select ``rg_westeurope_XXXXX``
* Instance details :
  - Virtual Machine Name : Enter myVM1
  - Region : Select West Europe
  - Availability options: Select No infrastructure redundancy required
  - Image : Select  Windows Server 2022 Datacenter - Azure Edition - Gen2
  - Azure Spot instance : Leave the default of unchecked.
  - Size : Click on see all sizes then select B2s and then click on select 

* Administrator Account :
  - Username : Enter a username
  - Password : Enter a password
  - Confirm password : Re-enter password

* Inbound Port rules :
  - Public inbound ports : Select None

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5b4e0146-6a73-4776-b0cb-27cd143e76e8)

- Leave the defaults on Disks, __Networking and Management tabs__, go to the __Monitoring tab__ and Disable the __Boot diagnostics__.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1575c0de-bd64-4d0d-9ee0-e3b8cac26186)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f6548dbd-4f1c-4589-8e34-cc2e94e4ca56)


### Step 3: Allow RDP traffic via NSG rules

- In the search box at the top of the Azure portal page, enter Virtual machine. Select Virtual Machines in the search results. Select the virtual machine you created “myVM1”.
- On the Overview page of your VM, go to the Networking section from left menu, here you can see the network interface which has the public ip address and the private ip address and also the inbound and outbound port rules.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8713737c-0884-4ade-b831-fbe161c8e025)

- Result :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/397d595e-403b-4cb8-8dda-d94b54ba6f85)

- Test connection to Vm:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/12f99ee1-87a8-4c67-a2ec-e7340cff2b99)



### Step 4: Allow HTTP traffic via NSG rules
1. In the __Windows virtual machine__, open the Server Manager and click on Add Roles and Features . We will now install a web server on this particular machine by adding a network security group rule to allow traffic to flow into this virtual machine on Port 80 so that we can access the web server.
2. Install web server :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/323eb111-93e5-4b03-b828-fd433229cffa)

- Access Web Page on localhost:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1633a79e-f8c0-4c6e-8cb5-b72f09aaec8c)

- In the Networking section of the virtual machine __“myVM1”__, select Add inbound port rule and enter or select the following information.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fb44f336-ebbc-4b5c-a1c9-c3b6c9c2cdf7)

- Review:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0c9b593b-f289-4d53-abb3-42a0c2239d97)

- Access Web page using its public IP:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ed40038e-ec86-4959-9a60-9cb956f49645)

Game Over 📌
Done.
- - -
