# Service Endpoints and Securing Storage

### What is a Service Endpoint?
- Service endpoints enable the securing of Azure service resources to your virtual network by extending VNet identity to the service.
- Once you enable service endpoints in your virtual network, you can add a virtual network rule to secure the Azure service resources to your virtual network. The rule addition provides improved security by fully removing public internet access to resources and allowing traffic only from your virtual network.
- Virtual Network (VNet) service endpoint policies allow you to filter egress virtual network traffic to Azure Storage accounts over service endpoint, and allow data exfiltration to only specific Azure Storage accounts.
- Endpoint policies provide granular access control for virtual network traffic to Azure Storage when connecting over service endpoints.

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a438b354-128f-4f8a-a259-0cdd8b8a6a18)



## Task 2: Create a virtual network

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7b449757-ee0d-4ab4-8fa6-5ad0313e5725)

## Task 3: Add a subnet and configure a storage endpoint

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/817c2072-4081-4d9b-b456-9ed3225e29da)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b1941d37-b324-4f0b-95e4-43f134ba1f46)

## Task 4: Configure an NSG to restrict access to the subnet

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f27eff72-9192-4a0b-b65b-bae3ea0be98e)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/23836c62-8206-4dfc-96e1-a3cd7a032464)

- Add second NSG outbound rules:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/16d37ea2-6f42-437a-b583-e1c92c4a1fa2)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3084fbf2-4e6d-4131-b63e-6f1964decbc1)


- Configure Inbound Security rules:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/71212f8e-cd9c-45d5-8dad-fd9c1bde545d)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/eb992ecc-9313-4a0b-8216-ec0ca14fa057)

- Associate Private subnet to a NSG:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/22125f10-7384-4435-823b-1de0bc94fa6a)


## Task 5: Configure an NSG to allow rdp on the public subnet

- Create a NSG public

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ace52bc4-7a89-49b0-ab22-b0947f597f88)

- Configure InboundSecurity Rule for Public NSG

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9d7841b0-ffc0-4c64-bb6a-4659580e9ad6)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6d91a74b-6aa7-4cf6-ae98-91528ccfef75)

- Associate Subnet to PUblic NSG:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c48ee87c-87ac-49d4-975d-c14f296c608f)

## Task 6: Create a storage account with a file share

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e2192a3a-f2b7-4497-9acb-e3aed329b246)

- Create a FileShare:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/604778ea-6a1e-4fdd-9e18-cc519abef1f2)

- Powerscript to connect file share :

```ps1
$connectTestResult = Test-NetConnection -ComputerName whizstoragedemoaddi.file.core.windows.net -Port 445
if ($connectTestResult.TcpTestSucceeded) {
    # Save the password so the drive will persist on reboot
    cmd.exe /C "cmdkey /add:`"whizstoragedemoaddi.file.core.windows.net`" /user:`"localhost\whizstoragedemoaddi`" /pass:`"AG/lijQivYzCW2ONLmN3yO5mos7KaapM2ieYI/jc/1hRckb6zRWVaxnLWFSNx+u6kSq2A5kJ96E3+ASt7Y2Sfw==`""
    # Mount the drive
    New-PSDrive -Name Z -PSProvider FileSystem -Root "\\whizstoragedemoaddi.file.core.windows.net\my-file-share" -Persist
} else {
    Write-Error -Message "Unable to reach the Azure storage account via port 445. Check to make sure your organization or ISP is not blocking port 445, or use Azure P2S VPN, Azure S2S VPN, or Express Route to tunnel SMB traffic over a different port."
}
```
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/889dd7ec-b882-43e1-a1ee-8440e7bd517b)

- Add vnet for fileshare access
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a8a5e745-38be-4358-a9ae-208febc35561)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1f09a75f-cbfa-438c-acac-abe2c9277724)


## Task 7: Deploy virtual machines 
- Create Public Vm on privatevnet :

- Create Public Vm on publicvnet:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c8d05c6a-b008-4c6e-9bb5-0c9d59814e6c)

## Task 8: Test the storage connection from the private subnet to confirm that access is allowed

- Access ¨Private Vm:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c378d3ee-a94f-4d61-a844-0dad92e05fc1)

- Access File Share from Private Vm:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/62c3cdb0-44f8-4421-acb4-519c639afaad)



## Task 9: Test the storage connection from the public subnet to confirm that access is denied

- Access denied for Public Vm from accessing File Share

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9d657b3b-f912-4506-822c-8008e944b643)

Done.
- - -
