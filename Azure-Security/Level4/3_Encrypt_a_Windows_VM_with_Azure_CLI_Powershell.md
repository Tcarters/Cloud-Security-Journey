# Encrypt a Windows VM with Azure CLI and Powershell

What is Azure Disk Encryption ?
Encryption is part of a layered approach to security and should be used with other recommendations to secure Virtual Machines and their disks. 

Azure Disk Encryption helps protect and safeguard your data to meet your organizational security and compliance commitments.

ADE encrypts the OS and data disks of Azure virtual machines (VMs) inside your VMs using the CPU of your VMs through the use of feature DM-Crypt of Linux or the BitLocker feature of Windows. 

ADE is integrated with Azure Key Vault to help you control and manage the disk encryption keys and secrets.

Azure Disk Encryption is zone resilient, the same way as Virtual Machines. 



## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c7d700b9-2f99-4fff-8cbe-2453ad32aa4c)


### Solution

### Task 2: Create an Azure Windows VM and Key Vault using CLI

- click on the Cloud Shell icon and then click on Bash.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7e2d04e9-bcf9-44dd-9267-3aa09e9ca78b)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3c95a938-734c-4524-87af-6f79148cef5d)

- Create a __Windows VM__

```bash
  az vm create --resource-group <ResourceGroupName> --name <EnteryourVMName> --image win2022datacenter --size <Standard_B2s> --admin-username azureuser --admin-password <Enteryourpassword>
  az vm create --resource-group rg_eastus_166013_1_170143237330 --name myVM1serv --image win2022datacenter --size "Standard_B2s" --admin-username uservm1 --admin-password Password@2023

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/bf50caa0-c1a3-4838-809e-6f453c3f458f)


```

- Azure disk encryption stores its encryption key in an Azure Key Vault. So, let us create a key vault using the below command :

```bash
  az keyvault create --name <unique-keyvault-name> --resource-group <yourResourceGroup> --location "eastus" --enabled-for-disk-encryption
  az keyvault create --name edmKeyvault1 --resource-group "rg_eastus_166013_1_170143237330" --location "eastus" --enabled-for-disk-encryption
```

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/882bbd11-5186-42ab-b9cf-8134dc707d84)


### Task 3: Encrypt the Virtual Machine using CLI

- Now, encrypt your VM by entering the following command :

```bash
az vm encryption enable -g <yourResourceGroup> --name <your-vm-name> --disk-encryption-keyvault <your-keyvault-name>
  
```

- Show the encryption Progress:

```bash
  az vm encryption show --name <your-vm-name> -g <yourResourceGroup>
  az vm encryption show --name myVM1serv -g rg_eastus_166013_1_170143237330
```
