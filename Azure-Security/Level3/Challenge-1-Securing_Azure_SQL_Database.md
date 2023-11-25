# Challenge 1 - Securing Azure SQL Database


## Cloud challenge details

In this challenge, your Azure SQL Database skills are put to the test. You will be given a requirement and you have to reach it using your knowledge of Azure services relevant to this challenge lab that helps you understand the real-time scenarios.

> An organization XYZ has a critical application that relies on an Azure SQL Database to store sensitive customer data. To meet evolving security requirements and regulatory compliance standards, the IT team has decided to implement advanced data protection measures, enhance data classification, and enable auditing for the database.  Now your challenge is to create a Azure SQL Database and Configure Advanced Data Protection.



Follow the below instructions to complete this challenge.

1. Use Region as East US
2. Deploy an Azure SQL Database
3. Configure Advanced Data Protection
4. Configure Data Classification
5. Configure Auditing



## Solutions


#### Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/366d3b37-21fc-45fb-b56e-03d39b5ec48d)

### 2. Deploy an Azure SQL Database

- Create a Template file :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1973e3ea-4769-45f7-8c35-be1217f22bb1)

- Template File for deployment:

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

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/054c1ffb-c0af-4dc3-a51b-ec07cd162791)

- Deployment successed

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4b89c6f9-c89a-417f-b983-ff7000b921ed)



### 3. Configure Advanced Data Protection

- Configure Advanced Data Protection by enabling Microsoft Defender for SQL on the SQL server

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f50bd416-17f5-4972-8113-b08d85bd367b)

- Save configuration

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a5bfb705-2342-460b-a1e1-0491c3e93333)


### 4. Configure Advanced Data Protection

- On the SQL database blade, in the Security section, click ``Data Discovery & Classification`` .
- Select the Classification tab. Click on ``+ Add classification``.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6ba3ccb2-abcb-4b2c-abb8-0f8b431d24d3)

- Add Classification Detail :

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/788bb455-6cb1-4fea-9f4d-b0c605b0926b)

- And Save config

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d9051f85-9dcd-4a15-bf06-af578fd2edf6)


### 5. Configure Auditing

- Enable Auditing on SQL Server
- Enable Azure SQL Auditing switch to ON to enable auditing.
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a2866a7f-5fc3-43ae-8087-c26f92baba62)

- Click create a new storage account for log auditing:
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/51cf7980-2c03-483a-bc80-ee583569354b)

- Save config:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/f911f2b2-e6b8-4dd6-b179-e0b3a1151d27)

- click Advanced properties by setting Retention days to `5`:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6cee456e-dde0-47e6-944b-a3b0ce5c692d)


Challenge completed
- - -
