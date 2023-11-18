# Deploy and configure Azure Firewall and policy using the Azure portal

### What is Azure Firewall?
Azure Firewall is a cloud-native and intelligent network firewall security service that provides the best of breed threat protection for your cloud workloads running in Azure.

It's a fully stateful, firewall as a service with built-in high availability and unrestricted cloud scalability. 

It provides both east-west and north-south traffic inspection.

Azure Firewall is offered in three SKUs: Standard, Premium, and Basic.

### What is Azure Policy?
- Azure Policy is a service in Azure which allows you to create policies which enforce and control the properties of a resource. When these policies are used they enforce different rules and effects over the resources, so those resources stay compliant with your IT governance standards.
- Azure Policy allows you to ensure that all resources are configured with required services, and will tell you when systems are out of compliance.
- Azure policy is basically 3 components; policy definition , assignment and parameters.

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/7cd931c3-6703-461a-a53d-8e7b1241b763)

## Task 2: Create a Virtual Network

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/cf31afed-4a07-4945-a355-91535bd6cd4b)

- Add a second subnet
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b16a3132-096c-442d-96de-01807920056e)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/c0af298e-3c98-4e33-9165-8999a37b3d3a)

- Add a 3rd subnet for firewall managemnt:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/4bef2dfa-ddea-473b-935b-13132b2decb4)

## Task 3: Create two virtual machines

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b6b968e7-5103-4094-9670-9f77982657a1)

## Task 4: Deploy the firewall and policy

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/545b51ac-15ec-4500-90ae-3d1962135594)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fa3a767b-9499-40bc-be81-57229cf2e44b)

- Record Public IP from Firewall: `20.120.10.123`

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/1d48beab-b523-44ca-a8cc-0ce9787544bb)


## Task 5: Create a default route

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/20661339-0a1c-401b-9a15-b397a765ce91)

- Assoicate subnet in route Table:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/94e30290-c7bd-4922-b97e-3e78aac16e5e)

- Add a Route:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b1e9deca-62bd-4060-b47e-5b3bb6d34c9d)

## Task 6: Configure an application rule 

- Add an  | Application rules policy:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b1b159e8-c9ae-4d0b-a7ad-0c4d4053839a)


## Task 7: Configure a network rule 

- Add a network rule:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/701ede3d-6a7a-49ce-9ff2-5877649f308c)

## Task 8: Configure a DNAT rule

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/fe16fc5d-a17b-4d05-9596-f751e483c254)

## Task 9: Change the primary and secondary DNS address

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/28fb177b-de2a-4175-93f4-d7f22f5ff8d7)

## Task 10: Test the firewall

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/02c2c90b-7f48-471e-8244-8c65bc1ef4e5)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/536f0156-e98f-46bb-964f-dd5b890e00cf)

- Connect wthrough rdp from public firewall IP:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/32bfae9e-68d3-451e-9de3-c9813f7aad6d)

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/22abcb39-7ba7-48a9-8285-14e33776feb7)


- ACCESS GOOGLE INSIDE VM:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/d933ce9f-3305-4b3b-a317-a518938a9b60)


