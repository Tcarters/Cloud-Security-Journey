# Challenge 1- Encrypt and Decrypt data at REST

## Cloud challenge details

Techwork is an advisory company that help its client by providing them with tech related advices. You work as a cloud security engineer and deals with the task of safeguarding their crucial information. The company wants to ensure that all of their client's as well the company's financial information is well secured. Your challenge is to ensure that data at rest is securely encrypted to comply with industry regulations and protect customer data from unauthorized access. To complete this challenge you are required to complete the following two tasks:

Create a Storage account and then perform Storage service Encryption on it.

Create a SQL Database and perform Transparent Data Encryption on it.

Follow the below instructions to complete this challenge.

1. Create a storage account:
   - Select region as East us.
   - Redundancy: LRS
   - Performance: Standard

2. Analyze Storage service Encryption:
   - Select Encryption type: Customer-Managed keys
   - Pricing tier: Standard
   - Region: Eastus

3. Create a SQL database server:
   - Location: East US
   - Analyze Transparent Data Encryption:
   - Transparent Data Encryption: Service Managed keys


## Solution:

__Architecture Diagram__

   ![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ae56602c-9bfa-4de5-8b23-02f06ee7d204)


### Step 1: Create a Storage Account

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ccf4b254-e437-4e0e-be0e-395b497551ec)


### Step 2: Analyze Storage Service Encryption (SSE)

- Manage custum key for storage
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/32da3f45-dd80-422a-b647-a4c95cababef)

- Create a new Key Vault after save config

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0e8ad37f-f5c4-499d-b1d4-fac3cef14614)

- Enable Access policy for key on second stage of key vault creation:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1e49f378-c787-45b3-ac0e-c89f242ddcb4)

- Create key:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a578d46f-3d56-40df-bcb9-f715323dd67f)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/53f98766-134a-4418-88ae-92628abe0d95)

- Save:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/43e1a7a3-3915-4612-83f5-8413195aa9ff)


### Task 4: Create a SQL Database server

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a81183aa-3ee0-4e84-935e-503683db78c8)


### Task 5: Analyze Transparent Data Encryption (TDE)

- TDE Enabled

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/609ca12f-fc5d-410a-b33c-da7e6578b83a)

DOne.


