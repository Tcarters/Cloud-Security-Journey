# Creating a private link service using an ARM template

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/22093565-dbdc-4562-97b8-380225084c86)


## Task 2: Explore the ARM template

- Template
```yaml
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "metadata": {
    "_generator": {
      "name": "bicep",
      "version": "0.5.6.12127",
      "templateHash": "4187161334981532249"
    }
  },
  "parameters": {
    "vmAdminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for the Virtual Machine."
      }
    },
    "vmAdminPassword": {
      "type": "secureString",
      "metadata": {
        "description": "Password for the Virtual Machine. The password must be at least 12 characters long and have lower case, upper characters, digit and a special character (Regex match)"
      }
    },
    "vmSize": {
      "type": "string",
      "defaultValue": "Standard_B2s",
      "metadata": {
        "description": "The size of the VM"
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Location for all resources."
      }
    }
  },
  "variables": {
    "vnetName": "WhizlabsVNet",
    "vnetConsumerName": "whizPEVnet",
    "vnetAddressPrefix": "10.0.0.0/16",
    "frontendSubnetPrefix": "10.0.1.0/24",
    "frontendSubnetName": "whizFrontendSubnet",
    "backendSubnetPrefix": "10.0.2.0/24",
    "backendSubnetName": "whizBackendSubnet",
    "consumerSubnetPrefix": "10.0.0.0/24",
    "consumerSubnetName": "whizPESubnet",
    "loadbalancerName": "whizILB",
    "backendPoolName": "whizBackEndPool",
    "loadBalancerFrontEndIpConfigurationName": "whizFrontEnd",
    "healthProbeName": "whizHealthProbe",
    "privateEndpointName": "whizPrivateEndpoint",
    "vmName": "[take(format('whizVm{0}', uniqueString(resourceGroup().id)), 15)]",
    "networkInterfaceName": "[format('{0}NetInt', variables('vmName'))]",
    "vmConsumerName": "[take(format('ComsumerVm{0}', uniqueString(resourceGroup().id)), 15)]",
    "publicIpAddressConsumerName": "[format('{0}PublicIP', variables('vmConsumerName'))]",
    "networkInterfaceConsumerName": "[format('{0}NetInt', variables('vmConsumerName'))]",
    "osDiskType": "StandardSSD_LRS",
    "privatelinkServiceName": "whizPvtLinkService",
    "loadbalancerId": "[resourceId('Microsoft.Network/loadBalancers', variables('loadbalancerName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Network/virtualNetworks",
      "apiVersion": "2021-05-01",
      "name": "[variables('vnetName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('vnetAddressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('frontendSubnetName')]",
            "properties": {
              "addressPrefix": "[variables('frontendSubnetPrefix')]",
              "privateLinkServiceNetworkPolicies": "Disabled"
            }
          },
          {
            "name": "[variables('backendSubnetName')]",
            "properties": {
              "addressPrefix": "[variables('backendSubnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.Network/loadBalancers",
      "apiVersion": "2021-05-01",
      "name": "[variables('loadbalancerName')]",
      "location": "[parameters('location')]",
      "sku": {
        "name": "Standard"
      },
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "[variables('loadBalancerFrontEndIpConfigurationName')]",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[resourceId('Microsoft.Network/virtualNetworks/subnets', variables('vnetName'), variables('frontendSubnetName'))]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "[variables('backendPoolName')]"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP-VM0",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[resourceId('Microsoft.Network/loadBalancers/frontendIpConfigurations', variables('loadbalancerName'), variables('loadBalancerFrontEndIpConfigurationName'))]"
              },
              "protocol": "Tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ],
        "loadBalancingRules": [
          {
            "name": "whizHTTPRule",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[resourceId('Microsoft.Network/loadBalancers/frontendIpConfigurations', variables('loadbalancerName'), variables('loadBalancerFrontEndIpConfigurationName'))]"
              },
              "backendAddressPool": {
                "id": "[resourceId('Microsoft.Network/loadBalancers/backendAddressPools', variables('loadbalancerName'), variables('backendPoolName'))]"
              },
              "probe": {
                "id": "[resourceId('Microsoft.Network/loadBalancers/probes', variables('loadbalancerName'), variables('healthProbeName'))]"
              },
              "protocol": "Tcp",
              "frontendPort": 80,
              "backendPort": 80,
              "idleTimeoutInMinutes": 15
            }
          }
        ],
        "probes": [
          {
            "properties": {
              "protocol": "Tcp",
              "port": 80,
              "intervalInSeconds": 15,
              "numberOfProbes": 2
            },
            "name": "[variables('healthProbeName')]"
          }
        ]
      },
      "dependsOn": [
        "[resourceId('Microsoft.Network/virtualNetworks', variables('vnetName'))]"
      ]
    },
    {
      "type": "Microsoft.Network/networkInterfaces",
      "apiVersion": "2021-05-01",
      "name": "[variables('networkInterfaceName')]",
      "location": "[parameters('location')]",
      "tags": {
        "displayName": "[variables('networkInterfaceName')]"
      },
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipConfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[resourceId('Microsoft.Network/virtualNetworks/subnets', variables('vnetName'), variables('backendSubnetName'))]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[resourceId('Microsoft.Network/loadBalancers/backendAddressPools', variables('loadbalancerName'), variables('backendPoolName'))]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[resourceId('Microsoft.Network/loadBalancers/inboundNatRules/', variables('loadbalancerName'), 'RDP-VM0')]"
                }
              ]
            }
          }
        ]
      },
      "dependsOn": [
        "[resourceId('Microsoft.Network/loadBalancers', variables('loadbalancerName'))]"
      ]
    },
    {
      "type": "Microsoft.Compute/virtualMachines",
      "apiVersion": "2021-11-01",
      "name": "[variables('vmName')]",
      "location": "[parameters('location')]",
      "tags": {
        "displayName": "[variables('vmName')]"
      },
      "properties": {
        "hardwareProfile": {
          "vmSize": "[parameters('vmSize')]"
        },
        "osProfile": {
          "computerName": "[variables('vmName')]",
          "adminUsername": "[parameters('vmAdminUsername')]",
          "adminPassword": "[parameters('vmAdminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2019-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[format('{0}OsDisk', variables('vmName'))]",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "managedDisk": {
              "storageAccountType": "[variables('osDiskType')]"
            },
            "diskSizeGB": 128
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('networkInterfaceName'))]"
            }
          ]
        }
      },
      "dependsOn": [
        "[resourceId('Microsoft.Network/networkInterfaces', variables('networkInterfaceName'))]"
      ]
    },
    {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "apiVersion": "2021-11-01",
      "name": "[format('{0}/{1}', variables('vmName'), 'installcustomscript')]",
      "location": "[parameters('location')]",
      "tags": {
        "displayName": "install software for Windows VM"
      },
      "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
          "commandToExecute": "powershell -ExecutionPolicy Unrestricted Install-WindowsFeature -Name Web-Server"
        }
      },
      "dependsOn": [
        "[resourceId('Microsoft.Compute/virtualMachines', variables('vmName'))]"
      ]
    },
    {
      "type": "Microsoft.Network/privateLinkServices",
      "apiVersion": "2021-05-01",
      "name": "[variables('privatelinkServiceName')]",
      "location": "[parameters('location')]",
      "properties": {
        "enableProxyProtocol": false,
        "loadBalancerFrontendIpConfigurations": [
          {
            "id": "[resourceId('Microsoft.Network/loadBalancers/frontendIpConfigurations', variables('loadbalancerName'), variables('loadBalancerFrontEndIpConfigurationName'))]"
          }
        ],
        "ipConfigurations": [
          {
            "name": "snet-provider-default-1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "privateIPAddressVersion": "IPv4",
              "subnet": {
                "id": "[reference(variables('loadbalancerId'), '2019-06-01').frontendIPConfigurations[0].properties.subnet.id]"
              },
              "primary": false
            }
          }
        ]
      },
      "dependsOn": [
        "[resourceId('Microsoft.Network/loadBalancers', variables('loadbalancerName'))]"
      ]
    },
    {
      "type": "Microsoft.Network/virtualNetworks",
      "apiVersion": "2021-05-01",
      "name": "[variables('vnetConsumerName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('vnetAddressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('consumerSubnetName')]",
            "properties": {
              "addressPrefix": "[variables('consumerSubnetPrefix')]",
              "privateEndpointNetworkPolicies": "Disabled"
            }
          },
          {
            "name": "[variables('backendSubnetName')]",
            "properties": {
              "addressPrefix": "[variables('backendSubnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.Network/publicIPAddresses",
      "apiVersion": "2021-05-01",
      "name": "[variables('publicIpAddressConsumerName')]",
      "location": "[parameters('location')]",
      "tags": {
        "displayName": "[variables('publicIpAddressConsumerName')]"
      },
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[toLower(variables('vmConsumerName'))]"
        }
      }
    },
    {
      "type": "Microsoft.Network/networkInterfaces",
      "apiVersion": "2021-05-01",
      "name": "[variables('networkInterfaceConsumerName')]",
      "location": "[parameters('location')]",
      "tags": {
        "displayName": "[variables('networkInterfaceConsumerName')]"
      },
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipConfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressConsumerName'))]"
              },
              "subnet": {
                "id": "[resourceId('Microsoft.Network/virtualNetworks/subnets', variables('vnetConsumerName'), variables('consumerSubnetName'))]"
              }
            }
          }
        ]
      },
      "dependsOn": [
        "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressConsumerName'))]",
        "[resourceId('Microsoft.Network/virtualNetworks', variables('vnetConsumerName'))]"
      ]
    },
    {
      "type": "Microsoft.Compute/virtualMachines",
      "apiVersion": "2021-11-01",
      "name": "[variables('vmConsumerName')]",
      "location": "[parameters('location')]",
      "tags": {
        "displayName": "[variables('vmConsumerName')]"
      },
      "properties": {
        "hardwareProfile": {
          "vmSize": "[parameters('vmSize')]"
        },
        "osProfile": {
          "computerName": "[variables('vmConsumerName')]",
          "adminUsername": "[parameters('vmAdminUsername')]",
          "adminPassword": "[parameters('vmAdminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2019-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[format('{0}OsDisk', variables('vmConsumerName'))]",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "managedDisk": {
              "storageAccountType": "[variables('osDiskType')]"
            },
            "diskSizeGB": 128
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('networkInterfaceConsumerName'))]"
            }
          ]
        }
      },
      "dependsOn": [
        "[resourceId('Microsoft.Network/networkInterfaces', variables('networkInterfaceConsumerName'))]"
      ]
    },
    {
      "type": "Microsoft.Network/privateEndpoints",
      "apiVersion": "2021-05-01",
      "name": "[variables('privateEndpointName')]",
      "location": "[parameters('location')]",
      "properties": {
        "subnet": {
          "id": "[resourceId('Microsoft.Network/virtualNetworks/subnets', variables('vnetConsumerName'), variables('consumerSubnetName'))]"
        },
        "privateLinkServiceConnections": [
          {
            "name": "[variables('privateEndpointName')]",
            "properties": {
              "privateLinkServiceId": "[resourceId('Microsoft.Network/privateLinkServices', variables('privatelinkServiceName'))]"
            }
          }
        ]
      },
      "dependsOn": [
        "[resourceId('Microsoft.Network/privateLinkServices', variables('privatelinkServiceName'))]",
        "[resourceId('Microsoft.Network/virtualNetworks', variables('vnetConsumerName'))]"
      ]
    }
  ]
}
```

- deploy

```bash
az deployment group create \
  --name mydeploypriv \
  --resource-group rg_eastus_166013_1_170022524478 \
  --template-file template.json \
  --parameters location=eastus vmAdminUsername=vm1 vmAdminPassword=Super@secret2023

```

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2629e17e-64ab-4929-9bc9-5625246ea12c)

- deployment success
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b025e1b1-039f-424a-ae40-49d986f5176a)


- Access the Web server from VmConsumer using the RDP Protocol

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/778f74fd-dc69-4302-9d82-6e94e9b3c24f)

or using cmd
```bash
Invoke-AzVMRunCommand -Name 'ComsumerVmdsrar' -ResourceGroupName 'rg_eastus_166013_1_170022524478' -CommandId 'RunPowerShellScript' -ScriptPath 'path-to-script'

```
- - -
