# Challenge 9 - Service Endpoints and securing storage



__Cloud challenge details__

__
You work as a cloud solutions architect for a fictional company called "Contoso Corporation." Contoso is migrating its on-premises infrastructure to Microsoft Azure to take advantage of its scalability and flexibility. One of the critical tasks is to secure the Azure Storage accounts and allow access only from authorized sources using Azure Service Endpoints. Your task is to configure Azure Service Endpoints and implement security measures to protect data stored in Azure Storage.

Please follow the below instructions to complete this challenge.

Create a virtual network

Region: Select (US) East US

IPv4 address space: Enter 10.0.0.0/16

Subnet address range: Enter 10.0.0.0/24

Add a subnet and configure a storage endpoint

Subnet address range: Enter 10.0.1.0/24

Service endpoints: Select Microsoft.Storage

Configure an NSG to restrict access to the subnet

Region: Select East US

Create a storage account with a file share

Region: Select (US) East US

Performance: Select Standard (general-purpose v2 account)

Redundancy: Select Locally-redundant storage (LRS)

Deploy virtual machines 

Region: Select (US) East US

Image: Select Windows Server 2022 Datacenter: Azure Edition - Gen2 

Size: Standard B2s

OS disk type: Select Standard HDD
__

## Solution

__Architecture Diagram__

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ccd37901-7473-410c-b6c2-b16f283f9623)

## Task 2: Create a virtual network

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4dca9d2d-bad1-4f55-b8a1-cbc75b9b84cc)

## Task 3: Add a subnet and configure a storage endpoint

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/dc8e0442-46aa-4f0f-a353-cf5c6f017e17)

## Task 4: Configure an NSG to restrict access to the subnet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3484cdea-ce43-43e7-bbb0-baf586b9b248)

- Add outbound rule for Storage Access:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0db2a2dd-c058-4d85-a7f3-5530a31ae008)

- Add second NSG outbound rules:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0a1b09a4-7d13-4428-a438-75e9e7fe634d)

- Configure Inbound Security rules:


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/96fe3082-c586-4d61-8a33-84b2d09fbe8c)

- Associate Private subnet to a NSG:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d25bc318-9158-4b4d-9906-1e23630eac0b)


## Task 5: Configure an NSG to allow rdp on the public subnet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/485d7d9d-5fe4-409d-936b-ef7499f5ae6c)

- Configure InboundSecurity Rule for Public NSG

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b3ec43f9-51ae-4bbd-8cca-9c9ebf893df9)

- Associate Subnet to PUblic NSG:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8e1d7e53-d736-425a-9877-7824467d03bd)


## Task 6: Create a storage account with a file share

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/5dba0992-255b-4711-8277-1a3db1a37630)

- File share:
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/32700b6b-9641-4979-bbf7-8c11aa010ef1)

```ps1
$connectTestResult = Test-NetConnection -ComputerName kekestorag23.file.core.windows.net -Port 445
if ($connectTestResult.TcpTestSucceeded) {
    # Save the password so the drive will persist on reboot
    cmd.exe /C "cmdkey /add:`"kekestorag23.file.core.windows.net`" /user:`"localhost\kekestorag23`" /pass:`"EUuLbu6mbwGGBNEQEWLHPhxvwfoD/bxeVEi+GhwMphd4+a2cleXezdtwW6eiKZ66JVyzePHBva99+AStvU2zKg==`""
    # Mount the drive
    New-PSDrive -Name Z -PSProvider FileSystem -Root "\\kekestorag23.file.core.windows.net\kkefileshare23" -Persist
} else {
    Write-Error -Message "Unable to reach the Azure storage account via port 445. Check to make sure your organization or ISP is not blocking port 445, or use Azure P2S VPN, Azure S2S VPN, or Express Route to tunnel SMB traffic over a different port."
}

```

Rest of Task refers to : https://github.com/Tcarters/Cloud-Security-Journey/blob/master/Azure-Security/Level2/Service_Endpoints_and_Securing_Storage.md

- - -


