# Creating a private endpoint using Bicep



## Architecture Diagram

## Task 2: Explore the Bicep file

- Bicep config file

```yaml

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

- 
