# Challenge 3 - Understand Network Security Group rules


## Cloud challenge details
You are tasked with securing a microservices-based application hosted on Azure Virtual Machines that communicate with each other over a network. The application consists of multiple services, each running on a separate virtual machine, and they need to communicate securely while adhering to the principle of least privilege. Your challenge is to design and implement a comprehensive security strategy using Network Security Group (NSG) rules to ensure that the microservices can communicate effectively while maintaining a high level of security.

Follow the below instructions to complete this challenge.

1. Use Region as East US
2. Virtual Machine
   - Image : Select Windows Server 2022 Datacenter : Azure Edition - Gen2
   - Size : Select B2s


__Solution__

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4f424d36-fcfb-4cc1-bc6c-2ec1b978e520)


## Step 1: Create a virtual machine

- Create a vm with none public port allowed


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0435bf0c-73a6-4802-9fa0-26daec42d9b8)


## Step 2: Allow RDP traffic via NSG rules

- In the search box at the top of the Azure portal page, enter Virtual machine. Select Virtual Machines in the search results. Select the virtual machine you created “keke-VM1”.
- On the Overview page of your VM, go to the Networking section from left menu, here you can see the network interface which has the public ip address and the private ip address and also the inbound and outbound port rules.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/17828e0d-78cf-4d59-a200-0aa020b97ff2)

* Test connection to Vm:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/856bda51-6e63-40dd-923a-d82963696b6d)


## Step 3: Allow HTTP traffic via NSG rules

- Install web server on VM

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4512082d-c1d0-406a-8b15-96d37e96926e)

- Access Web Page on localhost:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ab1e1106-bde2-461f-8ae8-4f14e7d2cc45)

- Add security group allowing web page access on Internet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0d9b0feb-7d6a-4569-a3c3-2a2c0dd6e99c)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cc2e727d-0e04-485a-846e-fd52544c8b45)

- Access Web page using its public IP:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d2078f96-18ec-4a18-99db-3b8686a8ed9a)


Challenge Over 📌 Done.
