
## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f3ef8692-f6b8-48cc-a38e-10162c14a3a0)


## Task 2: Create a virtual Network for the Load Balancer

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ff7bbb20-6a64-4a73-9adb-7ea4058b57a7)



## Task 3: Create a load balancer

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9fd89f7f-2650-44ef-b9f1-ca341f090581)



## Task 4: Create a private link service

```yaml
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "resourceName": {
            "type": "string",
            "metadata": {
                "description": "The name of the private link service"
            }
        },
        "location": {
            "type": "string",
            "metadata": {
                "description": "The location of the private link service"
            }
        },
        "extendedLocation": {
            "type": "object"
        }
    },
    "resources": [
        {
            "apiVersion": "2019-04-01",
            "type": "Microsoft.Network/privateLinkServices",
            "name": "[parameters('resourceName')]",
            "location": "[parameters('location')]",
            "extendedLocation": "[if(empty(parameters('extendedLocation')), json('null'), parameters('extendedLocation'))]",
            "tags": {},
            "properties": {
                "visibility": {
                    "subscriptions": []
                },
                "autoApproval": {
                    "subscriptions": []
                },
                "enableProxyProtocol": false,
                "loadBalancerFrontendIpConfigurations": [
                    {
                        "id": "/subscriptions/71fa0172-ce90-403c-94a9-14ce1e88f56a/resourceGroups/rg_eastus_166013_1_170022184848/providers/Microsoft.Network/loadBalancers/whizLB/frontendIPConfigurations/myFrontend"
                    }
                ],
                "ipConfigurations": [
                    {
                        "name": "myBackendSubnet-1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "privateIPAddressVersion": "IPv4",
                            "subnet": {
                                "id": "/subscriptions/71fa0172-ce90-403c-94a9-14ce1e88f56a/resourceGroups/rg_eastus_166013_1_170022184848/providers/Microsoft.Network/virtualNetworks/whizNet-LB/subnets/myBackendSubnet"
                            },
                            "primary": false
                        }
                    }
                ],
                "privateEndpointConnections": []
            },
            "dependsOn": [
                "UpdateSubnet-20231117131614"
            ]
        },
        {
            "apiVersion": "2017-05-10",
            "name": "UpdateSubnet-20231117131614",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "rg_eastus_166013_1_170022184848",
            "subscriptionId": "71fa0172-ce90-403c-94a9-14ce1e88f56a",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "resources": [
                        {
                            "name": "whizNet-LB/myBackendSubnet",
                            "id": "/subscriptions/71fa0172-ce90-403c-94a9-14ce1e88f56a/resourceGroups/rg_eastus_166013_1_170022184848/providers/Microsoft.Network/virtualNetworks/whizNet-LB/subnets/myBackendSubnet",
                            "properties": {
                                "provisioningState": "Succeeded",
                                "addressPrefixes": [
                                    "10.1.0.0/24"
                                ],
                                "ipConfigurations": [
                                    {
                                        "id": "/subscriptions/71fa0172-ce90-403c-94a9-14ce1e88f56a/resourceGroups/RG_EASTUS_166013_1_170022184848/providers/Microsoft.Network/loadBalancers/WHIZLB/frontendIPConfigurations/MYFRONTEND"
                                    }
                                ],
                                "delegations": [],
                                "privateEndpointNetworkPolicies": "Disabled",
                                "privateLinkServiceNetworkPolicies": "Disabled",
                                "defaultOutboundAccess": true
                            },
                            "type": "Microsoft.Network/virtualNetworks/subnets",
                            "apiVersion": "2021-05-01"
                        }
                    ]
                }
            }
        }
    ]
}
```

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/3f062193-fc59-4799-bdfe-c0741d915513)

## Task 5: Create a Virtual Network for private endpoint


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cdeec3fe-fb59-497c-9e16-2f7101e2c88e)

## Task 6: Create a private endpoint

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2f5caf1f-378a-49cc-92ef-c9d1b361b436)


## Task 7: Get IP address of private endpoint
