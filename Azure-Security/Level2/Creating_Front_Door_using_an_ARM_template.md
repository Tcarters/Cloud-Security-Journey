# Creating a Front Door using an ARM template

### What is an Azure Front Door?
- Azure Front Door is a global, highly available, and scalable service offered by Microsoft Azure that routes incoming traffic to your backends.
- It is designed to improve the performance and availability of your web applications and services. It does this by providing a global network of points of presence (POPs) that can be used to route traffic to the closest available backend.
- Front Door service supports various features including load balancing, custom routing, SSL offloading, and caching. It also provides a Web Application Firewall (WAF) that can be used to protect your web applications and services from various types of attacks.
- Front Door service is designed to work with other Azure services such as Azure Virtual Machines, Azure App Service, and Azure Container Instances. It can also be used with non-Azure backends such as on-premises servers or other cloud-based services.
- Front Door service can be deployed and managed through the Azure portal, Azure CLI, Azure PowerShell, or Azure Resource Manager (ARM) templates. This allows you to easily provision, configure, and manage Front Door service in a programmatic and automated way.

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/8968206e-9e56-43fd-925c-7765180e20ca)



## Task 2: Explore the ARM template

```yaml
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "metadata": {
      "_generator": {
        "name": "bicep",
        "version": "0.5.6.12127",
        "templateHash": "17606357911537037484"
      }
    },
    "parameters": {
      "frontDoorName": {
        "type": "string",
        "metadata": {
          "description": "The name of the frontdoor resource."
        }
      },
      "backendAddress": {
        "type": "string",
        "metadata": {
          "description": "The hostname of the backend. Must be an IP address or FQDN."
        }
      }
    },
    "variables": {
      "frontEndEndpointName": "frontEndEndpoint",
      "loadBalancingSettingsName": "loadBalancingSettings",
      "healthProbeSettingsName": "healthProbeSettings",
      "routingRuleName": "routingRule",
      "backendPoolName": "backendPool"
    },
    "resources": [
      {
        "type": "Microsoft.Network/frontDoors",
        "apiVersion": "2020-05-01",
        "name": "[parameters('frontDoorName')]",
        "location": "global",
        "properties": {
          "enabledState": "Enabled",
          "frontendEndpoints": [
            {
              "name": "[variables('frontEndEndpointName')]",
              "properties": {
                "hostName": "[format('{0}.azurefd.net', parameters('frontDoorName'))]",
                "sessionAffinityEnabledState": "Disabled"
              }
            }
          ],
          "loadBalancingSettings": [
            {
              "name": "[variables('loadBalancingSettingsName')]",
              "properties": {
                "sampleSize": 4,
                "successfulSamplesRequired": 2,
                "additionalLatencyMilliseconds": 10
              }
            }
          ],
          "healthProbeSettings": [
            {
              "name": "[variables('healthProbeSettingsName')]",
              "properties": {
                "path": "/",
                "protocol": "Https",
                "intervalInSeconds": 10
              }
            }
          ],
          "backendPools": [
            {
              "name": "[variables('backendPoolName')]",
              "properties": {
                "backends": [
                  {
                    "address": "[parameters('backendAddress')]",
                    "backendHostHeader": "[parameters('backendAddress')]",
                    "httpPort": 80,
                    "httpsPort": 443,
                    "weight": 50,
                    "priority": 1,
                    "enabledState": "Enabled"
                  }
                ],
                "loadBalancingSettings": {
                  "id": "[resourceId('Microsoft.Network/frontDoors/loadBalancingSettings', parameters('frontDoorName'), variables('loadBalancingSettingsName'))]"
                },
                "healthProbeSettings": {
                  "id": "[resourceId('Microsoft.Network/frontDoors/healthProbeSettings', parameters('frontDoorName'), variables('healthProbeSettingsName'))]"
                }
              }
            }
          ],
          "routingRules": [
            {
              "name": "[variables('routingRuleName')]",
              "properties": {
                "frontendEndpoints": [
                  {
                    "id": "[resourceId('Microsoft.Network/frontDoors/frontEndEndpoints', parameters('frontDoorName'), variables('frontEndEndpointName'))]"
                  }
                ],
                "acceptedProtocols": [
                  "Http",
                  "Https"
                ],
                "patternsToMatch": [
                  "/*"
                ],
                "routeConfiguration": {
                  "@odata.type": "#Microsoft.Azure.FrontDoor.Models.FrontdoorForwardingConfiguration",
                  "forwardingProtocol": "HttpsOnly",
                  "backendPool": {
                    "id": "[resourceId('Microsoft.Network/frontDoors/backEndPools', parameters('frontDoorName'), variables('backendPoolName'))]"
                  }
                },
                "enabledState": "Enabled"
              }
            }
          ]
        }
      }
    ]
```

- Create Deployment

```bash
az deployment group create --resource-group rg_eastus_166013_1_170031312929 --template-file template.json --parameters frontDoorName=lab3frontdoors backendAddress=youtube.com

```

## Task 4: Verify your deployments

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1732af6e-de8a-43e2-8e3b-c7d455088820)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cacc3326-1632-4694-b9b4-b4a2f865020c)

- Clicking the Front door url will redirect me to youtube app.

- - -
