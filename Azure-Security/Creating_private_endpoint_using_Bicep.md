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

- Test database sql server name

`nslookup sqlserveryejbzycvqyw72.database.windows.net`

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1dd55ef7-8581-407c-b366-bbfa5408c469)


- Setup sql server connection in vm
> https://aka.ms/ssmsfullsetup

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/084ed94c-700f-4164-9182-b80c26a6d225)


