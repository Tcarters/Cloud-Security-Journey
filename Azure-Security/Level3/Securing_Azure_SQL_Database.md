# Securing Azure SQL Database


## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d84ec8a4-5079-46d5-8e6f-f937681567f5)


## Stage 1: Deploy an Azure SQL Database

- Template file

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

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b7566df6-4843-4ae5-8f0f-2d450488dac4)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ac9e40c6-9cc7-48a1-b8e4-e29e344d8558)


## Stage 3: Configure Advanced Data Protection

- Configure Advanced Data Protection by enabling Microsoft Defender for SQL on the SQL server

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b6fd81fd-cdfe-4f99-adb1-b40f50313f65)

- Save configuration

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/9a0634a0-2484-41de-80ff-de1d841eb8bc)

## Stage 4: Configure Data Classification

- On the SQL database blade, in the Security section, click Data Discovery & Classification. Select the Classification tab. Click on `+ Add classification`.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a662dfbb-19d3-4038-9fc7-b5669e1119bf)


## Stage 5: Configure Auditing

- Enable Azure SQL Auditing switch to ON to enable auditing.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/451b04df-24d4-4e8c-918c-6647b0a28e72)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1adee7d3-4282-48c1-ac03-92ebefc229ff)


- - -



