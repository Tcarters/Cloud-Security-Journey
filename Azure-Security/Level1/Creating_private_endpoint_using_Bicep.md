# Creating a private endpoint using Bicep

What is a private endpoint?
- A Private endpoint in Azure is a network interface that connects a virtual network to a specific service instance in the same virtual network.
- It enables you to connect to a service over a private IP address from within a virtual network.
- This allows you to access the service securely and privately from within your virtual network, without going over the internet.
- It is typically used for services that are not publicly accessible, such as databases or storage accounts.
- Once a private endpoint is created, it can be used to configure connectivity to the service via Azure Private Link.
The private endpoint uses a private IP address from the virtual network address space, which can be accessed only within the same virtual network.
You can also use Network Security Group (NSG) to secure the communication to the service with a private endpoint.

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/66917db1-1b25-4a14-9d57-f7414a21e93a)

## Task 2: Explore the Bicep file

- Bicep config file

```yaml
@description('The administrator username of the SQL logical server')
param sqlAdministratorLogin string

@description('The administrator password of the SQL logical server.')
@secure()
param sqlAdministratorLoginPassword string

@description('Username for the Virtual Machine.')
param vmAdminUsername string

@description('Password for the Virtual Machine. The password must be at least 12 characters long and have lower case, upper characters, digit and a special character (Regex match)')
@secure()
param vmAdminPassword string

@description('The size of the VM')
param VmSize string = 'Standard_B2s'

@description('Location for all resources.')
param location string = resourceGroup().location

var vnetName = 'myVirtualNetwork'
var vnetAddressPrefix = '10.0.0.0/16'
var subnet1Prefix = '10.0.0.0/24'
var subnet1Name = 'mySubnet'
var sqlServerName = 'sqlserver${uniqueString(resourceGroup().id)}'
var databaseName = '${sqlServerName}/sample-db'
var privateEndpointName = 'myPrivateEndpoint'
var privateDnsZoneName = 'privatelink${environment().suffixes.sqlServerHostname}'
var pvtEndpointDnsGroupName = '${privateEndpointName}/mydnsgroupname'
var vmName = take('myVm${uniqueString(resourceGroup().id)}', 15)
var publicIpAddressName = '${vmName}PublicIP'
var networkInterfaceName = '${vmName}NetInt'
var osDiskType = 'StandardSSD_LRS'

resource sqlServer 'Microsoft.Sql/servers@2021-11-01-preview' = {
  name: sqlServerName
  location: location
  tags: {
    displayName: sqlServerName
  }
  properties: {
    administratorLogin: sqlAdministratorLogin
    administratorLoginPassword: sqlAdministratorLoginPassword
    version: '12.0'
    publicNetworkAccess: 'Disabled'
  }
}

resource database 'Microsoft.Sql/servers/databases@2021-11-01-preview' = {
  name: databaseName
  location: location
  sku: {
    name: 'Basic'
    tier: 'Basic'
    capacity: 5
  }
  tags: {
    displayName: databaseName
  }
  properties: {
    collation: 'SQL_Latin1_General_CP1_CI_AS'
    maxSizeBytes: 104857600
    sampleName: 'AdventureWorksLT'
  }
  dependsOn: [
    sqlServer
  ]
}

resource vnet 'Microsoft.Network/virtualNetworks@2021-05-01' = {
  name: vnetName
  location: location
  properties: {
    addressSpace: {
      addressPrefixes: [
        vnetAddressPrefix
      ]
    }
  }
}

resource subnet 'Microsoft.Network/virtualNetworks/subnets@2021-05-01' = {
  parent: vnet
  name: subnet1Name
  properties: {
    addressPrefix: subnet1Prefix
    privateEndpointNetworkPolicies: 'Disabled'
  }
}

resource privateEndpoint 'Microsoft.Network/privateEndpoints@2021-05-01' = {
  name: privateEndpointName
  location: location
  properties: {
    subnet: {
      id: subnet.id
    }
    privateLinkServiceConnections: [
      {
        name: privateEndpointName
        properties: {
          privateLinkServiceId: sqlServer.id
          groupIds: [
            'sqlServer'
          ]
        }
      }
    ]
  }
  dependsOn: [
    vnet
  ]
}

resource privateDnsZone 'Microsoft.Network/privateDnsZones@2020-06-01' = {
  name: privateDnsZoneName
  location: 'global'
  properties: {}
  dependsOn: [
    vnet
  ]
}

resource privateDnsZoneLink 'Microsoft.Network/privateDnsZones/virtualNetworkLinks@2020-06-01' = {
  parent: privateDnsZone
  name: '${privateDnsZoneName}-link'
  location: 'global'
  properties: {
    registrationEnabled: false
    virtualNetwork: {
      id: vnet.id
    }
  }
}

resource pvtEndpointDnsGroup 'Microsoft.Network/privateEndpoints/privateDnsZoneGroups@2021-05-01' = {
  name: pvtEndpointDnsGroupName
  properties: {
    privateDnsZoneConfigs: [
      {
        name: 'config1'
        properties: {
          privateDnsZoneId: privateDnsZone.id
        }
      }
    ]
  }
  dependsOn: [
    privateEndpoint
  ]
}

resource publicIpAddress 'Microsoft.Network/publicIPAddresses@2021-05-01' = {
  name: publicIpAddressName
  location: location
  tags: {
    displayName: publicIpAddressName
  }
  properties: {
    publicIPAllocationMethod: 'Dynamic'
  }
}

resource networkInterface 'Microsoft.Network/networkInterfaces@2021-05-01' = {
  name: networkInterfaceName
  location: location
  tags: {
    displayName: networkInterfaceName
  }
  properties: {
    ipConfigurations: [
      {
        name: 'ipConfig1'
        properties: {
          privateIPAllocationMethod: 'Dynamic'
          publicIPAddress: {
            id: publicIpAddress.id
          }
          subnet: {
            id: subnet.id
          }
        }
      }
    ]
  }
  dependsOn: [
    vnet
  ]
}

resource vm 'Microsoft.Compute/virtualMachines@2021-11-01' = {
  name: vmName
  location: location
  tags: {
    displayName: vmName
  }
  properties: {
    hardwareProfile: {
      vmSize: VmSize
    }
    osProfile: {
      computerName: vmName
      adminUsername: vmAdminUsername
      adminPassword: vmAdminPassword
    }
    storageProfile: {
      imageReference: {
        publisher: 'MicrosoftWindowsServer'
        offer: 'WindowsServer'
        sku: '2019-Datacenter'
        version: 'latest'
      }
      osDisk: {
        name: '${vmName}OsDisk'
        caching: 'ReadWrite'
        createOption: 'FromImage'
        managedDisk: {
          storageAccountType: osDiskType
        }
        diskSizeGB: 128
      }
    }
    networkProfile: {
      networkInterfaces: [
        {
          id: networkInterface.id
        }
      ]
    }
  }
}
```
## Task 3: Deploy the Bicep file

```bash
az deployment group create \
--name deployprivatendpoint \
--resource-group rg_eastus_166013_1_170026979692 \
--template-file main.bicep \
--parameters sqlAdministratorLogin=db-admin sqlAdministratorLoginPassword=db@Password2023 vmAdminUsername=lab5user vmAdminPassword=P@ssword2023 location=eastus
```

## Task 4: Test the Private Endpoint

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/be20a2f0-1116-410c-a429-1a5abeb279a3)

- Test database sql server name

`nslookup sqlserveryejbzycvqyw72.database.windows.net`

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1dd55ef7-8581-407c-b366-bbfa5408c469)


- Setup sql server connection in vm
> https://aka.ms/ssmsfullsetup

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/084ed94c-700f-4164-9182-b80c26a6d225)

## Connect to sql server from Vm

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/edf527ce-9689-41c3-aac6-d4d9a2698e79)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1311922b-799f-4e7e-8260-5cdc75224915)


