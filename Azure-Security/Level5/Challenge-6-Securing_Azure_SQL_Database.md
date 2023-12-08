# Challenge lab - Securing Azure SQL Database

__Cloud challenge details__
__
An organization XYZ has a critical application that relies on an Azure SQL Database to store sensitive customer data. To meet evolving security requirements and regulatory compliance standards, the IT team has decided to implement advanced data protection measures, enhance data classification, and enable auditing for the database.  Now your challenge is to create a Azure SQL Database and Configure Advanced Data Protection.

Follow the below instructions to complete this challenge.

1. Use Region as East US
2. Deploy an Azure SQL Database
3. Configure Advanced Data Protection
4. Configure Data Classification
5. Configure Auditing

__

## Solution

__Architecture Diagram__

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ff782c7a-88f4-4d81-a5b5-42525294aed9)


- Template deployment

```yaml
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
    },
    "variables": {
        "sqlAdministratorLogin": "sqladmin",
        "sqlAdministratorLoginPassword": "Pa55w.rd",
        "sqlServerName": "[concat('az500l11',uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Sql/servers",
            "apiVersion": "2015-05-01-preview",
            "name": "[variables('sqlServerName')]",
            "location": "eastus",
            "kind": "v12.0",
            "properties": {
                "administratorLogin": "[variables('sqlAdministratorLogin')]",
                "administratorLoginPassword": "[variables('sqlAdministratorLoginPassword')]",
                "version": "12.0"
            }
        },
        {
            "type": "Microsoft.Sql/servers/firewallRules",
            "apiVersion": "2015-05-01-preview",
            "name": "[concat(variables('sqlServerName'), '/AllowAllWindowsAzureIps')]",
            "dependsOn": [
                "[resourceId('Microsoft.Sql/servers', variables('sqlServerName'))]"
            ],
            "properties": {
                "startIpAddress": "0.0.0.0",
                "endIpAddress": "0.0.0.0"
            }
        },
        {
            "type": "Microsoft.Sql/servers/databases",
            "apiVersion": "2017-03-01-preview",
            "name": "[concat(variables('sqlServerName'), '/AZ500LabDb')]",
            "location": "eastus",
            "dependsOn": [
                "[resourceId('Microsoft.Sql/servers', variables('sqlServerName'))]"
            ],
            "sku": {
                "name": "Basic",
                "tier": "Basic"
            },
            "kind": "v12.0,user",
            "properties": {
                "collation": "SQL_Latin1_General_CP1_CI_AS",
                "maxSizeBytes": 2147483648,
                "catalogCollation": "SQL_Latin1_General_CP1_CI_AS",
                "zoneRedundant": false,
                "sampleName":"AdventureWorksLT"
            }
        }
    ]
}
```

## Stage 3: Configure Advanced Data Protection

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1de25bae-6a40-4372-8e5b-75b4ffae66e6)

- Save

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ce94ed27-8f4c-4fc7-a5fb-43010a0daea2)


## Stage 4: Configure Data Classification

- On the SQL database blade, in the Security section, click Data Discovery & Classification. Select the Classification tab. Click on + Add classification.

Follow : https://github.com/Tcarters/Cloud-Security-Journey/blob/master/Azure-Security/Level3/Securing_Azure_SQL_Database.md

DOne.
