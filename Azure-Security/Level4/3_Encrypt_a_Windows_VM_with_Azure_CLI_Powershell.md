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

```

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/bf50caa0-c1a3-4838-809e-6f453c3f458f)


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

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f85d007c-bc8b-4622-bd06-c1f04c1c5882)


### Task 4: Create an Azure Windows VM and Key Vault using PowerShell

- Now, enter the following command to set administrator account credentials for the virtual machine login :

```ps1
$cred = Get-Credential

```

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4ea85d84-e6ac-46e9-ac04-fd394d40401c)

-  create an azure virtual machine using __Powershell__

```ps1
New-AzVM -Name MyVm2serv -Credential $cred -ResourceGroupName "rg_eastus_166013_1_170143931790" -Image win2019datacenter -Size Standard_B2s

```

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4b7f0b4f-ad0a-4d7f-8b1c-71d5f683f674)


- Create vault using ps1

```ps1
New-AzKeyvault -name <unique-keyvault-name> -ResourceGroupName <ResourceGroupName> -Location EastUS -EnabledForDiskEncryption

```
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1f0f5443-3f12-4c16-941d-6ad164fb08f2)


### Task 5: Encrypt the Virtual Machine using Powershell

```ps1
$KeyVault = Get-AzKeyVault -VaultName <your-unique-keyvault-name> -ResourceGroupName <yourResourceGroup>
Set-AzVMDiskEncryptionExtension -ResourceGroupName yourResourceGroup -VMName <your-vm-name> -DiskEncryptionKeyVaultUrl $KeyVault.VaultUri -DiskEncryptionKeyVaultId $KeyVault.ResourceId -SkipVmBackup -VolumeType All

```
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0cb8da72-425b-4b5d-b90b-6dc025f74455)

- Verify VM encryption

```ps1
Get-AzVmDiskEncryptionStatus -VMName MyVm2serv -ResourceGroupName rg_eastus_166013_1_170143931790
```
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/73b1bcab-9465-464b-9f1f-e4d099cd78ca)

DOne .

