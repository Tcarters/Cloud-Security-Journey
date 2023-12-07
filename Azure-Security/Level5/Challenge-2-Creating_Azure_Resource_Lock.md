# Challenge-2- Creating Azure Resource Lock

### Cloud challenge details

You are an Azure Solutions Architect working for a fictional company called "TechCorp." TechCorp has a production environment in Azure that consists of several virtual machines (VMs), storage accounts, and networking resources. They have identified a critical VM named "ProdVM" in the "ProdResourceGroup" resource group that should be protected from accidental deletion.  As part of your role, you need to demonstrate your expertise in using Azure resource locks to address this concern.
At the end of the challenge you will be able to safeguard the company's Virtual Machine names as 'ProdVM' by making use of Azure locks.

Follow the below instructions to complete this challenge.

1. Create a Virtual Machine
  - Select VM Image as Ubuntu Server 20.04 LTS Gen1
  - VM size as B2


## Solution

__Architecture Diagram__

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8152e452-c06b-4baf-a3e7-55cc800a3c3e)



### Step 2: Deploying a Virtual Machine

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f409de38-3073-4ff2-b2ee-60b0ba43a121)


### Step 3: Creating a Delete Lock

- Click on the Virtual Machine you just created, and in the left panel click on Locks and then click Add.
- Delete Lock:

  ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b950018c-878f-4b34-9d92-141c5a66ebec)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c2782f60-65de-491a-b4bd-6afbe33bd6c6)

- Failed to delete Vm:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5ad687ce-4c1f-40ec-8311-a845f68314f3)


DOne...

  
