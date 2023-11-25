# Challenge 3 - Creating a private link service

### Cloud challenge details

> You work as a cloud infrastructure engineer for a company called "ABC Enterprises," which is committed to ensuring the security and privacy of its services. One of your current projects is to set up a private endpoint in Microsoft Azure to securely access a critical service hosted in the Azure cloud. This private endpoint will provide a secure and private connection to the service without exposing it to the public internet.
> Now you've been tasked with setting up a private load-balanced service for this application. The goal is to ensure that access to the application is restricted to only within the company's private network.

Follow the below instructions to complete this challenge.

1. Use Region as East US
2. Create a Virtual Network for the Load Balancer
3. Create an internal Load Balancer
- SKU: Select Standard
4. Create a private link service
5. Create a Virtual Network for private endpoint
6. Create a private endpoint
- Subscription: Select Pay-As-You-Go
7. Get the IP address of the private endpoint

### Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/74678df9-86fe-4d3c-aa70-561dd2bd72ee)

### 1. Create a Virtual Network for the Load Balancer


![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1b423205-a69f-4aa8-9035-251741de1b4a)

- Modify existing subnet to `subnet-1`

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2310b814-2b98-4f68-9189-e585c9cfc149)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4739984c-a05f-4fd3-86d2-1c38c9cc5372)


### 2.Create an internal Load Balancer

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/e24c13e3-26c3-4965-a5f1-9067e3aae139)

- Select **Next: Frontend IP configuration**.
- In Frontend IP configuration, select + Add a frontend IP configuration.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6049449b-2a8d-4921-9a48-00bc0983a731)

- Select __Next: Backend pools__.
- In Backend pools, select **+ Add a backend pool**.
- Enter **mybackendPool** for Name.

- Select NIC or IP Address for Backend Pool Configuration.

- Select Save.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/667e28d2-de9c-45f6-bc5b-667baaa9ab57)

- Select __Next: Inbound rules.__
- In Load balancing rule, select __+ Add a load balancing rule.__
- In Add load balancing rule, enter or select the following information:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c88c35f7-3089-4be0-834a-7cf73df09f8a)

- Save & create:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/bb2aeef4-ea38-4c42-b5d7-fb23e6afdc19)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/38774cf2-b92f-429d-a20f-57c5f2b82f8d)


### 3. Create a private link service

- In the search box at the top of the portal, enter Private link. Select Private link services in the search results.

- Outbound settings:
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b8d246c6-4b64-4522-bbcc-32d7687bb700)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/52aa1d8d-8df6-4070-8126-6006c2444ee2)


### 4. Create a Virtual Network for private endpoint

- Use following for second Vnet:
  
| Settings | Value |
|:------------ | -----:|
| Name | vnet-priv |
| Subnet name	| subnet-priv |
| Subnet address range	| 10.1.0.0/24 |

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/0cea0c9c-39d6-4cd3-a2de-e22edd4661fc)

- Save
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b25d5f48-e5bf-476d-bab8-df01b422944d)

### 5. Create a private endpoint

- In the search box at the top of the portal, enter Private endpoint. Select Private endpoints in the search results.

- Select + Create.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7457e9be-4e5a-4f3d-93d8-916babd7a1eb)


- *Resource Config* of Private Endpoint

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/11d7a3cc-7ff1-4c80-98d4-9972a84430e8)

- **ENable Policy **

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2999974a-9da8-43dc-affc-ab8c71d7b447)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/90aae6e5-474a-45ab-81ef-dc147202a603)

- Let rest as default:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c7562f96-0bf4-4446-a0a9-12048882ae1f)


### 6. Get the IP address of the private endpoint

1. Enter *your-rg* in the search box at the top of the portal. Select *test-rg* in the search results in Resource Groups.
2. In the *your-rg* resource group, select __myprivate-endpoint__.
3. In the Overview page of __myprivate-endpoint__, select the name of the network interface associated with the private endpoint.
4. The network interface name begins with __myprivate-endpoint.nic__.

In the Overview page of the private endpoint nic, the IP address of the endpoint is displayed in Private IP address.

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/2b870241-5f23-49c6-a5aa-f763abc54326)


Game Over 🏁

- - -
